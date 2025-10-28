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
