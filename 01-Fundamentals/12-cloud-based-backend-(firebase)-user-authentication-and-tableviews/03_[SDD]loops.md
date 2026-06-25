# Swift Deep Dive Notes: Loops

## What Are Loops?

* Loops allow code to be repeated automatically instead of writing the same instructions multiple times.
* They help programmers avoid repetitive code and make programs more efficient and easier to maintain.
* Common use case: repeating actions such as moving a robot and placing coins on tiles.

<p align="center">
    <img src="assets/easyWay.png" width="auto" style="border-radius: 1%">
</p>

---

# 1. For-In Loops

## Purpose

A **For-In Loop** repeats code for every item in a sequence.

### Syntax

```swift
for item in sequence {
    // code
}
```

### Example: Looping Through an Array

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]

for name in names {
    print("Hello \(name)")
}
```

### Output

```
Hello Anna
Hello Alex
Hello Brian
Hello Jack
```

### How It Works

* `name` is a constant created for the loop.
* It takes the value of each element in the array one at a time.
* The loop runs once for every element.

---

# 2. Looping Through Ranges

## Closed Range (`...`)

Includes both start and end values.

```swift
for number in 1...5 {
    print(number)
}
```

### Output

```
1
2
3
4
5
```

* Runs **5 times**.

---

## Half-Open Range (`..<`)

Includes the start value but excludes the end value.

```swift
for number in 1..<5 {
    print(number)
}
```

### Output

```
1
2
3
4
```

* Runs **4 times**.

---

# 3. Ignoring the Loop Variable

If you don't need the value from the sequence, use `_`.

```swift
for _ in 1...5 {
    print("Hello")
}
```

### Output

```
Hello
Hello
Hello
Hello
Hello
```

### Why Use `_`?

* Indicates the loop variable is unused.
* Useful when you only want to repeat code a certain number of times.

---

# 4. Practical Example: Robot Repetition

Instead of writing:

```swift
move()
putCoin()

move()
putCoin()

move()
putCoin()
```

Use:

```swift
for _ in 1...5 {
    move()
    putCoin()
}
```

### Benefits

* Less code
* Easier to read
* Easier to modify

---

# 5. Sequences You Can Loop Through

## Arrays

```swift
for fruit in fruits {
    print(fruit)
}
```

* Arrays maintain the order of elements.

---

## Sets

```swift
let fruitSet = Set(fruits)

for fruit in fruitSet {
    print(fruit)
}
```

### Key Difference

* Sets do **not guarantee order**.
* More efficient for storing large collections.

| Array                     | Set                |
| ------------------------- | ------------------ |
| Ordered                   | Unordered          |
| Preserves insertion order | No order guarantee |
| Slightly less efficient   | More efficient     |

---

## Dictionaries

```swift
for person in contacts {
    print(person.key)
}
```

Print values:

```swift
print(person.value)
```

### Dictionary Structure

* Stores **key-value pairs**
* Loop variable contains both key and value

---

## Strings

Strings are also sequences.

```swift
for letter in "supercalifragilisticexpialidocious" {
    print(letter)
}
```

### Result

* Loops through each character individually.
* Runs once per character.

---

# 6. While Loops

## Purpose

A **While Loop** repeats as long as a condition remains true.

### Syntax

```swift
while condition {
    // code
}
```

### Example

```swift
while 8 > 5 {
    print("Running")
}
```

Warning: This creates an infinite loop because the condition never becomes false.

---

# 7. Example: Running for One Second

```swift
import Foundation

var now = Date.timeIntervalSince1970
let oneSecondFromNow = now + 1

while now < oneSecondFromNow {
    print("waiting...")
    now = Date.timeIntervalSince1970
}
```

### How It Works

1. Store the current time.
2. Create a target time one second later.
3. Keep looping while current time is less than target time.
4. Update `now` inside the loop.

### Important

Without updating `now`, the loop would never end.

---

# 8. Infinite Loops

## What Is an Infinite Loop?

A loop that never stops because its condition is always true.

Example:

```swift
while 3 > 2 {
    print("Forever")
}
```

### Problems

* Consumes CPU resources.
* Can freeze or crash programs.
* May force the development environment (e.g., Xcode) to stop responding.

---

# 9. For Loop vs While Loop

| For-In Loop                 | While Loop                    |
| --------------------------- | ----------------------------- |
| Known number of repetitions | Unknown number of repetitions |
| Safer and easier to use     | More error-prone              |
| Less likely to create bugs  | Can create infinite loops     |
| Recommended for beginners   | Use carefully                 |

---

# When to Use Each

### Use a For-In Loop When:

* Looping through arrays, sets, dictionaries, strings, or ranges.
* You know how many times the code should run.

### Use a While Loop When:

* Repeating until a condition changes.
* The number of repetitions is unknown.
* Example: waiting for data to load from the internet.

---

# Key Takeaways

* **Loops automate repetitive tasks.**
* **For-In loops** work with sequences like arrays, ranges, dictionaries, sets, and strings.
* Use `_` when the loop variable isn't needed.
* **Closed range (`...`)** includes the end value.
* **Half-open range (`..<`)** excludes the end value.
* **Arrays preserve order; Sets do not.**
* **While loops** run until a condition becomes false.
* Always ensure a while-loop condition can eventually become false to avoid **infinite loops**.
* For beginners, prefer **For-In loops** because they are safer and simpler.
