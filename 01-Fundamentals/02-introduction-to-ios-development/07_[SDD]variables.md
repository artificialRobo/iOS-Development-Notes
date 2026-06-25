# Swift Deep Dive Notes: Variables

## What Are Variables?

* A **variable** is a way to store data with a name (label).
* It helps programmers easily reference data later in code.
* Example analogy:

  * A variable is like a **labeled box**.
  * The label tells you what’s inside.
  * You can store and retrieve data using the label.

---

## Why Variables Are Useful

* Without labels, data is hard to remember or identify.
* Variables make code:

  * easier to read,
  * easier to organize,
  * easier to reuse.

Example:

* Instead of remembering a random number,
* you store it with a meaningful name like `phoneNumber`.

---

## Creating Variables in Swift

Syntax:

```swift
var variableName = value
```

Example:

```swift
var a = 5
var b = 8
```

### Breakdown

* `var` → tells Swift you are creating a variable.
* `=` → assigns a value to the variable.
* Left side → variable name.
* Right side → value being stored.

---

## Variables Can Change

* Variables are called “variables” because their values can vary/change.

Example:

```swift
var name = "Angela"
name = "Jack"
```

* The variable `name` now stores a different value.

---

## Printing Variables

### Printing the Variable Value

```swift
print(a)
```

* Prints the value stored in `a`.

### Printing Text vs Variables

```swift
print("a")
```

* Prints the literal letter `"a"`.

```swift
print(a)
```

* Prints the value of variable `a`.

---

## String Interpolation

Used to insert variables into strings.

Syntax:

```swift
\(variableName)
```

Example:

```swift
print("The value of a is \(a)")
```

Output:

```swift
The value of a is 5
```

---

## Variable Swapping Challenge

### Goal

Swap values of `a` and `b` without typing numbers.

Initial values:

```swift
var a = 5
var b = 8
```

Desired result:

```swift
a = 8
b = 5
```

---

## Solution Using a Temporary Variable

```swift
var c = a
a = b
b = c
```

### Step-by-Step

1. Store `a` in `c`
2. Put `b` into `a`
3. Put old `a` (stored in `c`) into `b`

Final result:

* `a = 8`
* `b = 5`

---

## Key Takeaways

* Variables store data with labels.
* `var` creates a variable in Swift.
* Variables can change values.
* Use `print()` to display values.
* Use string interpolation with `\( )`.
* Temporary variables help swap values safely.
