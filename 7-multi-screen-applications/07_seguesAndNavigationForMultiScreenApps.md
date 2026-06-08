# Notes: Segues and Navigation in iOS (UIKit)

## 1. Why Use Segues?

* Previously, a new screen (`SecondViewController`) was created entirely in code.
* This demonstrated:

  * Inheritance from `UIViewController`
  * Overriding methods like `viewDidLoad()`
  * Accessing inherited properties and methods
* However, creating UI elements programmatically requires a lot of code.
* **Segues** provide an easier way to navigate between screens using the storyboard.

---

## 2. Creating a View Controller with Cocoa Touch Class

Instead of creating a plain Swift file:

1. Go to **File → New File → Cocoa Touch Class**
2. Name it `ResultViewController`
3. Set subclass to `UIViewController`

Benefits:

* Automatically imports UIKit
* Automatically inherits from `UIViewController`
* Includes a ready-made `viewDidLoad()` method

---

## 3. Connecting Storyboard to Code

To link a screen with its controller:

1. Select the View Controller in the storyboard.
2. Open the **Identity Inspector**.
3. Set its class to `ResultViewController`.

After linking:

* Use **Assistant Editor** to create:

  * `IBOutlet`s
  * `IBAction`s

Example:

```swift
@IBOutlet weak var bmiLabel: UILabel!
@IBOutlet weak var adviceLabel: UILabel!

@IBAction func recalculatePressed(_ sender: UIButton) {
}
```

---

## 4. Refactoring View Controller Names

Instead of manually renaming files and classes:

1. Right-click the class name.
2. Select **Refactor → Rename**.
3. Enter the new name (e.g., `CalculateViewController`).

Xcode updates:

* File name
* Class name
* Storyboard references
* Comments

---

## 5. Creating a Segue

A segue is a storyboard connection that transitions between screens.

### Steps:

1. Hold **Control**.
2. Drag from `CalculateViewController` to `ResultViewController`.
3. Choose **Present Modally**.
4. Select the segue arrow.
5. Set an Identifier:

```text
goToResult
```

---

## 6. Triggering a Segue in Code

Instead of manually creating a view controller:

```swift
performSegue(withIdentifier: "goToResult", sender: self)
```

### Parameters:

* `withIdentifier` → name of the segue
* `sender` → object initiating the segue (`self`)

---

## 7. Passing Data Between Screens

### Step 1: Create a property in ResultViewController

```swift
var bmiValue: String?
```

The value is optional because it isn't known when the controller is first created.

---

## 8. Using `prepare(for:sender:)`

Before a segue occurs, UIKit calls:

```swift
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
}
```

This is used to prepare data for the destination screen.

### Check the correct segue

```swift
if segue.identifier == "goToResult" {
}
```

Useful when one screen has multiple segues.

---

## 9. Accessing the Destination View Controller

The destination is initially treated as a generic `UIViewController`.

```swift
let destinationVC = segue.destination
```

To access custom properties, downcast it:

```swift
let destinationVC = segue.destination as! ResultViewController
```

Now custom properties become available:

```swift
destinationVC.bmiValue = bmiValue
```

---

## 10. Downcasting

### What is Downcasting?

Converting a superclass reference into a more specific subclass.

```swift
segue.destination as! ResultViewController
```

* `UIViewController` → superclass
* `ResultViewController` → subclass

### Force Downcast

```swift
as!
```

Means:

> "I am certain this object is a ResultViewController."

---

## 11. Storing BMI for Transfer

The BMI calculated in `calculatePressed` must be accessible in `prepare(for:)`.

Create a property:

```swift
var bmiValue = "0.0"
```

Update it when BMI is calculated:

```swift
bmiValue = String(format: "%.1f", bmi)
```

Then pass it through the segue:

```swift
destinationVC.bmiValue = bmiValue
```

---

## 12. Displaying Passed Data

Inside `ResultViewController`:

```swift
override func viewDidLoad() {
    super.viewDidLoad()

    bmiLabel.text = bmiValue
}
```

Result:

* User calculates BMI.
* BMI value is passed to the next screen.
* Result screen displays the value.

---

## 13. Returning to the Previous Screen

No need to create another segue.

Use:

```swift
dismiss(animated: true, completion: nil)
```

Inside:

```swift
@IBAction func recalculatePressed(_ sender: UIButton) {
    dismiss(animated: true, completion: nil)
}
```

Result:

* Current screen closes.
* Previous screen reappears.

---

## 14. View Controllers as a Stack

iOS presents screens like a stack:

```text
ResultViewController → CalculateViewController
```

When a new screen is presented:

* It appears on top of the current screen.

When dismissed:

* The top screen is removed.
* The previous screen becomes visible again.

---

## 15. Useful UIViewController Methods Learned

### Present Next Screen

```swift
performSegue(withIdentifier:sender:)
```

### Prepare Data Before Navigation

```swift
prepare(for:sender:)
```

### Close Current Screen

```swift
dismiss(animated:completion:)
```

All are available because the controllers inherit from `UIViewController`.

---

# Key Takeaways

* Use **segues** for easy storyboard navigation.
* Create custom controllers using **Cocoa Touch Class**.
* Connect screens with **IBOutlet** and **IBAction**.
* Trigger navigation using `performSegue()`.
* Pass data using `prepare(for:sender:)`.
* Use **downcasting (`as!`)** to access destination controller properties.
* Return to the previous screen with `dismiss()`.
* Multiple-screen apps work like a stack of view controllers layered on top of each other.
