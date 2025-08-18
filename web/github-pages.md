---
marp: true
theme: default
paginate: true
header: 'GitHub Pages Level Up'
footer: 'Office Hours - Jon Leibowitz'
---

# Leveling Up with GitHub Pages

## Your Personal Website on GitHub

This deck guides you through using GitHub Pages to host a personal website.

---

# What is GitHub Pages?

GitHub Pages is a static site hosting service. It takes HTML, CSS, and JavaScript files from a repository on GitHub, optionally runs the files through a build process, and publishes a website.

*   **Static Sites:** Suitable for personal portfolios, documentation, or basic project websites.
*   **Hosted on GitHub:** Uses existing GitHub infrastructure.
*   **Supports Jekyll:** Can transform Markdown into styled HTML.

---

# What is GitHub Pages? (cont.)

*   **User/Organization Pages:** Host a site at `<username>.github.io` or `<organization>.github.io`.
*   **Version Control Friendly:** Easy versioning and collaboration.

---

# Setting Up Your Personal Site

## 1. Create a Repository

*   Log in to your GitHub account.
*   Create a **new public repository** named `<username>.github.io`. Replace `<username>` with your GitHub username.
*   **Important:** Public visibility is usually required for personal sites.
*   Initialize the repository with a `README.md` file.

---

# Setting Up Your Personal Site (cont.)

## 2. Create your `index.md` file

*   In the new repository, create a file named `index.md` (or `index.html`). This is your website's main entry point.
*   Add some basic content using Markdown.

# Example `index.md` content:

```
# Welcome to My GitHub Pages Site!

This is *my* personal website.
```
---

# Setting Up Your Personal Site (cont.)

## 3. Configure your publishing source

*   Go to your repository's **Settings**.
*   Click on the **Pages** section in the sidebar.
*   Under "Build and deployment", select **Deploy from a branch**.
*   Choose the branch you want to use (e.g., `main`).
*   Your site will be built and published shortly. Visit your site at `<username>.github.io`.

---

# Adding a Custom Stylesheet

To customize your site's look:

*   Create a new file named `style.css`.
*   Add this at the top of `style.css`:

---
```
body {
  background-color: #f4f4ff;
}
```
---

# Adding a Custom Stylesheet (cont.)
*   In your `index.md`, link to the stylesheet by adding this line after the front matter:

```
<link rel="stylesheet" href="style.css">
```

--- 
*   Commit and push your changes to your repository.

---

# Homework Assignment: Build Your Site!

1.  **Create your personal GitHub Pages site:**
    Set up your website at `<username>.github.io`.

2.  **Add content with `index.md`:**
    Populate it with information about yourself or a project. Use Markdown syntax for formatting.

---

# Homework Assignment: Build Your Site! (cont.)

3.  **Apply a custom stylesheet:**
    Create a `style.css` file and add some basic styling.
    *   Examples: change fonts, colors, or add a header background.

4.  **Embrace Copyleft (required for this assignment!):**
    *   Make all your code and content free and open source.
    *   Choose a [copyleft license](https://en.wikipedia.org/wiki/Category:Copyleft_software_licenses), such as Creative Commons share-alike or GNU General Public License (GPL).
    *   Add a `LICENSE` file to your repository with the text of your chosen license.

---

# Importance of Open Source

Making your work open and libre with a copyleft license is a core requirement for this homework assignment and it's good practice. It promotes:

*   **Transparency**
*   **Collaboration**
*   **Accessibility**
*   **Innovation**
