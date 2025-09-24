---
marp: true
theme: default
paginate: true
---

# Loopback vs. 0.0.0.0  
## IIS Binding Behavior

---

## Loopback

- IP: 127.0.0.1  
- Alias: localhost  
- Scope: Local machine only  
- Traffic does not leave host  
- Not accessible from network  

---

## 0.0.0.0

- Binds to all interfaces  
- Includes:  
  - Loopback  
  - LAN IPs  
  - Public IPs  
- Accessible from network  

---

## IIS Default Binding

- Default: "All Unassigned"  
- Equivalent to 0.0.0.0  
- Allows external access unless restricted  

---

## Restrict IIS to Loopback  
### Option 1: IIS Manager

- Open Bindings  
- Edit site binding  
- Set IP to 127.0.0.1  

---

## Restrict IIS to Loopback  
### Option 2: netsh

Command:  
`netsh http add iplisten 127.0.0.1`  

Verify:  
`netsh http show iplisten`  

---

## Use Cases

| Scenario              | Bind To     |
|-----------------------|-------------|
| Local development     | 127.0.0.1   |
| Internal (example)   | 10.0.0.0/8  |
| Public access         | 0.0.0.0     |

---

## Summary

- 127.0.0.1: Local-only  
- 0.0.0.0: All interfaces  
- IIS defaults to all interfaces  
- Can be restricted via bindings or netsh  
