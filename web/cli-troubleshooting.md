---
marp: true
theme: default
paginate: true
---

# CLI Troubleshooting: A Mindful Approach

Avoid assumptions. Ask the right questions. Use the right tools.

---

## Why This Matters

- Jumping to conclusions wastes time
- External tools only show part of the picture
- CLI tools help us collect real data
- Troubleshooting is a process, not a guess

---

## External Tools Recap

- whatsmydns.net
- SSL Labs
- reqbin.com / httpstatus.io
- digwebinterface.com

> Great for quick checks—but limited visibility

---

## The Layered Approach

1. Is the host reachable?
2. Is DNS resolving?
3. Is the port open?
4. Is the service responding?
5. What’s the context?

---

## Layer 1: Reachability

**Tools:** `ping`, `tracert`, `mtr`

- Can we reach the host?
- Is there packet loss or latency?

---

## Layer 2: DNS Resolution

**Tools:** `nslookup`, `dig`, `host`, `whois`

- Is the domain resolving?
- What are the authoritative nameservers?
- What DNS records do we see?

---

## Layer 3: Port Connectivity

**Tools:** `nc`, `telnet`, `Test-NetConnection`

- Is the port open?
- Can we establish a TCP connection?

---

## Layer 4: Service Behavior

**Tools:** `curl`, `httpie`, `openssl s_client`

- What does the service return?
- Are there HTTP errors or TLS issues?

---

## Layer 5: Context

**Tools:** `netstat`, `ss`, `tcpdump`, logs

- What else is happening on the system?
- Are there local firewall rules or conflicts?

---

## Terminal Environments on Windows

| Environment | Pros | Cons |
|-------------|------|------|
| Console Host | Always available | Limited features |
| PowerShell | Powerful scripting | Verbose syntax |
| Windows Terminal | Modern UI | Just a frontend |
| Git Bash | Unix tools | Missing some tools |
| WSL | Full Linux | Setup required |
| Cygwin | Unix tools w/o WSL | Compatibility quirks |

---

## Demo Time

Let’s walk through a scenario using these tools.

---

## Final Thoughts

- Don’t assume—observe
- Use tools to ask better questions
- Build a repeatable process

---

## Questions?

Thanks for your time!
