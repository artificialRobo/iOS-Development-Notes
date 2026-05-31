# Swift Deep Dive Notes: Functions and Scope

## 1. What is a Function?

A **function** is a named block of code that groups multiple instructions together so they can be reused easily.

**Problem functions solve:**

* Without functions, you would need to repeatedly write the same instructions.
* Functions reduce repetition and make code shorter, cleaner, and easier to maintain.

**Example:**
Instead of writing many instructions for a robot to buy milk every day, you can create a function called `getMilk()` and simply call it whenever needed.

---

## Two Stages of a Function

#### A. Function Definition (Creation)

This is where you create the function and specify what it should do.

```swift
func greeting() {
    print("hello")
}
```

Components:

* `func` → keyword used to create a function.
* `greeting` → function name.
* `()` → parentheses (used for inputs/parameters later).
* `{}` → function body containing the code to execute.

---

#### B. Function Call (Execution)

Creating a function does not run it.

To execute the function, you must **call** it:

```swift
greeting()
```

When called:

1. Swift finds the function definition.
2. Executes all code inside the function body.

---

## Function Formatting

Preferred style:

```swift
func greeting() {
    print("hello")
}
```

Benefits:

* Easier to read.
* Helps avoid missing braces.
* Xcode automatically inserts matching closing braces.

---

## Calling Functions Multiple Times

You can repeat behavior by calling a function multiple times.

```swift
greeting()
greeting()
greeting()
greeting()
```

Output:

```text
hello
hello
hello
hello
```

Alternative:

* Put multiple `print()` statements inside the function.
* Or call the function repeatedly.

Both produce the same result.

---

## 2. Scope

**Scope** determines where variables and functions can be accessed.

#### Variable Scope Example

```swift
func greeting1() {
    let myName = "Angela"
    print(myName)
}
```

This works because `myName` is used inside the function where it was created.

```swift
func greeting2() {
    print(myName) // Error
}
```

This causes an error because `myName` exists only inside `greeting1()`.

**Key Rule:**

* Variables are only accessible within the block (`{}`) where they are created.

---

## Nested Functions and Scope

Functions can be created inside other functions.

```swift
func greeting1() {

    func greeting2() {
        print("hey")
    }

    greeting2()
}
```

`greeting2()` can only be called inside `greeting1()` because it was created there.

This will NOT work:

```swift
greeting2() // Error
```

outside of `greeting1()`.

**Key Rule:**

* A nested function can only be used within the scope where it was defined.

---

## Importance of Curly Braces `{}`

Curly braces define the boundaries (scope) of code blocks.

They determine:

* Where variables can be used.
* Where functions can be called.
* What code belongs together.

Think of them as the walls of a house:

* Anything created inside stays inside unless explicitly shared.

---

## Xcode Tips for Managing Braces

#### Auto-Insert Braces

When you type:

```swift
{
```

and press **Enter**, Xcode automatically adds the matching closing brace.

#### Find Matching Braces

* Double-click a closing brace `}` to highlight the entire block.
* Use arrow keys on a brace to flash its matching pair.

#### Fix Indentation

Select all:

```text
Command + A
```

Then:

```text
Editor → Structure → Re-indent
```

This automatically formats your code correctly.

---

# Key Takeaways

* Functions package instructions into reusable blocks of code.
* Every function has:

  1. A definition (creation).
  2. A call (execution).
* Creating a function does not run it.
* Use the function name followed by `()` to call it.
* Scope controls where variables and functions can be accessed.
* Variables and nested functions only exist within their surrounding `{}` braces.
* Proper indentation and brace management are important for readable code.
