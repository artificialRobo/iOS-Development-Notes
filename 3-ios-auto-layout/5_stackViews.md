# Notes: Stack Views in Auto Layout

## Problem with Container Views

* Container views were created to organize UI elements.
* However, the containers themselves had:

  * no dimensions
  * no positions
  * no layout constraints
* Because of this, Auto Layout becomes **ambiguous**.

---

# Stack Views

## What is a Stack View?

A **StackView** arranges views automatically:

* **Vertical Stack** → views placed top-to-bottom
* **Horizontal Stack** → views placed side-by-side

Example:

* Top, Middle, Bottom views → vertical stack
* Two dice views → horizontal stack

---

# Embedding Views in a Stack View

## How to Embed

1. Select multiple views
2. Go to:

   * **Editor → Embed In → Stack View**
   * or use the Stack View button

After embedding:

* Xcode understands how the views relate to each other.

---

# Stack View Still Needs Constraints

Even after embedding:

* Xcode still doesn’t know:

  * where the stack starts
  * where it ends

Therefore:

* The **StackView itself** needs constraints relative to its **superview**.

---

# Constraining the Stack View

## Goal

Make the StackView:

* fill the screen
* stay inside safe areas

## Constraints Added

Set:

* Top = 0
* Bottom = 0
* Leading = 0
* Trailing = 0

Relative to:

* **Safe Area**

### Important Note

Sometimes Safe Area doesn’t appear as an option because:

* the StackView extends outside the safe area

Fix:

* move the StackView slightly inside the safe area first.

---

# Configuring the Stack View

## Axis

StackView automatically chooses:

* **Vertical axis** if views are vertically arranged
* **Horizontal axis** if views are side-by-side

---

## Distribution

Set distribution to:

```text
Fill Equally
```

Purpose:

* all contained views get equal size
* example: equal heights in a vertical stack

---

# Aligning Elements Inside Containers

Once StackViews are configured:

* aligning elements becomes easier

Example:

* Roll button centered horizontally & vertically inside Bottom View

---

# Creating a Horizontal Stack

For the dice:

1. Select both dice views
2. Embed in StackView
3. Xcode automatically creates a horizontal stack
4. Center the stack inside the middle container

---

# Spacing in Stack Views

## Vertical Stack

* spacing can be adjusted
* larger spacing → more distance between views

Example:

```text
Spacing = 30
```

But small spacing is usually better for compact layouts.

---

## Horizontal Stack

Example:

```text
Spacing = 50
```

Keeps dice slightly apart.

---

# Removing Container Backgrounds

Container views were only for layout.

To make UI clean:

* change background to:

  * Default
  * Transparent/Clear

Result:

* layout remains
* containers become invisible

---

# Button Sizing Behavior

## Why the Roll Button Shrinks

The button:

* was centered
* had no width/height constraints

So Auto Layout:

* resized it to fit its text content

---

# Adding Size Constraints

Example:

* Width = 100
* Height = 50

Problem:

* fixed width may clip longer text

---

# Auto Layout Warning Solution

Instead of:

```text
Width = 100
```

Use:

```text
Width ≥ 100
```

Meaning:

* minimum width is 100
* button can expand if text is longer

This avoids clipping.

---

# Key Auto Layout Concepts Learned

## Constraints

* Alignment constraints
* Pinning constraints

## Stack Views

* Vertical stacks
* Horizontal stacks

## Constraint Modifiers

* Greater than or equal to
* Less than or equal to

---

# Main Takeaway

StackViews simplify UI layout by:

* automatically arranging views
* reducing manual constraints
* adapting layouts across orientations and screen sizes

Combined with proper constraints and safe areas, they make Auto Layout much easier to manage.
