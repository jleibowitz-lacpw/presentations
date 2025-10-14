---
marp: true
theme: default
paginate: true
---

# CLI Troubleshooting: A Mindful Approach

The right tools to collect the right information

---

## Why This Matters

- External tools show an external point of view
- The command line is easy. Commands are repeatable

---

## External Tools Recap

- WHOIS / Registration Data Access Protocol
- digwebinterface.com
- whatsmydns.net
- Qualys SSL Labs
- reqbin.com / httpstatus.io

> Quick external checks

---

## The Layered Approach

1. Is the host reachable (Network)?
2. Does a hostname resolve (DNS)?
3. Is the port open (Firewall)?
4. Is the service responding?
5. What else is happening (Context)?

---
## Your Terminal Environment (on Windows)

| Environment | Pros | Cons |
|-------------|------|------|
| Console Host | Simple | Old school |
| PowerShell | Powerful scripting | Complex syntax |
| Windows Terminal | Modern UI | Learning curve |
| Git Bash | Bash shell on Windows OS, installed with Git for Windows | Very simple environment |
| WSL | Full Linux | Setup required, Linux familiarity suggested |
| Cygwin | A Unix-like environment | Complexity, mostly supplanted by WSL |

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
