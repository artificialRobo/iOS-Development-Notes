# Notes: Containers and Subviews in Xcode

## 1. Reviewing Basic Constraints

* The green background view should:

  * Cover all four sides of the screen.
  * Ignore safe areas.
  * Work in both portrait and landscape orientations.

### Steps:

1. Select the green background view.
2. Add constraints:

   * Top = 0
   * Bottom = 0
   * Leading = 0
   * Trailing = 0
3. Ensure constraints are attached to the **Superview**, not the Safe Area.
4. Check layout in portrait and landscape.
5. Inspect constraints in the **Attribute Inspector**.

---

## 2. Problem With More Complex Layouts

The screen contains:

* A logo
* Two dice images
* A roll button

Challenges:

* Alignment alone won’t work because nothing is centered in the overall screen.
* Pinning alone won’t work because there isn’t enough vertical space.

---

## 3. Solution: Use Container Views

Split the screen into **three equal sections** using empty UIViews (containers).

Each UI element gets placed inside its own container:

* Top container → Logo
* Middle container → Dice images
* Bottom container → Roll button

This makes layout management easier.

---

## 4. Creating Container Views

### Method 1: Drag a UIView

* Open the **Object Library**.
* Search for **UIView**.
* Drag it onto the screen.
* Resize it as needed.

### Embedding Elements Inside Views

To place the logo inside a container:

* Drag the logo into the view hierarchy until it becomes indented under the container.

Indentation means:

* The element is **inside** the container.
* If aligned side-by-side, it is not embedded.

---

## 5. Other Ways to Embed Views

### Method 2:

* Select elements.
* Go to:

  * **Editor → Embed In → View**

### Method 3:

* Use the **Embed** button.
* Choose **View**.

All methods achieve the same result.

---

## 6. Renaming Views

To avoid confusion:

1. Select a view.
2. Open the **Identity Inspector**.
3. Rename views:

   * `TopView`
   * `MiddleView`
   * `BottomView`

Important:

* Ensure all three views are at the same hierarchy level.
* None should accidentally be embedded inside another.

---

## 7. Aligning Elements Inside Containers

Example:

* The Dicee logo can be:

  * Horizontally centered
  * Vertically centered
    inside `TopView`.

---

## 8. Constraint Errors & Ambiguous Layouts

After centering the logo, Xcode may show errors because:

* The logo has constraints,
* BUT the container view itself has no position constraints.

The container’s:

* X position
* Y position

are undefined.

This creates an **ambiguous layout**.

---

## Key Concept

Constraints must be added to:

1. The UI elements
2. Their container views

Otherwise, Auto Layout cannot determine where to place them.
