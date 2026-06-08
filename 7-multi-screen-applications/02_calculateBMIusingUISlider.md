# Notes: Calculate BMI using UISliders in Swift

## Accessing Slider Values Outside IBAction

* `sender.value` only works inside the slider’s IBAction because `sender` refers to the slider that triggered the action.
* To access slider values elsewhere (like inside a button action), create **IBOutlets** for the sliders.

### Example

```swift
@IBOutlet weak var heightSlider: UISlider!
@IBOutlet weak var weightSlider: UISlider!
```

* These outlets connect directly to the sliders in Interface Builder.
* Now their values can be accessed anywhere in the `ViewController`.

---

# Calculate Button IBAction

A new IBAction is created for the Calculate button:

```swift
@IBAction func calculatePressed(_ sender: UIButton) {

}
```

Inside this action:

```swift
let height = heightSlider.value
let weight = weightSlider.value
```

---

# BMI Formula

BMI is calculated using:

[
BMI = \frac{weight}{height^2}
]

BMI = \frac{weight}{height^2}

Where:

* Weight is in kilograms
* Height is in meters

---

# Implementing BMI in Swift

### Method 1: Multiply Height by Itself

```swift
let bmi = weight / (height * height)
```

### Method 2: Using `pow()`

Swift provides a power function:

```swift
let bmi = weight / pow(height, 2)
```

* `pow(number, exponent)`
* `pow(height, 2)` means “height squared”

---

# Printing BMI

```swift
print(bmi)
```

Example:

* Height = `1.8`
* Weight = `63`

Result:

```swift
19.44
```

---

# Important: BODMAS / Order of Operations

Programming follows mathematical order of operations:

1. Brackets `()`
2. Exponents or powers
3. Division & multiplication
4. Addition & subtraction

---

# Common Mistake

Incorrect:

```swift
weight / height * height
```

This evaluates as:

```swift
(weight / height) * height
```

which gives the wrong BMI.

Correct:

```swift
weight / (height * height)
```

or

```swift
weight / pow(height, 2)
```

---

# Key Concepts Learned

* Using `UISlider`
* Creating `IBOutlets`
* Accessing slider values globally
* Creating button IBActions
* Performing BMI calculations
* Using `pow()` in Swift
* Understanding BODMAS/operator precedence

---

# Next Topic

The next lesson introduces **Classes** in Swift.
