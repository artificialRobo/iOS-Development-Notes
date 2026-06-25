# Notes: Connecting UI to Code in Xcode (Swift)

## 1. Purpose of Programming the UI

* In `Main.storyboard`, you can visually design the app and set properties manually.
* Example: changing an image from `DiceOne` to `DiceTwo` using the Attribute Inspector.
* But once the app is installed on a user’s phone, you cannot manually edit the storyboard anymore.
* To change UI elements while the app is running, you must use **code**.

---

## 2. Important Files in an Xcode Project

### `Main.storyboard`

* Design file
* Used to create and arrange UI elements visually

### `ViewController.swift`

* Code file
* Used to control app behavior and UI programmatically

These two files are separate, so we need a way to connect them.

---

## 3. Assistant Editor

* Open `Main.storyboard`
* Click the editor options button (top-right)
* Select **Assistant**

This shows:

* Storyboard on the left
* Corresponding Swift file (`ViewController.swift`) on the right

---

## 4. IB Outlet (Interface Builder Outlet)

### Purpose

An **IBOutlet** creates a connection between:

* A UI element in the storyboard
* A variable in Swift code

This lets us modify UI elements through code.

---

### Creating an IBOutlet

Steps:

1. Hold **Control**
2. Click and drag from the UI element
3. Drop inside `ViewController.swift`
4. Place it inside the class but outside functions
5. Give it a name
6. Click **Connect**

Example:

```swift
@IBOutlet weak var diceImageView1: UIImageView!
```

---

## 5. Camel Case Naming Convention

Used for naming variables in programming.

### Rules

* First word → lowercase
* Every next word → starts with uppercase letter

Example:

```swift
diceImageView1
```

Benefits:

* Easier readability
* Helps separate words clearly

---

## 6. IBOutlet Errors & App Crashes

### Common Beginner Error

Renaming an IBOutlet manually in code can break the connection.

Example:

```swift
diceImageView1
```

changed to:

```swift
diceImageViewOne
```

This may crash the app with:

```text
SIGABRT
```

or:

```text
not key value coding-compliant
```

### Why It Happens

* Storyboard still stores the old IBOutlet name internally
* Code and storyboard become mismatched

### Fixing the Problem

#### Option 1: Delete Broken Connection

* Right-click the UI element
* Remove the broken outlet connection
* Reconnect it

#### Option 2 (Best Method): Refactor Rename

Use:

```text
Right Click → Refactor → Rename
```

This safely renames the outlet everywhere.

---

## 7. Understanding `viewDidLoad()`

```swift
override func viewDidLoad() {
    super.viewDidLoad()
}
```

### Purpose

* Runs when the screen/view loads for the first time
* Used to set up UI or initial values

Everything inside `{ }` is called a **block of code**.

---

## 8. Blocks of Code

A block of code:

* Starts with `{`
* Ends with `}`

Everything inside runs together when triggered.

Example:

```swift
override func viewDidLoad() {

}
```

Helpful Xcode features:

* Clicking braces highlights matching pairs
* Double-clicking a brace selects the whole block

---

## 9. Changing UI Properties with Code

### Basic Syntax

```swift
Who.What = Value
```

### Example

```swift
diceImageView1.image = #imageLiteral(resourceName: "DiceSix")
```

Breakdown:

* `diceImageView1` → Who
* `.image` → What property to change
* `#imageLiteral(...)` → New value

---

## 10. Dot Notation

Used to access properties or functions of an object.

Example:

```swift
diceImageView1.image
```

After typing a dot (`.`), Xcode shows available properties.

---

## 11. Image Literals

### Purpose

Lets you visually select an image asset.

Example:

```swift
#imageLiteral(resourceName: "DiceSix")
```

Benefits:

* Avoids typing mistakes
* Easier image selection

---

## 12. Autocomplete in Xcode

Xcode suggests code automatically while typing.

Benefits:

* Prevents typos
* Speeds up coding
* Reduces errors

Example error from typo:

```text
Use of unresolved identifier
```

Meaning:

* Xcode doesn’t recognize the variable name

---

## 13. Changing Other Properties (Alpha Example)

### Alpha Property

Controls transparency:

* `1` = fully visible
* `0` = invisible

Example:

```swift
diceImageView1.alpha = 0.5
```

This makes the image 50% transparent.

---

## 14. Creating a Second IBOutlet

Example:

```swift
@IBOutlet weak var diceImageView2: UIImageView!
```

Changing its image:

```swift
diceImageView2.image = #imageLiteral(resourceName: "DiceTwo")
```

---

## 15. Comments in Code

### Purpose

Used to leave notes for yourself or teammates.

Syntax:

```swift
// This is a comment
```

Comments:

* Improve readability
* Help future understanding
* Are ignored by the compiler

Example:

```swift
// Who.What = Value
```

---

## Key Takeaways

* Storyboards design the UI visually
* Swift code changes UI dynamically
* IBOutlet connects UI to code
* Use camelCase naming
* Use `viewDidLoad()` for setup tasks
* UI properties are changed using:

```swift
Who.What = Value
```

* Use autocomplete to avoid errors
* Rename outlets safely using Refactor
* Comments improve code readability
