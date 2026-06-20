# Introduction: SwiftUI

## What is SwiftUI?

* **SwiftUI** is Apple’s modern UI framework introduced at **WWDC 2019**.
* It uses **declarative Swift code** to build user interfaces.
* Designed to make iOS development easier, especially for beginners.

---

## Drag-and-Drop Interface

* Developers can drag UI elements (Text, Buttons, etc.) from the Object Library.
* SwiftUI automatically generates the required code.
* Properties like:

  * Font
  * Font weight
  * Colors
  * Other attributes
* can also be dragged onto components.

### Live Preview Canvas

* UI updates instantly as code or components are modified.
* Makes designing and testing interfaces much faster.

---

## Easy Layouts VHZ Stack

SwiftUI simplifies layouts using three types of stacks:

### VStack (Vertical Stack)

* Arranges elements vertically (top to bottom).

### HStack (Horizontal Stack)

* Arranges elements horizontally (side by side).

### ZStack (Depth Stack)

* Places elements on top of each other (layered view).

**Example:**

* Purple background
* Black circle on top
* Button above the circle

The order of elements in a ZStack determines their layer position.

---

## Highly Reusable UI

SwiftUI encourages reusable UI components.

### How it works:

1. Build a UI component.
2. Extract it as a **Subview**.
3. Give it a name.
4. Add properties for dynamic content.

**Example:**

* Create a `BookView`
* Pass different book titles as properties
* Reuse the same design multiple times

### Benefits:

* Less duplicate code
* Easier maintenance
* Faster development

---

## Lists and Forms

### List

* Similar to a table view.
* Displays multiple items in a scrollable list.

### Form

* Groups related controls together.
* Useful for settings screens and data entry forms.

Simply replacing a `VStack` with a `List` or `Form` changes the interface structure.

---

## Live Interactive Preview

SwiftUI provides a **live preview mode** where developers can:

* Interact with text fields
* Use steppers
* Select picker options
* Test scrolling

without:

* Running the app
* Launching a simulator
* Using a physical device

---

## Cross-Platform Development in Apple Ecosystem

SwiftUI allows developers to build interfaces across Apple's platforms:

* iPhone (iOS)
* iPad (iPadOS)
* Mac (macOS)
* Apple Watch (watchOS)

### Advantages

* Reuse UI code across platforms.
* Maintain consistent app designs.

---

## Project Catalyst

**Project Catalyst** lets developers convert iPad/iPhone apps into Mac apps.

### Process:

1. Build an iOS app.
2. Enable Mac support in project settings.
3. Run the app on macOS.

### Benefit:

* Easier expansion from iOS to Mac.

---

## Requirements for SwiftUI Development

### macOS

* macOS Catalina (10.15) or later
* Latest version recommended

### Xcode

* Xcode 11.0 or later

### Device Requirements

SwiftUI apps require **iOS 13+**.

Supported devices include:

* iPhone 6S and newer
* iPhone SE
* iPad Air 2 and newer
* iPad Mini 4 and newer

Older devices cannot run SwiftUI apps.

---

## Current State of SwiftUI (At Introduction)

* SwiftUI was considered an **early-adopter technology** when introduced.
* Initially, few major production apps used it.
* Learning SwiftUI early provides a head start for future iOS development.

---

## Quick Revision

### SwiftUI

* Apple’s declarative UI framework introduced in 2019.

### Main Layout Containers

* `VStack` → Vertical layout
* `HStack` → Horizontal layout
* `ZStack` → Layered layout

### Major Benefits

* Drag-and-drop UI creation
* Live previews
* Reusable components
* Cross-platform development
* Easier Mac app creation through Project Catalyst

### Requirements

* macOS Catalina+
* Xcode 11+
* iOS 13+ devices only
