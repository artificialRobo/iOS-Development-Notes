# Notes: Advanced Swift Properties

## 1. What Are Properties?

* Properties store data related to an object or class.
* A property can be:

  * **Constant (`let`)**
  * **Variable (`var`)**
* Example:

  ```swift
  let color = "red"
  var type = "coupe"
  ```
* Both constants and variables can be properties.

---

## 2. Stored Properties

* The properties used so far are called **stored properties**.
* They act like containers that:

  * Hold a value.
  * Store the value until it is needed.
  * Allow retrieval of the stored value later.

**Example:**

```swift
var color = "red"
var type = "coupe"
```

These values are stored directly in the properties.

---

## 3. Computed Properties

* A different type of property is the **computed property**.
* Instead of storing a value directly, it **calculates a value when needed** using code.
* The value is generated "on the fly."

**Key Idea:**

* Stored Property → stores data.
* Computed Property → calculates data.

---

## 4. Spreadsheet Analogy

* Computed properties work similarly to formulas in an Excel spreadsheet.
* If one value changes, the computed result automatically updates.

**Example:**

* Wall Area = Height × Width
* If the wall height changes from **2.6 m** to **2.3 m**, the area is automatically recalculated.

---

## 5. Benefits of Computed Properties

* Avoid storing redundant data.
* Ensure values are always up-to-date.
* Automatically reflect changes in related properties.
* Useful for calculations based on existing data.

---

## Key Takeaway

**Stored properties** keep values in memory, while **computed properties** generate values dynamically based on other data. Computed properties are especially useful when a value depends on other properties and should automatically update when those properties change.
