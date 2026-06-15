## Notes: Applying MVC to the Quiz App and Understanding Parameter Names

### 1. Organizing the Project into MVC

The project is restructured into three groups:

* **Model**

  * Contains `Question.swift`
  * Stores quiz data and business logic

* **View**

  * Contains `Main.storyboard`
  * Responsible for displaying the UI

* **Controller**

  * Contains `ViewController.swift`
  * Manages communication between the Model and View

---

### 2. Responsibilities of the Controller

The `ViewController` should:

* Handle user interactions
* Tell the View what to display
* Fetch data from the Model
* Instruct the Model to update itself

The controller **should not contain quiz data or quiz logic**.

---

### 3. Creating the QuizBrain Model

A new Swift file called **QuizBrain.swift** is created inside the Model folder.

```swift
struct QuizBrain {
}
```

Purpose:

* Acts as the "brain" of the quiz
* Contains quiz data
* Handles quiz logic

---

### 4. Moving Data into QuizBrain

Move the following from `ViewController.swift` to `QuizBrain.swift`:

* `quiz` array
* `questionNumber` variable

Benefits:

* Keeps quiz-related data inside the Model
* Makes the controller cleaner

---

### 5. Creating an Instance of QuizBrain

Inside `ViewController.swift`:

```swift
var quizBrain = QuizBrain()
```

This allows the controller to access quiz data and functionality through the model.

---

### 6. Moving Answer Checking Logic

Previously, `answerPressed()` handled:

1. Checking answers
2. Moving to the next question

To follow MVC, answer checking is moved to `QuizBrain`.

---

### 7. Creating the `checkAnswer()` Method

Inside `QuizBrain`:

```swift
func checkAnswer(_ userAnswer: String) {
    // Check answer
}
```

This method receives the user's selected answer and performs the answer validation.

---

### 8. Calling the Method from ViewController

Instead of checking answers directly:

```swift
quizBrain.checkAnswer(userAnswer)
```

The controller delegates the task to the model.

---

### 9. Parameters vs Arguments

**Parameter**

* Variable defined in the function declaration

```swift
func checkAnswer(_ userAnswer: String)
```

`userAnswer` is a parameter.

**Argument**

* Actual value passed into the function

```swift
quizBrain.checkAnswer(userAnswer)
```

The value of `userAnswer` is the argument.

---

### 10. External and Internal Parameter Names

Swift supports both:

```swift
func checkAnswer(answer userAnswer: String)
```

* External name: `answer`
* Internal name: `userAnswer`

Called as:

```swift
checkAnswer(answer: userAnswer)
```

Using `_` removes the external name:

```swift
func checkAnswer(_ userAnswer: String)
```

Called as:

```swift
checkAnswer(userAnswer)
```

---

### 11. Handling Optional Strings

`currentTitle` returns an optional string:

```swift
sender.currentTitle
```

Since the buttons always have titles, force unwrap it:

```swift
let userAnswer = sender.currentTitle!
```

This converts it to a regular `String`.

---

### 12. Comparing Answers

Inside `QuizBrain`:

```swift
if userAnswer == quiz[questionNumber].answer {
    // Correct answer
} else {
    // Wrong answer
}
```

The user's answer is compared with the correct answer for the current question.

---

### 13. MVC Challenge Encountered

Problem:

* Answer checking now occurs inside `QuizBrain` (Model).
* UI updates (button colors, etc.) must happen in `ViewController` (Controller/View).

Question:

How can `QuizBrain` communicate the result of answer checking back to `ViewController`?

**Solution preview:** Use functions that return outputs (return values), which will be covered in the next lesson.

---

## Key Takeaways

* MVC separates data, UI, and control logic.
* `QuizBrain` becomes the Model for quiz data and logic.
* `ViewController` should coordinate between Model and View, not contain business logic.
* Methods can use parameters, arguments, and optional external parameter names.
* Force unwrapping is acceptable when a value is guaranteed to exist.
* Returning values from functions helps Models communicate results back to Controllers.
