# Swift Deep Dive Notes: Naming Conventions, Commenting, and String Interpolation

### Purpose of Swift Deep Dives

* Provides deeper explanations of Swift concepts covered earlier.
* Helps beginners better understand programming fundamentals.
* Acts as both:

  * Revision/recap
  * Detailed conceptual learning

---

## 1. Naming Conventions

### Camel Case (Used in Swift)

* Starts with a lowercase letter.
* Every new word begins with a capital letter.

Example:

```swift
myButtonOutlet
calculateTotalScore
```

### Other Naming Styles

#### Kebab Case

* All lowercase words separated by dashes (`-`)
* Common in web development

Example:

```text
my-file-name
```

#### Snake Case

* Words separated by underscores (`_`)

Example:

```text
my_file_name
```

### Swift Standard

* Swift primarily uses **camelCase**
* Use camelCase when naming:

  * Variables
  * Functions
  * IBOutlets
  * IBActions

---

## 2. Comments in Swift

### Single-Line Comments

Use:

```swift
// This is a comment
```

#### Purpose

* Explain code
* Disable code temporarily

Example:

```swift
// print("Hello World")
```

This line becomes inactive and will not execute.

---

## Xcode Shortcut for Commenting

Shortcut:

```text
Command + /
```

* Automatically comments/uncomments a line.
* Useful for quickly toggling code.

---

## Multi-Line Comments

Use:

```swift
/*
This is a
multi-line comment
*/
```

Everything inside is treated as a comment.

---

# 3. Swift Playgrounds

### Creating a Playground

Steps:

1. File → New → Playground
2. Choose blank iOS template
3. Save and open

### Important Playground Areas

* **Code Editor** → where code is written
* **Interpreter Area** → shows intermediate results
* **Debug Console** → displays output/errors

### Helpful Setting

Enable:

```text
Automatically Run Code
```

This runs code instantly as you type.

---

## 4. Print Statements

### Basic Syntax

```swift
print("Hello World")
```

* Displays output in the debug console.

---

## 5. Strings

### Definition

* Text in programming is called a **String**
* A string is a sequence of characters.

Example:

```swift
"Hello World"
```

---

## 6. String Interpolation

### Purpose

Insert code or variables inside strings.

### Syntax

```swift
\(code)
```

Example:

```swift
print("Hello \(2 + 3) World")
```

Output:

```text
Hello 5 World
```

---

## Why It’s Useful

* Combine text and calculations
* Display variable values
* Debug code easily

Example:

```swift
print("The result of 5 + 3 = \(5 + 3)")
```

Output:

```text
The result of 5 + 3 = 8
```

---

## Key Takeaways

* Swift uses **camelCase** naming.
* `//` creates single-line comments.
* `/* */` creates multi-line comments.
* `Command + /` quickly comments code in Xcode.
* `print()` displays output.
* Text is called a **String**.
* `\( )` allows **string interpolation** (embedding code inside strings).
