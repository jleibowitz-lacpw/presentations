---
marp: true
theme: default
class: center, middle
paginate: true
---

# Domain Forwarding Options

## Network Solutions vs. GitHub Pages

---

# Network Solutions Web Forwarding

-   A service designed for domain redirection
-   Offers optional masking for branding
-   Typically uses 301 redirects
-   Generally good for SEO
-   Easy to set up in their portal

---

# GitHub Pages (Meta Refresh)

-   Uses static website hosting
-   Requires a meta refresh tag in an HTML file for redirection
-   Meta refresh is a client-side redirect
-   Less optimal for SEO compared to 301 redirects
-   Requires manual management of an HTML file
-   Supports HTTPS, but watch for subdomain to apex domain issues

---

# Key Differences

-   Network Solutions uses server-side 301 redirects
-   GitHub Pages uses client-side meta refresh
-   Network Solutions has optional domain masking
-   SEO impact favors Network Solutions' 301 redirects
-   Setup is different for each option

---

# Choosing Your Approach

-   Consider SEO needs carefully
-   Network Solutions is often better for SEO
-   GitHub Pages offers more control for static hosting needs
-   Think about future requirements
-   Meta refresh should include a canonical tag for the destination URL

---

# Example HTML for GitHub Pages

This code would go into an index.html file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Redirecting</title>
  <meta http-equiv="refresh" content="0; URL=https://yourdesiredwebsite.com/">
  <link rel="canonical" href="https://yourdesiredwebsite.com/"> 
</head>
<body>
  <p>If not redirected, follow this <a href="https://yourdesiredwebsite.com/">link</a>.</p>
</body>
</html>
