# 1.1b Layer 2 and Layer 3 Switches — CCNA v1.1

## What is a Switch?

A **switch** is a network device that connects multiple end hosts (like computers, servers, printers) within the same Local Area Network (LAN).

---

## Key Characteristics of Switches

### Many Network Interfaces

- Switches typically have **24+ ports** to connect end hosts
- Examples: Cisco Catalyst 9200, Catalyst 3650

### LAN Connectivity Only

- Switches provide connectivity **within the same LAN**
- They connect hosts in the same local network together
- **Switches do NOT provide connectivity between different LANs or over the Internet**

---

## Layer 2 vs Layer 3 Switches

### Layer 2 Switches

- Operate at the **Data Link Layer** (Layer 2 of the OSI model)
- Forward traffic based on **MAC addresses**
- Connect devices within the same network/VLAN

### Layer 3 Switches

- Operate at both Layer 2 **and** the **Network Layer** (Layer 3 of the OSI model)
- Can perform **routing** functions in addition to switching
- Forward traffic based on **IP addresses**
- Combine the functionality of switches and routers

---

## Switches vs Routers

| **Switches**                       | **Routers**                         |
| ---------------------------------- | ----------------------------------- |
| Many ports (24+)                   | Fewer ports                         |
| Connect hosts in the **same LAN**  | Connect **different LANs** together |
| Do NOT route between networks      | Route traffic **between networks**  |
| Cannot send data over the Internet | Send data **over the Internet**     |

---

## Exam Focus

For **CCNA Exam Objective 1.1b**, you need to:

- Understand the **role** of Layer 2 and Layer 3 switches in a network
- Know that switches have **many ports** for connecting end hosts
- Recognize that switches provide **LAN connectivity only**
- Understand the basic difference between Layer 2 and Layer 3 switches

**Note:** Switches are covered in much more detail in Domain 2.0 (Network Access), including VLANs, trunking, and STP.

---

## Quick Reference

**Switch** = Network device with many ports that connects hosts within the same LAN

**Layer 2 Switch** = Operates at Data Link Layer, uses MAC addresses

**Layer 3 Switch** = Operates at Network Layer too, can route using IP addresses
