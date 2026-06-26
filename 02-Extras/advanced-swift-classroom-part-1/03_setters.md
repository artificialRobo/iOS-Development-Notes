# Notes: Setters

## What is a Setter?

* A **setter** is a block of code that runs whenever a computed property's value is **assigned (set)**.
* It is defined using the `set` keyword inside a computed property.

### Example

```swift
var numberOfSlices: Int {
    get {
        // return value
    }
    set {
        print("numberOfSlices now has a new value which is \(newValue)")
    }
}
```

### `newValue`

* Inside a setter, Swift provides a special variable called **`newValue`**.
* `newValue` contains the value being assigned to the property.

Example:

```swift
numberOfSlices = 12
```

Output:

```swift
numberOfSlices now has a new value which is 12
```

## Why Use a Setter?

* Lets you detect the exact moment a property's value changes.
* Allows you to:

  * Perform calculations.
  * Run additional code.
  * React to value updates automatically.

## Read-Only Computed Properties

* If a computed property has only a `get` block and no `set` block, it becomes **read-only**.

Example:

```swift
var numberOfSlices: Int {
    get {
        return 8
    }
}
```

Attempting to assign a value:

```swift
numberOfSlices = 12
```

Results in:

```swift
Cannot assign to value: 'numberOfSlices' is a get-only property
```

---

## Key Takeaways

* **Getter (`get`)** → Executes when the property's value is accessed.
* **Setter (`set`)** → Executes when the property's value is assigned.
* **`newValue`** → Automatically holds the incoming value in a setter.
* A computed property with only a getter is **read-only** and cannot be assigned a new value.
