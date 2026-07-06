# Notes: Prototyping with Keynote

## Overview

* Keynote can create simple and impressive UI prototype animations.
* No advanced design software is required.
* Ideal for quick prototyping on Mac.

---

## Step 1: Create a New Presentation

* Open **Keynote**.
* Create a **new presentation** with:

  * Wide format
  * White background
* Delete all default text and objects.

## Step 2: Prepare the Phone Mockup

* Paste a phone frame image.
* Change the slide background color to make the white phone visible.
* Make the phone screen transparent:

  * Select image.
  * Go to **Format → Image → Instant Alpha**.
  * Remove the white center.
* Result: Transparent phone outline.

## Step 3: Add Map Content

* Open **Google Maps**.
* Take a screenshot of the desired map.

  * Mac shortcut: **Command + Control + Shift + 4**
* Paste the screenshot into Keynote.
* Right-click → **Send to Back**.

## Step 4: Duplicate the Slide

* Copy the slide.
* Both slides must contain **exactly the same objects** for animations like **Magic Move** to work.

## Step 5: Create the Zoom Effect

* On the second slide:

  * Enlarge the map.
  * Pan it to a different location.
* This becomes the ending state of the zoom animation.

## Step 6: Hide Unwanted Map Areas

* Insert large rectangles around the phone.
* Match rectangle color to the slide background.
* Remove shadows.
* Cover everything outside the phone screen.
* Arrange layers:

  1. Phone frame (top)
  2. Covering rectangles
  3. Map (bottom)
* Copy these rectangles to the second slide.

## Step 7: Add a Map Pin

* Duplicate the slide again.
* Find a map pin image.
* Remove its white background using **Instant Alpha**.
* Resize and position the pin where desired.

## Step 8: Create Animations

### A. Zoom & Pan Animation

* Select the first slide.
* Go to **Animate → Add Effect → Magic Move**.
* Adjust:

  * Duration
  * Speed
* Example duration: **1.5 seconds**.

### B. Pin Drop Animation

* Select the pin.
* Go to:

  * **Animate → Build In**
  * Choose **Drop** effect.
* The pin drops onto the map.

---

## Final Prototype Flow

1. Display full map.
2. Zoom and pan to the target location.
3. Drop a pin onto the destination.

### Advantages

* Free with macOS.
* Very quick to create prototypes.
* Produces smooth animations.
* Great for early UI/UX demonstrations.

### Limitations

* No traditional layer panel.
* Layers must be managed using:

  * Send Forward
  * Send Backward
  * Bring to Front
  * Send to Back
* Less convenient than design tools like Photoshop.

### Key Features Used

* **Instant Alpha** – Removes image backgrounds.
* **Magic Move** – Creates smooth transitions between slides.
* **Build In → Drop** – Creates a pin drop animation.

---

## Key Takeaway

Keynote is a simple, free tool for creating UI prototype animations such as zooming, panning, and pin-drop effects. While layer management is less intuitive than dedicated graphics software, it is an effective option for fast, lightweight prototyping.
