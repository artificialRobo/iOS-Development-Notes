# Notes: Dark Mode and Vector Assets

## 1. Dark Mode in iOS 13

* iOS 13 introduced **Dark Mode**, allowing apps to automatically adapt their appearance.
* Users can switch between **Light** and **Dark** appearance system-wide.
* Developers should design apps to support both modes for a better user experience.

### How to Preview Dark Mode

* In **Interface Builder**, open the **Size Inspector**.
* Change **Interface Style** between:

  * Light
  * Dark
* This previews how the UI will appear in each mode.

---

## 2. SF Symbols

* **SF Symbols** is a collection of over **1,500 Apple-designed icons** introduced in iOS 13.
* Available for apps targeting **iOS 13 and later**.
* Useful for weather icons and many other UI elements.
* Icons can be selected:

  * From the SF Symbols browser.
  * By typing the symbol name (e.g., `cloud.rain`).

### Benefits

* Fully vector-based.
* Automatically scales to different screen sizes.
* Remains sharp on all devices without extra work.

---

## 3. Using System Colors for Dark Mode

* Custom colors do **not** automatically adapt to Dark Mode.
* System colors (e.g., Label Color, System Pink, System Orange) automatically adjust.

### Example

* **Label Color**

  * Light Mode → Black
  * Dark Mode → White

### Recommendation

* Prefer system colors whenever possible for automatic Dark Mode support.

---

## 4. Creating Custom Colors That Support Dark Mode

When a custom color is needed:

1. Open **Assets.xcassets**.
2. Create a **New Color Set**.
3. Set **Appearances → Any, Light, Dark**.
4. Define:

   * Light mode color
   * Dark mode color
5. Give the color set a name (e.g., `weatherColor`).
6. Use the named color in Interface Builder.

### Result

* The color automatically changes based on the current appearance.

---

## 5. Vector Assets vs Raster Images

### Raster Images (PNG/JPEG)

* Made of pixels.
* Become blurry or pixelated when enlarged.
* Require multiple resolutions:

  * 1x
  * 2x
  * 3x

### Vector Images (PDF)

* Defined mathematically.
* Stay sharp at any size.
* One file works across all screen resolutions.

---

## 6. Using PDF Vector Assets

To use a PDF as a vector asset:

1. Drag the PDF into **Assets.xcassets**.
2. Enable:

   * **Preserve Vector Data**
3. Change scaling to:

   * **Single Scale**
4. Use the asset in the app.

### Benefits

* Smaller asset management workload.
* Sharp appearance on iPhone and iPad screens.

---

## 7. Different Images for Light and Dark Mode

Assets can contain different versions for each appearance.

### Steps

1. Select the image asset.
2. Change **Appearances** to:

   * Any, Light, Dark
3. Assign:

   * Light Mode image (`light_background.pdf`)
   * Dark Mode image (`dark_background.pdf`)

### Result

* Light Mode → Trees and mountains background.
* Dark Mode → Moon, stars, clouds, and mountains background.

The app automatically switches between them when the system appearance changes.

---

## 8. Storyboard Preview vs Actual Device

* Vector images may appear blurry inside **Main.storyboard** because Interface Builder uses a fixed preview image.
* When run on:

  * Simulator
  * Physical device
* The vector asset renders at full resolution and remains sharp.

---

## Key Takeaways

* **Dark Mode** support was introduced in iOS 13.
* Use **System Colors** for automatic appearance adaptation.
* Create **named color assets** for custom Dark Mode colors.
* **SF Symbols** provide scalable vector icons built into iOS.
* **PDF vector assets** stay sharp at any size and replace multiple image scales.
* Assets can provide separate versions for **Light** and **Dark** appearances.
* Vector assets look best when the app runs on a device or simulator.
