# Notes: Using Structures (`struct`) for Quiz Questions in Swift

## Why Use a Structure?

* Replaces a **2D array** with a more organized and readable data model.
* Makes code easier to understand, maintain, and extend.
* Each quiz question becomes an object with clearly named properties.

---

## Creating a Structure

### 1. Create a New Swift File

* Create a new Swift file named **Question.swift**.
* Convention: File name should match the structure name.

### 2. Define the Structure

```swift
struct Question {
    let text: String
    let answer: String
}
```

### Properties

* `text` → Stores the question.
* `answer` → Stores the correct answer.
* Both are constants (`let`) of type `String`.

---

## Creating Question Objects

Instead of:

```swift
["A slug's blood is green.", "True"]
```

Use:

```swift
Question(text: "A slug's blood is green.", answer: "True")
```

### Quiz Array

```swift
let quiz = [
    Question(text: "A slug's blood is green.", answer: "True"),
    Question(text: "Approximately one quarter of human bones are in the feet.", answer: "True")
]
```

### Benefits

* More readable.
* Clearly shows each question's text and answer.
* Avoids confusing index-based access in a 2D array.

---

## Accessing Structure Properties

### Direct Access

```swift
quiz[questionNumber].answer
```

### Using an Intermediate Variable

```swift
let actualQuestion = quiz[questionNumber]
actualQuestion.text
actualQuestion.answer
```

This makes it easier to inspect and understand the data.

---

## Updating Existing Code

### Old 2D Array Access

```swift
quiz[questionNumber][1]
```

### New Structure Access

```swift
quiz[questionNumber].answer
```

### Updating the Question Label

```swift
questionLabel.text = quiz[questionNumber].text
```

---

## Custom Initializer

To reduce typing, create a custom initializer:

```swift
struct Question {
    let text: String
    let answer: String

    init(q: String, a: String) {
        text = q
        answer = a
    }
}
```

### Usage

```swift
Question(q: "A slug's blood is green.", a: "True")
```

### Advantages

* Shorter syntax.
* Cleaner and more concise code.

---

## Final Improvements

* Replace all practice questions with the predefined quiz questions from the README.
* The completed quiz contains **12 question items**.
* App functionality remains the same, but the code is:

  * More organized
  * Easier to read
  * Easier to expand with additional structures

---

## Key Takeaways

1. Use `struct` to model related data.
2. Store question data in properties (`text`, `answer`).
3. Replace 2D arrays with an array of `Question` objects.
4. Access data using dot notation (`.text`, `.answer`).
5. Custom initializers can make object creation cleaner.
6. Structured code improves readability and maintainability.
