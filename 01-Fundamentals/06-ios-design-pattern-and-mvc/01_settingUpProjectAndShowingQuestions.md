# Notes: StoryBoard Linking and Showing the Questions

## Lesson Goal

Set up the project and connect the storyboard UI to the View Controller so that:

* Buttons become interactive.
* Questions can be displayed and updated on the screen.
* The app can progress through multiple quiz questions.

---

## 1. UI Components in Main.storyboard

The interface contains:

1. **Question Label** (top)
2. **True Button**
3. **False Button**
4. **Progress View** (bottom)

---

## 2. Connecting UI Elements to Code

### IBOutlets Created

Used to access UI elements from code:

```swift
@IBOutlet weak var questionLabel: UILabel!
@IBOutlet weak var progressBar: UIProgressView!
@IBOutlet weak var trueButton: UIButton!
@IBOutlet weak var falseButton: UIButton!
```

### IBAction Created

Both buttons are connected to the same action:

```swift
@IBAction func answerButtonPressed(_ sender: UIButton) {
    
}
```

This function runs whenever either the True or False button is pressed.

---

## 3. Displaying a Question on App Launch

### Using `viewDidLoad()`

`viewDidLoad()` is called once when the screen loads.

Example:

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    
    questionLabel.text = "Four + Two is equal to Six."
}
```

Result:

* The placeholder text ("Question Text") is replaced when the app starts.

---

## 4. Storing Questions in an Array

Instead of hardcoding questions:

```swift
let quiz = [
    "Four + Two is equal to Six.",
    "Five - Three is greater than One.",
    "Eight + One is equal to Ten."
]
```

Display the first question:

```swift
questionLabel.text = quiz[0]
```

### Benefits

* Easier to manage multiple questions.
* More dynamic than hardcoded text.

---

## 5. Tracking the Current Question

Create a variable:

```swift
var questionNumber = 0
```

Use it to select the current question:

```swift
questionLabel.text = quiz[questionNumber]
```

---

## 6. Moving to the Next Question

Increase the question number when a button is pressed:

```swift
questionNumber += 1
```

or

```swift
questionNumber = questionNumber + 1
```

### Important Observation

Increasing `questionNumber` alone does **not** update the label because the label text is only set inside `viewDidLoad()`, which runs once.

---

## 7. Creating an `updateUI()` Function

Move the label update code into a reusable function:

```swift
func updateUI() {
    questionLabel.text = quiz[questionNumber]
}
```

Call it whenever the UI needs updating.

### In `viewDidLoad()`

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    updateUI()
}
```

### After Button Press

```swift
@IBAction func answerButtonPressed(_ sender: UIButton) {
    questionNumber += 1
    updateUI()
}
```

Result:

* Questions change each time a button is pressed.

---

## 8. App Crash: "Index Out of Range"

### What Happens?

After the last question:

```swift
quiz[3]
```

is requested.

But the array only contains:

```text
Index 0
Index 1
Index 2
```

Therefore:

```text
Fatal Error: Index out of range
```

The app crashes.

### Why?

`questionNumber` becomes 3, but there is no item at index 3.

---

## 9. Debugging Tips

When the app crashes:

### Check the Highlighted Line

Xcode highlights the line that caused the crash.

### Read the Debug Console

Look at the top of the console for error messages.

Example:

```text
Fatal error: Index out of range
```

### Inspect Variable Values

Use Xcode's variable inspector to see values at the moment of the crash.

Example:

```swift
questionNumber = 3
```

This helps identify why the array access failed.

---

# Key Takeaways

* Use **IBOutlets** to connect UI elements to code.
* Use **IBActions** to respond to user interactions.
* `viewDidLoad()` runs once when the view loads.
* Store questions in an **array** for dynamic content.
* Track the current question using a variable.
* Create an **updateUI()** function to avoid repeating code.
* Always ensure array indexes stay within valid bounds.
* Use Xcode's debugger and console to diagnose crashes.
