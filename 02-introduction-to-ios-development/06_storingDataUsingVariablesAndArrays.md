# Notes: Storing Data using Variables and Arrays

## Current App Behavior

* The app changes dice images only when it loads.
* Pressing the **Roll** button currently shows fixed dice faces.
* Goal: make the dice images change every time the button is pressed.

---

# Arrays in Swift

## What is an Array?

* An **Array** is an ordered collection of items.
* In this app, the array stores all six dice images.

Example:

```swift
let diceArray = [
    #imageLiteral(resourceName: "DiceOne"),
    #imageLiteral(resourceName: "DiceTwo"),
    #imageLiteral(resourceName: "DiceThree"),
    #imageLiteral(resourceName: "DiceFour"),
    #imageLiteral(resourceName: "DiceFive"),
    #imageLiteral(resourceName: "DiceSix")
]
```

---

# Types of Brackets in Swift

| Bracket Type | Purpose                                     |
| ------------ | ------------------------------------------- |
| `()`         | Round brackets for functions/parameters     |
| `{}`         | Curly brackets for code blocks              |
| `[]`         | Square brackets for collections like Arrays |

---

# Accessing Array Items

## Array Indexing

* Arrays use **index positions**.
* Swift starts counting from **0**.

| Position | Image     |
| -------- | --------- |
| 0        | DiceOne   |
| 1        | DiceTwo   |
| 2        | DiceThree |
| 3        | DiceFour  |
| 4        | DiceFive  |
| 5        | DiceSix   |

Example:

```swift
diceImageView1.image = diceArray[1]
```

* Displays the second image (`DiceTwo`).

---

# Variables

## Creating a Variable

Variables store data that can change.

Example:

```swift
var leftDiceNumber = 1
```

* `var` creates a variable.
* `leftDiceNumber` stores the current dice position.

Using it:

```swift
diceImageView1.image = diceArray[leftDiceNumber]
```

---

# Updating Variable Values

## Increasing the Dice Number

```swift
leftDiceNumber = leftDiceNumber + 1
```

What happens:

1. Show current image.
2. Increase number by 1.
3. Next button press shows the next image.

---

# Program Flow Example

### First Press

* `leftDiceNumber = 1`
* Shows DiceTwo
* Then becomes `2`

### Second Press

* `leftDiceNumber = 2`
* Shows DiceThree
* Then becomes `3`

And so on.

---

# Array Out of Range Error

Problem:

* After index `5`, there is no next image.
* Accessing beyond the array size crashes the app.

This is called:

* **Out of Range Error**

---

# Variable Scope

## Wrong Placement

If the variable is created inside the button action:

```swift
@IBAction func rollButtonPressed(_ sender: UIButton) {
    var leftDiceNumber = 1
}
```

Then:

* It resets to `1` every button press.
* The image never changes properly.

---

## Correct Placement

Create variables outside the function:

```swift
var leftDiceNumber = 1
```

Benefits:

* Value is remembered between button presses.
* App can track changes over time.

---

# Using Print Statements for Debugging

Example:

```swift
print(leftDiceNumber)
```

Better version with string interpolation:

```swift
print("leftDiceNumber at beginning = \(leftDiceNumber)")
```

Useful for:

* Tracking variable changes
* Finding bugs
* Understanding program flow

---

# Right Dice Challenge

## Goal

* Left dice increases
* Right dice decreases

---

# Right Dice Variable

```swift
var rightDiceNumber = 5
```

Display image:

```swift
diceImageView2.image = diceArray[rightDiceNumber]
```

Decrease value:

```swift
rightDiceNumber = rightDiceNumber - 1
```

---

# Final Behavior

When pressing Roll:

* Left dice counts upward:

  * 2 → 3 → 4 → 5 → 6
* Right dice counts downward:

  * 6 → 5 → 4 → 3 → 2

Eventually:

* App crashes when indices go out of range.

---

# Key Concepts Learned

## Arrays

* Ordered collections
* Access items using indexes

## Indexing

* Starts from `0`

## Variables

* Store changeable values
* Use `var`

## Scope

* Variables outside functions retain values

## Debugging

* Use `print()` statements
* String interpolation improves readability

## Updating UI

* Image views can change dynamically using arrays and variables
