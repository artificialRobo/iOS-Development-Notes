## Notes: Refactoring Quiz App with MVC

### 1. Making `checkAnswer()` Return a Value

* The `checkAnswer()` function in `QuizBrain` should return a **Boolean (`Bool`)**.
* Purpose:

  * `true` → user answered correctly.
  * `false` → user answered incorrectly.
* Add a return type and return the appropriate value.

```swift
func checkAnswer(_ userAnswer: String) -> Bool {
    if userAnswer == correctAnswer {
        return true
    } else {
        return false
    }
}
```

### 2. Capturing the Returned Value in ViewController

* When calling `checkAnswer()`, store the returned Boolean in a constant.

```swift
let userGotItRight = quizBrain.checkAnswer(sender.currentTitle!)
```

* Use the Boolean directly in an `if` statement:

```swift
if userGotItRight {
    // Show green color
} else {
    // Show red color
}
```

**Key Idea:**
No need to compare with `true` or `false` explicitly because the variable is already a Boolean.

---

### 3. Prioritize Readability

* Code can often be shortened.
* However, readable code is usually better than overly compact code.
* Consider whether other developers can easily understand your code.

---

### 4. Moving Logic into the Model (`QuizBrain`)

Following MVC, quiz-related logic should live in the model.

#### `getQuestionText()`

* Create a function that returns the current question text.

```swift
func getQuestionText() -> String {
    return quiz[questionNumber].text
}
```

* Use it in `ViewController`:

```swift
questionLabel.text = quizBrain.getQuestionText()
```

---

#### `getProgress()`

* Create a function that returns quiz progress as a `Float`.

```swift
func getProgress() -> Float {
    return Float(questionNumber) / Float(quiz.count)
}
```

* Use it in `ViewController`:

```swift
progressBar.progress = quizBrain.getProgress()
```

---

### 5. Moving Question Progression Logic

* Tracking the next question is quiz functionality.
* Move this responsibility from `ViewController` to `QuizBrain`.

#### Create `nextQuestion()`

```swift
func nextQuestion() {
    // Logic for advancing questionNumber
}
```

#### Call it from ViewController

```swift
quizBrain.nextQuestion()
```

---

### 6. Benefits of MVC Refactoring

The **Model (`QuizBrain`)** now handles:

* Storing quiz questions.
* Checking answers.
* Determining the next question.
* Tracking quiz progress.

The **ViewController** now:

* Updates the UI.
* Delegates quiz-related tasks to the model.

This creates a cleaner separation of responsibilities.

---

### 7. New Issue: Immutability Error

After moving logic into `QuizBrain`, an error appears:

> "Left side of mutating operator isn't mutable: 'self' is immutable"

This happens because the code is trying to modify data in a context where `self` is immutable.

**Next Topic:** Understanding **immutability** and why Swift prevents modifications in certain situations.

---

## Key Takeaways

* Functions can return values using output types.
* Capture returned values and use them in the UI.
* Move business logic into the model to follow MVC.
* Create helper methods like:

  * `getQuestionText()`
  * `getProgress()`
  * `nextQuestion()`
* Keep code readable.
* MVC improves code organization and maintainability.
* Refactoring can reveal issues such as immutability, which must be addressed next.
