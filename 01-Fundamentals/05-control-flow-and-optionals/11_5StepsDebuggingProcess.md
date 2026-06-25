# Notes: Debugging Process (5 Steps Process)

## 1. What did you expect the code to do?

* When a button (Soft, Medium, Hard) is pressed:

  * The timer should count down.
  * The progress bar should gradually fill up.
  * For example, the Soft egg (3 seconds) should update progress every second until complete.

## 2. What actually happened?

* Pressing any button immediately reset the progress bar to **0**.
* The progress bar never advanced as expected.

## 3. What does the expectation depend on?

The progress calculation:

```swift
percentageProgress = secondsPassed / totalTime
```

Expected values for a 3-second timer:

* 0 / 3 = 0.0
* 1 / 3 = 0.333...
* 2 / 3 = 0.666...
* 3 / 3 = 1.0

The progress bar relies on:

* `secondsPassed` increasing every second.
* `totalTime` remaining constant.
* The division producing **decimal values**.

---

## 4. How can we test our assumptions?

Use print statements:

```swift
print(percentageProgress)
print(Float(percentageProgress))
```

Output:

```text
0
0.0
0
0.0
0
0.0
```

This showed the calculation was always returning **0**.

---

### Root Cause: Integer Division

Example:

```swift
let a = 5
let b = 2

Float(a / b)
```

Output:

```swift
2.0
```

Why?

1. `a / b` happens first.
2. Since both are integers, Swift performs **integer division**.
3. `5 / 2 = 2`
4. Then `2` is converted to `2.0`.

---

### Correct Solution

Convert values to `Float` **before dividing**:

```swift
Float(a) / Float(b)
```

Output:

```swift
2.5
```

---

## 5. Fix the Code

Incorrect:

```swift
Float(secondsPassed / totalTime)
```

Correct:

```swift
Float(secondsPassed) / Float(totalTime)
```

Now the progress values become:

```text
0.0
0.3333
0.6666
1.0
```

and the progress bar updates correctly.

---

## Second Bug: Progress Bar Stops at 2/3

### Problem

The progress bar never reached 100%.

Reason:

```swift
if secondsPassed < totalTime
```

The maximum value of `secondsPassed` before stopping was `2`, so:

```swift
2 / 3 = 0.666
```

The progress bar stopped at two-thirds.

---

### Fix

Move the increment statement before calculating progress:

```swift
secondsPassed += 1
```

This allows:

```text
1/3
2/3
3/3
```

Result:

```text
0.333
0.666
1.0
DONE!
```

---

## Final Cleanup

Remove debugging print statements.

### Reset Progress Bar

When a new hardness button is selected:

```swift
progressBar.progress = 0.0
secondsPassed = 0
```

This ensures every timer starts from the beginning.

---

### Reset Title Label

After completion, the label shows:

```text
DONE!
```

When a new egg type is selected, reset it:

```swift
titleLabel.text = hardness
```

This displays the currently selected egg hardness.

---

## Final App Behavior

### Soft Egg

* Runs for 3 seconds
* Progress bar fills completely
* Displays "DONE!"

### Medium Egg

* Runs for 4 seconds

### Hard Egg

* Runs for 7 seconds

---

## Key Takeaways

* Follow the **5-step debugging process**:

  1. Define expectations.
  2. Observe actual behavior.
  3. Identify dependencies.
  4. Test assumptions with debugging tools (`print`).
  5. Fix the code.

* Integer division truncates decimals:

  ```swift
  5 / 2 = 2
  ```

* Convert operands before division:

  ```swift
  Float(a) / Float(b)
  ```

* Use print statements strategically to inspect variable values.

* Reset UI state (progress bar, timer, labels) when restarting functionality.

### Challenge

Add an alarm sound that plays when the timer reaches completion (`DONE!`) using the sound-playing techniques learned in the Xylophone app project.
