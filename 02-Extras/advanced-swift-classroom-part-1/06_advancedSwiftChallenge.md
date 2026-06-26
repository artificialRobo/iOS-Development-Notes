# Notes: Advanced Properties Challenge

## Objective

Build a **Paint Calculator** using **computed properties** (getter and setter) instead of regular methods.

---

## 1. Create Variables

```swift
var width: Float = 1.5
var height: Float = 2.3
```

* `width` = wall width (meters)
* `height` = wall height (meters)

---

## 2. Create a Computed Property

```swift
var bucketsOfPaint: Int {
    get {
        ...
    }
}
```

* The property should calculate the number of paint buckets needed.
* Since paint is sold in whole buckets, the return type is `Int`.

---

## 3. Calculate Wall Area

Formula:

```swift
let area = width * height
```

Example:

```
1.5 × 2.3 = 3.45 m²
```

---

## 4. Paint Coverage

Each bucket covers:

```swift
let areaCoveredPerBucket: Float = 1.5
```

---

## 5. Calculate Buckets Needed

Formula:

```swift
let numberOfBuckets = area / areaCoveredPerBucket
```

Example:

```
3.45 / 1.5 = 2.3 buckets
```

---

## 6. Round Up with `ceilf()`

Simply converting to `Int`:

```swift
Int(numberOfBuckets)
```

would return:

```
2
```

This is incorrect because **2 buckets won't fully cover the wall**.

Instead use:

```swift
Int(ceilf(numberOfBuckets))
```

`ceilf()` always **rounds up**.

Examples:

* 2.1 → 3
* 2.3 → 3
* 2.9 → 3
* 3.0 → 3

---

## 7. Getter

```swift
get {
    let area = width * height
    let areaCoveredPerBucket: Float = 1.5
    let numberOfBuckets = area / areaCoveredPerBucket
    return Int(ceilf(numberOfBuckets))
}
```

Printing:

```swift
print(bucketsOfPaint)
```

Example outputs:

* Wall: **1.5 × 2.3** → **3 buckets**
* Wall: **3.4 × 2.1** → **5 buckets**

The value updates automatically whenever `width` or `height` changes.

---

## Part 2 – Add a Setter

Previously, `bucketsOfPaint` was **read-only** (getter only).

Now add a setter:

```swift
set {
    ...
}
```

---

## Setter Goal

When assigning:

```swift
bucketsOfPaint = 4
```

calculate how much wall area these buckets can cover.

---

## Area Covered

Formula:

```swift
let areaCanCover = Double(newValue) * 1.5
```

* `newValue` = new bucket count
* Convert `newValue` to `Double` because it cannot be multiplied directly by a `Double`.

---

## Print Result

```swift
print("This amount of paint can cover an area of \(areaCanCover)")
```

Example:

```swift
bucketsOfPaint = 4
```

Output:

```
This amount of paint can cover an area of 6.0
```

---

## Key Concepts Learned

* **Computed Property** calculates values automatically.
* **Getter (`get`)** returns a calculated value.
* **Setter (`set`)** performs an action when a value is assigned.
* **`newValue`** represents the value being assigned inside a setter.
* **`ceilf()`** rounds a `Float` **up** to the nearest whole number.
* Use **type casting** (`Double(newValue)` or `Int(...)`) when working with different numeric types.

### Why Computed Properties Are Useful

* Automatically update values when related variables change.
* Reduce the need for extra functions and methods.
* Keep code cleaner and easier to maintain.
* Can easily update UI elements (e.g., labels or button titles) whenever underlying data changes.

---

## **Quick Summary**

* Define `width` and `height`.
* Compute wall area (`width × height`).
* Divide by paint coverage (1.5 m² per bucket).
* Use `ceilf()` to always round **up**.
* Getter returns required buckets.
* Setter uses `newValue` to calculate total area the available paint can cover.
* Computed properties make code dynamic, reusable, and easier to maintain.
