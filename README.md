# HTML2

Learn advanced HTML &amp; CSS to build clean, modern web pages. Topics include responsive layouts, typography, images, forms, transformations, animations, and clean CSS practices. Master the techniques to design professional, visually engaging, and user-friendly websites.

## Lesson: Setting Up a New GitHub Repo (The Correct Way)

1. **Create a New Repository on GitHub**

   - Go to [github.com/new](https://github.com/new)
   - Add a **repository name** (e.g. `HTML2`)
   - ✅ Check the boxes for:
     - “Add a README file”
     - “Add .gitignore” → choose `Node` or your language of choice
   - Click **Create Repository**

2. **Clone the Repo to Your Local Machine**

   - Navigate to your main projects folder (not inside another repo):
     ```bash
     cd ~/Dev-Projects/Mosh
     ```
   - Clone the repository:
     ```bash
     git clone https://github.com/Dev-Craig44/HTML2.git
     ```
   - This creates a new folder:
     ```
     ~/Dev-Projects/Mosh/HTML2
     ```

3. **Verify and Pull Remote Changes**

   - Move into your project folder:
     ```bash
     cd HTML2
     ```
   - Make sure your local repo is connected:
     ```bash
     git remote -v
     ```
   - Pull any updates from the remote:
     ```bash
     git pull origin main
     ```

4. **Push Local Changes Back to GitHub**
   - Stage and commit your work:
     ```bash
     git add .
     git commit -m "📦 Initialize local project and sync with remote"
     ```
   - Push to GitHub:
     ```bash
     git push -u origin main
     ```

---

**🧠 Quick Tip:**  
Always run `git clone` _one level above_ your target folder.  
Never clone inside an existing repo — it creates a nested repo and breaks the workflow.

## What You Need To Know

- Basic HTML elements
- Basic CSS properties
- CSS selectors & pseudo-classes
- Chrome DevTools

## 1. Layouts

### Intro

- CSS Box Model
- Sizing elements
- Overflowing
- Measurement units
- Positioning elements
- Floating elements
- Flexbox & Grid layouts
- Media queries

### The Box Model

At the core of every HTML element lies the **content area** — where your actual content (text, images, etc.) is displayed. Surrounding this content are three distinct layers:

- **Padding**: Creates space between the content and the border
- **Border**: A visible line that wraps around the element
- **Margin**: Adds space outside the border, separating elements from each other

#### Margin Collapsing

When two vertical margins meet, they **collapse** into a single margin equal to the larger of the two values. This prevents excessive spacing between stacked elements and maintains consistent vertical rhythm in your layouts.

**Example:**

```css
.element-1 {
  margin-bottom: 20px;
}
.element-2 {
  margin-top: 30px;
}
/* Result: 30px gap between elements (not 50px) */
```

### Sizing Elements

When working with CSS, understanding how element sizing works is crucial for creating predictable layouts.

#### Default Box Model Behavior

By default, the `width` and `height` properties only apply to an element's **content area**. When you add `padding` or `border`, these values are added to the specified dimensions, making the element larger than intended.

**Example:**

```css
.box {
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 2px solid black;
  background-color: gold;
}
/* Total size: 124px × 124px (100 + 20 + 4) */
```

#### The box-sizing Solution

The `box-sizing` property allows you to control how the box model calculates an element's total size:

```css
.box {
  box-sizing: border-box;
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 2px solid black;
}
/* Total size remains: 100px × 100px */
```

#### Universal Box-Sizing Reset

Rather than applying `box-sizing` to individual elements, use the universal selector to apply it globally:

```css
* {
  box-sizing: border-box;
}
```

This ensures consistent sizing behavior across all elements on your page.

#### Sizing Limitations with Inline Elements

The `width` and `height` properties only work on **block-level** elements. Inline elements ignore these properties entirely.

To size inline elements, change their display property:

```css
.inline-element {
  display: inline-block; /* or block */
  width: 200px;
  height: 50px;
}
```

**Note:** Margins do not affect an element's actual size — they only add space around it.

### Overflowing

When an element's content exceeds its defined size, it can overflow its container. The `overflow` property controls how this excess content is handled.

- **Visible** (default): Content spills out of the container.
- **Hidden**: Excess content is clipped and not visible.
- **Scroll**: Adds scrollbars to view the overflowing content.
- **Auto**: Adds scrollbars only when necessary.

If we wanted to hid the content on the horizontal axis but allow scrolling on the vertical axis, we could use:

```css
.box {
  overflow: hidden scroll;
}
```

### Measurement Units

CSS offers various units to define sizes, each serving different purposes:

#### Absolute Units

- **`px` (pixels)**: Fixed size, best for screen elements
- **`cm`, `mm`, `in`**: Physical measurements, rarely used in web design

#### Relative Units

Relative units adapt to different screen sizes and user settings:

- **`%` (percentage)**: Relative to the parent element's size
- **`em`**: Relative to the element's font size
  - ⚠️ **Issue**: Can compound in nested elements if font size isn't explicitly set
- **`rem`**: Relative to the root element's font size (usually `<html>`)
  - 💡 **Pro tip**: Set `html { font-size: 62.5%; }` so 1rem = 10px for easier calculations
- **`vw`, `vh`**: Relative to viewport dimensions
  - `1vw` = 1% of viewport width
  - `1vh` = 1% of viewport height

#### Flexible Units

- **`fr`**: Fractional unit for CSS Grid layouts to allocate space proportionally
- **`ch`**: Relative to the width of the "0" character, useful for controlling text width

**Key Takeaway**: The choice between `px`, `em`, or `rem` depends on the specific problem you're solving, not rigid rules.

### Positioning

CSS provides several positioning schemes to control the layout of elements on a webpage:

- **Static** (default): Elements flow naturally in the document
- **Relative**: Positioned relative to its normal position
- **Absolute**: Positioned relative to the nearest positioned ancestor
- **Fixed**: Positioned relative to the viewport, stays in place on scroll
- **Sticky**: Switches between relative and fixed based on scroll positions

- When we moved the box using absolute positioning, the blue box moved to the top-left corner of the container because using absolute positioning the element is removed from the normal document flow, from the parents view, that element doesn't even exist.

### Floating Elements

The `float` property allows elements to be taken out of the normal document flow and positioned to the left or right of their container, allowing other content to wrap around them.

There's a problem with floats called parent collapse. When all child elements inside a parent are floated, the parent element collapses to a height of zero because it no longer contains any non-floated content.

### Flexbox

Flexbox is a one-dimensional layout model that allows you to design flexible and responsive layout structures. It works by defining a flex container and its flex items.

Axes:

- **Main Axis**: The primary axis along which flex items are laid out (default is horizontal).
- **Cross Axis**: The axis perpendicular to the main axis (default is vertical).

If you set the direction to column, the main axis becomes vertical and the cross axis becomes horizontal. If you set the direction to row, the main axis is horizontal and the cross axis is vertical.

#### Aligning Items

- **justify-content**: Aligns items along the main axis
  - `flex-start`: Items are packed toward the start of the main axis
  - `flex-end`: Items are packed toward the end of the main axis
  - `center`: Items are centered along the main axis
  - `space-between`: Items are evenly distributed, with the first item at the start and the last item at the end
  - `space-around`: Items are evenly distributed with equal space around them
- **align-items**: Aligns items along the cross axis
  - `flex-start`: Items are aligned to the start of the cross axis
  - `flex-end`: Items are aligned to the end of the cross axis
  - `center`: Items are centered along the cross axis
  - `stretch`: Items stretch to fill the container along the cross axis
- **align-content**: This only works if we have multiple lines in our flex container. It aligns the lines of items along the cross axis.

#### Sizing items

- **flex-basis**: The initial size of a flex item before any space distribution
- **flex-grow**: Defines how much a flex item will grow relative to the rest of the flex items
- **flex-shrink**: Defines how much a flex item will shrink relative to the rest of the flex items
- **flex**: A shorthand property for `flex-grow`, `flex-shrink`, and `flex-basis`
- All of these should be applied to the flex items, not the flex container.
