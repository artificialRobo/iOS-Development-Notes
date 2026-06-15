## Notes: Creating a Typing Animation in Swift Using Loops and Timers

### Objective

Create a typing animation where the characters of a title label appear one by one, similar to someone typing text on the screen.

---

## 1. Understanding Loops

A **for-in loop** allows you to iterate through every item in a collection.

### Example with an Array

```swift
let fruitBasket = ["Apple", "Pear", "Orange"]

for fruit in fruitBasket {
    print(fruit)
}
```

**Output:**

```
Apple
Pear
Orange
```

* The loop runs once for each item in the array.
* The code inside the loop executes repeatedly.

---

## 2. Looping Through a String

Strings can also be looped through character by character.

```swift
let titleText = "⚡️FlashChat"

for letter in titleText {
    print(letter)
}
```

**Output:**

```
⚡️
F
l
a
s
h
C
h
a
t
```

Each character is processed individually.

---

## 3. Displaying Characters in a Label

Start with an empty label:

```swift
titleLabel.text = ""
```

Append each character:

```swift
for letter in titleText {
    titleLabel.text?.append(letter)
}
```

### Problem

The text appears instantly because the loop executes extremely fast (within a fraction of a second).

---

## 4. Using a Timer for Delays

To create a typing effect, add a delay before displaying each character.

### Timer Syntax

```swift
Timer.scheduledTimer(withTimeInterval: 0.1, repeats: false) { timer in
    self.titleLabel.text?.append(letter)
}
```

### Notes

* `withTimeInterval: 0.1` = wait 0.1 seconds.
* `repeats: false` = run only once.
* `self` is required because the code is inside a closure.

---

## 5. Why the First Attempt Doesn't Work

Inside the loop, every timer is scheduled with the **same delay (0.1 seconds)**.

Example:

* Emoji timer → 0.1 sec
* F timer → 0.1 sec
* L timer → 0.1 sec

Result: all characters appear at nearly the same time.

---

## 6. Adding Incremental Delays

Create a variable to track the character position:

```swift
var characterIndex = 0.0
```

Use it to increase the delay for each character:

```swift
for letter in titleText {

    Timer.scheduledTimer(withTimeInterval: 0.1 * characterIndex,
                         repeats: false) { timer in
        self.titleLabel.text?.append(letter)
    }

    characterIndex += 1
}
```

### Delay Timeline

| Character | Delay   |
| --------- | ------- |
| ⚡️        | 0.0 sec |
| F         | 0.1 sec |
| l         | 0.2 sec |
| a         | 0.3 sec |
| s         | 0.4 sec |
| ...       | ...     |

This creates the typing animation effect.

---

## 7. Data Type Issue

This causes an error:

```swift
0.1 * characterIndex
```

if `characterIndex` is an `Int`.

### Fix Options

**Option 1: Make it a Double**

```swift
var characterIndex = 0.0
```

**Option 2: Cast it**

```swift
0.1 * Double(characterIndex)
```

Both approaches work.

---

## Complete Solution

```swift
let titleText = "⚡️FlashChat"

titleLabel.text = ""

var characterIndex = 0.0

for letter in titleText {

    Timer.scheduledTimer(withTimeInterval: 0.1 * characterIndex,
                         repeats: false) { timer in
        self.titleLabel.text?.append(letter)
    }

    characterIndex += 1
}
```

---

## Key Takeaways

* **For loops** allow iteration through arrays and strings.
* Strings can be processed **one character at a time**.
* Loops execute very quickly, making animations invisible without delays.
* **Timers** can introduce delays between actions.
* Using a **character index** creates progressively longer delays for each letter.
* The typing animation is achieved by appending characters one by one at timed intervals.
* When using closures, references to UI elements often require `self`.
* Be mindful of data types (`Int` vs `Double`) when performing arithmetic.
