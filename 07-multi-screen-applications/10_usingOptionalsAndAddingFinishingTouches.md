# Notes: Using Optionals and Adding Finishing Touches with Color Literals

## Lesson Goal

Enhance the BMI Calculator app by:

* Displaying BMI advice text.
* Changing the background color based on BMI category.
* Applying the **MVC (Model-View-Controller)** design pattern.
* Practicing **optionals**, **optional chaining**, and **nil coalescing**.
* Learning to use **Color Literals** and `UIColor`.

---

## 1. Handling Optional BMI Values

The `bmi` property was changed from a normal value to an **optional**.

### Option 1: Nil Check

```swift
if bmi != nil {
    return String(format: "%.1f", bmi!)
} else {
    return "0.0"
}
```

### Option 2: Optional Binding

```swift
if let safeBMI = bmi {
    return String(format: "%.1f", safeBMI)
} else {
    return "0.0"
}
```

### Option 3: Nil Coalescing (Preferred)

```swift
return String(format: "%.1f", bmi ?? 0.0)
```

**Why preferred?**

* Cleaner syntax.
* More readable.
* Clearly expresses "use value if available, otherwise use default."

---

## 2. Creating a BMI Model (MVC Pattern)

Instead of storing only a BMI number, create a dedicated model that stores:

* BMI value
* Advice text
* Background color

### BMI Struct

```swift
struct BMI {
    let value: Float
    let advice: String
    let color: UIColor
}
```

### Important

Import UIKit because `UIColor` belongs to UIKit:

```swift
import UIKit
```

---

## 3. Updating CalculatorBrain

Change:

```swift
var bmi: Float?
```

to:

```swift
var bmi: BMI?
```

BMI now stores an entire BMI object instead of just a number.

---

## 4. Accessing Values with Optional Chaining

Since `bmi` is optional:

```swift
bmi?.value
```

means:

* If `bmi` exists → get its value.
* If `bmi` is nil → return nil.

Example:

```swift
String(format: "%.1f", bmi?.value ?? 0.0)
```

---

## 5. Creating BMI Categories

Calculate BMI:

```swift
let bmiValue = weight / (height * height)
```

Classify the result:

### Underweight

```swift
if bmiValue < 18.5
```

### Normal Weight

```swift
else if bmiValue < 24.9
```

### Overweight

```swift
else
```

---

## 6. Creating BMI Objects Based on Category

### Underweight

```swift
bmi = BMI(
    value: bmiValue,
    advice: "Eat more pies!",
    color: UIColor.blue
)
```

### Normal Weight

```swift
bmi = BMI(
    value: bmiValue,
    advice: "Fit as a fiddle!",
    color: UIColor.green
)
```

### Overweight

```swift
bmi = BMI(
    value: bmiValue,
    advice: "Eat less pies!",
    color: UIColor.red
)
```

---

## 7. Using Color Literals

Instead of:

```swift
UIColor.blue
```

Use:

```swift
#colorLiteral(...)
```

Benefits:

* Visual color picker.
* Easy customization.
* Can choose RGB values directly.

---

## 8. Passing Data Between View Controllers

In `CalculateViewController`:

```swift
destinationVC.advice = calculatorBrain.getAdvice()
destinationVC.color = calculatorBrain.getColor()
```

---

## 9. Adding Properties to ResultViewController

### Advice

```swift
var advice: String?
```

### Color

```swift
var color: UIColor?
```

These are optional because values are assigned after the view controller is created.

---

## 10. Creating Getter Functions

### Get Advice

```swift
func getAdvice() -> String {
    return bmi?.advice ?? "No advice"
}
```

### Get Color

```swift
func getColor() -> UIColor {
    return bmi?.color ?? UIColor.white
}
```

### Why Default Values?

If `bmi` is nil:

* Prevent crashes.
* Provide fallback values.
* Help detect unexpected errors.

---

## 11. Displaying Data in ResultViewController

Inside `viewDidLoad()`:

### Show BMI

```swift
bmiLabel.text = bmiValue
```

### Show Advice

```swift
adviceLabel.text = advice
```

No unwrapping needed because UILabel's `text` property accepts an optional string.

---

## 12. Changing Background Color

Every `UIViewController` has a built-in `view` property.

To change the screen background:

```swift
view.backgroundColor = color
```

This updates the entire screen color according to the BMI category.

---

## Key Concepts Learned

### MVC Design Pattern

* **Model:** `BMI` struct
* **View:** Labels, colors, UI elements
* **Controller:** View Controllers and CalculatorBrain

### Optionals

* Nil checking
* Optional binding (`if let`)
* Optional chaining (`?.`)
* Nil coalescing (`??`)

### UIKit

* Import UIKit for `UIColor`

### Data Passing

* Send values from one View Controller to another using properties.

### UI Updates

* Change label text.
* Change screen background color dynamically.

---

## Final App Behavior

| BMI Category        | Advice           | Background Color |
| ------------------- | ---------------- | ---------------- |
| Underweight (<18.5) | Eat more pies!   | Blue             |
| Normal (18.5–24.9)  | Fit as a fiddle! | Green            |
| Overweight (>24.9)  | Eat less pies!   | Red              |

### Outcome

The BMI Calculator now:

1. Calculates BMI.
2. Classifies the BMI.
3. Shows personalized advice.
4. Changes background color based on BMI category.
5. Follows the MVC architecture more closely.
