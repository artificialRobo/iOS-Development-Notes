## Notes: Using Mutating Functions to track the Score

### 1. Why the Error Happened

* `QuizBrain` is a **struct**.
* Properties inside a struct (e.g., `questionNumber`, `score`) belong to the struct instance.
* Struct properties cannot be modified from a method unless that method is marked with `mutating`.
* When trying to update `questionNumber` in `nextQuestion()`, Xcode generated an error because the method was changing a property without being declared as `mutating`.

**Example:**

```swift
mutating func nextQuestion() {
    questionNumber += 1
}
```

### 2. Types of Methods in a Struct

#### Non-mutating Methods

* Do not change any properties.
* Simply return values or perform calculations.

Example:

```swift
func getProgress() -> Float
```

#### Mutating Methods

* Modify one or more properties of the struct.
* Must be marked with the `mutating` keyword.

Example:

```swift
mutating func nextQuestion()
```

### 3. Benefits of Moving Logic into `QuizBrain`

The app's quiz logic was moved from the `ViewController` into a separate `QuizBrain` model.

#### ViewController Responsibilities

* Handles UI updates.
* Communicates with the model (`QuizBrain`).
* Updates button colors, labels, and screen content.

#### QuizBrain Responsibilities

* Provides questions.
* Checks answers.
* Tracks quiz progress.
* Manages quiz state.

This separation follows the **MVC (Model-View-Controller)** design pattern.

### 4. MVC Design Pattern

#### Model (`QuizBrain`)

* Stores quiz data.
* Contains quiz-related logic.

#### View

* User interface elements (buttons, labels, etc.).

#### Controller (`ViewController`)

* Connects the Model and View.
* Requests data from the model.
* Updates the UI based on model data.

**Benefits:**

* Cleaner code.
* Easier maintenance.
* Better reusability.
* More modular structure.

---

## Challenge: Add Score Tracking

### Goal

Display and manage the user's score.

### UI Changes

1. Add a new label at the top of the stack view.
2. Change its text color to white.
3. Create an IBOutlet:

```swift
@IBOutlet weak var scoreLabel: UILabel!
```

### Update the UI

Inside `updateUI()`:

```swift
scoreLabel.text = "Score: \(quizBrain.getScore())"
```

---

## Implementing Score Tracking in `QuizBrain`

### Step 1: Create a Score Variable

```swift
var score = 0
```

* Similar to `questionNumber`.
* Starts at zero.

### Step 2: Increase Score When Answer Is Correct

Inside `checkAnswer()`:

```swift
mutating func checkAnswer(_ userAnswer: String) -> Bool {
    if userAnswer == quiz[questionNumber].answer {
        score += 1
        return true
    }
    return false
}
```

### Important

* Since `score` is modified, `checkAnswer()` must be marked as `mutating`.

---

### Step 3: Create `getScore()`

```swift
func getScore() -> Int {
    return score
}
```

Purpose:

* Allows the ViewController to retrieve the current score.

---

### Step 4: Reset Score When Quiz Restarts

When the quiz reaches the end:

```swift
questionNumber = 0
score = 0
```

This ensures:

* Quiz restarts from the beginning.
* Score returns to zero.

---

## Result

* Score starts at **0**.
* Correct answers increase score by **1**.
* Wrong answers do not affect score.
* Score resets when the quiz restarts.
* Errors disappear because `getScore()` now exists.

---

## Optional Challenge: Multiple Choice Quiz

### Task

Replace the current true/false questions with multiple-choice questions.

### Expected Changes

* Display **three answer options** instead of two.
* Allow the user to select one of three answers.
* Update the UI and logic to support multiple-choice questions.

### Learning Objective

Practice modifying only the **Model (`QuizBrain`)** and related components while maintaining the MVC architecture.

---

## Key Takeaways

* Use `mutating` when a struct method changes its properties.
* Keep business logic inside the **Model**.
* The **Controller** should only coordinate between the Model and View.
* MVC improves organization, readability, and maintainability.
* Score tracking belongs in `QuizBrain`, not `ViewController`.
