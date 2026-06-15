## Notes: 2D Arrays and Quiz Answer Checking in Swift

### 1. Goal of the Lesson

* Add answer checking to a quiz app.
* Learn how to use **two-dimensional (2D) arrays** in Swift.
* Prevent app crashes when reaching the end of the quiz.
* Prepare for a cleaner data structure using Swift structs.

---

## 2. Why Use a 2D Array?

Each quiz question needs:

1. The question text
2. The correct answer

A 2D array allows related data to be grouped together:

```swift
let quiz = [
    ["4 + 2 = 6", "True"],
    ["5 - 3 > 1", "True"],
    ["3 + 8 < 10", "False"]
]
```

* Outer array = collection of quiz items.
* Inner arrays = individual question-answer pairs.

---

## 3. Accessing Elements in a 2D Array

### Syntax

```swift
array[outerIndex][innerIndex]
```

* First index selects the inner array.
* Second index selects an item within that array.

### Example

```swift
let numbers = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

To get `9`:

```swift
numbers[2][2]
```

---

## 4. Retrieving Quiz Questions

Assume:

```swift
var questionNumber = 0
```

Get the current question:

```swift
let quizQuestion = quiz[questionNumber][0]
```

* `questionNumber` selects the current question array.
* `[0]` selects the question text.

---

## 5. Getting the User's Answer

When a button is pressed:

```swift
let userAnswer = sender.currentTitle
```

This returns:

```swift
"True"
```

or

```swift
"False"
```

---

## 6. Retrieving the Correct Answer

```swift
let actualAnswer = quiz[questionNumber][1]
```

* `[1]` accesses the answer stored in the question-answer pair.

---

## 7. Checking if the Answer is Correct

```swift
if userAnswer == actualAnswer {
    print("Right!")
} else {
    print("Wrong!")
}
```

### Logic

* If user's answer matches the stored answer → Correct.
* Otherwise → Incorrect.

---

## 8. The Crash Problem

After the last question:

```swift
questionNumber += 1
```

The app tries to access:

```swift
quiz[3]
```

But only indices `0, 1, 2` exist.

Result:

```text
Index out of range
```

App crashes.

---

## 9. Preventing the Crash

### Incorrect Check

```swift
if questionNumber < quiz.count {
    questionNumber += 1
}
```

Problem:

* When `questionNumber = 2`
* `2 < 3` is true
* It becomes `3`
* Crash occurs.

### Correct Check

```swift
if questionNumber + 1 < quiz.count {
    questionNumber += 1
}
```

This prevents `questionNumber` from exceeding the last valid index.

---

## 10. Restarting the Quiz

Instead of stopping at the end, loop back to the beginning.

```swift
if questionNumber + 1 < quiz.count {
    questionNumber += 1
} else {
    questionNumber = 0
}
```

### Result

```text
Question 1
Question 2
Question 3
Question 1
Question 2
...
```

Creates an endless quiz loop.

---

## 11. Drawback of the 2D Array

A 2D array is:

* Hard to read
* Hard to maintain
* Less descriptive

Example:

```swift
["4 + 2 = 6", "True"]
```

It's not immediately obvious what each item represents.

---

## 12. Better Solution: Swift Structures

Create a custom type:

```swift
struct Question {
    let title: String
    let answer: String
}
```

Then use:

```swift
let quiz = [
    Question(title: "4 + 2 = 6", answer: "True"),
    Question(title: "5 - 3 > 1", answer: "True"),
    Question(title: "3 + 8 < 10", answer: "False")
]
```

### Benefits

* More readable
* Easier to understand
* Better organization
* More scalable for larger apps

---

## Key Takeaways

* A **2D array** stores arrays inside another array.
* Access elements using `array[row][column]`.
* Store quiz questions and answers together in inner arrays.
* Compare `userAnswer` with `actualAnswer` using an `if` statement.
* Prevent crashes by checking array bounds before increasing the index.
* Use an `else` statement to restart the quiz.
* For cleaner code, replace 2D arrays with **Swift structs**.
