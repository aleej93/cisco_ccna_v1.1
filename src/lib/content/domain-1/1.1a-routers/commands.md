# 💻 Commands: Routers

**Essential CLI commands for understanding routers at the foundational level.**

---

## 🔍 Viewing Router Information

### **Show Routing Table**
```cisco
Router# show ip route
```
**Purpose:** Displays the router's routing table, including all known networks and how to reach them.

**What you'll see:**
- Route source codes (C, S, D, O, R)
- Network prefixes and subnet masks
- Next-hop IP addresses
- Administrative Distance [AD] and Metric values
- Outgoing interfaces

**Example output:**
```
C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
S    10.0.0.0/8 [1/0] via 192.168.1.1
O    172.16.0.0/16 [110/20] via 192.168.1.2
```

---

### **Show Specific Route**
```cisco
Router# show ip route 192.168.10.5
```
**Purpose:** Shows which route the router will use for a specific destination IP.

**Exam tip:** Use this command to verify longest prefix match decisions.

---

### **Show Interface Status**
```cisco
Router# show ip interface brief
```
**Purpose:** Displays a summary of all interfaces, their IP addresses, and status.

**Example output:**
```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.1.1     YES manual up                    up
GigabitEthernet0/1     10.0.0.1        YES manual up                    up
Serial0/0/0            unassigned      YES unset  administratively down down
```

**Key status combinations:**
- `up / up` = Interface is working
- `up / down` = Layer 1 is up, but Layer 2 has an issue (e.g., wrong encapsulation)
- `administratively down / down` = Interface is shut down

---

### **Show Running Configuration**
```cisco
Router# show running-config
```
**Purpose:** Displays the current active configuration, including interface settings and routing protocol config.

**For routers, look for:**
- Interface IP addresses
- Static routes
- Routing protocol configurations

---

## ⚙️ Basic Router Configuration

### **Set Hostname**
```cisco
Router(config)# hostname R1
```
**Purpose:** Changes the router's name (cosmetic but useful for identification).

---

### **Configure Interface IP Address**
```cisco
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
```
**Purpose:** Assigns an IP address to an interface and brings it up.

**Key point:** `no shutdown` is required! Interfaces are administratively down by default.

---

### **Add a Static Route**
```cisco
Router(config)# ip route 10.0.0.0 255.0.0.0 192.168.1.2
```
**Purpose:** Manually creates a route to network 10.0.0.0/8 via next-hop 192.168.1.2.

**Format:** `ip route [destination-network] [subnet-mask] [next-hop-IP or exit-interface]`

---

### **Add a Default Route**
```cisco
Router(config)# ip route 0.0.0.0 0.0.0.0 192.168.1.1
```
**Purpose:** Creates a "gateway of last resort" — if no specific route matches, use this one.

**Common use case:** Point to your ISP's router for Internet access.

---

## 🔧 Verification Commands

### **Show Interface Details**
```cisco
Router# show interface GigabitEthernet0/0
```
**Purpose:** Displays detailed information about a specific interface (errors, packets, speed, duplex).

---

### **Show Version**
```cisco
Router# show version
```
**Purpose:** Displays IOS version, uptime, hardware details, and configuration register value.

---

### **Show Protocols**
```cisco
Router# show ip protocols
```
**Purpose:** Displays routing protocol information (not heavily used in Domain 1.1, but useful later for OSPF/EIGRP).

---

## 📌 Commands You'll Use in Later Domains

**Note:** These are mentioned here for awareness but will be covered in depth in Domain 3.0 (IP Connectivity).

- `show ip ospf neighbor` — View OSPF neighbors
- `show ip eigrp neighbors` — View EIGRP neighbors
- `traceroute [destination]` — Trace packet path hop-by-hop
- `ping [destination]` — Test connectivity

---

## 🎯 Exam-Relevant Command Tips

1. **Memorize `show ip route` output format** — You'll see this on the exam!
2. **Know the difference between:**
   - `show running-config` (active config)
   - `show startup-config` (saved config)
3. **Remember:** Interfaces are shut down by default (use `no shutdown`)
4. **Route codes to memorize:**
   - **C** = Connected
   - **S** = Static
   - **D** = EIGRP
   - **O** = OSPF
   - **R** = RIP

---

## 🔗 Related Exam Objectives

- **3.1** — Interpret the components of routing table
- **3.2** — Determine how a router makes a forwarding decision
- **3.3** — Configure and verify IPv4 and IPv6 static routing

**Note:** You'll practice these commands extensively in Domain 3.0!

---

**💡 Pro Tip:** For the CCNA exam, focus on *reading* command outputs more than memorizing exact syntax. Cisco loves to show you a `show ip route` output and ask "which route is used?"