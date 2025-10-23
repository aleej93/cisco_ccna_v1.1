# Commands: Next-generation Firewalls and IPS

## 📌 Important Note

**CCNA Domain 1.0 Focus:** The CCNA exam focuses on understanding the **role and function** of firewalls and IPS, not deep configuration. However, you should be familiar with basic verification commands and concepts.

**More Advanced Configuration:** Detailed firewall and IPS configuration is covered in CCNA Security (Cisco Certified CyberOps Associate) and other security-focused certifications.

---

## 🔧 Cisco ASA Firewall Commands

### **Basic Verification Commands**

These commands help you verify firewall operation and status.

#### **Show Firewall Version and Status**

```cisco
ASA# show version
```

**What it shows:**

- ASA software version
- Hardware model
- Uptime
- License information
- Memory usage

**Example Output:**

```
Cisco Adaptive Security Appliance Software Version 9.12(4)
Device Manager Version 7.12(1)

Hardware:   ASA5516, 8192 MB RAM, CPU Xeon 5500 series 2400 MHz
Internal ATA Compact Flash, 8192MB
```

**Why it matters:** Verify you're running a supported version and have proper licensing.

---

#### **Show Firewall Interface Status**

```cisco
ASA# show interface ip brief
```

**What it shows:**

- All interfaces and their status
- IP addresses
- Up/Down state

**Example Output:**

```
Interface                  IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0         192.168.1.1     YES manual up                    up
GigabitEthernet0/1         10.0.0.1        YES manual up                    up
Management0/0              192.168.100.1   YES manual up                    up
```

**What to look for:**

- ✅ Status = "up" and Protocol = "up" (interface is working)
- ❌ Status = "down" (physical problem or shutdown)
- ❌ Protocol = "down" (Layer 2 issue)

---

#### **Show Active Connections Through Firewall**

```cisco
ASA# show conn
```

**What it shows:**

- Active connections passing through the firewall
- Source and destination IPs
- Ports and protocols
- Number of bytes transferred

**Example Output:**

```
TCP outside 203.0.113.50:443 inside 192.168.1.100:54321, idle 0:00:05, bytes 2048
UDP inside 192.168.1.50:53 outside 8.8.8.8:53, idle 0:00:01, bytes 512
```

**Reading the output:**

- `TCP outside 203.0.113.50:443` = External host on port 443 (HTTPS)
- `inside 192.168.1.100:54321` = Internal host on random source port
- `idle 0:00:05` = Connection has been idle for 5 seconds
- `bytes 2048` = 2048 bytes transferred

**Why it matters:** Troubleshoot connectivity issues and verify traffic is flowing.

---

#### **Show Access Lists (Firewall Rules)**

```cisco
ASA# show access-list
```

**What it shows:**

- Configured access control lists (ACLs)
- Permit/deny rules
- Hit counts (how many times each rule was matched)

**Example Output:**

```
access-list outside_in; 2 elements
access-list outside_in line 1 extended permit tcp any host 192.168.1.100 eq www (hitcnt=150)
access-list outside_in line 2 extended deny ip any any (hitcnt=2500)
```

**Reading the output:**

- `permit tcp any host 192.168.1.100 eq www` = Allow HTTP to web server
- `hitcnt=150` = This rule has been matched 150 times
- `deny ip any any` = Default deny rule (block everything else)

**Why it matters:** Verify security policies are applied correctly.

---

#### **Show Firewall Threat Detection**

```cisco
ASA# show threat-detection statistics
```

**What it shows:**

- Security threats detected
- Top attacking hosts
- Top targeted hosts

**Why it matters:** Identify potential attacks and security incidents.

---

### **Basic Configuration Commands**

#### **Set Interface Security Levels**

```cisco
ASA(config)# interface GigabitEthernet0/0
ASA(config-if)# nameif outside
ASA(config-if)# security-level 0
ASA(config-if)# ip address 203.0.113.1 255.255.255.0
```

**Explanation:**

- `nameif outside` — Assigns logical name "outside" to the interface
- `security-level 0` — Sets security level (0 = untrusted, 100 = most trusted)
- `ip address` — Assigns IP address to the interface

**Security Level Rules:**

- **0** = Outside (Internet) — least trusted
- **50** = DMZ
- **100** = Inside (internal network) — most trusted

**Default behavior:** Traffic can flow from higher security to lower security (inside → outside), but NOT from lower to higher without explicit rules.

---

#### **Basic Access Control List**

```cisco
ASA(config)# access-list OUTSIDE-IN extended permit tcp any host 192.168.1.100 eq 443
ASA(config)# access-list OUTSIDE-IN extended deny ip any any
ASA(config)# access-group OUTSIDE-IN in interface outside
```

**Explanation:**

- Line 1: Allow HTTPS (port 443) to internal web server 192.168.1.100
- Line 2: Deny all other traffic (default deny)
- Line 3: Apply the ACL to the outside interface (inbound direction)

---

## 🔧 Cisco Firepower (NGFW) Commands

### **Show Firepower Status**

```cisco
> show version
```

**What it shows:**

- Firepower software version
- Model information
- License status

---

### **Show Intrusion Prevention Status**

```cisco
> show ips status
```

**What it shows:**

- IPS engine status (running/stopped)
- Signature version
- Last update time

**Example Output:**

```
Intrusion Prevention: Enabled
Signature Version: S1234
Last Update: 2024-10-20 08:00:00
```

**Why it matters:** Verify IPS is active and signatures are current.

---

### **Show IPS Events (Detected Threats)**

```cisco
> show ips events
```

**What it shows:**

- Recent security events detected by IPS
- Attack signatures matched
- Source and destination IPs
- Actions taken (alert, drop, block)

**Example Output:**

```
Event ID: 12345
Signature: SQL Injection Attempt
Source IP: 203.0.113.50
Dest IP: 192.168.1.100
Action: Dropped
Timestamp: 2024-10-23 10:15:30
```

**Why it matters:** Identify attacks and verify IPS is blocking threats.

---

## 🖥️ Host-Based Firewall Commands

### **Windows Firewall**

#### **Check Firewall Status**

```powershell
netsh advfirewall show allprofiles
```

**What it shows:**

- Firewall state for all profiles (Domain, Private, Public)
- Whether it's ON or OFF

**Example Output:**

```
Domain Profile Settings:
State: ON

Private Profile Settings:
State: ON

Public Profile Settings:
State: ON
```

---

#### **Show Firewall Rules**

```powershell
netsh advfirewall firewall show rule name=all
```

**What it shows:**

- All configured firewall rules
- Enabled/disabled status
- Direction (inbound/outbound)
- Action (allow/block)

---

#### **Enable Windows Firewall**

```powershell
netsh advfirewall set allprofiles state on
```

**What it does:** Enables the firewall for all network profiles.

---

### **Linux iptables (Host-Based Firewall)**

#### **Show Current Firewall Rules**

```bash
sudo iptables -L -v -n
```

**Explanation:**

- `-L` = List all rules
- `-v` = Verbose (show packet counts)
- `-n` = Numeric (don't resolve hostnames)

**Example Output:**

```
Chain INPUT (policy DROP)
target     prot opt source               destination
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:22
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:80
DROP       all  --  0.0.0.0/0            0.0.0.0/0
```

**Reading the output:**

- Chain INPUT (policy DROP) = Default action is to drop packets
- ACCEPT tcp dpt:22 = Allow SSH (port 22)
- ACCEPT tcp dpt:80 = Allow HTTP (port 80)

---

#### **Allow Specific Port**

```bash
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

**Explanation:**

- `-A INPUT` = Append rule to INPUT chain
- `-p tcp` = Protocol is TCP
- `--dport 443` = Destination port 443 (HTTPS)
- `-j ACCEPT` = Action is ACCEPT (allow)

---

## 📊 Useful Show Commands Summary

### **Cisco ASA Firewall**

| Command                            | Purpose                                  |
| ---------------------------------- | ---------------------------------------- |
| `show version`                     | Display ASA version and hardware info    |
| `show interface ip brief`          | Show interface status and IP addresses   |
| `show conn`                        | Display active connections               |
| `show access-list`                 | Show firewall rules and hit counts       |
| `show threat-detection statistics` | Display detected threats                 |
| `show nameif`                      | Show interface names and security levels |

---

### **Cisco Firepower NGFW**

| Command           | Purpose                          |
| ----------------- | -------------------------------- |
| `show version`    | Display Firepower version        |
| `show ips status` | Show IPS engine status           |
| `show ips events` | Display detected security events |
| `show network`    | Show network configuration       |

---

## 🎯 Troubleshooting Scenarios

### **Scenario 1: Users Can't Access Internet**

**Step 1: Check interface status**

```cisco
ASA# show interface ip brief
```

✅ Verify outside interface is up/up

**Step 2: Check active connections**

```cisco
ASA# show conn
```

✅ Look for connections from internal users to Internet

**Step 3: Check NAT configuration**

```cisco
ASA# show nat
```

✅ Verify NAT rules are configured (covered in later domains)

---

### **Scenario 2: Firewall Blocking Legitimate Traffic**

**Step 1: Check access lists**

```cisco
ASA# show access-list
```

✅ Look for deny rules that might be blocking traffic

**Step 2: Check hit counts**

- If hitcnt=0, the rule isn't being matched
- If a deny rule has high hitcnt, it might be blocking legitimate traffic

**Step 3: Review logs**

```cisco
ASA# show log | include Deny
```

✅ Look for denied connections in logs

---

### **Scenario 3: IPS Not Blocking Attacks**

**Step 1: Verify IPS is enabled**

```cisco
> show ips status
```

✅ Check that status shows "Enabled"

**Step 2: Check signature version**

```cisco
> show ips status
```

✅ Verify signatures are up-to-date

**Step 3: Review IPS events**

```cisco
> show ips events
```

✅ Check if threats are being detected but not blocked (may need policy adjustment)

---

## 🚨 Important Exam Notes

### **What You Need to Know for CCNA**

✅ **DO know:**

- Basic `show` commands for verification
- How to check interface status
- How to view active connections
- The concept of security levels (ASA)
- That ACLs control firewall traffic

❌ **DON'T need to know (for Domain 1.0):**

- Complex ACL configuration syntax
- NAT configuration details (covered in Domain 3.0/4.0)
- Deep IPS signature configuration
- Advanced Firepower management

---

## 📝 Command Comparison: Router vs. Firewall

| Task                | Router                     | Firewall (ASA)            |
| ------------------- | -------------------------- | ------------------------- |
| Show version        | `show version`             | `show version`            |
| Show interfaces     | `show ip interface brief`  | `show interface ip brief` |
| Show routes         | `show ip route`            | `show route`              |
| Show connections    | `show ip nat translations` | `show conn`               |
| Show security rules | N/A                        | `show access-list`        |

**Key Difference:** Routers focus on routing, firewalls focus on security filtering.

---

## 💡 Final Command Tips for the Exam

1. **Know the difference** between router and firewall show commands
2. **Understand** what `show conn` displays (active connections)
3. **Remember** ASA uses security levels (0-100)
4. **Know** that access-lists on firewalls control security policies
5. **Be familiar** with basic host-based firewall concepts (Windows Firewall, iptables)

**Most Important:** For CCNA Domain 1.0, focus on **understanding the purpose** of these commands, not memorizing exact syntax!
