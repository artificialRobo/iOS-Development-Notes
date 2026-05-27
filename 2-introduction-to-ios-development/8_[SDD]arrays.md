# Swift Deep Dive Notes: Arrays

## What is an Array?

* An **Array** is a collection of related items stored together.
* Variables usually store **one piece of data**, while arrays store **multiple values**.

Example:

```swift
let names = ["Angela", "Jack", "Philip"]
```

* Arrays use **square brackets `[ ]`**
* Items are separated by **commas**

---

# Accessing Items in an Array

You access items using:

```swift
arrayName[index]
```

Example:

```swift
names[0]
```

This retrieves:

```swift
"Angela"
```

---

# Array Index Positions

Swift arrays start counting from **0**.

| Position (Index) | Value  |
| ---------------- | ------ |
| 0                | Angela |
| 1                | Jack   |
| 2                | Philip |

This is called **zero-based indexing**.

---

# Storing Arrays in Variables

Arrays can be stored inside variables just like other data types.

Example:

```swift
var codeFriends = ["Angela", "Jack", "Philip"]
```

Accessing items:

```swift
codeFriends[1]
```

Output:

```swift
"Jack"
```

---

# Visualizing Arrays

Think of an array like:

* A spreadsheet column
* A list of items with numbered positions

Example:

| Index | Name     |
| ----- | -------- |
| 0     | Person A |
| 1     | Person B |
| 2     | Person C |

---

# Challenge Exercise Summary

Given:

```swift
var numbers = [45, 73, 195, 53]
```

Goal:
Create another array called `computedNumbers` where:

* First item = first × second
* Second item = second × third
* Third item = third × fourth

---

# Multiplication in Swift

Swift uses the `*` symbol for multiplication.

Example:

```swift
1 * 2
```

Output:

```swift
2
```

---

# Expected Logic

Using:

```swift
[45, 73, 195, 53]
```

You should calculate:

```swift
45 * 73
73 * 195
195 * 53
```

Without manually typing the numbers directly.

---

# Example Solution

```swift
var numbers = [45, 73, 195, 53]

var computedNumbers = [
    numbers[0] * numbers[1],
    numbers[1] * numbers[2],
    numbers[2] * numbers[3]
]

print(computedNumbers)
```

---

# Key Takeaways

* Arrays store multiple related values.
* Arrays use square brackets `[ ]`.
* Access elements using indexes.
* Indexes start at `0`.
* Arrays can be stored in variables.
* Mathematical operations can be performed using array values.
