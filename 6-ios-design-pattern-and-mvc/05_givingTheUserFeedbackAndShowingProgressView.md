## Notes: Visual Feedback, Timer Delay & Progress Bar

### 1. Replacing Debug Prints with Visual Feedback

**Problem:**
`print()` statements showing whether an answer is correct are only visible to developers.

**Solution:**
Change the background color of the button the user taps:

```swift
sender.backgroundColor = .green   // Correct answer
sender.backgroundColor = .red     // Wrong answer
```

* `sender` refers to the button that was pressed.
* `.green` and `.red` are built-in `UIColor` values.

---

### 2. Resetting Button Colors

**Issue:**
Once a button turns green or red, the color remains on screen.

**Fix:**
Reset both button colors inside `updateUI()`:

```swift
trueButton.backgroundColor = .clear
falseButton.backgroundColor = .clear
```

This ensures the buttons return to their default appearance whenever the next question loads.

---

### 3. Why the Color Disappeared

**Problem:**
After adding the reset code, the colors no longer appear.

**Cause:**
`updateUI()` is called immediately after changing the button color.

Sequence:

1. Button turns green/red.
2. `updateUI()` runs instantly.
3. Button color resets to `.clear`.

The color changes so quickly that users never see it.

---

### 4. Adding a 0.2-Second Delay

**Goal:**
Show the green/red color briefly before resetting.

**Solution:**
Use a timer:

```swift
Timer.scheduledTimer(
    timeInterval: 0.2,
    target: self,
    selector: #selector(updateUI),
    userInfo: nil,
    repeats: false
)
```

Key points:

* `timeInterval: 0.2` → waits 0.2 seconds.
* `selector` → calls `updateUI()` after the delay.
* `repeats: false` → timer runs only once.
* No variable needed because the timer does not repeat.

---

### 5. Objective-C Annotation Requirement

Because selectors rely on Objective-C, mark `updateUI()` with:

```swift
@objc func updateUI() {
    ...
}
```

Without `@objc`, the selector will not work.

---

### 6. Implementing the Progress Bar

The app already has a `UIProgressView` connected via:

```swift
@IBOutlet weak var progressBar: UIProgressView!
```

Update the progress bar inside `updateUI()`:

```swift
progressBar.progress =
    Float(questionNumber + 1) / Float(quiz.count)
```

---

### 7. Why Convert to Float?

`progress` expects a value between **0.0 and 1.0**.

Both values must be converted before division:

```swift
Float(questionNumber + 1)
Float(quiz.count)
```

Avoid:

```swift
Float(questionNumber / quiz.count) // Incorrect
```

because integer division occurs first.

---

### 8. Why Add 1 to `questionNumber`?

`questionNumber` starts at `0`.

Without adding 1:

```swift
0 / totalQuestions = 0
```

The progress bar starts empty.

Using:

```swift
questionNumber + 1
```

means the first question already shows some progress, representing that the user is currently on Question 1.

---

## Key Takeaways

* Use button colors instead of debug prints for user feedback.
* Reset button colors in `updateUI()`.
* Add a short timer delay so users can see feedback.
* Use `@objc` when calling methods through a selector.
* Update progress with:

```swift
progressBar.progress =
    Float(questionNumber + 1) / Float(quiz.count)
```

* Convert integers to `Float` before division.
* Add `1` to `questionNumber` so progress starts visibly and reaches 100% on the last question.
