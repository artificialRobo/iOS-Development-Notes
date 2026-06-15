## Notes: Creating UI Programmatically in Swift (Without Storyboards)

### 1. Creating a UILabel in Code

* A label can be created entirely through code instead of using the Object Library.
* Components created from the Object Library are connected using **IBOutlets**.
* You can **Option + Click** a component in Xcode to inspect its class type.

  * `heightSlider` → `UISlider`
  * `weightLabel` → `UILabel`

### 2. Setting a Label's Frame

* Programmatically created labels do not automatically have a size or position.
* Use the `frame` property to define:

  * Position (`x`, `y`)
  * Size (`width`, `height`)

```swift
label.frame = CGRect(x: 0, y: 0, width: 100, height: 50)
```

* `CGRect` stands for **Core Graphics Rectangle**.
* Example above places the label:

  * Top-left corner `(0,0)`
  * Width: `100`
  * Height: `50`

---

### 3. Adding the Label to the Screen

* Every `UIViewController` contains a root `view`.
* To display the label, add it as a subview:

```swift
view.addSubview(label)
```

* `addSubview()` adds a child view to a parent view.

#### Why does UILabel work with addSubview()?

* `addSubview()` expects a `UIView`.
* `UILabel` inherits from `UIView`.
* Therefore, a label can be used anywhere a `UIView` is expected.

Inheritance:

```text
UIView
  └── UILabel
```

---

### 4. Setting a Background Color

* A new view controller's view starts transparent.
* Set a background color to make it visible:

```swift
view.backgroundColor = .red
```

* `.red` is shorthand for:

```swift
UIColor.red
```

---

### 5. Presenting a Second View Controller

* Create an instance of the second view controller:

```swift
let secondVC = SecondViewController()
```

* Display it using the current view controller:

```swift
self.present(secondVC, animated: true, completion: nil)
```

Parameters:

* `animated: true` → show transition animation.

* `completion: nil` → no extra action after presentation.

* This code is typically placed inside the `calculatePressed` IBAction.

---

### 6. Passing Data Between View Controllers

#### Step 1: Create a Property in SecondViewController

```swift
var bmiValue = "0.0"
```

#### Step 2: Display the Property in the Label

```swift
label.text = bmiValue
```

#### Step 3: Pass Data Before Presenting

```swift
secondVC.bmiValue = ...
```

* Assign the BMI value before presenting the second view controller.

---

### 7. Converting BMI (Float) to String

* The calculated BMI is a floating-point number.
* `bmiValue` expects a string.

Use string formatting:

```swift
secondVC.bmiValue = String(format: "%.1f", bmi)
```

* `%.1f` rounds the value to **1 decimal place**.

Example:

```text
22.47 → 22.5
```

---

## Key Concepts Learned

* Create UI elements completely in code.
* Use `CGRect` to define size and position.
* Add views using `addSubview()`.
* Understand inheritance (`UILabel` → `UIView`).
* Customize views with properties such as `backgroundColor`.
* Present view controllers programmatically using `present()`.
* Pass data between view controllers through properties.
* Convert numbers to strings using `String(format:)`.

### Step-by-step overview

```text
- Create UILabel
- Set frame (position & size)
- Add to parent view
- Customize appearance
- Create SecondViewController
- Pass BMI value
- Present View Controller
- Display BMI in label
```

**Note:** You can build an entire user interface, navigate between screens, and pass data without using Storyboards.
