# Notes: Randomization of images in the Dicee app

## 1. Removing Unnecessary Code

* The app no longer needs code inside `viewDidLoad`.
* Since nothing happens when the view loads, that block can be deleted.
* This simplifies the codebase.

---

## 2. Shorter Assignment Operators in Swift

Instead of writing:

```swift
leftDiceNumber = leftDiceNumber + 1
```

You can write:

```swift
leftDiceNumber += 1
```

### Similar Operators

* `+=` → add and assign
* `-=` → subtract and assign
* `*=` → multiply and assign
* `/=` → divide and assign

### Example

```swift
score += 1
lives -= 1
```

These operators make code shorter and cleaner.

---

## 3. Problem: App Crashes

### Why?

The dice images are stored in an array with indexes:

```swift
0...5
```

If the app tries to access:

```swift
diceArray[6]
```

the app crashes because index 6 does not exist.

---

## 4. Generating Random Numbers in Swift

### Syntax

```swift
Int.random(in: 1...10)
```

### Explanation

* `Int` → whole number type
* `.random` → generates a random value
* `1...10` → range operator
* Includes both 1 and 10

---

## 5. Using Random Numbers for Dice

Since the dice images are stored from index `0` to `5`:

```swift
Int.random(in: 0...5)
```

This safely selects a random image from the array.

### Result

* App no longer crashes
* Dice rolls become truly random

---

## 6. Refactoring Code

### Refactoring

Improving code structure without changing functionality.

Goals:

* Remove repetition
* Simplify code
* Improve readability

---

## 7. Creating a Shared Dice Array

Instead of duplicating the same array multiple times:

```swift
let diceArray = [
    #imageLiteral(resourceName: "DiceOne"),
    #imageLiteral(resourceName: "DiceTwo"),
    ...
]
```

Then reuse it:

```swift
diceImageView.image = diceArray[Int.random(in: 0...5)]
```

Benefits:

* Less duplication
* Cleaner code
* Easier maintenance

---

## 8. Swift Style Rule: Spacing Around `=`

Good:

```swift
let score = 0
```

Bad:

```swift
let score= 0
```

Swift prefers symmetric spacing around operators.

---

## 9. Xcode Warnings vs Errors

### Warning (Yellow Triangle)

* App can still run
* Something might be wrong

### Error (Red Stop Sign)

* App cannot run until fixed

### White Dot in Warning/Error

* Xcode suggests an automatic fix

Important:

* Understand the fix before clicking it
* Xcode suggestions are not always correct

---

## 10. `var` vs `let`

### `var`

Used when a value can change.

Example:

```swift
var score = 0
score += 1
```

### `let`

Used when a value should never change.

Example:

```swift
let diceArray = [...]
```

Since `diceArray` never changes, it should be a constant (`let`).

---

## 11. Why Use `let`?

Benefits:

* Safer code
* Prevents accidental changes
* Removes Xcode warnings

If you try to modify a `let` constant:

```swift
diceArray = []
```

Swift gives an error.

---

## 12. Easier Random Selection with `.randomElement()`

Instead of:

```swift
diceArray[Int.random(in: 0...5)]
```

You can use:

```swift
diceArray.randomElement()
```

### Advantage

* Simpler
* Automatically handles array size
* Cleaner syntax

---

## Key Concepts Learned

* Refactoring code
* Random number generation
* Range operator (`...`)
* Arrays
* Constants vs variables (`let` vs `var`)
* Assignment operators (`+=`, `-=`)
* Xcode warnings/errors
* `.randomElement()`

---

## Main Takeaway

The dice app was improved by:

1. Making dice rolls random
2. Preventing crashes
3. Reducing repeated code
4. Using constants appropriately
5. Refactoring for cleaner, more maintainable code
