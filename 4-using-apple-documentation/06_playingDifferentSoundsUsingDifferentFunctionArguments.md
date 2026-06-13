# Notes: Playing Different Xylophone Sounds using Functions with Inputs/Arguments

## Goal

Modify the `playSound` function so that it can play different sounds depending on which xylophone key is pressed.

---

## Challenge Tasks

1. Add a **String parameter** called `soundName` to `playSound`.
2. Replace the hardcoded sound file name (`"C"`) with `soundName`.
3. Pass `sender.currentTitle` as the argument when calling `playSound`.
4. Handle the optional value returned by `sender.currentTitle`.

---

## Step 1: Add a Parameter to `playSound`

Before:

```swift
func playSound() {
    // plays C.wav
}
```

After:

```swift
func playSound(soundName: String) {
    // plays soundName.wav
}
```

**Key Idea:**
Functions can accept inputs (parameters), allowing them to work with different values instead of fixed ones.

---

## Step 2: Use the Parameter Inside the Function

Replace the hardcoded sound file name:

```swift
resourceName: soundName
```

Instead of always playing `"C.wav"`, the function now plays whichever sound name is passed in.

---

## Step 3: Pass an Argument When Calling the Function

When calling `playSound`, provide the button's title:

```swift
playSound(soundName: sender.currentTitle!)
```

**Flow:**

* User taps a button.
* `sender.currentTitle` gets the button title (e.g., `"C"`, `"D"`, `"E"`).
* That title is passed as `soundName`.
* The corresponding `.wav` file is played.

Example:

```swift
"C" → soundName → C.wav
"D" → soundName → D.wav
```

---

## Step 4: Understanding the Exclamation Mark (`!`)

`sender.currentTitle` has the type:

```swift
String?
```

This means it is an **optional String**, which could contain:

* A valid string value, or
* `nil` (no value)

Using:

```swift
sender.currentTitle!
```

force unwraps the optional.

**Why is it safe here?**

* Every button connected to the IBAction has a title.
* Therefore, `currentTitle` will not be `nil`.

The `!` tells Swift:

> "I've checked this value exists, so use it as a normal String."

---

## Result

Each button now plays its own sound:

| Button Pressed | Sound Played |
| -------------- | ------------ |
| C              | C.wav        |
| D              | D.wav        |
| E              | E.wav        |
| F              | F.wav        |
| G              | G.wav        |
| A              | A.wav        |
| B              | B.wav        |

---

## Key Concepts Learned

### Function Parameters

Inputs defined in a function.

```swift
func playSound(soundName: String)
```

### Function Arguments

Actual values passed into a function.

```swift
playSound(soundName: "C")
```

### Optionals

A variable that may contain a value or `nil`.

```swift
String?
```

### Force Unwrapping

Extracting the value from an optional using `!`.

```swift
sender.currentTitle!
```

---

## Summary

The Xylophone app was completed by:

* Creating a reusable `playSound(soundName:)` function.
* Passing the button title dynamically as the sound name.
* Using `sender.currentTitle!` to handle the optional string.
* Allowing each xylophone key to play its corresponding sound file automatically.

This demonstrates how **function parameters, arguments, and optionals** can be used to make code more flexible and reusable.
