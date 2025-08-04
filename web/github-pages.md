---
marp: true
theme: default
paginate: true
header: 'GitHub Pages Level Up'
footer: 'Public Sector DevSecOps'
---

# Leveling Up with GitHub Pages

## Your Personal Website on GitHub

This deck guides you through using GitHub Pages to host a personal website. The focus is on public sector best practices for open-source and libre licensing.

---

# What is GitHub Pages?

GitHub Pages is a static site hosting service. It takes HTML, CSS, and JavaScript files from a repository on GitHub, optionally runs the files through a build process, and publishes a website.

*   **Static Sites:** Suitable for personal portfolios, documentation, or basic project websites.
*   **Hosted on GitHub:** Uses existing GitHub infrastructure.
*   **Supports Jekyll:** Can transform Markdown into styled HTML, {Link: according to GitHub Pages https://pages.github.com/}.

---

# What is GitHub Pages? (cont.)

*   **User/Organization Pages:** Host a site at `<username>.github.io` or `<organization>.github.io`.
*   **Project Pages:** Host a site for a specific project at `<username>.github.io/<repository>`.
*   **Version Control Friendly:** Uses a Markdown-based approach for easy versioning and collaboration.

---

# Setting Up Your Personal Site

## 1. Create a Repository

*   Log in to your GitHub Enterprise account (public cloud).
*   Create a **new public repository** named `<username>.github.io`. Replace `<username>` with your GitHub username.
*   **Important:** Public visibility is usually required for personal sites, unless using GitHub Enterprise Cloud for a private project site.
*   Initialize the repository with a `README.md` file.

---

# Setting Up Your Personal Site (cont.)

## 2. Create your `index.md` file

*   In the new repository, create a file named `index.md` (or `index.html`). This is your website's main entry point.
*   Add some basic content using Markdown.

# Example `index.md` content:

# Welcome to My GitHub Pages Site!

This is my personal website.

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

*   Create a folder named `assets/css` in the root of your repository.
*   Inside `assets/css`, create a new file named `style.scss`.
*   Add this at the top of `style.scss`:

---
---
@import "{{ site.theme }}";

*   This imports the default Jekyll theme's styles.

---

# Adding a Custom Stylesheet (cont.)

*   Add custom CSS or Sass rules below the `@import` line. These rules will override or extend the default styles.

# Example Custom Styling:

h1 {
  color: #007bff; /* Public sector blue */
}

p {
  font-family: Arial, sans-serif;
  line-height: 1.6;
}

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
    Create a `style.scss` file and add some basic styling.
    *   Examples: change fonts, colors, or add a header background.

4.  **Embrace Copyleft (Non-negotiable!):**
    *   Make all your code and content free and open source.
    *   Choose a {Link: copyleft license https://pitt.libguides.com/openlicensing/opensoftware}, such as the GNU General Public License (GPL).
    *   Add a `LICENSE` file to your repository with the text of your chosen license.

---

# Importance of Open Source

As a public sector entity, making your work open and libre with a copyleft license is a core requirement and a good practice. It promotes:

*   **Transparency**
*   **Collaboration**
*   **Accessibility**
*   **Innovation**

---
