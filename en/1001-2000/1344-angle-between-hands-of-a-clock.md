# 1344. Angle Between Hands of a Clock - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [1344. Angle Between Hands of a Clock - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1344-angle-between-hands-of-a-clock) for a better experience!

LeetCode link: [1344. Angle Between Hands of a Clock](https://leetcode.com/problems/angle-between-hands-of-a-clock), difficulty: **Medium**.

## LeetCode description of "1344. Angle Between Hands of a Clock"

Given two numbers, `hour` and `minutes`, return the smaller angle (in degrees) formed between the `hour` and the `minute` hand.

Answers within `10^-5` of the actual value will be accepted as correct.

### [Example 1]

![](../../images/examples/1344_1.png)

**Input**: `hour = 12, minutes = 30`

**Output**: `165`

### [Example 2]

![](../../images/examples/1344_2.png)

**Input**: `hour = 3, minutes = 30`

**Output**: `75`

### [Example 3]

![](../../images/examples/1344_3.png)

**Input**: `hour = 3, minutes = 15`

**Output**: `7.5`

### [Constraints]

- `1 <= hour <= 12`
- `0 <= minutes <= 59`

### [Hints]

<details>
  <summary>Hint 1</summary>
  The tricky part is determining how the minute hand affects the position of the hour hand.

  
</details>

<details>
  <summary>Hint 2</summary>
  Calculate the angles separately then find the difference.

  
</details>

## Intuition

To find the angle between the hour and minute hands, we can calculate the angle of each hand relative to the 12 o'clock position (0 degrees) and then find the absolute difference between these two angles.

First, let's look at the **minute hand**:
The clock has 360 degrees and 60 minutes. Therefore, the minute hand moves `360 / 60 = 6` degrees per minute.
So, the angle of the minute hand is simply `minutes * 6`.

Next, let's consider the **hour hand**:
The clock has 360 degrees and 12 hours. Thus, the hour hand moves `360 / 12 = 30` degrees per hour.
However, the hour hand also moves slightly as the minutes pass! In 60 minutes, it moves 30 degrees, which means it moves `30 / 60 = 0.5` degrees per minute.
So, the angle of the hour hand is `(hour % 12) * 30 + minutes * 0.5`. (We use `hour % 12` because 12 o'clock is the same starting position as 0).

Finally, we calculate the absolute difference between the two angles: `diff = abs(hour_angle - minute_angle)`.

Since the problem asks for the **smaller** angle, and the hands divide the clock into two angles that sum to 360 degrees, we return the minimum of `diff` and `360 - diff`.

## Step-by-Step Solution

1. Calculate the minute hand angle: `minute_angle = minutes * 6.0`.
2. Calculate the hour hand angle: `hour_angle = (hour % 12) * 30.0 + minutes * 0.5`.
3. Find the absolute difference: `diff = abs(hour_angle - minute_angle)`.
4. Return the smaller angle: `min(diff, 360.0 - diff)`.

## Complexity

> - **Time Complexity:** `O(1)`, because we only perform a few basic arithmetic operations.
- **Space Complexity:** `O(1)`, as we only use a few variables to store the angles.

- Time complexity: `O(1)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def angleClock(self, hour: int, minutes: int) -> float:
        # Calculate the angle of the minute hand
        minute_angle = minutes * 6
        
        # Calculate the angle of the hour hand
        hour_angle = (hour % 12) * 30 + minutes * 0.5
        
        # Find the absolute difference between the two angles
        diff = abs(hour_angle - minute_angle)
        
        # Return the smaller angle
        return min(diff, 360 - diff)
```

## Java

```java
class Solution {
    public double angleClock(int hour, int minutes) {
        // Calculate the angle of the minute hand
        double minuteAngle = minutes * 6.0;
        
        // Calculate the angle of the hour hand
        double hourAngle = (hour % 12) * 30.0 + minutes * 0.5;
        
        // Find the absolute difference between the two angles
        double diff = Math.abs(hourAngle - minuteAngle);
        
        // Return the smaller angle
        return Math.min(diff, 360.0 - diff);
    }
}
```

## JavaScript

```javascript
/**
 * @param {number} hour
 * @param {number} minutes
 * @return {number}
 */
var angleClock = function(hour, minutes) {
    // Calculate the angle of the minute hand
    const minuteAngle = minutes * 6;
    
    // Calculate the angle of the hour hand
    const hourAngle = (hour % 12) * 30 + minutes * 0.5;
    
    // Find the absolute difference between the two angles
    const diff = Math.abs(hourAngle - minuteAngle);
    
    // Return the smaller angle
    return Math.min(diff, 360 - diff);
};
```

## C++

```cpp
class Solution {
public:
    double angleClock(int hour, int minutes) {
        // Calculate the angle of the minute hand
        double minute_angle = minutes * 6.0;
        
        // Calculate the angle of the hour hand
        double hour_angle = (hour % 12) * 30.0 + minutes * 0.5;
        
        // Find the absolute difference between the two angles
        double diff = abs(hour_angle - minute_angle);
        
        // Return the smaller angle
        return min(diff, 360.0 - diff);
    }
};
```

## C#

```csharp
public class Solution {
    public double AngleClock(int hour, int minutes) {
        // Calculate the angle of the minute hand
        double minuteAngle = minutes * 6.0;
        
        // Calculate the angle of the hour hand
        double hourAngle = (hour % 12) * 30.0 + minutes * 0.5;
        
        // Find the absolute difference between the two angles
        double diff = Math.Abs(hourAngle - minuteAngle);
        
        // Return the smaller angle
        return Math.Min(diff, 360.0 - diff);
    }
}
```

## Go

```go
import "math"

func angleClock(hour int, minutes int) float64 {
    // Calculate the angle of the minute hand
    minuteAngle := float64(minutes) * 6.0
    
    // Calculate the angle of the hour hand
    hourAngle := float64(hour % 12) * 30.0 + float64(minutes) * 0.5
    
    // Find the absolute difference between the two angles
    diff := math.Abs(hourAngle - minuteAngle)
    
    // Return the smaller angle
    return math.Min(diff, 360.0 - diff)
}
```

## Ruby

```ruby
# @param {Integer} hour
# @param {Integer} minutes
# @return {Float}
def angle_clock(hour, minutes)
    # Calculate the angle of the minute hand
    minute_angle = minutes * 6.0
    
    # Calculate the angle of the hour hand
    hour_angle = (hour % 12) * 30.0 + minutes * 0.5
    
    # Find the absolute difference between the two angles
    diff = (hour_angle - minute_angle).abs
    
    # Return the smaller angle
    [diff, 360.0 - diff].min
end
```

## Rust

```rust
impl Solution {
    pub fn angle_clock(hour: i32, minutes: i32) -> f64 {
        // Calculate the angle of the minute hand
        let minute_angle = (minutes as f64) * 6.0;
        
        // Calculate the angle of the hour hand
        let hour_angle = ((hour % 12) as f64) * 30.0 + (minutes as f64) * 0.5;
        
        // Find the absolute difference between the two angles
        let diff = (hour_angle - minute_angle).abs();
        
        // Return the smaller angle
        diff.min(360.0 - diff)
    }
}
```

## Kotlin

```kotlin
import kotlin.math.*

class Solution {
    fun angleClock(hour: Int, minutes: Int): Double {
        // Calculate the angle of the minute hand
        val minuteAngle = minutes * 6.0
        
        // Calculate the angle of the hour hand
        val hourAngle = (hour % 12) * 30.0 + minutes * 0.5
        
        // Find the absolute difference between the two angles
        val diff = abs(hourAngle - minuteAngle)
        
        // Return the smaller angle
        return min(diff, 360.0 - diff)
    }
}
```

## Swift

```swift
class Solution {
    func angleClock(_ hour: Int, _ minutes: Int) -> Double {
        // Calculate the angle of the minute hand
        let minuteAngle = Double(minutes) * 6.0
        
        // Calculate the angle of the hour hand
        let hourAngle = Double(hour % 12) * 30.0 + Double(minutes) * 0.5
        
        // Find the absolute difference between the two angles
        let diff = abs(hourAngle - minuteAngle)
        
        // Return the smaller angle
        return min(diff, 360.0 - diff)
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [1344. Angle Between Hands of a Clock - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1344-angle-between-hands-of-a-clock) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

