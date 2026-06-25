# Notes: Part 1 - Designing a Layout using Spacers and Subviews

## Module Goals

* Build a **Dicee app** using SwiftUI.
* Learn how to create an app with both:

  * User Interface (UI)
  * Functionality (user interaction)
* Practice:

  * SwiftUI layouts
  * Stacks (`VStack`, `HStack`, `ZStack`)
  * Padding and spacing
  * Creating reusable Subviews
* Main takeaway: **Managing app state in SwiftUI**.

---

## Project Setup

### Create a New Project

1. Open Xcode.
2. Create a new **iOS Single View App**.
3. Name it **Dicer-SwiftUI**.
4. Select **SwiftUI** as the User Interface.
5. Save and create the project.

### Add Assets

1. Download the Dicee assets.
2. Unzip the folder.
3. Open `Assets.xcassets`.
4. Delete the default `AppIcon`.
5. Drag all provided app icons and images into Assets.

---

# Building the UI

## 1. Add a Background Image

Use a `ZStack` to place a background image behind everything.

```swift
ZStack {
    Image("background")
        .resizable()
        .edgesIgnoringSafeArea(.all)
}
```

### Important Modifiers

* `.resizable()` → allows image resizing.
* `.edgesIgnoringSafeArea(.all)` → fills the entire screen.

---

## 2. Add the Dicee Logo

Inside the `ZStack`, add:

```swift
Image("diceeLogo")
```

---

## 3. Organize Content with VStack

Wrap UI elements in a `VStack`.

```swift
VStack {
    Image("diceeLogo")
}
```

Purpose:

* Arrange elements vertically.

---

## 4. Add Dice Images

Add an image for the dice face:

```swift
Image("dice1")
```

### Resize Properly

```swift
.resizable()
.aspectRatio(1, contentMode: .fit)
```

### Why?

* Prevents image stretching.
* Keeps the dice square (1:1 ratio).

---

## Creating a Reusable Subview

Instead of duplicating dice images:

### Create `DiceView`

```swift
struct DiceView: View {
    let n: Int

    var body: some View {
        Image("dice\(n)")
            .resizable()
            .aspectRatio(1, contentMode: .fit)
    }
}
```

### Benefits

* Reusable component.
* Dynamic dice face based on value.

Example:

```swift
DiceView(n: 1)
```

---

## Display Two Dice

Use an `HStack`:

```swift
HStack {
    DiceView(n: 1)
    DiceView(n: 1)
}
```

### Add Horizontal Padding

```swift
.padding(.horizontal)
```

Purpose:

* Prevents dice from touching screen edges.

---

## Add a Roll Button

### Button Structure

```swift
Button(action: {

}) {
    Text("Roll")
}
```

---

## Style the Button Text

```swift
.font(.system(size: 50))
.fontWeight(.heavy)
.foregroundColor(.white)
```

### Effects

* Large text
* Heavy font weight
* White text color

---

## Style the Button Background

```swift
.background(Color.red)
.padding(.horizontal)
```

Result:

* Red button
* Extra horizontal spacing

---

## Improve Dice Appearance

Add padding inside `DiceView`:

```swift
.padding()
```

Benefits:

* Creates space around dice.
* Makes layout cleaner.

---

## Using Spacer

### What is Spacer?

A flexible SwiftUI component that automatically takes up available space.

```swift
Spacer()
```

### Example Layout

```swift
VStack {
    Image("diceeLogo")

    Spacer()

    HStack {
        DiceView(n: 1)
        DiceView(n: 1)
    }

    Spacer()

    Button("Roll") {

    }
}
```

### Advantages

* Automatically adapts to different screen sizes.
* No need for manual constraints.
* Creates balanced spacing.

---

## SwiftUI Concepts Learned

### Layout Components

* `ZStack` → layers views on top of each other.
* `VStack` → vertical arrangement.
* `HStack` → horizontal arrangement.
* `Spacer()` → flexible spacing.

### Image Modifiers

* `.resizable()`
* `.aspectRatio()`
* `.edgesIgnoringSafeArea()`

### Spacing

* `.padding()`
* `.padding(.horizontal)`

### Reusable Views

* Extracting a Subview (`DiceView`)
* Using properties (`n`) to make views dynamic

---

## Key Takeaway

The UI for the Dicee app is built using:

* `ZStack` for the background
* `VStack` for vertical layout
* `HStack` for the dice
* `Spacer` for responsive spacing
* A reusable `DiceView` component

The next step is learning **SwiftUI State Management**, which will allow the **Roll** button to change the dice images dynamically.
