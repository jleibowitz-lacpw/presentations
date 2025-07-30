---
marp: true
theme: default
class: center, middle
paginate: true
---

# Web Traffic Terminology

## Clearing Up the Language of Domains and Servers

---

# Forwarding

-   Forwarding means sending a request from one address to another.
-   Often used by domain registrars to send traffic from one domain name to another website.
-   Example: `olddomain.com` forwards to `newdomain.com`.

---

# Redirection

-   Redirection is an action that changes the URL a user's browser is trying to access.
-   This is typically done using HTTP status codes like 301 (permanent) or 302 (temporary).
-   The browser is told to go to a new address, and the URL in the address bar usually changes.

---

# Pointing to (DNS Records)

-   This refers to using DNS records to link a domain name to a server or another domain.
-   **A Record:** Connects a domain name (like `example.com`) directly to an IP address (like `192.168.1.1`).
-   **CNAME Record:** Creates an alias, pointing one domain or subdomain (like `www.example.com`) to another domain name (like `example.com`).

---

# Reverse Proxy

-   A server that sits in front of web servers.
-   It intercepts client requests before they reach the actual web servers.
-   The reverse proxy then forwards the request to the correct server behind it and returns the response to the client.
-   Benefits include security, load balancing, and caching.

---

# Origin Server

-   This is the server where the original web content, application, or data is stored and managed.
-   It's the authoritative source for delivering content to users.
-   When you access a website, the origin server is the ultimate source that holds the files and processes dynamic requests.
-   Reverse proxies often sit in front of one or more origin servers.

---

# Analogy Time!

-   Think of a **domain name** as a street address.
-   **Pointing (DNS)** is like telling the mail service which physical building (server IP) your street address belongs to.
-   **Forwarding / Redirection** is like the postal service telling a visitor "The person you're looking for moved to a new address (URL), go there instead!".


---
# Analogy 2

-   A **Reverse Proxy** is like a security guard and receptionist at the entrance of a big office building (your network).
-   The guard (reverse proxy) checks incoming requests and directs them to the right person or department (Origin Server) inside, without the visitor (client) knowing who exactly is behind the desk.
-   The **Origin Server** is the specific person or department inside the building that actually handles your request and gives you what you need.

---

# Putting it Together

-   When you type `yourdomain.com` in your browser:
    1.  DNS (A Record or CNAME) `points` to a server's IP address.
    2.  This server might be a `reverse proxy`.
    3.  The `reverse proxy` handles the request and `forwards` it to an `origin server`.
    4.  If the `origin server` determines the content has moved, it might issue a `redirection` to a new URL.
    5.  The browser then goes to the new URL, potentially starting the process again, or directly displaying the content.

---

# Why Does This Matter?

-   Understanding these terms helps in configuring domains and servers effectively.
-   It impacts website performance, security, and user experience.
-   It ensures clearer communication within your team about technical concepts.

---

# Thank You!

## Let's Build Better Understanding Together
