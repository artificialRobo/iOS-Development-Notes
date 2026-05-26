# Notes: Building the Dicee App UI in Xcode

## 1. Setting Up the Background Image

* Open `Main.storyboard`.
* Add an **Image View** from the Object Library.
* Resize it to cover the entire screen.
* Go to `Assets.xcassets` and use the provided `green background` image.
* In the **Attributes Inspector**, set the Image View’s image to `green background`.

### Image View Content Modes

Three important display modes:

1. **Aspect Fit**

   * Keeps image proportions.
   * Entire image remains visible.
   * May leave empty spaces.

2. **Scale to Fill**

   * Stretches image to fill the entire area.
   * Can distort the image.

3. **Aspect Fill**

   * Fills the entire area while keeping proportions.
   * Some parts of the image may be cropped.

> For the background, either **Scale to Fill** or **Aspect Fill** works.

---

## 2. Adding the Dicee Logo

* Add another **Image View**.
* Set its image to the `Dicee logo`.
* Position it near the upper third of the screen.

---

## 3. Adding the First Dice Image

* Add an **Image View**.
* Set the image to `DiceOne`.
* Use the **Size Inspector** to set:

  * Width = `120`
  * Height = `120`
* Place it near the middle-left of the screen.

---

## 4. Duplicating UI Elements Quickly

### Shortcut:

* Hold `Option/Alt`
* Click and drag the element
* Release mouse before releasing the key

This creates an exact copy of the selected element.

Useful for:

* Duplicating dice images
* Creating multiple identical UI components quickly

---

## 5. Adding a Button

* Add a **Button** from the Object Library.
* Change the button title to `Roll`.

### Customize the Button

* Increase font size (example: `30 pt`)
* Change text color to white
* Change background color

### Design Tip

Use the **Color Picker/Dropper Tool** to match the button color with the dice background for a consistent UI theme.

---

# Key Xcode Concepts Learned

* Using `Main.storyboard`
* Adding UI elements from the Object Library
* Working with Image Views
* Understanding content modes
* Editing properties in the Attributes Inspector
* Resizing elements in the Size Inspector
* Duplicating UI elements efficiently
* Styling buttons and maintaining color consistency

---

# Next Step

The next lesson will focus on:

* Using `ViewController.swift`
* Changing UI elements with code instead of manually in the storyboard.
