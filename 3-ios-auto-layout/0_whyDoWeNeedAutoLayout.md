# Notes: Auto Layout in iOS

## Problem with App Layouts

* Apps may look fine in one orientation or screen size but break when:

  * rotating the device (portrait ↔ landscape)
  * running on different iPhone/iPad sizes
* Example:

  * Parts of the UI can get cut off
  * Users may not be able to interact with the app properly
* Before publishing an app, the UI must adapt correctly to all screen sizes and orientations.

---

# What is Auto Layout?

* **Auto Layout** is a system of rules that tells iOS how UI elements should be positioned and sized on different screens.
* These rules help the app automatically adjust layouts based on:

  * screen size
  * aspect ratio
  * orientation

---

# Example of Layout Rules

### Blue Button

* Positioned:

  * 10 px from the top
  * 10 px from the left
* Result:

  * pinned to the top-left corner

### Red Button

* Positioned:

  * horizontally centered
  * vertically centered
* Result:

  * always stays in the middle of the screen

### Green Button

* Positioned:

  * centered vertically
  * 10 px from the bottom
* Result:

  * stays near the bottom center

---

# Topics Covered in the Module

## 1. Auto Layout

* Learn the rules that control UI layout.

## 2. Size Classes

* Define layouts for different device sizes in Xcode Interface Builder.

## 3. Constraints

* Rules that specify:

  * position
  * spacing
  * sizing of UI components

## 4. Alignment & Pinning

* Design layouts for:

  * portrait mode
  * landscape mode

## 5. Containers

* Views that wrap other views.
* Provide finer control over layouts.

## 6. Stack Views

* Arrange UI elements:

  * vertically
  * horizontally

---

# Key Takeaway

Auto Layout ensures apps look good and function properly across all devices, orientations, and screen sizes by using constraints and layout rules.

---

# Setup Instructions

* Download the **AutoLayout-iOS13** starter repository from GitHub.
* Clone it to the local system.
* Open the next lesson to begin working with Auto Layout.
