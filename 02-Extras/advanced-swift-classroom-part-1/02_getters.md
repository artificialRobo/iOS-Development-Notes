# Notes: Getters

## Setting Up the Playground

* Create a new **Blank iOS Playground**.
* Enable **Automatically Run** instead of Manual Run.
* Remove the default variable to start with a clean workspace.

## Playground Performance Fix

If the playground runs indefinitely:

1. Open **File Inspector**.
2. Change **Playground Settings** from **iOS** to **macOS**.
3. Replace:

   ```swift
   import UIKit
   ```

   with:

   ```swift
   import Foundation
   ```

This helps avoid a known Playground performance issue.

## Example: Pizza Size and Number of Slices

```swift
let pizzaInInches = 10
var numberOfSlices = pizzaInInches - 4
```

* `pizzaInInches` stores the pizza size.
* `numberOfSlices` stores the calculated number of slices.
* Formula used:

  ```
  numberOfSlices = pizzaInInches - 4
  ```
* For a 10-inch pizza:

  ```
  10 - 4 = 6 slices
  ```

## Stored Properties

Stored properties simply hold values.

Example:

```swift
let pizzaInInches = 10
var numberOfSlices = 6
```

* Values are manually assigned.
* If pizza size changes, `numberOfSlices` must be updated manually.

---

## Computed Properties

### Problem

When pizza size changes, the number of slices should update automatically.

### Solution

Use a computed property:

```swift
let pizzaInInches = 14

var numberOfSlices: Int {
    return pizzaInInches - 4
}
```

### How It Works

* The value is **calculated whenever it is accessed**.
* No need to manually update it.
* If `pizzaInInches` changes, `numberOfSlices` updates automatically.

Example:

```swift
let pizzaInInches = 14
// numberOfSlices = 10
```

---

## Rules for Computed Properties

### Rule 1: Must Be a Variable (`var`)

```swift
var numberOfSlices: Int {
    return pizzaInInches - 4
}
```

Not allowed:

```swift
let numberOfSlices: Int {
    return pizzaInInches - 4
}
```

Reason:

* Computed values can change, so they cannot be constants.

### Rule 2: Explicit Data Type Required

```swift
var numberOfSlices: Int {
    return pizzaInInches - 4
}
```

Reason:

* Swift cannot reliably infer the type for computed properties.
* Always specify the data type.

---

## Benefits of Computed Properties

* Automatically stay synchronized with dependent values.
* Reduce manual updates.
* Prevent bugs and inconsistencies.
* Useful for values such as:

  * Area = width × height
  * Volume = length × width × height
  * Pizza slices based on pizza size

---

## Getter

The code inside a computed property is called a **getter** because it runs when Swift needs to retrieve the property's value.

Example:

```swift
var numberOfSlices: Int {
    return pizzaInInches - 4
}
```

The getter runs when:

```swift
print(numberOfSlices)
```

or

```swift
let a = numberOfSlices * 2
```

---

## Getter Syntax (Full Form)

The previous example is shorthand. The full version is:

```swift
var numberOfSlices: Int {
    get {
        return pizzaInInches - 4
    }
}
```

* `get` defines the code that executes when the property's value is requested.
* Both versions behave the same way.

---

## Computed Property vs Function

### Function Approach

```swift
var numberOfSlices = 0

func calcPizzaSlices() {
    numberOfSlices = pizzaInInches - 4
}
```

### Drawbacks

* More code.
* Must remember to call the function.
* Greater chance of errors.

### Computed Property Approach

```swift
var numberOfSlices: Int {
    return pizzaInInches - 4
}
```

### Advantages

* Cleaner code.
* Automatic updates.
* No extra method calls required.

---

## Key Takeaways

* **Stored properties** store values directly.
* **Computed properties** calculate values dynamically.
* Computed properties:

  * Must use `var`.
  * Must specify a data type.
  * Use a **getter** to calculate and return values.
* They are often a cleaner alternative to simple calculation functions.
