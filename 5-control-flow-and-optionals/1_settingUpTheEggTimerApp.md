# Notes: Setting Up the Egg Timer App (Storyboard & IBAction)

## 1. Exploring the Project

* After cloning the starter project, review the project structure.
* Focus on **Main.storyboard** to understand the UI elements and their connections.

---

## 2. Working with Labels

### Problem: Text Truncation

* Large text may get cut off on smaller screens.

### Solution 1: Allow Multiple Lines

* Set **Number of Lines = 0**
* This removes the line limit and allows text to wrap onto multiple lines.

### Solution 2: Autoshrink Font Size

* Enable **Autoshrink** and set a **Minimum Font Size**.
* Example:

  * Default font size: 30
  * Minimum font size: 15
* The label automatically reduces font size to fit the available space.

### Key Takeaway

To ensure text is visible on all screen sizes:

* Use multiple lines (`Number of Lines = 0`)
* Or enable font shrinking with a minimum size.

---

## 3. Understanding Layer Order in Storyboard

### UI Components

* 3 Buttons:

  * Soft
  * Medium
  * Hard
* 3 Egg Image Views

### Why Button Titles Aren't Visible

* The image views are positioned **above** the buttons in the view hierarchy.
* Since views are layered, the image covers the button text.

### Fix

* Change the order in the **Document Outline**.
* Move buttons above image views if you want button titles visible.

### Why Use Separate Image Views?

Instead of setting images directly on buttons:

* Scaling images on buttons can be more difficult.
* Separate image views make layout easier.
* The button sits on top and handles user interaction.

---

## 4. Connecting Storyboard to Code

### Challenge

Create **one IBAction** for all three buttons.

#### Action Name

```swift
@IBAction func hardnessSelected(_ sender: UIButton) {
    
}
```

### Steps

1. Open Assistant Editor.
2. Control-drag from a button to the ViewController.
3. Choose:

   * Connection: **Action**
   * Type: **UIButton**
   * Name: **hardnessSelected**
4. Connect all three buttons to the same IBAction.

### Benefit

One function handles multiple buttons.

---

## 5. Identifying Which Button Was Pressed

Use the sender parameter:

```swift
@IBAction func hardnessSelected(_ sender: UIButton) {
    print(sender.currentTitle)
}
```

### Output

* Press Soft → `"Soft"`
* Press Medium → `"Medium"`
* Press Hard → `"Hard"`

### Important

* `sender` refers to the button that triggered the action.
* `currentTitle` returns the button's displayed text.

---

## 6. Storing Egg Boiling Times

### Recommended Times

| Egg Type | Time (minutes) |
| -------- | -------------- |
| Soft     | 5              |
| Medium   | 7              |
| Hard     | 12             |

### Create Constants

```swift
let softTime = 5
let mediumTime = 7
let hardTime = 12
```

---

## 7. Saving User Selection

Store the selected hardness:

```swift
let hardness = sender.currentTitle
```

This gives access to the user's chosen egg type.

---

## 8. Understanding the Xcode Warning

### Warning

> Initialization of immutable value 'hardness' was never used

### Meaning

* A constant or variable was created but not used anywhere in the code.

Example:

```swift
let hardness = sender.currentTitle
```

If `hardness` isn't referenced later, Xcode warns about it.

### Why Xcode Warns

* Helps remove unnecessary code.
* Encourages cleaner and more efficient programs.

### Learning Tip

* Copy warning/error messages into Google or Stack Overflow to understand them quickly.

---

## 9. Next Programming Challenge

### Goal

Print the correct cooking time based on the selected hardness.

Expected behavior:

| Button Pressed | Output |
| -------------- | ------ |
| Soft           | 5      |
| Medium         | 7      |
| Hard           | 12     |

### Hint

Use:

* `if`
* `else if`
* `else`
* Conditional statements

Example logic:

```swift
if hardness == "Soft" {
    print(softTime)
}
```

(The complete solution is covered in the next lesson.)

---

## Summary

* Explore `Main.storyboard`.
* Fix label truncation using:

  * Multiple lines (`0`)
  * Autoshrink font size.
* Understand view layering in the document outline.
* Connect all egg buttons to a single `IBAction`.
* Use `sender.currentTitle` to identify which button was tapped.
* Store egg cooking times using constants.
* Xcode warnings often indicate unused variables/constants.
* Use conditional statements to match egg hardness with cooking time.
