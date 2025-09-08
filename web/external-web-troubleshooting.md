---
marp: true
theme: default
paginate: true
---

# Web Troubleshooting: The Outside-In Approach

**Or: How to diagnose like a user (because that's what matters)**

*When internal tools lie to you, the internet tells the truth*

---

# Why Start External?

- **Your users don't care about your internal network**
- DNS cache poisoning happens
- CDNs fail silently  
- Firewalls lie about what they're blocking
- **The internet sees what users see**

*Start where the problem actually lives*

---

# The Stack

```
1. Domain Registration  ← Is it even valid?
2. DNS Resolution       ← Can the world find it?
3. IP Intelligence     ← Where does it actually live?
4. Port/Protocol Test   ← Is anything listening?
5. HTTPS/TLS Analysis   ← Is encryption borked?
```

**Each layer can fail independently**

---

# Layer 1: Domain Registration

## Tool: ICANN Lookup
**https://lookup.icann.org/en**

### What You're Hunting For:
- Domain status (expired domains are embarrassing)
- EPP status codes (locks, holds, transfers)
- Nameserver delegation
- Expiration dates

**Pro tip:** Registry NIC sites have more detail than WHOIS

---

# Layer 2: DNS Resolution

## Query Tools:
- **whatsmydns.net** - Global propagation view
- **digwebinterface.com** - Detailed queries
- **intodns.com** - Comprehensive DNS health check

### Records That Matter:
```
SOA   → Who's authoritative
NS    → Nameserver delegation  
A     → IPv4 addresses
AAAA  → IPv6 addresses
CNAME → Aliases
TXT   → SPF, DKIM, verification records
```

---

# Layer 3: IP Intelligence  

## Tool: ipinfo.io

### What You Learn:
- ASN and hosting provider
- Geographic location
- Network metadata

**Reality check:** One IP = potentially thousands of sites
*(Name-based virtual hosting is everywhere)*

---

# Layer 4: Port & Protocol Testing

## Standard Web Ports:
- **80** - HTTP (cleartext, usually redirects)
- **443** - HTTPS (the real deal)
- **Others** - Edge cases exist

---

## Tools: 
**reqbin.com** - HTTP request testing
**httpstatus.io** - HTTP status code checker
**whatsmydns.net/redirect-checker** - Redirect chain analysis

- Performs HTTP requests (works like Curl or Postman)
- Response codes and headers
- Redirect chains

---

# Layer 5: HTTPS/TLS Analysis

## Tool: SSL Labs
**https://www.ssllabs.com/ssltest/**

### The Good Stuff:
- Certificate validation, expiration
- Letter grade (A+ to F) shows you conform to best practices
- Protocol support
- Cipher strength

---

# Common Failure Patterns

| Layer | Typical Issues |
|-------|----------------|
| Domain | Expired, locked, wrong nameservers |
| DNS | Cache lag, missing records |
| IP | Unexpected hosting provider, geo-blocking |
| Ports | Firewalls, service down |
| TLS | Expired certs, weak config |

**Each layer can mask problems in others**

---

# Live Demo Time

*Let's break something and fix it*

**Demo target:** [Your choice of problematic site]

1. Domain check
2. DNS resolution  
3. IP lookup
4. Port test
5. TLS analysis

---

# The "But We Use..." Objection

**Them:** "But we use [internal tool] for this"

**You:** "Cool. Does it show what users actually see?"

**Internal tools assume your network is working**
**External tools assume nothing**

*Trust, but verify from the outside*

---

# Next Steps: CLI Tools

*to cover in an upcoming presentation...*

## Git Bash / WSL:
- `dig`, `nslookup`, `whois`
- `curl`, `wget` 
- `openssl s_client`

---

## PowerShell:
- `Resolve-DnsName`, `Test-NetConnection`
- `Invoke-WebRequest`, `Invoke-RestMethod`

## Windows CLI:
- `nslookup`, `ping`, `telnet`
- `netsh`, `certlm.msc`

**Today:** External perspective  
**Next time:** Automating these checks

---

# Bonus: Automating External Checks

```bash
# Quick domain intel one-liner
curl -s "https://ipinfo.io/$(dig +short example.com)" | jq

# SSL Labs API (wait for completion)
curl -s "https://api.ssllabs.com/api/v3/analyze?host=example.com"

# DNS propagation check via API
curl -s "https://www.whatsmydns.net/api/check?server=all&type=A&query=example.com"
```


---

# Key Takeaways

1. **Start external, move internal**
2. **Each layer can fail independently** 
3. **Document what you find**
4. **External tools don't lie**

---

# Resources

- **ICANN Lookup:** https://lookup.icann.org/en
- **DNS Global Check:** https://whatsmydns.net  
- **DNS Queries:** https://digwebinterface.com
- **IP Intelligence:** https://ipinfo.io
- **HTTP Testing:** https://reqbin.com
- **SSL Analysis:** https://www.ssllabs.com/ssltest/

---

# Backup Arsenal & Deep Dives

## Backup Tools:
- **mxtoolbox.com** - DNS + email delivery + blacklists
- **Google Admin Toolbox** - Verify DNS issues
- **mxtoolbox.com** - DNS + email delivery + blacklists
- **downforeveryoneorjustme.com** - Is it just me?
- **shodan.io** - What's actually exposed on those IPs
- **bgp.he.net** - ASN and routing info

---

## Learning Resources:
- **MDN Web Docs** - HTTP/networking fundamentals
- **Cloudflare Learning Center** - DNS, CDN, security concepts
- **SSL Labs Research Wiki** - TLS/encryption deep dives
