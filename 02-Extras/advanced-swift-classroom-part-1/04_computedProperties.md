# Notes: Computed Properties

## Purpose of the Pizza Calculator

The calculator allows users to:

* Specify the **pizza size** (in inches).
* Specify the **number of people** to feed.
* Specify **slices per person**.
* Automatically calculate how many pizzas are needed.

---

## Key Variables

```swift
pizzaInInches
numberOfPeople
slicesPerPerson
```

Example values:

* 12-inch pizza
* 6 people
* 5 slices per person

---

## Computed Property: `numberOfPizza`

A computed property is created to calculate the required number of pizzas.

```swift
var numberOfPizza: Int {
    get {
        ...
    }
}
```

### Getter Logic

1. Calculate how many people one pizza can feed:

   ```swift
   let numberOfPeopleFedPerPizza =
       numberOfSlices / slicesPerPerson
   ```

2. Calculate pizzas required:

   ```swift
   return numberOfPeople / numberOfPeopleFedPerPizza
   ```

### Benefit

* No need to manually recalculate.
* Whenever dependent values change, the getter automatically computes the latest result.

Example:

* 12-inch pizzas
* 6 people
* 5 slices each

Result:

* Need **6 pizzas**.

---

## Dynamic Updates

If values change, the computed property updates automatically.

Example:

* Pizza size: 16 inches
* People: 12
* Slices per person: 4

When `numberOfPizza` is accessed, Swift automatically runs the getter and calculates the new result.

**No extra method calls are required.**

---

## Adding a Setter

A setter makes the computed property writable.

```swift
set {
    ...
}
```

### Purpose

Instead of calculating pizzas needed, calculate **how many people can be fed** with a given number of pizzas.

### Setter Logic

1. Calculate total slices:

   ```swift
   let totalSlices = numberOfSlices * newValue
   ```

   * `newValue` is the value being assigned to the property.
   * It is predefined by Swift and cannot be renamed.

2. Calculate number of people:

   ```swift
   numberOfPeople = totalSlices / slicesPerPerson
   ```

3. `numberOfPeople` must be declared as a `var` because it is modified by the setter.

---

## Example of Setter Usage

```swift
numberOfPizza = 4
```

Given:

* Four 16-inch pizzas

The setter calculates:

* Total slices available
* Number of people that can be fed

Result:

* Can feed **12 people**.

---

## Advantages of Computed Properties

* Automatically update values when dependencies change.
* Reduce repetitive code.
* Minimize errors.
* Improve maintainability.
* Make code easier to understand.

---

## Real-World Analogy: Spreadsheet

Computed properties work like a spreadsheet:

* Change an input value (e.g., pizza size).
* All dependent values update automatically.
* No need to manually recalculate everything.

**Main Idea:** Computed properties use **getters** to calculate values on demand and **setters** to update related data, creating dynamic and maintainable code.
