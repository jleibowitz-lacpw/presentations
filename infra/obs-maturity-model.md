---
marp: true
theme: default
paginate: true
---

# Monitoring Maturity Model  
*"From band-aids to observability"*

---

## Level 1: Band-Aid Phase
- **Tools:** ad-hoc scripts, Telerik QA checks  
- **Where it runs:** someone's desktop  
- **What you get:** "Is it up?" (maybe)  
- **Risks:** fragile, no timeline, no history, no alerts if the checker itself dies  

---

## Level 2: Hobbyist Phase
- **Tools:** Uptime Kuma, cron + curl, homegrown dashboards  
- **Where it runs:** small VM or container on-prem  
- **What you get:** uptime history, basic alerts  
- **Risks:** single maintainer, not standardized, limited integrations  

---

## Level 3: Pro-sumer Phase
- **Tools:** Grafana Cloud (free), Better Stack, New Relic free tier  
- **Where it runs:** SaaS, with optional on-prem agents  
- **What you get:** dashboards, alert routing (Teams, email), some log integration  
- **Risks:** data caps, culture shift needed (teams must *look* at dashboards)  

---

## Level 4: Enterprise Phase
- **Tools:** Datadog, Dynatrace, New Relic enterprise plans  
- **Where it runs:** hybrid—agents on-prem + SaaS backend  
- **What you get:** full observability → metrics, logs, traces, synthetic tests  
- **Risks:** cost, complexity, requires buy-in across teams  

---

## Takeaway
- We’re currently **between Level 1 and 2**  
- Even a small step to Level 2/3 → huge leap in professionalism  
- Long-term: Level 4 isn’t mandatory, but **a monitoring system of record is**  
