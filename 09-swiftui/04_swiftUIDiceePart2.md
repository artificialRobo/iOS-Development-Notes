# Notes: Part 2 - Building in Functionality and Managing State

## 1. Creating Variables for Dice Values

* Added two variables inside `ContentView`:

  ```swift
  var leftDiceNumber = 1
  var rightDiceNumber = 1
  ```
* These variables determine which dice face image is displayed.
* Replaced hardcoded values in `DiceView` with:

  ```swift
  n: leftDiceNumber
  n: rightDiceNumber
  ```

---

## 2. Making the Roll Button Work

* Added code inside the button's `action` closure.
* Generated random numbers between 1 and 6:

  ```swift
  leftDiceNumber = Int.random(in: 1...6)
  rightDiceNumber = Int.random(in: 1...6)
  ```
* Purpose:

  * Simulate rolling dice.
  * Update dice images with random values.

---

## 3. Understanding the Immutability Error

* Xcode error:

  > "self is immutable"
* Reason:

  * Swift structs are immutable by default.
  * Changing a property requires creating a new copy of the struct.

---

## 4. Using `@State` Property Wrapper

* Solution:

  ```swift
  @State var leftDiceNumber = 1
  @State var rightDiceNumber = 1
  ```
* `@State` allows SwiftUI to:

  * Track changes to variables.
  * Rebuild the view when values change.

---

## 5. Using `self` Inside Closures

* Inside a closure, Swift requires explicit references:

  ```swift
  self.leftDiceNumber = Int.random(in: 1...6)
  self.rightDiceNumber = Int.random(in: 1...6)
  ```
* This clarifies that the properties belong to the current struct.

---

## 6. How SwiftUI Updates the UI

When the Roll button is pressed:

1. Random numbers are generated.
2. `@State` variables change.
3. SwiftUI detects the changes.
4. `ContentView` is rebuilt.
5. New `DiceView` instances are created.
6. Updated dice faces appear on the screen.

---

## 7. Why `@State` Is Important

* SwiftUI keeps track of all properties marked with `@State`.
* It monitors:

  * Reads
  * Writes
* SwiftUI knows which views depend on those properties.
* Only affected views are refreshed when the state changes.

---

## 8. Relationship Between Structs and State

* In regular Swift structs:

  * Functions that modify properties require the `mutating` keyword.
* In SwiftUI:

  * Properties that can change must be marked with `@State`.

Example:

```swift
@State var leftDiceNumber = 1
```

---

## Key Takeaways

* Use variables to control UI elements dynamically.
* Use `Int.random(in: 1...6)` to generate dice values.
* Swift structs are immutable by default.
* `@State` enables mutable properties in SwiftUI views.
* SwiftUI automatically rebuilds views when `@State` values change.
* State management is a core concept in SwiftUI and powers reactive UI updates.

### Final Working Logic

```swift
@State var leftDiceNumber = 1
@State var rightDiceNumber = 1

Button("Roll") {
    self.leftDiceNumber = Int.random(in: 1...6)
    self.rightDiceNumber = Int.random(in: 1...6)
}
```

**Result:** Each tap on the Roll button generates new random dice values and updates the displayed dice images automatically. 
