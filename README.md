# Learn-Rails-by-Reading-Source-Code

### Before you research Rails 5 source code
1) I suggest you learn Rack [http://rack.github.io/](http://rack.github.io/) first. You need to know that an object respond to `call` method is the most important convention.

So which is the object with `call` method in Rails?

I will answer this question later.

2) You need a good IDE with debugging function. I use [RubyMine](https://www.jetbrains.com/).

### Follow the process of Rails when starting
As Rack described, `config.ru` is the entry file.
```ruby
# ./config.ru
# This file is used by Rack-based servers to start the application.

require_relative 'config/environment'

run Rails.application # We can guess 'Rails.application' has a 'call' method.

puts Rails.application.respond_to?(:call) # Returned 'true'. Bingo!
```

Let's dig deeper for `Rails.application`.
```ruby
module Rails
  class << self
    @application = @app_class = nil

    attr_accessor :app_class
    def application # Oh, 'application' is a class method for module 'Rails'. It is not an object.
      # But it returns an object which is an instance of 'app_class'.
      # So it is important for us to know what class 'app_class' is.
      @application ||= (app_class.instance if app_class)  
    end
  end
end
```

Because `Rails.application.respond_to?(:call) # Returned 'true'.`, `app_class.instance` has a `call` method.

When was `app_class` set?
```ruby
module Rails
  class Application < Engine
    class << self
      def inherited(base) # This is a hooked method.
        Rails.app_class = base # This line set the 'app_class'.
      end
    end
  end
end
```

When `Rails::Application` is inherited like below,
```ruby
# ./config/application.rb
module YourProject
  class Application < Rails::Application # Here the hooked method `inherited` defined in eigenclass of 'Rails::Application' is invoked.
  end
end
```
`YourProject::Application` will become the `Rails.app_class`. Let's replace `app_class.instance` to `YourProject::Application.instance`.

But where is the `call` method? `call` method should be a method of `YourProject::Application.instance`.

Then Rack can `run YourProject::Application.new` (equal to `run Rails.application`).

The `call` method processes every request. Here it is.
```ruby
# ../gems/railties/lib/rails/engine.rb
module Rails
  class Engine < Railtie
    def call(env) # This method will process every request. It is invoked by Rack. So it is very important. 
      req = build_request env
      app.call req.env
    end
  end
end

# ../gems/railties/lib/rails/application.rb
module Rails
  class Application < Engine
  end
end

# ./config/application.rb
module YourProject
  class Application < Rails::Application
  end
end

```

Ancestor's chain is `YourProject::Application < Rails::Application < Rails::Engine < Rails::Railtie`.

So `YourProject::Application.new.respond_to?(:call) # Will return 'true'`.

But what does `app_class.instance` really do?

`instance` is just a method name. What we really need is `app_class.new`.

When I was reading these code
```ruby
# ../gems/railties/lib/rails/application.rb
module Rails
  class Application < Engine
    def instance
      super.run_load_hooks! # This line confused me. 
    end
  end
end
```
After a deep research, I realized that this code is equal to
```ruby
def instance
  a_returned_value = super # Keyword 'super' will call the ancestor's same name method: 'instance'.
  a_returned_value.run_load_hooks!
end
```

```ruby
# ../gems/railties/lib/rails/railtie.rb
module Rails
  class Railtie
    def instance
      @instance ||= new # 'Rails::Railtie' is the top ancestor. Now 'app_class.instance' is 'YourProject::Application.new'.
    end
  end
end
```