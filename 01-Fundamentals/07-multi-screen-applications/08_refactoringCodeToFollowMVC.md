## Notes: Refactoring BMI Calculator to Follow MVC

### 1. Problem: View Controller Is Doing Too Much

* As the app grows, the `ViewController` is taking on too many responsibilities.
* It currently:

  * Calculates BMI.
  * Formats BMI to one decimal place.
  * Manages UI logic.
* This violates the MVC design pattern because business logic should belong in the **Model**, not the **View Controller**.

---

### 2. Moving Logic to the Model

* Create a new Swift file: **CalculatorBrain.swift**
* Add a struct:

```swift
struct CalculatorBrain {
    
}
```

* The `CalculatorBrain` model will handle:

  * BMI calculation
  * BMI interpretation
  * Advice generation
  * Background color selection

---

### 3. Updating the View Controller

Remove:

* `bmiValue`
* BMI calculation code
* BMI string formatting code

Add:

```swift
var calculatorBrain = CalculatorBrain()
```

In `calculatePressed()`:

```swift
calculatorBrain.calculateBMI(height: height, weight: weight)
```

To retrieve the result:

```swift
calculatorBrain.getBMIValue()
```

The View Controller now delegates BMI-related work to the model.

---

### 4. Implementing BMI Calculation

Create a BMI property:

```swift
var bmi: Float = 0.0
```

Add the calculation method:

```swift
mutating func calculateBMI(height: Float, weight: Float) {
    bmi = weight / (height * height)
}
```

#### Why `mutating`?

* Structs are value types.
* Changing a property inside a struct method requires the `mutating` keyword.

---

### 5. Returning the BMI Value

Create a getter method:

```swift
func getBMIValue() -> String {
    let bmiTo1DecimalPlace = String(format: "%.1f", bmi)
    return bmiTo1DecimalPlace
}
```

This:

* Converts BMI to a string.
* Rounds it to one decimal place.

---

### 6. Result of Refactoring

Benefits:

* Cleaner View Controller.
* Better separation of concerns.
* BMI logic is centralized in one place.
* Easier to maintain and extend.

---

### 7. Issue with Default BMI Value

Current implementation:

```swift
var bmi: Float = 0.0
```

Problem:

* BMI is unknown when `CalculatorBrain` is initialized.
* Assigning `0.0` is not an accurate representation of the state.

A better approach:

```swift
var bmi: Float?
```

* BMI starts as `nil`.
* Gets a value only after calculation.

---

### 8. Optional-Related Problem

If `getBMIValue()` is called before `calculateBMI()`:

```swift
bmi == nil
```

Attempting to force unwrap:

```swift
bmi!
```

causes a crash:

> "Unexpectedly found nil while unwrapping an Optional value"

Example:

* Calling `getBMIValue()` in `viewDidLoad()` before calculating BMI will crash the app.

---

### 9. Key Takeaway About Optionals

* When a value may not exist yet, use an **Optional**.
* Avoid force unwrapping (`!`) unless you're absolutely sure the value exists.
* Safer optional handling techniques will be explored in the next lesson.

---

## Summary

* Refactor BMI logic into a **CalculatorBrain** model.
* Keep the View Controller focused on UI management.
* Use a `mutating` method to update struct properties.
* Format BMI in the model using `getBMIValue()`.
* Replace placeholder values like `0.0` with Optionals when data may not yet exist.
* Avoid force unwrapping Optionals to prevent crashes.
