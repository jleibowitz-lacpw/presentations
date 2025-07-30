---
marp: true
theme: default
paginate: true
---

# Deploying Marp Presentations on GitHub Pages

## Why use Marp + GitHub Pages?

-   **Version Control:** Treat presentations like code, track changes with Git.
-   **Collaboration:** Utilize pull requests for streamlined team collaboration.
-   **Automated Deployment:** GitHub Actions can automate conversion and deployment.
-   **Easy Sharing:** Host your presentations as web pages on GitHub Pages.

---

# Options for Deployment

## 1. Marp CLI + GitHub Actions

-   **Simplest Approach:** Convert your Marp Markdown files (.md) to HTML using Marp CLI.
-   **Automate with GitHub Actions:** Set up a workflow to automatically convert and publish to GitHub Pages on every push.
-   **Example Workflow:** {Link: See an example here https://github.com/robalexdev/marp-to-pages}.

---

# 2. Integrate with a Static Site Generator (SSG)

-   **More Control:** Use an SSG like Jekyll, Hugo, or Eleventy for greater site structure and design customization.
-   **Jekyll Integration (GitHub Pages):** Jekyll, the default SSG for GitHub Pages, can be extended to process Marp Markdown files.
-   **Workflow:**  Jekyll generates the main site, and Marp CLI converts Markdown slides into HTML snippets that Jekyll can incorporate.
-   **Resource:** {Link: Explore an article discussing Marp CLI within a Jekyll setup https://riedmann.dev/2022/07/16/blog-automation-marp-slides.html}.

---

# 3. Dedicated Marp Static Site Generators

-   **Streamlined Process:** Tools specifically designed for building Marp-based websites.
-   **Built-in Features:** Often include simplified setup and GitHub Pages integration.
-   **Examples:**
    -   **Marp Pages:** A static site generator focused on Marp.
    -   **Marp Slides Template:** A minimal template for building and publishing on GitHub Pages, {Link: available here https://github.com/codebytes/marp-slides-template}.

---

# Improving Documentation Culture

By adopting Marp and integrating it with GitHub Pages and these deployment strategies, you can foster a culture where:

-   Documentation is easily created and updated.
-   Presentations are readily available as web pages.
-   Collaboration and version control become standard practices for documentation.

---

# Getting Started

-   **Choose your approach:** Based on your needs and technical comfort, select the deployment method that suits you best.
-   **Explore Resources:** The provided links offer valuable guides and examples to help you get started.
