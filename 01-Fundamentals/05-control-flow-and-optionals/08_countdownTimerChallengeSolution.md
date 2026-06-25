# Notes: Egg Timer Challenge Solution (Swift)

## 1. Goal of the Previous Challenge

Create an egg timer where:

* **Soft** = 300 seconds (5 minutes)
* **Medium** = 420 seconds (7 minutes)
* **Hard** = 720 seconds (12 minutes)

When a button is pressed, a countdown starts and updates every second.

---

## 2. Converting Time to Seconds

Since the timer updates every second, all cooking times are stored in seconds.

```swift
var secondsRemaining = 0
```

When a user selects an egg hardness:

```swift
secondsRemaining = eggTimes[hardness]
```

The value assigned will be:

* Soft → 300
* Medium → 420
* Hard → 720

---

## 3. Creating a Timer

A timer is created using:

```swift
Timer.scheduledTimer(
    timeInterval: 1.0,
    target: self,
    selector: #selector(updateTimer),
    userInfo: nil,
    repeats: true
)
```

### Important Parameters

* **timeInterval: 1.0**

  * Timer fires every 1 second.

* **repeats: true**

  * Timer continues running instead of stopping after one execution.

* **selector**

  * Specifies which function is called whenever the timer fires.

---

## 4. Using `@objc`

The timer uses Objective-C selectors.

Therefore the function must be marked with:

```swift
@objc func updateTimer() {
}
```

Without `@objc`, Swift will show an error because selectors require Objective-C compatibility.

---

## 5. Countdown Logic

The timer calls `updateTimer()` every second.

```swift
@objc func updateTimer() {
    if secondsRemaining > 0 {
        print(secondsRemaining)
        secondsRemaining -= 1
    }
}
```

### How It Works

1. Check if time remains.
2. Print current value.
3. Subtract 1 second.
4. Repeat every second.

This creates the countdown effect.

---

## 6. Bug: Timer Speeds Up

### Problem

If the user:

1. Presses Soft
2. Then presses Medium
3. Then presses Hard

The countdown becomes faster and faster.

### Why?

Every button press creates a **new timer**, but the old timer is never stopped.

Example:

* 1 button press → 1 timer running
* 2 button presses → 2 timers running
* 3 button presses → 3 timers running

As a result, `updateTimer()` gets called multiple times per second.

---

## 7. Fixing the Bug

Create a timer variable:

```swift
var timer = Timer()
```

Before starting a new timer:

```swift
timer.invalidate()
```

Then create a new timer.

### Result

* Old timer stops.
* New timer starts.
* Countdown always decreases at the correct speed (1 second per second).

---

## 8. Challenge: Show "DONE!"

### Objective

When the countdown reaches zero:

* Stop the timer.
* Change the title label text to `"DONE!"`.

---

## 9. Create an Outlet

Connect the title label from Storyboard:

```swift
@IBOutlet weak var titleLabel: UILabel!
```

This allows code to modify the label text.

---

## 10. Using an Else Statement

Update the timer function:

```swift
@objc func updateTimer() {

    if secondsRemaining > 0 {
        secondsRemaining -= 1
    } else {
        timer.invalidate()
        titleLabel.text = "DONE!"
    }
}
```

### What Happens?

When `secondsRemaining` becomes 0:

1. Timer stops.
2. Label text changes to `"DONE!"`.

Example output:

```
3
2
1
DONE!
```

---

## 11. Testing Tip

To avoid waiting several minutes during testing, temporarily change:

```swift
"Soft": 3
"Medium": 4
"Hard": 7
```

This makes it much faster to verify that the timer and `"DONE!"` message work correctly.

---

## Key Takeaways

* Store cooking times in **seconds**.
* Use `Timer.scheduledTimer()` for repeated actions.
* Mark timer functions with **`@objc`**.
* Decrease `secondsRemaining` every second.
* Always call **`timer.invalidate()`** before creating a new timer.
* Use an **IBOutlet** to update UI elements.
* Display **"DONE!"** when the countdown reaches zero and stop the timer.
