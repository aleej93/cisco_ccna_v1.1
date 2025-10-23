# 1.1c Next-generation Firewalls and IPS — CCNA v1.1

## What is a Firewall?

A **firewall** is a network security device that monitors and controls network traffic entering and exiting your network based on configured security rules.

Think of a firewall as a security guard at the entrance of a building — it checks who's coming in and going out, and only allows authorized traffic to pass through.

---

## Key Functions of Firewalls

### 1. **Monitor and Control Traffic**

Firewalls inspect network traffic and make decisions based on:

- Source and destination IP addresses
- Port numbers
- Protocols (TCP, UDP, etc.)
- Configured security rules

### 2. **Protect Networks from Threats**

Firewalls can be placed:

- **"Inside" the network** — between internal network segments
- **"Outside" the network** — between the internal network and the Internet

### 3. **Filter Unwanted Traffic**

Firewalls block malicious traffic such as:

- Unauthorized access attempts
- Known attack patterns
- Traffic from blacklisted sources

---

## Types of Firewalls

### **Network Firewalls**

- **Hardware devices** that filter traffic between networks
- Typically placed at the network perimeter (edge)
- Examples: Cisco ASA 5500-X, Cisco Firepower 2100

### **Host-based Firewalls**

- **Software applications** that filter traffic entering and exiting a host machine (like a PC)
- Examples: Windows Firewall, macOS Firewall

---

## What is a Next-Generation Firewall (NGFW)?

A **Next-Generation Firewall (NGFW)** is a firewall that includes **modern and advanced filtering capabilities** beyond traditional firewalls.

### Traditional Firewall vs. Next-Generation Firewall

| **Traditional Firewall**                            | **Next-Generation Firewall**                            |
| --------------------------------------------------- | ------------------------------------------------------- |
| Filters based on IP addresses, ports, and protocols | All traditional features **PLUS** advanced capabilities |
| Basic packet filtering                              | Application-aware filtering                             |
| Stateful inspection                                 | Deep packet inspection                                  |
| -                                                   | Intrusion Prevention System (IPS)                       |
| -                                                   | Advanced threat detection                               |
| -                                                   | Integration with threat intelligence                    |

---

## What is an Intrusion Prevention System (IPS)?

An **Intrusion Prevention System (IPS)** is a security technology that monitors network traffic for malicious activity and can **automatically block or prevent** threats in real-time.

### Key Features of IPS

- **Signature-based detection** — Identifies known attack patterns
- **Anomaly-based detection** — Detects unusual behavior that may indicate an attack
- **Inline deployment** — Sits directly in the traffic path and can block threats immediately
- **Prevention capabilities** — Actively stops attacks (unlike IDS which only detects and alerts)

### IPS vs. IDS

| **IDS (Intrusion Detection System)** | **IPS (Intrusion Prevention System)**     |
| ------------------------------------ | ----------------------------------------- |
| **Detects** threats and sends alerts | **Detects AND prevents** threats          |
| Passive monitoring (out-of-band)     | Active prevention (inline)                |
| Cannot block traffic                 | Can block malicious traffic automatically |

---

## Real-World Scenario

**Scenario:**  
Your company has offices in New York and Tokyo. Each office has a local network (LAN) with PCs, servers, and switches. The two offices are connected over the Internet, and there are potential attackers trying to access your network.

**Without a firewall:**

- Attackers can attempt to access your servers and PCs directly
- There's no filtering of malicious traffic
- Your network is vulnerable

**With a Next-Generation Firewall + IPS:**

- Traffic from legitimate users (New York ↔ Tokyo) is allowed
- Traffic from attackers is **blocked automatically** by the IPS
- The NGFW inspects traffic at a deeper level, identifying and stopping advanced threats
- Your network is protected from unauthorized access and attacks

---

## Summary

- A **firewall** monitors and controls network traffic based on configured rules
- **Network firewalls** are hardware devices that filter traffic between networks
- **Host-based firewalls** are software applications on individual computers
- A **Next-Generation Firewall (NGFW)** includes advanced features like deep packet inspection, application awareness, and integrated IPS
- An **Intrusion Prevention System (IPS)** actively detects and blocks threats in real-time
- NGFWs and IPS are commonly deployed together to provide comprehensive network security

---

## Exam Connection

✅ **Maps to CCNA v1.1 Exam Objective:**  
**1.1c** — Explain the role and function of network components: **Next-generation firewalls and IPS**

**For the exam, remember:**

- The difference between traditional firewalls and NGFWs
- Network firewalls vs. host-based firewalls
- The role of IPS in preventing (not just detecting) threats
- Where firewalls are typically deployed in a network

---

## Check Your Understanding

1. What is the main difference between a traditional firewall and a next-generation firewall?
2. Can a host-based firewall protect an entire network?
3. What is the key difference between IDS and IPS?
4. Where would you typically deploy a firewall in a network?

---

## Related Exam Objectives

- **5.6** — Configure and verify access control lists (ACLs)
- **5.7** — Configure and verify Layer 2 security features (DHCP snooping, dynamic ARP inspection, and port security)

**Note:** Security topics like firewalls and IPS are covered in more depth in Domain 5.0 (Security Fundamentals). This section provides a foundational understanding of their role and function as network components.
