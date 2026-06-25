# Notes: IBAction and User Interaction in iOS (Swift/Xcode)

## 1. Review of IBOutlets

* In the previous lesson:

  * **IBOutlets** were used to create references to UI elements.
  * This allows code to **change UI properties programmatically**.
* Examples:

  * Changing image views
  * Updating labels
  * Modifying buttons

### Purpose of IBOutlet

* Used when code needs to **control or modify** a UI element.
* Example:

  * Change a dice image from code.

---

## 2. Detecting User Interaction with IBAction

### Problem

* The **Roll button** does not need its appearance changed.
* Instead, we need to:

  * Detect when the user taps it
  * Run code in response

### Solution: IBAction

* **IBAction** connects a UI element to code that runs after user interaction.

#### Difference Between IBOutlet and IBAction

| IBOutlet                   | IBAction                        |
| -------------------------- | ------------------------------- |
| Code → UI                  | UI → Code                       |
| Used to modify UI elements | Used to respond to user actions |

---

## 3. Creating an IBAction

### Steps

1. Hold **Control**
2. Click and drag from the button into the code
3. Drop above the closing curly brace

### Important Settings

#### Connection Type

* Automatically set to **Action**

#### Event

* Usually:

  * **Touch Up Inside**
* Meaning:

  * User taps and releases inside button boundaries

#### Naming Convention

* Name should describe the action/event.
* Example:

```swift
rollButtonPressed
```

#### Sender Type

* Set to:

```swift
UIButton
```

---

## 4. Generated IBAction Code

Example:

```swift
@IBAction func rollButtonPressed(_ sender: UIButton) {

}
```

* `IBAction` means:

  * Code runs when a UI action occurs.

---

## 5. Using Print Statements

### Syntax

```swift
print("button got tapped")
```

### Notes

* Text must be inside **double quotes** in Swift.
* Used for debugging/testing.

#### Purpose

* Prints messages to the **debug console**.

---

## 6. Testing the Button

When the app runs:

* Pressing the Roll button:

  * Triggers the IBAction
  * Executes all code inside the function

Example output:

```swift
button got tapped
```

---

## 7. Understanding Flow Between UI and Code

### IBOutlet

* Direction:

```text
Code → User Interface
```

* Used when code changes UI.

### IBAction

* Direction:

```text
User Interface → Code
```

* Used when user interaction triggers code.

---

## 8. Changing Dice Images on Button Press

### Original Behavior

Inside `viewDidLoad`:

* Left dice shows 6
* Right dice shows 2

These run only once when the view loads.

---

## 9. Updating Images Inside IBAction

### Example

```swift
diceImageView1.image = UIImage(imageLiteralResourceName: "DiceFour")

diceImageView2.image = UIImage(imageLiteralResourceName: "DiceFour")
```

### Result

* When the Roll button is tapped:

  * Both dice images change to DiceFour.

---

## 10. Key Concept

### `viewDidLoad`

* Runs automatically when the screen loads.

### IBAction

* Runs only after the user performs the connected action.

---

## 11. Important Programming Concept

The lesson emphasizes:

```text
Who.What = Value
```

Example:

```swift
diceImageView1.image = DiceFour
```

* `Who` → object
* `What` → property
* `Value` → new value assigned

---

## Additional Topics Mentioned

Next lesson covers:

* Naming conventions
* Camel casing
* Comments
* Print statements
* String interpolation

If you are an advanced programmer, you may skip it.
