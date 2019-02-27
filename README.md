# Learn-Rails-by-Reading-Source-Code

## Part 0: Before you research Rails 5 source code
1) I suggest you learn Rack [http://rack.github.io/](http://rack.github.io/) first. 

You need to know that an object respond to `call` method is the most important convention.

So which is the object with `call` method in Rails App? I will answer this question in Part 1.

2) You need a good IDE with debugging function. I use [RubyMine](https://www.jetbrains.com/).


### What you will learn from this tutorial?
* How rails start your application?

* How rails process every request? 

* How rails combine ActionController, ActionView and Routes?

I should start with the command `$ rails server`. But I put this to Part 4. Because it's not interesting.

## Part 1: Your app: an instance of YourProject::Application.
First, I will give you a piece of important code.
```ruby
# ./gems/railties-5.2.2/lib/rails/commands/server/server_command.rb
module Rails
  module Command
    class ServerCommand < Base
      def perform
        # ...
        Rails::Server.new(server_options).tap do |server|
          # APP_PATH is '/Users/your_name/your-project/config/application'.
          # require APP_PATH will create the 'Rails.application' object.
          # 'Rails.application' is 'YourProject::Application.new'.
          # Rack server will start 'Rails.application'.
          require APP_PATH
          Dir.chdir(Rails.application.root)
          server.start
        end
      end
    end
  end
  
  class Server < ::Rack::Server
    def start
      #...
      # 'wrapped_app' is invoked in method 'log_to_stdout'.
      # It will get an well prepared app from './config.ru' file.
      # It will use the app created at the 'perform' method in Rails::Command::ServerCommand.
      wrapped_app   

      super # Will invoke ::Rack::Server#start. 
    end
  end
end
```
A rack server need to start with an App. The App should have a `call` method.

`config.ru` is the conventional entry file for rack app. So let's view it.
```ruby
# ./config.ru
require_relative 'config/environment'

run Rails.application # It seems that this is the app.
```

Let's test it by `Rails.application.respond_to?(:call) # Returned 'true'`.

Let's step into `Rails.application`.

```ruby
# ./gems/railties-5.2.2/lib/rails.rb
module Rails
  class << self
    @application = @app_class = nil

    attr_accessor :app_class
    
    # Oh, 'application' is a class method for module 'Rails'. It is not an object.
    # But it returns an object which is an instance of 'app_class'.
    # So it is important for us to know what class 'app_class' is.
    def application
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

`Rails::Application` is inherited like below,
```ruby
# ./config/application.rb
module YourProject
  # The hooked method `inherited` defined in eigenclass of 'Rails::Application' is invoked.
  class Application < Rails::Application
  end
end
```
`YourProject::Application` will become the `Rails.app_class`.

You may have a question: how we reach this file (`./config/application.rb`)?

Let's look back to `config.ru` to see the first line of this file `require_relative 'config/environment'`.

```ruby
# ./config/environment.rb
# Load the Rails application.
require_relative 'application' # Let's step into this line.

# Initialize the Rails application.
Rails.application.initialize!
```

```ruby
# ./config/application.rb
require_relative 'boot'

require 'rails/all'

# Require the gems listed in Gemfile, including any gems
# you've limited to :test, :development, or :production.
Bundler.require(*Rails.groups)

module YourProject
  # The hooked method `inherited` defined in eigenclass of 'Rails::Application' is invoked.
  class Application < Rails::Application
    config.load_defaults 5.2
    config.i18n.default_locale = :zh
  end
end
```
Let's replace `app_class.instance` to `YourProject::Application.instance`.

But where is the `call` method? `call` method should be a method of `YourProject::Application.instance`.

The `call` method processes every request. Here it is.
```ruby
# ./gems/railties/lib/rails/engine.rb
module Rails
  class Engine < Railtie
    def call(env) # This method will process every request. It is invoked by Rack. So it is very important. 
      req = build_request env
      app.call req.env # The 'app' object we will discuss later.
    end
  end
end

# ./gems/railties/lib/rails/application.rb
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

Let's look at the definition of instance.
```ruby
# ./gems/railties/lib/rails/application.rb
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
  return_value = super # Keyword 'super' will call the ancestor's same name method: 'instance'.
  return_value.run_load_hooks!
end
```

```ruby
# ./gems/railties/lib/rails/railtie.rb
module Rails
  class Railtie
    def instance
      # 'Rails::Railtie' is the top ancestor.
      # Now 'app_class.instance' is 'YourProject::Application.new'.
      @instance ||= new
    end
  end
end
```
And `YourProject::Application.new` is `Rails.application`.
```ruby
module Rails
  def application
    @application ||= (app_class.instance if app_class)
  end
end
```
Rack server will start `Rails.application` in the end.

It is the most important object in the whole Rails object.

And you'll only have one `Rails.application` in one process. Multiple thread shared only one `Rails.application`.

## Part 2: config
We first time see the config is in `./config/application.rb`.
```ruby
# ./config/application.rb
#...
module YourProject
  class Application < Rails::Application
    # Actually, config is a method of YourProject::Application.
    # It is defined in it's grandfather's father: Rails::Railtie
    config.load_defaults 5.2  # Let's go to see what is config
    config.i18n.default_locale = :zh
  end
end
```

```ruby
module Rails
  class Railtie
    class << self
      delegate :config, to: :instance # Method :config is defined here.
      
      def instance
        @instance ||= new # return an instance of YourProject::Application. 
      end
    end
  end
  
  class Engine < Railtie
  end
  
  class Application < Engine
    class << self
      def instance
        # This line is equal to:
        # return_value = super # 'super' will call :instance method in Railtie, which will return an instance of YourProject::Application. 
        # return_value.run_load_hooks!
        super.run_load_hooks!
      end
    end
    
    def run_load_hooks!
      return self if @ran_load_hooks
      @ran_load_hooks = true

      # ...
      self # return self! self is an instance of YourProject::Application. And it is Rails.application.
    end
    
    # This is the method config.
    def config
      # It is an instance of class Rails::Application::Configuration. 
      # Please notice that Rails::Application is father of YourProject::Application (self's class).   
      @config ||= Application::Configuration.new(self.class.find_root(self.class.called_from))
    end
  end
end
```
In the end, `YourProject::Application.config` will become `Rails.application.config`.

`YourProject::Application.config === Rails.application.config # return ture.`

Invoke Class's 'config' method become invoke the class's instance's 'config' method.

```ruby
module Rails
  class << self
    def configuration
      application.config
    end 
  end
end
```
So `Rails.configuration === Rails.application.config # return ture.`.

```ruby
module Rails
  class Application
    class Configuration < ::Rails::Engine::Configuration
      
    end
  end
  
  class Engine
    class Configuration < ::Rails::Railtie::Configuration
      attr_accessor :middleware

      def initialize(root = nil)
        super()
        #...
        @middleware = Rails::Configuration::MiddlewareStackProxy.new
      end
    end  
  end
  
  class Railtie
    class Configuration
    end
  end
end
```

## Part 3: Every request and response.
Imagine we have this route for the home page. 
```ruby
# ./config/routes.rb
Rails.application.routes.draw do
  root 'home#index' # HomeController#index
end
```

Rack need a `call` method to process request. 

Rails provide this call method in `Rails::Engine#call`.

```ruby
# ./gems/railties/lib/rails/engine.rb
module Rails
  class Engine < Railtie
    def call(env) # This method will process every request. It is invoked by Rack. 
      req = build_request env
      app.call req.env # The 'app' method is blow.
    end
    
    def app
      # You may want to know when does the @app first time initialized.
      # It is initialized when 'config.ru' is load by rack server.
      # Please look at Rack::Server#build_app_and_options_from_config for more information.
      # When Rails.application.initialize! (in ./config/environment.rb), @app is initialized.
      @app || @app_build_lock.synchronize { # '@app_build_lock = Mutex.new', so multiple threads share one '@app'.
        @app ||= begin
          # In the end, config.middleware will be an instance of ActionDispatch::MiddlewareStack with preset instance variable @middlewares (which is an Array). 
          stack = default_middleware_stack # Let's step into this line
          # 'middleware' is a 'middleware_stack'!
          config.middleware = build_middleware.merge_into(stack)
          config.middleware.build(endpoint) # look at this endpoint below
        end
      }
      
#@app is #<Rack::Sendfile:0x00007ff14d905f60 
#          @app=#<ActionDispatch::Static:0x00007ff14d906168 
#                 @app=#<ActionDispatch::Executor:0x00007ff14d9061b8 
#                        ...
#                           @app=#<Rack::ETag:0x00007fa1e540c4f8  
#                                  @app=#<Rack::TempfileReaper:0x00007fa1e540c520 
#                                         @app=#<ActionDispatch::Routing::RouteSet:0x00007fa1e594cbe8>
#                                 >
#                         ...    
#                        >
#                             
#                 >
#         >
      @app
    end
    
    # Defaults to an ActionDispatch::Routing::RouteSet.
    def endpoint
      ActionDispatch::Routing::RouteSet.new_with_config(config)
    end
  end
    
  class Application < Engine
    def default_middleware_stack
      default_stack = DefaultMiddlewareStack.new(self, config, paths)
      default_stack.build_stack # Let's step into this line.
    end
    
    class DefaultMiddlewareStack
      attr_reader :config, :paths, :app

      def initialize(app, config, paths)
        @app = app
        @config = config
        @paths = paths
      end

      def build_stack
        ActionDispatch::MiddlewareStack.new do |middleware|
          if config.force_ssl
            middleware.use ::ActionDispatch::SSL, config.ssl_options
          end

          middleware.use ::Rack::Sendfile, config.action_dispatch.x_sendfile_header

          if config.public_file_server.enabled
            headers = config.public_file_server.headers || {}

            middleware.use ::ActionDispatch::Static, paths["public"].first, index: config.public_file_server.index_name, headers: headers
          end

          if rack_cache = load_rack_cache
            require "action_dispatch/http/rack_cache"
            middleware.use ::Rack::Cache, rack_cache
          end

          if config.allow_concurrency == false
            # User has explicitly opted out of concurrent request
            # handling: presumably their code is not threadsafe

            middleware.use ::Rack::Lock
          end

          middleware.use ::ActionDispatch::Executor, app.executor

          middleware.use ::Rack::Runtime
          middleware.use ::Rack::MethodOverride unless config.api_only
          middleware.use ::ActionDispatch::RequestId
          middleware.use ::ActionDispatch::RemoteIp, config.action_dispatch.ip_spoofing_check, config.action_dispatch.trusted_proxies

          middleware.use ::Rails::Rack::Logger, config.log_tags
          middleware.use ::ActionDispatch::ShowExceptions, show_exceptions_app
          middleware.use ::ActionDispatch::DebugExceptions, app, config.debug_exception_response_format

          unless config.cache_classes
            middleware.use ::ActionDispatch::Reloader, app.reloader
          end

          middleware.use ::ActionDispatch::Callbacks
          middleware.use ::ActionDispatch::Cookies unless config.api_only

          if !config.api_only && config.session_store
            if config.force_ssl && config.ssl_options.fetch(:secure_cookies, true) && !config.session_options.key?(:secure)
              config.session_options[:secure] = true
            end
            middleware.use config.session_store, config.session_options
            middleware.use ::ActionDispatch::Flash
          end

          unless config.api_only
            middleware.use ::ActionDispatch::ContentSecurityPolicy::Middleware
          end

          middleware.use ::Rack::Head
          middleware.use ::Rack::ConditionalGet
          middleware.use ::Rack::ETag, "no-cache"

          middleware.use ::Rack::TempfileReaper unless config.api_only
        end
       end
     end
  end
end
```

As we see in the Rack middleware stack, the last one is 

`@app=#<ActionDispatch::Routing::RouteSet:0x00007fa1e594cbe8>`
```ruby
# ./gems/actionpack5.2.2/lib/action_dispatch/routing/route_set.rb
module ActionDispatch
  module Routing
    class RouteSet
      def initialize(config = DEFAULT_CONFIG)
        @set    = Journey::Routes.new
        @router = Journey::Router.new(@set)
      end
    
      def call(env)
        req = make_request(env) # return ActionDispatch::Request.new(env)
        req.path_info = Journey::Router::Utils.normalize_path(req.path_info)
        @router.serve(req) # Let's step into this line.
      end
    end
  end
  
# ./gems/actionpack5.2.2/lib/action_dispatch/journey/router.rb  
  module Journey
    class Router
      class RoutingError < ::StandardError
      end
    
      attr_accessor :routes
        
      def initialize(routes)
        @routes = routes
      end
        
      def serve(req)
        find_routes(req).each do |match, parameters, route| # Let's step into 'find_routes'
          set_params  = req.path_parameters
          path_info   = req.path_info
          script_name = req.script_name
        
          unless route.path.anchored
            req.script_name = (script_name.to_s + match.to_s).chomp("/")
            req.path_info = match.post_match
            req.path_info = "/" + req.path_info unless req.path_info.start_with? "/"
          end
        
          parameters = route.defaults.merge parameters.transform_values { |val|
            val.dup.force_encoding(::Encoding::UTF_8)
          }
        
          req.path_parameters = set_params.merge parameters
        
          # route is an instance of ActionDispatch::Journey::Route. 
          # route.app is an instance of ActionDispatch::Routing::RouteSet::Dispatcher.
          status, headers, body = route.app.serve(req) # Let's step into method 'serve'
        
          if "pass" == headers["X-Cascade"]
            req.script_name     = script_name
            req.path_info       = path_info
            req.path_parameters = set_params
            next
          end
        
          return [status, headers, body]
        end
    
        [404, { "X-Cascade" => "pass" }, ["Not Found"]]
      end
      
      def find_routes(req)
        routes = filter_routes(req.path_info).concat custom_routes.find_all { |r|
          r.path.match(req.path_info)
        }

        routes =
          if req.head?
            match_head_routes(routes, req)
          else
            match_routes(routes, req)
          end

        routes.sort_by!(&:precedence)

        routes.map! { |r|
          match_data = r.path.match(req.path_info)
          path_parameters = {}
          match_data.names.zip(match_data.captures) { |name, val|
            path_parameters[name.to_sym] = Utils.unescape_uri(val) if val
          }
          [match_data, path_parameters, r]
        }
      end

    end
  end
end

# ./gems/actionpack5.2.2/lib/action_dispatch/routing/route_set.rb
module ActionDispatch
  module Routing
    class RouteSet
      class Dispatcher < Routing::Endpoint
        def serve(req)
          params     = req.path_parameters # params: { action: 'index', controller: 'home' }
          controller = controller(req) # controller: HomeController
          # The definition of make_response! is ActionDispatch::Response.create.tap do |res| res.request = request; end
          res        = controller.make_response!(req) 
          dispatch(controller, params[:action], req, res) # Let's step into this line.
        rescue ActionController::RoutingError
          if @raise_on_name_error
            raise
          else
            return [404, { "X-Cascade" => "pass" }, []]
          end
        end
        
        private
        
        def controller(req)
          req.controller_class
        rescue NameError => e
          raise ActionController::RoutingError, e.message, e.backtrace
        end

        def dispatch(controller, action, req, res)
          controller.dispatch(action, req, res) # Let's step into this line.
        end
      end
    end
  end    
end

# ./gems/actionpack-5.2.2/lib/action_controller/metal.rb
module ActionController
  class Metal < AbstractController::Base
    abstract!
    
    def self.controller_name
      @controller_name ||= name.demodulize.sub(/Controller$/, "").underscore
    end

    def self.make_response!(request)
      ActionDispatch::Response.new.tap do |res|
        res.request = request
      end
    end
    
    class_attribute :middleware_stack, default: ActionController::MiddlewareStack.new
    
    def self.inherited(base)
      base.middleware_stack = middleware_stack.dup
      super
    end
    
    # Direct dispatch to the controller. Instantiates the controller, then
    # executes the action named +name+.
    def self.dispatch(name, req, res)
      if middleware_stack.any?
        middleware_stack.build(name) { |env| new.dispatch(name, req, res) }.call req.env
      else
        # self is HomeController, so in this line Rails will new a HomeController instance.  
        # See `HomeController.ancestors`, you can find many parents classes.
        # These are some typical ancestors of HomeController. 
        # HomeController 
        # < ApplicationController
        # < ActionController::Base 
        # < ActiveRecord::Railties::ControllerRuntime (module included)
        # < ActionController::Instrumentation (module included)
        # < ActionController::Rescue (module included)
        # < AbstractController::Callbacks (module included)
        # < ActionController::ImplicitRender (module included)
        # < ActionController::BasicImplicitRender (module included)
        # < ActionController::Renderers (module included) 
        # < ActionController::Rendering (module included) 
        # < ActionView::Layouts (module included) 
        # < ActionView::Rendering (module included)
        # < ActionDispatch::Routing::UrlFor (module included) 
        # < AbstractController::Rendering (module included)
        # < ActionController::Metal
        # < AbstractController::Base
        new.dispatch(name, req, res) # Let's step into this line.
      end
    end
    
    def dispatch(name, request, response)
      set_request!(request)
      set_response!(response)
      process(name) # Let's step into this line.
      request.commit_flash
      to_a
    end
    
    def to_a
      response.to_a
    end
  end
end

# .gems/actionpack-5.2.2/lib/abstract_controller/base.rb
module AbstractController
  class Base
    def process(action, *args)
      @_action_name = action.to_s

      unless action_name = _find_action_name(@_action_name)
        raise ActionNotFound, "The action '#{action}' could not be found for #{self.class.name}"
      end

      @_response_body = nil

      process_action(action_name, *args) # Let's step into this line.
    end
  end
end

# .gems/actionpack-5.2.2/lib/action_controller/metal/instrumentation.rb
module ActionController
  module Instrumentation
    def process_action(*args)
      raw_payload = {
        controller: self.class.name,
        action: action_name,
        params: request.filtered_parameters,
        headers: request.headers,
        format: request.format.ref,
        method: request.request_method,
        path: request.fullpath
      }
    
      ActiveSupport::Notifications.instrument("start_processing.action_controller", raw_payload.dup)
    
      ActiveSupport::Notifications.instrument("process_action.action_controller", raw_payload) do |payload|
        begin
          # self: #<HomeController:0x00007fcd3c5dfd48>
          result = super # Let's step into this line.
          payload[:status] = response.status
          result
        ensure
          append_info_to_payload(payload)
        end
      end
    end
  end
end

# .gems/actionpack-5.2.2/lib/action_controller/metal/rescue.rb
module ActionController
  module Rescue
    def process_action(*args)
      super # Let's step into this line.
    rescue Exception => exception
      request.env["action_dispatch.show_detailed_exceptions"] ||= show_detailed_exceptions?
      rescue_with_handler(exception) || raise
    end
  end  
end

# .gems/actionpack-5.2.2/lib/abstract_controller/callbacks.rb
module AbstractController
  # = Abstract Controller Callbacks
  #
  # Abstract Controller provides hooks during the life cycle of a controller action.
  # Callbacks allow you to trigger logic during this cycle. Available callbacks are:
  #
  # * <tt>after_action</tt>
  # * <tt>before_action</tt>
  # * <tt>skip_before_action</tt>
  # * ...
  module Callbacks
    def process_action(*args)
      run_callbacks(:process_action) do
        # self: #<HomeController:0x00007fcd3c5dfd48>
        super # Let's step into this line.
      end
    end
  end
end

# .gems/actionpack-5.2.2/lib/action_controller/metal/rendering.rb
module ActionController
  module Rendering
    def process_action(*)
      self.formats = request.formats.map(&:ref).compact
      super # Let's step into this line.
    end
  end
end

# .gems/actionpack-5.2.2/lib/abstract_controller/base.rb
module AbstractController
  class Base
    def process_action(method_name, *args)
      # self: #<HomeController:0x00007fcd3c5dfd48>, method_name: 'index' 
      send_action(method_name, *args) # In the end, method 'send_action' is method 'send' as the below line shown.
    end

    alias send_action send
  end
end

# .gems/actionpack-5.2.2/lib/action_controller/metal/basic_implicit_render.rb
module ActionController
  module BasicImplicitRender
    def send_action(method, *args)
      # self: #<HomeController:0x00007fcd3c5dfd48>, method_name: 'index'    
      # Because 'send_action' is an alias of 'send', so  
      # self.send('index', *args) will goto HomeController#index.
      x = super
      x.tap { default_render unless performed? } # Let's step into 'default_render' later.
    end
  end
end

# ./your_project/app/controllers/home_controller.rb
class HomeController < ApplicationController
  # Will go back to BasicImplicitRender#send_action when method 'index' is done.
  def index
    # Question: How does this instance variable '@users' in HomeController can be accessed in './app/views/home/index.html.erb' ?
    # Will answer this question later. 
    @users = User.all.pluck(:id, :name)
  end
end
```

```html
# ./app/views/home/index.html.erb
<div class="container">
  <h1 class="display-4 font-italic">
    <%= t('home.banner_title') %>
    <%= @users %>
  </h1>
</div>
```

```ruby
# .gems/actionpack-5.2.2/lib/action_controller/metal/implicit_render.rb 
module ActionController
  # Handles implicit rendering for a controller action that does not
  # explicitly respond with +render+, +respond_to+, +redirect+, or +head+.
  module ImplicitRender
    def default_render(*args)
      # Let's step into template_exists?
      if template_exists?(action_name.to_s, _prefixes, variants: request.variant)
        # Rails have found the default template './app/views/home/index.html.erb', so render it.
        render(*args) # Let's step into this line later
      elsif any_templates?(action_name.to_s, _prefixes)
        message = "#{self.class.name}\##{action_name} is missing a template " \
          "for this request format and variant.\n" \
          "\nrequest.formats: #{request.formats.map(&:to_s).inspect}" \
          "\nrequest.variant: #{request.variant.inspect}"

        raise ActionController::UnknownFormat, message
      elsif interactive_browser_request?
        message = "#{self.class.name}\##{action_name} is missing a template " \
          "for this request format and variant.\n\n" \
          "request.formats: #{request.formats.map(&:to_s).inspect}\n" \
          "request.variant: #{request.variant.inspect}\n\n" \
          "NOTE! For XHR/Ajax or API requests, this action would normally " \
          "respond with 204 No Content: an empty white screen. Since you're " \
          "loading it in a web browser, we assume that you expected to " \
          "actually render a template, not nothing, so we're showing an " \
          "error to be extra-clear. If you expect 204 No Content, carry on. " \
          "That's what you'll get from an XHR or API request. Give it a shot."

        raise ActionController::UnknownFormat, message
      else
        logger.info "No template found for #{self.class.name}\##{action_name}, rendering head :no_content" if logger
        super
      end
    end
  end
end

# .gems/actionview-5.2.2/lib/action_view/lookup_context.rb
module ActionView
  class LookupContext
    module ViewPaths
      # Rails find out that the default template is './app/views/home/index.html.erb'
      def exists?(name, prefixes = [], partial = false, keys = [], **options)
        @view_paths.exists?(*args_for_lookup(name, prefixes, partial, keys, options))
      end
      alias :template_exists? :exists?
    end
  end  
end

# .gems/actionpack-5.2.2/lib/action_controller/metal/instrumentation.rb
module ActionController
  module Instrumentation
    def render(*args)
      render_output = nil
      self.view_runtime = cleanup_view_runtime do
        Benchmark.ms {
          # self: #<HomeController:0x00007fa7e9c54278> 
          render_output = super # Let's step into super 
        }
      end
      render_output
    end
  end  
end

# .gems/actionpack-5.2.2/lib/action_controller/metal/rendering.rb
module ActionController
  module Rendering
    # Check for double render errors and set the content_type after rendering.
    def render(*args)
      raise ::AbstractController::DoubleRenderError if response_body
      super # Let's step into super
    end
  end
end

# .gems/actionpack-5.2.2/lib/abstract_controller/rendering.rb
module AbstractController
  module Rendering
    # Normalizes arguments, options and then delegates render_to_body and
    # sticks the result in <tt>self.response_body</tt>.
    def render(*args, &block)
      options = _normalize_render(*args, &block)
      rendered_body = render_to_body(options) # Let's step into this line.
      if options[:html]
        _set_html_content_type
      else
        _set_rendered_content_type rendered_format
      end
      self.response_body = rendered_body
    end
  end
end

# .gems/actionpack-5.2.2/lib/action_controller/metal/renderers.rb
module ActionController
  module Renderers
    def render_to_body(options)
      _render_to_body_with_renderer(options) || super # Let's step into this line and super later.
    end
    
    # For this example, this method return nil in the end.
    def _render_to_body_with_renderer(options)
      # The '_renderers' is defined at line 31: class_attribute :_renderers, default: Set.new.freeze.
      # '_renderers' is an instance predicate method. For more information, 
      # see ./gems/activesupport/lib/active_support/core_ext/class/attribute.rb  
      _renderers.each do |name|
        if options.key?(name)
          _process_options(options)
          method_name = Renderers._render_with_renderer_method_name(name)
          return send(method_name, options.delete(name), options)
        end
      end
      nil
    end
  end  
end

# .gems/actionpack-5.2.2/lib/action_controller/metal/renderers.rb
module ActionController
  module Rendering
    def render_to_body(options = {})
      super || _render_in_priorities(options) || " " # Let's step into super
    end
  end
end
```

```ruby
# .gems/actionview-5.2.2/lib/action_view/rendering.rb
module ActionView
  module Rendering
    def render_to_body(options = {})
      _process_options(options)
      _render_template(options) # Let's step into this line.
    end
    
    def _render_template(options)
      variant = options.delete(:variant)
      assigns = options.delete(:assigns)
      context = view_context # We will step into this line later.
        
      context.assign assigns if assigns
      lookup_context.rendered_format = nil if options[:formats]
      lookup_context.variants = variant if variant
        
      view_renderer.render(context, options) # Let's step into this line.
    end
  end
end

# .gems/actionview-5.2.2/lib/action_view/renderer/renderer.rb
module ActionView
  class Renderer
    def render(context, options)
      if options.key?(:partial)
        render_partial(context, options)
      else
        render_template(context, options) # Let's step into this line.
      end
    end
    
    # Direct access to template rendering.
    def render_template(context, options)
      TemplateRenderer.new(@lookup_context).render(context, options) # Let's step into this line.
    end
  end
end

# .gems/actionview-5.2.2/lib/action_view/renderer/template_renderer.rb
module ActionView
  class TemplateRenderer < AbstractRenderer
    def render(context, options)
      @view    = context
      @details = extract_details(options)
      template = determine_template(options)

      prepend_formats(template.formats)

      @lookup_context.rendered_format ||= (template.formats.first || formats.first)

      render_template(template, options[:layout], options[:locals]) # Let's step into this line.
    end
    
    def render_template(template, layout_name = nil, locals = nil)
      view, locals = @view, locals || {}

      render_with_layout(layout_name, locals) do |layout| # Let's step into this line
        instrument(:template, identifier: template.identifier, layout: layout.try(:virtual_path)) do
          # template: #<ActionView::Template:0x00007f822759cbc0>
          template.render(view, locals) { |*name| view._layout_for(*name) } # Let's step into this line
        end
      end
    end
    
    def render_with_layout(path, locals)
      layout  = path && find_layout(path, locals.keys, [formats.first])
      content = yield(layout)

      if layout
        view = @view
        view.view_flow.set(:layout, content)
        layout.render(view, locals) { |*name| view._layout_for(*name) }
      else
        content
      end
    end
  end
end

# .gems/actionview-5.2.2/lib/action_view/template.rb
module ActionView
  class Template
    def render(view, locals, buffer = nil, &block)
      instrument_render_template do
        # self: #<ActionView::Template:0x00007f89bab1efb8 
        #           @identifier="/path/to/your/project/app/views/home/index.html.erb" 
        #           @source="<div class='container'\n ..."
        #        >
        compile!(view)
        # method_name: "_app_views_home_index_html_erb___3699380246341444633_70336654511160" (This method is defined in 'def compile(mod)' below)
        # view: #<#<Class:0x00007ff10d6c9d18>:0x00007ff10ea050a8>, view is an instance of <a subclass of ActionView::Base> which has same instance variables in the instance of HomeController.
        # The method 'view.send' will return the result html!
        view.send(method_name, locals, buffer, &block)
      end
    rescue => e
      handle_render_error(view, e)
    end
    
    # Compile a template. This method ensures a template is compiled
    # just once and removes the source after it is compiled.
    def compile!(view)
      return if @compiled

      # Templates can be used concurrently in threaded environments
      # so compilation and any instance variable modification must
      # be synchronized
      @compile_mutex.synchronize do
        # Any thread holding this lock will be compiling the template needed
        # by the threads waiting. So re-check the @compiled flag to avoid
        # re-compilation
        return if @compiled

        if view.is_a?(ActionView::CompiledTemplates)
          mod = ActionView::CompiledTemplates
        else
          mod = view.singleton_class
        end

        instrument("!compile_template") do
          compile(mod) # Let's step into this line.
        end

        # Just discard the source if we have a virtual path. This
        # means we can get the template back.
        @source = nil if @virtual_path
        @compiled = true
      end
    end
    
    def compile(mod)
      encode!
      # @handler: #<ActionView::Template::Handlers::ERB:0x00007ff10e1be188>
      code = @handler.call(self) # Let's step into this line.

      # Make sure that the resulting String to be eval'd is in the
      # encoding of the code
      source = <<-end_src.dup
        def #{method_name}(local_assigns, output_buffer)
          _old_virtual_path, @virtual_path = @virtual_path, #{@virtual_path.inspect};_old_output_buffer = @output_buffer;#{locals_code};#{code}
        ensure
          @virtual_path, @output_buffer = _old_virtual_path, _old_output_buffer
        end
      end_src

      # Make sure the source is in the encoding of the returned code
      source.force_encoding(code.encoding)

      # In case we get back a String from a handler that is not in
      # BINARY or the default_internal, encode it to the default_internal
      source.encode!

      # Now, validate that the source we got back from the template
      # handler is valid in the default_internal. This is for handlers
      # that handle encoding but screw up
      unless source.valid_encoding?
        raise WrongEncodingError.new(@source, Encoding.default_internal)
      end

      #  source:   def _app_views_home_index_html_erb___1187260686135140546_70244801399180(local_assigns, output_buffer)
      #              _old_virtual_path, @virtual_path = @virtual_path, "home/index";_old_output_buffer = @output_buffer;;
      #              @output_buffer = output_buffer || ActionView::OutputBuffer.new;
      #              @output_buffer.safe_append='<div class="container">
      #                <h1 class="display-4 font-italic">
      #                  '.freeze;
      #                   @output_buffer.append=( t('home.banner_title') );
      #                   @output_buffer.append=( @users ); 
      #                   @output_buffer.safe_append='
      #                </h1>
      #              </div>
      #              '.freeze;
      #              @output_buffer.to_s
      #            ensure
      #              @virtual_path, @output_buffer = _old_virtual_path, _old_output_buffer
      #            end
      mod.module_eval(source, identifier, 0) # This line will actually define the method '_app_views_home_index_html_erb___1187260686135140546_70244801399180'
      # mod: ActionView::CompiledTemplates
      ObjectSpace.define_finalizer(self, Finalizer[method_name, mod])
    end

# .gems/actionview-5.2.2/lib/action_view/template/handler/erb.rb     
    module Handlers
      class ERB
        def call(template)
          # First, convert to BINARY, so in case the encoding is
          # wrong, we can still find an encoding tag
          # (<%# encoding %>) inside the String using a regular
          # expression
          template_source = template.source.dup.force_encoding(Encoding::ASCII_8BIT)

          erb = template_source.gsub(ENCODING_TAG, "")
          encoding = $2

          erb.force_encoding valid_encoding(template.source.dup, encoding)

          # Always make sure we return a String in the default_internal
          erb.encode!

          self.class.erb_implementation.new(
            erb,
            escape: (self.class.escape_whitelist.include? template.type),
            trim: (self.class.erb_trim_mode == "-")
          ).src
        end
      end
    end
  end
end
```

It's time to answer the question before: 

How can instance variable like `@users` defined in `HomeController` be accessed in `./app/views/home/index.html.erb`?

```ruby
# ./gems/actionview-5.2.2/lib/action_view/rendering.rb
module ActionView
  module Rendering
    def view_context
      view_context_class.new( # Let's step into this line later.
        view_renderer,
        view_assigns, # Let's step into this line.
        self
      )
    end
    
    def view_assigns
      # self: #<HomeController:0x00007f83ecfed310>
      protected_vars = _protected_ivars
      # instance_variables is an instance method of Object and it will return an array. And the array contains @users.  
      variables      = instance_variables 

      variables.reject! { |s| protected_vars.include? s }
      ret = variables.each_with_object({}) { |name, hash|
        hash[name.slice(1, name.length)] = instance_variable_get(name)
      }
      # ret: {"marked_for_same_origin_verification"=>true, "users"=>[[1, "Lane"], [2, "John"], [4, "Frank"]]}
      ret
    end
    
    def view_context_class
      # will return a subclass of ActionView::Base.
      @_view_context_class ||= self.class.view_context_class
    end
    
    # How this ClassMethods works? Please look at ActiveSupport::Concern in ./gems/activesupport-5.2.2/lib/active_support/concern.rb
    # FYI, the method 'append_features' will be executed before method 'included'. 
    # https://apidock.com/ruby/v1_9_3_392/Module/append_features  
    module ClassMethods
      def view_context_class
        # self: HomeController
        @view_context_class ||= begin
          supports_path = supports_path?
          routes  = respond_to?(:_routes)  && _routes
          helpers = respond_to?(:_helpers) && _helpers

          Class.new(ActionView::Base) do
            if routes
              include routes.url_helpers(supports_path)
              include routes.mounted_helpers
            end

            if helpers
              include helpers
            end
          end
        end
      end
    end
  end
end

# ./gems/actionview-5.2.2/lib/action_view/base.rb
module ActionView
  class Base
    def initialize(context = nil, assigns = {}, controller = nil, formats = nil)
      @_config = ActiveSupport::InheritableOptions.new

      if context.is_a?(ActionView::Renderer)
        @view_renderer = context
      else
        lookup_context = context.is_a?(ActionView::LookupContext) ?
          context : ActionView::LookupContext.new(context)
        lookup_context.formats  = formats if formats
        lookup_context.prefixes = controller._prefixes if controller
        @view_renderer = ActionView::Renderer.new(lookup_context)
      end

      @cache_hit = {}
      assign(assigns) # Let's step into this line.
      assign_controller(controller)
      _prepare_context
    end
    
    def assign(new_assigns)
      @_assigns = 
        new_assigns.each do |key, value| 
          instance_variable_set("@#{key}", value) # This line will set the instance variables in HomeController like '@users' to itself.
        end
    end
  end
end

```

## Part 4: What does `$ rails server` do?
Assume your rails project app class name is `YourProject::Application` (defined in `./config/application.rb`).

First, I will give you a piece of important code.
```ruby
# ./gems/railties-5.2.2/lib/rails/commands/server/server_command.rb
module Rails
  class Server < ::Rack::Server
    def start
      #...
      log_to_stdout

      super # Will invoke ::Rack::Server#start. 
    ensure
      puts "Exiting" unless @options && options[:daemonize]
    end
    
    def log_to_stdout
      # 'wrapped_app' will get an well prepared app from './config.ru' file.
      # It's the first time invoke 'wrapped_app'.
      # The app is an instance of YourProject::Application.
      # The app is not created in 'wrapped_app'.
      # It has been created when `require APP_PATH` in previous code,
      # just at the 'perform' method in Rails::Command::ServerCommand. 
      wrapped_app

      # ...
    end
  end
end
```

Then, let's start rails by `rails server`. The command `rails` locates at `./bin/`.
```ruby
#!/usr/bin/env ruby
APP_PATH = File.expand_path('../config/application', __dir__)

require_relative '../config/boot'
require 'rails/commands' # Let's look at this file.
```  

```ruby
# ./railties-5.2.2/lib/rails/commands.rb
require "rails/command"

aliases = {
  "g"  => "generate",
  "d"  => "destroy",
  "c"  => "console",
  "s"  => "server",
  "db" => "dbconsole",
  "r"  => "runner",
  "t"  => "test"
}

command = ARGV.shift
command = aliases[command] || command # command is 'server'

Rails::Command.invoke command, ARGV # Let's step into this line.
```

```ruby
# ./railties-5.2.2/lib/rails/command.rb
module Rails
  module Command
    class << self
      def invoke(full_namespace, args = [], **config)
        # ...
        # In the end, we got this result: {"rails server" => Rails::Command::ServerCommand}
        command = find_by_namespace(namespace, command_name) # command value is Rails::Command::ServerCommand
        # command_name is 'server'  
        command.perform(command_name, args, config) # Rails::Command::ServerCommand.perform
      end
    end
  end   
end
```

```ruby
# ./gems/railties-5.2.2/lib/rails/commands/server/server_command.rb
module Rails 
  module Command
    class ServerCommand < Base # There is a class method 'perform' in the Base class.
      def initialize
      end
    
      # 'perform' here is a instance method. But for Rails::Command::ServerCommand.perform, 'perform' is a class method. 
      # Where is this 'perform' class method? Answer: In the parent class 'Base'.
      def perform
        # ...
        Rails::Server.new(server_options).tap do |server|
          #...
          server.start
        end
      end
    end
  end
end
```

Inheritance relationship: `Rails::Command::ServerCommand < Rails::Command::Base < Thor`

```ruby
# ./gems/railties-5.2.2/lib/rails/command/base.rb
module Rails
  module Command
    class Base < Thor # https://github.com/erikhuda/thor Thor is a toolkit for building powerful command-line interfaces. 
      class << self
        # command is 'server'
        def perform(command, args, config)
          #...
          dispatch(command, args.dup, nil, config) # Thor.dispatch
        end
      end
    end
  end
end
```

```ruby
# ./gems/thor/lib/thor.rb
class Thor
  class << self
    # meth is 'server'
    def dispatch(meth, given_args, given_opts, config)
      # ...
      instance = new(args, opts, config) # Here will new a Rails::Command::ServerCommand instance.
      # ...
      # command is {Thor::Command}#<struct Thor::Command name="server" ...> 
      instance.invoke_command(command, trailing || []) # Method 'invoke_command' is in Thor::Invocation.
    end
  end
end

# ./gems/thor/lib/thor/invocation.rb
class Thor
  module Invocation # This module is included in Thor. Thor is grandfather of Rails::Command::ServerCommand
    def invoke_command(command, *args) # 'invoke_command' is defined at here.
      # ...
      command.run(self, *args) # command is {Thor::Command}#<struct Thor::Command name="server" ...>
    end
  end
end

# ./gems/thor/lib/thor.rb
class Thor
  # ...
  include Thor::Base # Will invoke hook method 'Thor::Base.included(self)'
end

# ./gems/thor/lib/thor/base.rb
module Thor
  module Base
    class << self
      def included(base) # hook method when module 'Thor::Base' included.
        base.extend ClassMethods
        base.send :include, Invocation # 'Invocation' included in 'Thor'. So 'invoke_command' will be an instance method of Rails::Command::ServerCommand
        base.send :include, Shell
      end
    end
    
    module ClassMethods
      # This is also a hook method. In the end, 
      # this method will help to "alias_method('server', 'perform')".
      # The 'server' is the 'server' for `$ rails server`.
      # So it's important. We will discuss it later.
      def method_added(meth)
        # ...
        # here self is {Class} Rails::Command::ServerCommand 
        create_command(meth) # meth is 'perform'. Let's step into this line.
      end
    end
  end
end

# ./gems/railties-5.2.2/lib/rails/command/base.rb
module Rails
  module Command
    module Base # Rails::Command::Base is father of Rails::Command::ServerCommand
      class << self
        def create_command(meth)
          if meth == "perform"
            # Instance method 'server' of Rails::Command::ServerCommand will be delegated to 'perform' method now.
            alias_method('server', meth) 
          end
        end  
      end
    end
  end
end

# ./gems/thor/lib/thor/command.rb
class Thor
  class Command
    def run(instance, args = [])
      #...
      # instance is {Rails::Command::ServerCommand}#<Rails::Command::ServerCommand:0x00007fa5f319bf40> 
      instance.__send__(name, *args) # name is 'server'. Will actually invoke 'instance.perform(*args)'. 
    end
  end
end

# ./gems/railties-5.2.2/lib/rails/commands/server/server_command.rb
module Rails
  module Command
    # In ServerCommand class, there is no instance method 'server' explicitly defined.
    # It is defined by a hook method 'method_added'
    class ServerCommand < Base
      def perform
        # ...
        Rails::Server.new(server_options).tap do |server|
          # APP_PATH is '/Users/your_name/your-project/config/application'.
          # require APP_PATH will create the 'Rails.application' object.
          # 'Rails.application' is 'YourProject::Application.new'.
          # Rack server will start 'Rails.application'.
          require APP_PATH 
          Dir.chdir(Rails.application.root)
          server.start # Let's step into this line.
        end
      end
    end
  end
end

# ./gems/railties-5.2.2/lib/rails/commands/server/server_command.rb
module Rails
  class Server < ::Rack::Server
    def start
      print_boot_information
      
      # All lines in the block of trap() will not be executed  
      # unless a signal of terminating the process (like `$ kill -9 process_id`) has been received.
      trap(:INT) do
        #...
        exit
      end
      
      create_tmp_directories
      setup_dev_caching
      
      log_to_stdout # This line is important. Although the method name seems not. Let step into this line.

      super # Will invoke ::Rack::Server#start. I will show you later. 
    ensure
      puts "Exiting" unless @options && options[:daemonize]
    end
    
    def log_to_stdout
      # 'wrapped_app' will get an well prepared app from './config.ru' file.
      # It's the first time invoke 'wrapped_app'.
      # The app is an instance of YourProject::Application.
      # The app is not created in 'wrapped_app'.
      # It has been created when `require APP_PATH` in previous code,
      # just at the 'perform' method in Rails::Command::ServerCommand.   
      wrapped_app

      # ...
    end
  end
end

# ./gems/rack-2.0.6/lib/rack/server.rb
module Rack
  class Server
    def wrapped_app
      @wrapped_app ||= 
        build_app(
          app # Let's step into this line.
        )
    end
    
    def app
      @app ||= build_app_and_options_from_config # Let's step into this line.
      @app
    end
    
    def build_app_and_options_from_config
      # ...
      # self.options[:config] is 'config.ru'. Let's step into this line.
      app, options = Rack::Builder.parse_file(self.options[:config], opt_parser)
      # ...
      app
    end
    
    def start(&blk)
      #...
      wrapped_app

      trap(:INT) do
        if server.respond_to?(:shutdown)
          server.shutdown
        else
          exit
        end
      end

      # server is {Module} Rack::Handler::Puma
      # wrapped_app is {YourProject::Application} #<YourProject::Application:0x00007f7fe5523f98>
      server.run(wrapped_app, options, &blk) # We will step into this line later.
    end
  end
end

# ./gems/rack/lib/rack/builder.rb
module Rack
  module Builder
    def self.parse_file(config, opts = Server::Options.new)
      cfgfile = ::File.read(config) # config is 'config.ru'
      
      app = new_from_string(cfgfile, config)
      
      return app, options
    end

    # Let's guess what will 'run Rails.application' do in config.ru?
    # First, we will get an instance of YourProject::Application.
    # Then we will run it. But 'run' may isn't what you are thinking about.
    # Because the 'self' object in config.ru is an instance of Rack::Builder, 
    # so 'run' is an instance method of Rack::Builder.
    # Let's look at the definition of the 'run' method: 
    # def run(app)
    #   @run = app # Just set an instance variable :)
    # end
    def self.new_from_string(builder_script, file="(rackup)")
      # Rack::Builder implements a small DSL to iteratively construct Rack applications.
      eval "Rack::Builder.new {\n" + builder_script + "\n}.to_app",
        TOPLEVEL_BINDING, file, 0
    end
  end
end

# ./gems/puma-3.12.0/lib/rack/handler/puma.rb
module Rack
  module Handler
    module Puma
      def self.run(app, options = {})
        conf   = self.config(app, options)

        # ...
        launcher = ::Puma::Launcher.new(conf, :events => events)

        begin
          # Let's stop our journey here. It's puma's turn now. 
          # Puma will run your app (instance of YourProject::Application)
          launcher.run  
        rescue Interrupt
          puts "* Gracefully stopping, waiting for requests to finish"
          launcher.stop
          puts "* Goodbye!"
        end
      end
    end  
  end
end
```
Now puma has been started successfully with your app (instance of YourProject::Application) running. 


