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
