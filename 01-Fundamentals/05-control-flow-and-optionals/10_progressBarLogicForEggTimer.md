# Notes: Progress Bar Logic for Egg Timer App

## 1. Progress Bar Basics

* The progress bar uses a **Float** value ranging from:

  * `0.0` = 0% complete (start)
  * `1.0` = 100% complete (finished)
* Example:

  * `0.56` = 56% complete

---

## 2. Problem

* Current code uses `secondsRemaining`, which counts down every second.
* This value cannot directly show progress in the progress bar.
* Need a way to calculate **how much of the total cooking time has elapsed**.

---

## 3. New Approach: Track Time Passed

Instead of:

```swift
secondsRemaining
```

Use:

```swift
totalTime
secondsPassed
```

* `totalTime` = total cooking time for selected egg hardness.
* `secondsPassed` = time elapsed since timer started.

Example:

| Egg Hardness | Total Time                  |
| ------------ | --------------------------- |
| Soft         | 300 sec (3 sec for testing) |
| Medium       | 420 sec (4 sec for testing) |
| Hard         | 720 sec (7 sec for testing) |

---

## 4. Progress Formula

Progress should be calculated as:

[
\text{percentageProgress} = \frac{\text{secondsPassed}}{\text{totalTime}}
]

\text{percentageProgress}=\frac{\text{secondsPassed}}{\text{totalTime}}

Examples:

| Seconds Passed | Total Time | Progress |
| -------------- | ---------- | -------- |
| 0              | 10         | 0.0      |
| 5              | 10         | 0.5      |
| 10             | 10         | 1.0      |

---

## 5. Code Changes

### Variables

Replace:

```swift
var secondsRemaining = 0
```

With:

```swift
var totalTime = 0
var secondsPassed = 0
```

---

### Set Total Time

When a hardness button is selected:

```swift
totalTime = eggTimes[hardness]!
```

---

### Update Timer

Instead of decreasing time:

```swift
secondsRemaining -= 1
```

Increase elapsed time:

```swift
secondsPassed += 1
```

---

### Check If Timer Is Still Running

Replace:

```swift
if secondsRemaining > 0
```

With:

```swift
if secondsPassed < totalTime
```

* Timer continues while elapsed time is less than total time.
* When `secondsPassed == totalTime`, the egg is finished.

---

## 6. Update Progress Bar

Calculate progress:

```swift
let percentageProgress = secondsPassed / totalTime
```

Set progress bar value:

```swift
progressBar.progress = percentageProgress
```

---

## 7. Type Mismatch Issue

Problem:

* `secondsPassed` and `totalTime` are **Integers**.
* `progressBar.progress` requires a **Float**.

Xcode suggests:

```swift
Float(percentageProgress)
```

However, the app still doesn't work correctly because there is a bug in the logic (to be debugged in the next lesson).

---

## Key Takeaways

* Progress bars require values between `0.0` and `1.0`.
* Track **elapsed time** (`secondsPassed`) rather than **remaining time**.
* Calculate progress using:

[
\text{Progress} = \frac{\text{Time Passed}}{\text{Total Time}}
]

* Be careful with **Int vs Float** data types.
* A bug remains due to how the calculation is being performed, which will be solved through debugging in the next lesson.
