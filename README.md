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

## Sizing Elements

- We made a box classed "box" in the HTML file.
- The box has a fixed width and height of 100px.
- The box has a gold background color.
- One thing people might not know is when you add padding or border to an element, it increases the total size of that element beyond the specified width and height.
- By default, the width and height only account for the content area, not including padding, border, or margin.
- The margin does not affect the size of the element itself; it only adds space outside the element.
- box sizing property comes to the rescue! Because it allows us to change the default box model behavior.
- Theres a problem though, we don't apply this to every single element on the page. What if you have another element with the class of product, we don't repeat the same box sizing code again.
- To fix this, we can use the universal selector (\*) to apply box-sizing: border-box; to all elements on the page.
- The width and height properties are only applied to block level elements. Inline elements ignore these properties.
- If you want to set width and height on inline elements, you need to change their display property to inline-block or block.
