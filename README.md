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

### Grid

CSS Grid is a two-dimensional layout system that allows you to create complex grid-based designs with rows and columns.

Previously we were laying out elements in one direction, either a row or a column. With grid we can layout elements in both directions, rows and columns, at the same time.

#### Defining the Grid

- First, we define a grid container by setting `display: grid` on a parent element.
- Then we're going to use these two properties to define the number of rows and columns in our grid:
  - `grid-template-columns`: Defines the number and size of columns
  - `grid-template-rows`: Defines the number and size of rows

If we go to chrome devtools and click the layout tab, we can change the options to see the grid lines, areas, and gaps.

#### Aligning Items

- **justify-items**: Aligns items along the row (horizontal) axis
  - `start`: Items are aligned to the start of the row axis
  - `end`: Items are aligned to the end of the row axis
  - `center`: Items are centered along the row axis
  - `stretch`: Items stretch to fill the grid cell along the row axis
- **align-items**: Aligns items along the column (vertical) axis

  - `start`: Items are aligned to the start of the column axis
  - `end`: Items are aligned to the end of the column axis
  - `center`: Items are centered along the column axis
  - `stretch`: Items stretch to fill the grid cell along the column axis

- So if you see the word `content` that represents the size of the entire grid the entire content. But if you see the word `item` that represents the size of an individual grid item inside of a grid cell.

- You would want to use fr instead of percentages because fr will take up the available space after any fixed sizes have been allocated, percentage will always be a percentage of the total size regardless of any fixed sizes.

#### Gaps

- **row-gap**: The space between rows in a grid layout.\*\*
- **column-gap**: The space between columns in a grid layout.
- **grid-area**: A shorthand property that allows you to specify a grid item's start and end positions within the grid, using line numbers or named grid areas.

#### Placing Items

- **grid-column**: Specifies the starting and ending column lines for a grid item.
- **grid-row**: Specifies the starting and ending row lines for a grid item.
- **grid-area**: A shorthand property that allows you to specify a grid item's start and end positions within the grid, using line numbers or named grid areas.

#### Placing Items In Named Areas

- You can name areas of your grid using the `grid-template-areas` property on the grid container.
- Then you can place individual grid items into these named areas using the `grid-area` property on the grid items.

### Hiding Elements

- **visibility: hidden**: Hides the element but it still takes up space in the layout.
- **display: none**: Completely removes the element from the layout, and it does not take up any space.

### Media Queries

Media queries allow you to apply different styles based on the characteristics of the device or viewport, such as its width, height, resolution, or orientation.

#### Responsive Design

- Desktop first approach: Start with styles for larger screens and use media queries to adjust for smaller screens.
- Mobile first approach: Start with styles for smaller screens and use media queries to enhance for larger. **Majority of developers prefer this approach.**

#### Devtools tip

- You can simulate different device screen sizes using Chrome DevTools by pressin option + command + I (Mac) or control + shift + I (Windows), then clicking the device toolbar icon (phone/tablet) in the top-left corner of DevTools.

### Summary

#### Key Concepts

**Box Model**

- When rendering an HTML document, the browser puts each element inside a box containing four areas: content area, padding area, border area, and margin area
- Padding is the space between the border and content area
- Margin is the space outside of an element and should be used to separate elements from each other
- Margin collapsing happens when top and bottom margins of elements are combined into a single margin equal to the largest of the two margins

**Element Types**

- **Block-level elements**: Always start on a new line and take up the entire available horizontal space (e.g., `<p>`, `<div>`)
- **Inline elements**: Don't start on a new line and take up only necessary width (e.g., `<span>`, `<a>`, `<img>`)

**Sizing Elements**

- Width and height properties have no effect on inline elements
- To size an inline element, set its `display` property to `inline-block`
- By default, width and height are applied to the content box, so paddings and borders increase the visible box size
- Change this behavior by setting `box-sizing: border-box`

**Positioning**

- **Static** (default): Normal document flow
- **Relative**: Position relative to element's normal position
- **Absolute**: Position relative to positioned parent
- **Fixed**: Position relative to viewport

**Layout Systems**

- **FlexBox**: One-dimensional layout (row or column) - great for navigation menus
- **Grid Layout**: Two-dimensional grid system - ideal for major page areas, photo galleries
- **Floating**: Pushes elements left or right, other elements flow around them

**Responsive Design**

- Media queries provide different styles for different devices based on features like screen size
- Combine media queries with relative units to build responsive websites that adjust to various screen sizes

#### CSS Cheat Sheet

##### Box Model

```css
padding: 10px 20px;
padding-top: 30px;
margin: 1px 2px 3px 4px;
margin-top: 5px;
border: 1px solid black;
border-top: 1px solid black;
```

##### Sizing Elements

```css
width: 5rem;
height: 20%;
box-sizing: border-box; /* Prevents paddings/borders from increasing visible box size */
```

##### Overflow

```css
overflow: hidden; /* Hides overflown content */
overflow: scroll; /* Always shows scroll bars */
overflow: auto; /* Shows scroll bars only if content overflows */
```

##### Positioning

```css
position: static; /* Default value */
position: relative; /* Position relative to element's normal position */
position: absolute; /* Position relative to positioned parent */
position: fixed; /* Position relative to viewport */
z-index: 1; /* Change stacking order */
```

##### Floating

```css
float: left;
float: right;
clear: both;
```

##### FlexBox

**Container Properties:**

```css
display: flex;
flex-direction: column; /* Direction (row, column) */
justify-content: center; /* Align items along main axis */
align-items: center; /* Align items along cross axis */
flex-wrap: wrap; /* Enable wrapping */
align-content: center; /* Align flex lines along cross axis */
```

**Item Properties:**

```css
align-self: center; /* Overwrite alignment */
flex-basis: 10rem; /* Initial size of item */
flex-grow: 1; /* Growth factor */
flex-shrink: 0; /* Shrink factor */
flex: 0 1 10rem; /* Shorthand (grow shrink basis) */
```

##### Grid

**Defining Grid:**

```css
display: grid;
grid-template-rows: repeat(3, 100px);
grid-template-columns: repeat(2, 100px);
grid-template: repeat(3, 100px) / repeat(2, 100px);
grid-template-areas:
  "header   header"
  "sidebar  main"
  "footer   footer";
```

**Gaps:**

```css
row-gap: 10px;
column-gap: 20px;
gap: 10px 20px; /* Shorthand (row column) */
```

**Alignment:**

```css
justify-items: center; /* Align items horizontally within their cell */
align-items: center; /* Align items vertically within their cell */
justify-content: center; /* Align grid horizontally within container */
align-content: center; /* Align grid vertically within container */
```

**Placing Items:**

```css
grid-column: 2;
grid-column: 1 / 3; /* Span from line 1 to 3 */
grid-column: 1 / -1; /* Span full width */
grid-column: 1 / span 2; /* Span 2 columns */
grid-row: 2 / 4;
grid-area: header; /* Use named area */
```

##### Hiding Elements

```css
display: none; /* Hides element completely */
visibility: hidden; /* Hides element but keeps reserved space */
```

##### Media Queries

```css
@media screen and (min-width: 500px) {
}
@media screen and (min-width: 500px) and (max-width: 700px) {
}
@media print {
}
```

---

**💡 Key Takeaways:**

- Floated elements are invisible to their parent (collapsing parent) - clear floated elements to fix layout issues
- FlexBox is perfect for one-dimensional layouts
- Grid is ideal for two-dimensional layouts
- Media queries + relative units = responsive design

---

### Exercises

#### 🧭 Navigation Bar

**Objective**: Create a responsive navigation bar that adapts to different screen sizes.

**Requirements**:

- **Mobile**: Items stacked vertically, center-aligned
- **Tablets (768px+)**: Items displayed horizontally, right-aligned
- **Approach**: Mobile-first responsive design

**Features Implemented**:

- Semantic HTML with `<nav>` and `<ul>` structure
- FlexBox layout for responsive behavior
- Smooth hover transitions
- Clean, accessible design

**View**: [Navigation Bar Exercise](exercises/navbar/index.html)

#### 📸 Photo Gallery

**Objective**: Build a responsive photo gallery with adaptive column layouts.

**Requirements**:

- **Mobile**: Single column layout
- **Tablets (768px+)**: Two column grid
- **Laptops (1024px+)**: Three column grid with featured large image

**Features Implemented**:

- CSS Grid layout system
- Responsive image handling with `object-fit: cover`
- Random Unsplash images with cache-busting
- Hover effects and smooth transitions
- Mobile-first approach

**View**: [Photo Gallery Exercise](exercises/photo-gallery/index.html)

#### 🎯 How to Test

1. **Start Local Server**: `python3 -m http.server 8080`
2. **Open**: [http://localhost:8080/exercises/](http://localhost:8080/exercises/)
3. **Use DevTools**: F12 → Device toolbar → Test different screen sizes
4. **Key Breakpoints**: 320px (mobile), 768px (tablet), 1024px (desktop)

## 2. Typography

### Intro

The art of creating beautiful, and easy-to-read text.

- Style fonts
- Embedding custom fonts
- Using font services (e.g., Google Fonts)
- Best practices for text size & spacing
- Formatting text

### Styling Fonts

- We have three main categories of fonts:
  - Serif: Fonts with small lines or strokes attached to the ends of larger strokes in letters `(e.g., Times New Roman, Georgia)`
  - Sans-serif: Fonts without the small lines or strokes `(e.g., Avenir, Arial, Futura, Helvetica, Roboto)`
  - Monospace: Fonts in which each character takes up the same amount of horizontal space `(e.g., Courier New, Consolas, Ubuntu)`

These are what we would call web-safe fonts. These are fonts that are commonly installed on most devices.

### Embedding Web Fonts

#### Where to find fonts?

**Free Font Resources:**

- [Font Squirrel](https://www.fontsquirrel.com) - High-quality free fonts with web font kits
- [Google Fonts](https://fonts.google.com) - Extensive library of open-source fonts

**Premium Font Resources:**

- [Fonts.com](https://www.fonts.com) - Professional font licensing and web fonts
- [MyFonts](https://www.myfonts.com) - Large marketplace for premium typefaces
- [Adobe Fonts](https://fonts.adobe.com) - Included with Creative Cloud subscriptions

#### Font Formats

- **TTF**: TrueType Font, widely supported but larger file size
- **OTF**: OpenType Font, supports advanced typographic features
- **EOT**: Embedded OpenType, compact format for web use
- **WOFF**: Web Open Font Format, optimized for web with compression (recommended)
- **WOFF2**: Improved version of WOFF with better compression (best choice)

**💡 Recommendation**: Use WOFF and WOFF2 formats for web fonts as they are more compressed and optimized for web use, resulting in faster loading times.

When we download the font zips from sites like Font Squirrel, we're going to use the webfont generator to create the webfont files we need.

Upload the font files you have (TTF or OTF) to the webfont generator, select optimized for web, and download the generated webfont kit.

### Flash of Unstyled Text (FOUT)

When using custom web fonts, browsers may initially display text using a fallback font before the custom font loads, causing a "flash" of unstyled text. To mitigate this, you can use the `font-display` property in your `@font-face` declaration.

#### Testing Font Loading Performance

**DevTools Setup:**

1. Open **DevTools** → **Network** tab
2. Check **"Disable cache"** - simulates first-time visits on every refresh
3. Use **Throttle options** to simulate slower network speeds and observe font loading behavior

#### Font Display Options

The `font-display` property controls how fonts are displayed during the loading process:

- **`font-display: swap;`** ✅ **Recommended**

  - Browser uses fallback font immediately
  - Swaps to custom font once loaded
  - Reduces FOUT impact on user experience

- **`font-display: fallback;`**

  - Uses fallback font if custom font doesn't load within a short period
  - Ensures text remains readable without significant delays

- **`font-display: optional;`**

  - Uses fallback font if custom font doesn't load quickly
  - Prioritizes performance and user experience over font fidelity

- **`font-display: block;`** ❌ **Never Use**
  - Forces browser to wait for custom font before displaying text
  - Can cause blank/invisible text if font fails to load
  - Poor user experience

#### Example Implementation

```css
@font-face {
  font-family: "CustomFont";
  src: url("customfont.woff2") format("woff2"), url("customfont.woff") format("woff");
  font-display: swap; /* Recommended for better UX */
}
```

### Font Services

- Some of these fonts need licensing, and the licensing can cost a few hundred dollars for a website license. So this is where font services come in.

- **Google Fonts** is a free font service that hosts hundreds of open-source fonts that you can easily embed into your website. ([google fonts](https://fonts.google.com))

- **Adobe Fonts** (formerly Typekit) is a premium font service included with Adobe Creative Cloud subscriptions. It offers a vast library of high-quality fonts for web and desktop use. ([adobe fonts](https://fonts.adobe.com))

- **Fonts.com** and **MyFonts** are other popular font services that provide both free and premium fonts for web use. They offer easy embedding options and licensing for commercial use. ([fonts.com](https://www.fonts.com), [myfonts](https://www.myfonts.com))

- **Fontdeck** is another premium font service that offers a wide range of high-quality fonts for web use. It provides easy integration and licensing options for commercial projects. ([fontdeck](https://fontdeck.com))

- All these services have subscription models or pay-as-you-go options depending on your needs.

#### Using Google Fonts

1. Go to [Google Fonts](https://fonts.google.com)
2. Browse and select the font(s) you want to use
3. Click on the selected font to open its details page
4. Choose which styles, they have something called variable fonts, which is a single font file that contains multiple styles.
5. Copy the `<link>` tag provided by Google Fonts and paste it into the `<head>` section of your HTML document

### System Font Stacks

We can tell the browser to use the default font of the operating system on the user's device.

#### Benefits

- Can Boost Performance: System fonts are already installed on the user's device, so they load instantly without additional HTTP requests.
- This means there will be no FOUT (Flash of Unstyled Text) because the font is already available.
- Native Look and Feel: Using system fonts can help your website blend seamlessly with the user's operating system, providing a more native experience.
- Overall: We provide a better experience for user. **Problem with approach** The default system font on each operating system is different, so your website may look different across devices.

### Sizing Fonts

#### Why Avoid Pixels?

❌ **Don't use pixels** for font sizes because:

- Pixels are not consistent across different devices and screen resolutions
- Mac devices use **Retina Display** technology, allowing smaller pixels to fit more on screen
- Creates accessibility issues for users who need larger text
- Not responsive to user preferences or device capabilities

#### Better Alternatives

✅ **Use relative units instead:**

- **`rem`**: Relative to root element font size (recommended)
- **`em`**: Relative to parent element font size
- **`%`**: Percentage of parent element font size
- **`vw/vh`**: Viewport-relative units for responsive typography

#### Typography Scale Tool

🔧 **[Type Scale](https://type-scale.com)** - Visual tool for:

- Exploring different font size ratios
- Previewing text at various sizes
- Finding the right font size hierarchy for headings
- Creating consistent typographic scales

#### Example Implementation

```css
/* Good: Using relative units */
html {
  font-size: 16px;
} /* Base size */
h1 {
  font-size: 2.5rem;
} /* 40px */
h2 {
  font-size: 2rem;
} /* 32px */
h3 {
  font-size: 1.5rem;
} /* 24px */
p {
  font-size: 1rem;
} /* 16px */

/* Avoid: Fixed pixel sizes */
h1 {
  font-size: 40px;
} /* Not responsive */
```

### Vertical Spacing

- Two main properties for vertical spacing:
  - `line-height`: Controls the space between lines of text within a paragraph
  - `margin`: Controls the space outside of elements, separating them from other elements

What we have in the html is breaking the law of proximity. Objects that are closer are perceived to be related.

### Horizontal Spacing

#### Key Properties

**Character & Word Spacing:**

- **`letter-spacing`**: Controls space between individual characters
- **`word-spacing`**: Controls space between words in text
- **`width`**: Controls overall width of text blocks (affects line breaks)

#### Testing with DevTools

🔧 **Live Testing**:

1. Inspect any text element in DevTools
2. Adjust properties in real-time:
   - `letter-spacing`: Try values like `0.1em`, `0.2em`
   - `word-spacing`: Try values like `0.2em`, `0.5em`
   - `width`: Adjust to see line break changes

#### Readability Guidelines

📏 **Optimal Line Length**: **50-70 characters per line**

- Too short: Creates choppy reading rhythm
- Too long: Hard to track from line to line
- Use `width` or `max-width` to control line length

#### Example Implementation

```css
.readable-text {
  width: 65ch; /* ~65 characters wide */
  letter-spacing: 0.025em; /* Slight character spacing */
  word-spacing: 0.1em; /* Small word spacing */
  line-height: 1.6; /* Good vertical rhythm */
}

.spaced-heading {
  letter-spacing: 0.1em; /* More dramatic for headings */
  text-transform: uppercase;
}
```

### Formatting Text

#### Alignment & Layout

- **`text-align`**: Controls horizontal text alignment

  - Values: `left`, `right`, `center`, `justify`
  - Use `justify` sparingly - can create uneven spacing

- **`text-indent`**: Controls first-line indentation
  - Common values: `1em`, `2em`, `1rem`
  - Tip: Use `p + p` selector for subsequent paragraphs only

#### Text Styling

- **`text-decoration`**: Adds visual decorations to text

  - Values: `none`, `underline`, `line-through`, `overline`
  - Shorthand: `text-decoration: underline wavy red;`

- **`text-transform`**: Controls text capitalization
  - Values: `none`, `uppercase`, `lowercase`, `capitalize`
  - Great for headings and buttons

#### Whitespace Control

- **`white-space`**: Controls whitespace and line breaks
  - `normal`: Default behavior, collapses whitespace
  - `nowrap`: Prevents text wrapping
  - `pre`: Preserves all whitespace (like `<pre>` tag)
  - `pre-wrap`: Preserves whitespace but allows wrapping

#### Multi-Column Layouts

- **`column-count`**: Number of columns (e.g., `3`)
- **`column-gap`**: Space between columns (e.g., `2rem`)
- **`column-width`**: Optimal width per column (e.g., `250px`)
- **`column-rule`**: Visual separator between columns

#### Text Direction

- **`direction`**: Controls text reading direction
  - `ltr`: Left-to-right (default for English)
  - `rtl`: Right-to-left (for Arabic, Hebrew)

#### Example Implementation

```css
/* Text alignment */
.centered-text {
  text-align: center;
}
.justified-text {
  text-align: justify;
}

/* Text styling */
.uppercase-heading {
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.decorated-link {
  text-decoration: underline;
  text-decoration-color: blue;
  text-decoration-style: wavy;
}

/* Whitespace control */
.no-wrap {
  white-space: nowrap;
}
.preserve-formatting {
  white-space: pre-wrap;
}

/* Multi-column layout */
.article-columns {
  column-count: 2;
  column-gap: 3rem;
  column-rule: 1px solid #ddd;
}

/* Paragraph indentation (avoid first paragraph) */
p + p {
  text-indent: 1.5rem;
}
```

### Exercise: � Recipe Blog Page

**Objective**: Create a well-formatted recipe blog page demonstrating typography principles and responsive design.

**Font Requirements**:

- Use **Google Fonts** - 2 sans-serif fonts + 1 serif font (italic)
- **Serif font** (italic): Lead paragraph before image
- **Sans-serif fonts**: Body text and headings
- Base font size: **62.5%** for easier rem calculations
- Use **[Type Scale](https://type-scale.com)** to determine heading sizes (h1-h6)

**Container Requirements**:

- Max width: **1140px**
- Horizontal margin: **auto** (centers container with equal left/right spacing)

**Page Elements**:

- **Proper heading hierarchy**: One `<h1>` per page, no skipped headings
- **Lead paragraph**: Slightly larger than body text
- **Responsive image**: 100% width from [Unsplash](https://unsplash.com/photos/C1Q3qOTlegg)
- **Mobile-first**: Ensure everything looks good on smaller screens
- **Compare with solution**: Investigate missed styles and their impact

**Features to Implement**:

- Google Fonts integration with proper font stack
- Semantic HTML structure with heading hierarchy
- Custom typography with lead paragraph styling
- Responsive image sizing (`width: 100%`)
- Optimal line length and spacing
- Centered container layout

**Emmet Shorthand**:

```
.container>h1{Sweet Potato and Kale Bowl}+p.lead>lorem20^^img[src="images/recipe.jpg"][alt=""]^h2{Ingredients}+h3{For the sweet potato}+ul>li*4>lorem1+strong{ingredient}^^^h3{For the kale}+ul>li*3>lorem1+strong{ingredient}^^^h2{Instructions}+ol>li*3>lorem15
```

**View**: [Recipe Blog Exercise](exercises/recipe-blog/index.html)

---

## Typography Summary

### Terms

- **Browser cache**: Permanent storage on disk where browsers store web page assets
- **Flash of Invisible Text (FOIT)**: Browser hides text while downloading custom font
- **Flash of Unstyled Text (FOUT)**: Browser shows fallback font then swaps to custom font
- **Font services**: Platforms providing access to thousands of fonts (e.g., Google Fonts)
- **Font stack**: Multiple fonts listed as fallbacks in CSS
- **Law of proximity**: Objects that are closer are perceived to be related
- **Monospace fonts**: Fonts where each character has equal width (used for code)
- **Query string parameters**: URL parameters used to prevent caching (e.g., `?v=1`)
- **Retina display**: High-density displays that fit more pixels on screen
- **Sans-serif fonts**: Modern, warm fonts without decorative strokes
- **Serif fonts**: Professional fonts with decorative lines/strokes at character edges
- **System fonts**: Default fonts provided by operating systems
- **Throttling**: Simulating slow network connections in DevTools
- **Web safe fonts**: Fonts commonly installed on most devices

### Key Concepts

**Typography Importance**

- Typography is the art of creating beautiful and easy-to-read text
- 95% of web content is text - proper typography is essential
- Must ensure text is easy to read and visually appealing on all screen sizes

**Font Categories**

- **Serif**: Professional and serious (e.g., Times New Roman, Georgia)
- **Sans-serif**: Modern, warm, and friendly (e.g., Arial, Helvetica, Roboto)
- **Monospace**: Equal-width characters for displaying code (e.g., Courier, Consolas)

**Best Practices**

- Default body text color (#000) is too harsh - use dark grey instead
- Use `font-family` with font stacks containing multiple fallback fonts
- Embed custom fonts using modern formats (WOFF, WOFF2) for better compression
- Convert font files to WOFF format at [Font Squirrel](https://fontsquirrel.com)

**Custom Fonts**

- Register custom fonts using `@font-face` rule
- WOFF and WOFF2 formats are recommended (more compressed, faster downloads)
- Be aware of FOUT/FOIT when custom fonts load
- Use `font-display` property to control font loading behavior

**Font Services**

- Provide access to thousands of fonts with zero or minimal cost
- **Google Fonts** is the most popular free service
- Fonts and `@font-face` rules served from provider's servers
- Eliminates need to host font files yourself

**System Font Stack**

- Uses default OS fonts for better performance
- No font downloads needed - eliminates FOUT/FOIT
- Page looks familiar to users (same as their device)
- Drawback: Font varies across different devices

**Sizing & Spacing**

- Use `rem` units for font sizes (relative to root element)
- Set `html { font-size: 62.5%; }` so 1rem = 10px for easier calculations
- Use media queries to resize base font - all elements recalculate automatically
- Use `rem` for vertical margins to maintain consistency

**Heading Hierarchy**

- Top margin should be greater than bottom margin
- Separates heading from previous content, connects to following content
- Follows the **law of proximity** principle

**Line Height**

- Use unitless value around **1.5** for optimal readability
- Value multiplies by element's font size automatically
- No need to update if font size changes

**Horizontal Spacing**

- **`letter-spacing`**: Space between characters
- **`word-spacing`**: Space between words
- **`width`**: Controls text block width (affects line breaks)
- Apply negative letter-spacing to headings for compact look

**Optimal Line Length**

- Ideal: **60-70 characters per line**
- Use `width: 50ch` to achieve this
- `ch` unit = width of "0" character
- 50 zeros ≈ 60-70 characters (accounting for narrow characters like i, 1)

**Development Tools**

- **Network Throttling**: Simulate slow connections in DevTools
- **Browser Cache**: Can be cleared to test fresh page loads
- **Network Tab**: Monitor font file downloads and performance

---

### Exercise: � Stylish Blog Post

---

### CSS Cheat Sheet

#### Styling Fonts

```css
font-family: Arial, Helvetica, sans-serif;
font-size: 1rem;
font-weight: bold;
font-style: italic;
```

#### Vertical Spacing

```css
margin: 3rem 0 1rem;  /* top, left/right, bottom */
line-height: 1.5;
```

#### Horizontal Spacing

```css
letter-spacing: -1px;
word-spacing: 2px;
width: 50ch;
```

#### Formatting Text

```css
text-align: center;
text-indent: 1rem;
text-decoration: underline;
text-transform: uppercase;
white-space: nowrap;
direction: rtl;  /* right-to-left */
```

#### Multi-column Text

```css
column-count: 2;
column-gap: 2rem;
column-rule: 3px dotted #999;
```
