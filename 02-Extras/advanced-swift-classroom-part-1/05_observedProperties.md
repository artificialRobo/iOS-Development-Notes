# Notes: Observed Properties (`willSet` & `didSet`)

## What are Observed Properties?

* Used to **monitor changes** to a property's value.
* Unlike **computed properties**, observed properties do **not** calculate values.
* They simply execute code **before** or **after** a property's value changes.

> Use observed properties when you want to react to value changes rather than compute values.

---

## Property Observers

Swift provides two observers:

### `willSet`

* Runs **before** the property value changes.
* Gives access to:

  * `newValue` → the value that will be assigned.

Example:

```swift
willSet {
    print(newValue)
}
```

### `didSet`

* Runs **after** the property value changes.
* Gives access to:

  * `oldValue` → the property's previous value.

Example:

```swift
didSet {
    print(oldValue)
}
```

---

## Important Rule

Observed properties **must be declared with `var`**, not `let`.

```swift
var pizzaInInches = 10
```

---

## Accessing Values

### Inside `willSet`

* `newValue` → incoming value.
* `pizzaInInches` → current value (before change).

Example:

```swift
willSet {
    print(newValue)         // New value
    print(pizzaInInches)    // Old/current value
}
```

### Inside `didSet`

* `oldValue` → previous value.
* `pizzaInInches` → updated value.

Example:

```swift
didSet {
    print(oldValue)         // Previous value
    print(pizzaInInches)    // New value
}
```

---

## Order of Execution

If:

```swift
pizzaInInches = 8
```

Execution order:

1. `willSet`

   * `newValue = 8`
   * `pizzaInInches = 10`
2. Value changes to `8`
3. `didSet`

   * `oldValue = 10`
   * `pizzaInInches = 8`

---

## Practical Example: Validation

Observed properties can enforce valid values.

Example:

```swift
var pizzaInInches = 10 {
    didSet {
        if pizzaInInches >= 18 {
            print("Invalid size specified.")
            pizzaInInches = 18
        }
    }
}
```

If someone sets:

```swift
pizzaInInches = 33
```

Output:

```
Invalid size specified.
```

Final value:

```swift
pizzaInInches == 18
```

The property automatically resets to a valid value.

---

## When to Use Observed Properties

Use them to:

* Validate user input.
* Restrict values to acceptable ranges.
* Print logs when values change.
* Trigger updates after a property changes.
* Execute additional logic whenever a property is modified.

---

## Computed Properties vs Observed Properties

| Computed Properties                               | Observed Properties                     |
| ------------------------------------------------- | --------------------------------------- |
| Calculate a value.                                | Monitor value changes.                  |
| Use `get` and `set`.                              | Use `willSet` and `didSet`.             |
| Used when property value depends on other values. | Used when you want to react to changes. |

---

## Key Takeaways

* Observed properties watch for changes to a property's value.
* `willSet` runs **before** the value changes (`newValue` available).
* `didSet` runs **after** the value changes (`oldValue` available).
* Property observers require a **`var`**.
* They are useful for **validation, logging, enforcing limits, and triggering additional logic** after a value changes.
