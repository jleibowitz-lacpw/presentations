---
marp: true
---

# PCI-Compliant iPad Kiosks

### Field Office Permit & Payment Devices

📅 June 2025
👤 Prepared by: Jon Leibowitz - Student Worker, IT
🏛️ Los Angeles County Public Works

---

## Purpose of This Review

✅ Understand how to securely configure iPads used as payment kiosks
✅ Ensure PCI DSS v4.0 compliance for devices processing cardholder data
✅ Provide actionable guidance for field deployment using Intune & FIS gateway

---

## iPad Kiosk Use Case

* Devices located in field offices
* Used to access a county-developed permit/payment web app
* Accept payment details via FIS processor
* Locked-down Safari-based experience
* Managed via Microsoft Intune (MDM)

---

## Key Compliance Goals

🛡️ Prevent unauthorized access
🔐 Protect cardholder data
📵 Block insecure behaviors
🧰 Enable remote management
📁 Maintain auditability

---

## PCI Compliance Overview

| PCI Scope Area       | Kiosk Focus             |
| -------------------- | ----------------------- |
| Encryption           | TLS & P2PE for payments |
| Storage Restrictions | No PAN or CVV locally   |
| Physical Security    | Enclosure & access logs |
| Device Hardening     | MDM policies enforced   |
| Software Integrity   | Web app + secure Safari |
| Monitoring           | Logs, alerts, updates   |

---

## Kiosk Configuration Summary

| Area             | Action Required                     |
| ---------------- | ----------------------------------- |
| Lockdown Mode    | Single App or Multi-App via Intune  |
| App Access       | Only payment web app (Safari)       |
| Web Restrictions | Whitelist FIS/payment URLs only     |
| Form Data        | Autofill disabled in Safari         |
| Screen Capture   | Block screenshots/screen record     |
| Supervision      | Use Apple Business Manager → Intune |

---

## Payment Security Requirements

* TLS 1.2+ for all web and API communication
* Use P2PE card readers (FIS-approved)
* Tokenize payment data via FIS Gateway
* Never store PAN, CVV, or cardholder data
* Avoid local caching of forms or logs

---

## Network & Remote Access Controls

* Devices on separate VLAN or Wi-Fi SSID
* Only allow traffic to FIS and permit app domains
* Disable ability to join unknown networks
* VPN optional for further segmentation
* Use Intune to push Wi-Fi & firewall rules

---

## Physical & Operational Security

🔒 Lock iPads in tamper-evident mounts
🧯 Field staff inspect devices weekly
📋 Maintain chain-of-custody & logs
📸 Block use of camera, mic, and other apps
🛑 Block personal hotspot and iOS Settings access

---

## Intune Policy Recommendations

| Setting                  | Recommendation   |
| ------------------------ | ---------------- |
| Safari Autofill          | Disabled         |
| Screen Capture           | Blocked          |
| Personal Hotspot         | Blocked          |
| Allowed Apps             | Safari only      |
| Allowed URLs             | FIS + Permit App |
| Device Update Compliance | Enforced         |
| Jailbreak Detection      | Enabled          |

---

## App & Payment Gateway Considerations

* County web app must follow PCI secure coding standards
* Use HTTPS and avoid storing card data server-side
* Use FIS-hosted fields or iframes to isolate payment input
* FIS tokenization reduces PCI scope on the web app

---

## Audit & Compliance Tracking

📝 Document all kiosk setup steps and security controls
🛠️ Use Intune’s compliance dashboard
📤 Enable alerting for jailbroken/offline/non-compliant devices
📂 Maintain change logs, device checklists, and incident response plans

---

## Staff Roles & Training

👷 Field Staff

* Understand kiosk security basics
* Identify tampering or misuse
* Know how to escalate incidents

🧑‍💻 Admin Team

* Enforce Intune policy
* Monitor device compliance
* Manage remote updates & wipes

---

## Summary

✅ Kiosks can meet PCI DSS if locked down properly
✅ Intune and Apple Business Manager are essential tools
✅ Use encrypted card readers + tokenization with FIS
✅ Document and monitor everything for audit readiness

---

## Appendix: Source Materials

* PCI DSS v4.0 Quick Reference Guide
* Microsoft Intune: iOS Kiosk Mode & Restrictions
* Apple Business Manager + Supervision Setup
* FIS Developer Portal & P2PE Requirements
* PCI SSC: Mobile Payment Acceptance Guidelines

---

## Questions & Next Steps

📌 Review config with infrastructure/security leads
📌 Coordinate with development team on web app controls
📌 Schedule test deployment of pilot kiosk
📌 Prepare compliance documentation binder

