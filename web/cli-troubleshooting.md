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

| Terminal or Shell | Pros | Cons |
|-------------|------|------|
| Console Host | Simple | Old school, uses `cmd.exe` |
| Windows Terminal | Modern UI | additional installation |
| PowerShell | Powerful scripting | Complex syntax, more than one "powershell" to be aware of |

---
##  Environments (continued)

| Environment | Pros | Cons |
|-------------|------|------|
| Git Bash | Bash shell on Windows, installed by Git for Windows | Simple environment, command availability |
| WSL | Full Linux | Setup required, Linux familiarity suggested |
| Cygwin | A Unix-like environment | Complexity, mostly supplanted by WSL |

---
## Considerations

Know your environment and the PATH. Shells and terminal emulators can behave differently. 

---

## Layer 1: Reachability

**Tools:** `ping`, `tracert`, `mtr`

- Can we reach the host?
- Is there packet loss or latency?

---

A ping example. A DNS lookup is performed by `ping` to resolve the hostname to an IP address:
```
$ ping example.com

Pinging example.com [23.220.75.232] with 32 bytes of data:
Reply from 23.220.75.232: bytes=32 time=7ms TTL=46
Reply from 23.220.75.232: bytes=32 time=15ms TTL=46
```

---

Windows `tracert` in a Bash shell (denoted by the `$` prompt):

```
$ TRACERT.EXE 10.48.222.88

Tracing route to 10.48.222.88 over a maximum of 30 hops

  1     2 ms    <1 ms    <1 ms  10.1.18.254
  2     1 ms     1 ms     1 ms  10.1.2.5
  3     1 ms     1 ms     1 ms  159.83.240.195
  4     3 ms     3 ms     3 ms  10.11.222.233
  5     3 ms     2 ms     2 ms  10.251.191.253
  6     3 ms     3 ms     3 ms  10.50.246.12
  7     3 ms     2 ms     2 ms  10.48.222.88

Trace complete.
```

---

## Layer 2: DNS Resolution

**Tools:** `nslookup`, `dig`, `host`, `whois`

- Is the domain resolving?
- What are the authoritative nameservers?
- What DNS records do we see?

---
Simple `A` record query for jonleibowitz.com:
```
$ dig A jonleibowitz.com

; <<>> DiG 9.11.9 <<>> A jonleibowitz.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 29053
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;jonleibowitz.com.              IN      A

;; ANSWER SECTION:
jonleibowitz.com.       300     IN      A       104.21.38.82
jonleibowitz.com.       300     IN      A       172.67.220.196

;; Query time: 39 msec
;; SERVER: 10.5.64.43#53(10.5.64.43)
;; WHEN: Tue Oct 14 09:12:39 PDT 2025
;; MSG SIZE  rcvd: 77

```
---

Query `NS` (Nameserver) records for jonleibowitz.com (with +short option):
```
$ dig NS jonleibowitz.com +short
john.ns.cloudflare.com.
rosa.ns.cloudflare.com.

```
Query `A` record for pwiis04.dpw.co.la.ca.us:
```
$ dig A pwiis04.dpw.co.la.ca.us +short
10.48.222.88
```

---

Query `SOA` (Start of Authority) record for dpw.co.la.ca.us:
```
$ dig SOA dpw.co.la.ca.us

; <<>> DiG 9.11.9 <<>> SOA dpw.co.la.ca.us
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 53081
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;dpw.co.la.ca.us.               IN      SOA

;; ANSWER SECTION:
dpw.co.la.ca.us.        3600    IN      SOA     pwdc05.dpw.co.la.ca.us. admin.dpw.co.la.ca.us. 43511192 900 600 86400 3600

;; ADDITIONAL SECTION:
pwdc05.dpw.co.la.ca.us. 3600    IN      A       10.5.64.43

;; Query time: 0 msec
;; SERVER: 10.5.64.43#53(10.5.64.43)
;; WHEN: Tue Oct 14 09:11:29 PDT 2025
;; MSG SIZE  rcvd: 109

```

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
