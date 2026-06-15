## Notes: Creating a Second View Controller in iOS (Swift)

### Purpose

* The BMI value calculated on the first screen should be displayed on a **separate screen** when the Calculate button is pressed.
* To do this, we need to create a **new View Controller** for the second screen and later pass the BMI result to it.

---

## 1. Creating a New View Controller File

### Steps

1. Right-click the **Controllers** folder.
2. Select **New File**.
3. Choose **Swift File**.
4. Name it **SecondViewController.swift**.

### Naming Convention

* In Swift, it is standard practice to give the file and the class the **same name**.
* Example:

```swift
class SecondViewController: UIViewController {
}
```

---

## 2. Understanding Classes

### Class Declaration Structure

```swift
class SecondViewController: UIViewController {
}
```

Components:

* `class` → keyword used to create a class.
* `SecondViewController` → class name.
* `UIViewController` → superclass (parent class).

### Naming Rules

* Class names begin with a **capital letter**.
* Variable and function names usually begin with a **lowercase letter**.
* Capitalized names indicate a blueprint (Class or Struct).

---

## 3. Foundation vs UIKit

### Foundation Framework

```swift
import Foundation
```

Provides:

* Core Swift functionality.
* Basic data types and language features.

### UIKit Framework

```swift
import UIKit
```

Provides:

* iOS-specific UI components.
* Includes everything from Foundation plus additional UI functionality.

Examples of UIKit components:

* `UILabel`
* `UISlider`
* `UIViewController`
* `UIColor`
* `UIImageView`

### Why UIKit is Needed

* `UIViewController` belongs to UIKit.
* If only Foundation is imported, Xcode cannot recognize `UIViewController`.

---

## 4. Frameworks

Frameworks are collections of pre-written code provided by Apple that simplify app development.

Benefits:

* Avoid building common components from scratch.
* Provide ready-made UI elements and functionality.
* Include properties and methods already implemented by Apple.

Example:

```swift
UILabel
```

Already includes:

* Text property
* Text color property
* Background color property

---

## 5. Creating viewDidLoad()

When creating a View Controller manually, we need to add `viewDidLoad()` ourselves.

### Example

```swift
override func viewDidLoad() {
    super.viewDidLoad()
}
```

### Purpose of viewDidLoad()

* Called when the view is loaded into memory.
* Used for initial setup and configuration.

### Important

Always include:

```swift
super.viewDidLoad()
```

to ensure the parent class performs its setup.

---

## 6. UIViewController Documentation

Since `UIViewController` is one of the most important classes in iOS development:

### Recommended Resources

* Xcode → Help → Developer Documentation
* Apple Documentation:

  * developer.apple.com/documentation

### Benefits of Reading Documentation

* Understand View Controller lifecycle.
* Learn available methods and properties.
* Better understand screen management in iOS apps.

---

## Key Takeaways

* Create a new Swift file called **SecondViewController.swift**.
* Define a class named **SecondViewController** that inherits from **UIViewController**.
* Use **UIKit**, not just Foundation, when working with UI components.
* Frameworks provide pre-built functionality and UI elements.
* Manually add `viewDidLoad()` when creating a View Controller from scratch.
* Include `super.viewDidLoad()` inside the method.
* Explore Apple's documentation to better understand `UIViewController` and iOS app architecture.
