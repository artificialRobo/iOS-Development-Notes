# Swift Deep Dive Notes: Constants, Randomization, and Range Operator

## 1. Constants vs Variables in Swift

### Variables (`var`)

* A variable stores data that **can change**.
* Declared using the keyword `var`.

```swift
var a = 3
a = 5
```

* Think of it like:

  * A box with a lid
  * You can replace the value anytime

---

### Constants (`let`)

* A constant stores data that **cannot change** after creation.
* Declared using the keyword `let`.

```swift
let a = 3
```

* Trying to change it causes an error:

```swift
a = 5 // Error
```

* Think of it like:

  * A sealed box
  * Once created, the value stays fixed

---

### Why Use Constants?

* More memory efficient
* Compiler can optimize storage
* Safer because values cannot accidentally change

### Best Practice

* Use `let` by default
* Only use `var` when the value needs to change

### Examples

| Use Constant (`let`) | Use Variable (`var`) |
| -------------------- | -------------------- |
| Pi value             | User score           |
| App name             | Game points          |
| Date of birth        | Counter              |

---

## 2. Basic Data Types in Swift

### String

* A sequence of characters (text)

```swift
let name = "Angela"
```

* Written inside quotation marks `" "`.

---

### Int (Integer)

* Whole numbers
* No decimal points

```swift
let age = 25
```

Examples:

* `12`
* `-5`
* `1000`

---

### Float

* Decimal numbers
* Less precision

```swift
let height = 5.8
```

---

### Double

* Decimal numbers with greater precision
* More accurate than `Float`

```swift
let pi = 3.1415926535
```

---

### Bool (Boolean)

* Only two values:

  * `true`
  * `false`

```swift
let isLoggedIn = true
```

Used for conditions and decision-making.

---

## 3. Randomization in Swift

### Random Integers

```swift
let randomNumber = Int.random(in: 1...3)
```

* Generates numbers between `1` and `3`
* Includes both 1 and 3

Possible outputs:

* 1
* 2
* 3

---

## 4. Range Operators

### Closed Range (`...`)

Includes upper bound.

```swift
1...3
```

Possible values:

* 1
* 2
* 3

### Half-Open Range (`..<`)

Excludes upper bound.

```swift
1..<3
```

Possible values:

* 1
* 2
* NOT 3

---

## 5. Random Floating Numbers

```swift
let randomFloat = Float.random(in: 1...3)
```

* Generates decimal values
* Example:

  * `1.45`
  * `2.98`

---

## 6. Arrays and Random Elements

### Random Element from Array

```swift
array.randomElement()
```

* Picks a random item from the array

---

### Shuffle Array

```swift
array.shuffle()
```

* Randomly changes order of items in the array

---

## 7. String Concatenation

* Combining strings using `+`

```swift
let password = "a" + "b"
```

Output:

```swift
ab
```

This process is called **concatenation**.

---

## 8. Password Generator Challenge

### Goal

Create a random 6-letter password using letters from an alphabet array.

### Concepts Used

* Arrays
* Random elements
* Strings
* Concatenation
* Constants/Variables

Example alphabet array:

```swift
let alphabet = ["a", "b", "c", ...]
```

Possible password:

```swift
"kqtmza"
```

---

## Key Takeaways

* `let` = constant (unchangeable)
* `var` = variable (changeable)
* Prefer constants unless changes are needed
* Common data types:

  * `String`
  * `Int`
  * `Float`
  * `Double`
  * `Bool`
* Random numbers use `.random(in:)`
* `...` includes upper bound
* `..<` excludes upper bound
* Arrays support:

  * `.randomElement()`
  * `.shuffle()`
* Strings combine with `+` (concatenation)
