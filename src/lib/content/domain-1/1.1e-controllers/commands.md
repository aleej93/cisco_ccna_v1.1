# Commands Reference: 1.1.e Controllers

**Exam Objective:** *Domain 1.1.e — Explain the role and function of network components: Controllers*

---

## 📋 Overview

This reference covers **Wireless LAN Controller (WLC)** commands and related switch configurations. The CCNA exam focuses more on **conceptual knowledge** of WLCs, but understanding basic commands helps reinforce concepts.

**Important Notes:**
- WLCs are primarily configured via **GUI (web interface)**, not CLI
- CLI is available but less commonly used than GUI
- Commands shown here are for **understanding and troubleshooting**, not extensive configuration
- Switch commands help you support lightweight AP deployments

---

## 🔷 WLC CLI Basics

### Accessing the WLC CLI

**Via Console:**
```
[Connect to WLC console port with terminal program]
User: admin
Password: ********
(Cisco Controller) >
```

**Via SSH:**
```bash
ssh admin@192.168.1.100
Password: ********
(Cisco Controller) >
```

**Via Telnet (not recommended - insecure):**
```bash
telnet 192.168.1.100
User: admin
Password: ********
(Cisco Controller) >
```

---

## 🔷 WLC Show Commands

### 1. General WLC Information

**Show WLC Summary:**
```cisco-wlc
(Cisco Controller) > show sysinfo
```
**Output includes:**
- System name, location, contact
- Software version
- MAC address
- IP address configuration
- Uptime
- Number of APs joined

**Example Output:**
```
Manufacturer's Name.......................... Cisco Systems Inc.
Product Name................................. Cisco Controller
Product Version.............................. 8.10.151.0
System Name.................................. WLC1
System Location.............................. Building A
System Contact............................... admin@company.com
System Up Time............................... 5 days 12 hours 34 mins
```

---

**Show WLC Network Configuration:**
```cisco-wlc
(Cisco Controller) > show network summary
```
**Shows:**
- RF Network Name
- Mobility domain
- Network mode (IPv4/IPv6)
- Management interface details

---

### 2. AP Information Commands

**Show All Access Points:**
```cisco-wlc
(Cisco Controller) > show ap summary
```
**Output includes:**
- AP Name
- AP Model
- Ethernet MAC address
- IP address
- Status (joined/registering/downloading)
- Number of clients

**Example Output:**
```
AP Name           Model        MAC Address      IP Address      Status  Clients
-------------------------------------------------------------------------------
AP-Floor1-101     AIR-CAP3702  00:1a:2b:3c:4d:5e  192.168.1.10   Joined  12
AP-Floor2-201     AIR-CAP3702  00:1a:2b:3c:4d:5f  192.168.1.11   Joined  8
```

---

**Show Detailed AP Information:**
```cisco-wlc
(Cisco Controller) > show ap config general AP-Floor1-101
```
**Shows:**
- AP name, model, serial number
- IP address, subnet mask, gateway
- CAPWAP state
- Software version
- Country code
- Radios enabled
- PoE status

---

**Show AP Join Statistics:**
```cisco-wlc
(Cisco Controller) > show ap join stats summary all
```
**Purpose:** Troubleshoots why APs aren't joining
**Shows:**
- Discovery attempts
- Join requests sent
- Join failures and reasons
- DTLS setup status

---

### 3. CAPWAP Troubleshooting

**Show CAPWAP Status:**
```cisco-wlc
(Cisco Controller) > show ap summary
```
Look for **Status** column:
- `Registered` - AP has registered with WLC but not fully joined
- `Downloading` - AP is downloading software from WLC
- `Joined` - AP is fully operational
- `Disconnected` - AP has lost connection to WLC

---

**Show CAPWAP Debugging (use cautiously):**
```cisco-wlc
(Cisco Controller) > debug capwap info enable
(Cisco Controller) > debug capwap errors enable
```
**Purpose:** See real-time CAPWAP messages
**Warning:** Generates significant output; disable when done

**Disable debugging:**
```cisco-wlc
(Cisco Controller) > debug disable-all
```

---

### 4. WLC Interface Commands

**Show All Interfaces:**
```cisco-wlc
(Cisco Controller) > show interface summary
```
**Output includes:**
- Interface Name
- Type (Management, Virtual, Dynamic, etc.)
- VLAN ID
- IP Address
- Status

**Example Output:**
```
Interface Name       Type       VLAN  IP Address       Status
----------------------------------------------------------------
management           Static     10    192.168.1.100    Up
virtual              Static     N/A   1.1.1.1          Up
guest                Dynamic    200   10.1.0.100       Up
internal             Dynamic    100   10.0.0.100       Up
```

---

**Show Detailed Interface Configuration:**
```cisco-wlc
(Cisco Controller) > show interface detailed management
```
**Shows:**
- IP address, subnet mask, gateway
- VLAN assignment
- Primary/Secondary DHCP server
- ACLs applied
- Active clients

---

### 5. WLAN (SSID) Commands

**Show All WLANs:**
```cisco-wlc
(Cisco Controller) > show wlan summary
```
**Output includes:**
- WLAN ID
- Profile Name (internal name)
- SSID (broadcasted name)
- Status (Enabled/Disabled)
- Security Policy

**Example Output:**
```
WLAN ID  Profile Name   SSID           Status    Security
-----------------------------------------------------------
1        internal       Internal       Enabled   WPA2-PSK
2        guest          Guest          Enabled   Web Auth
17       voice          VoIP           Enabled   WPA2-Enterprise
```

---

**Show Detailed WLAN Configuration:**
```cisco-wlc
(Cisco Controller) > show wlan 1
```
**Shows:**
- SSID name
- Status
- Security settings (WPA2, 802.1X, PSK)
- Interface mapping (which dynamic interface)
- QoS settings
- Client limits

---

### 6. Client Information Commands

**Show All Connected Clients:**
```cisco-wlc
(Cisco Controller) > show client summary
```
**Output includes:**
- Client MAC address
- AP Name
- WLAN (SSID)
- Status (Associated/Authenticated/Run)
- Protocol (802.11a/b/g/n/ac)

---

**Show Detailed Client Information:**
```cisco-wlc
(Cisco Controller) > show client detail 00:11:22:33:44:55
```
**Shows:**
- MAC address, IP address
- Username (if 802.1X)
- Associated AP
- SSID
- Authentication method
- Encryption cipher
- Data rates
- Signal strength (RSSI)
- Time associated

---

**Show Number of Clients per AP:**
```cisco-wlc
(Cisco Controller) > show ap summary
```
Check **Clients** column to see load distribution

---

### 7. RF Management Commands

**Show Country Code:**
```cisco-wlc
(Cisco Controller) > show country
```
**Purpose:** Verify regulatory domain for proper channel/power selection

---

**Show 802.11a Radio Summary (5 GHz):**
```cisco-wlc
(Cisco Controller) > show 802.11a summary
```
**Shows:**
- 802.11a network status (Enabled/Disabled)
- Number of APs
- Channels in use

---

**Show 802.11b Radio Summary (2.4 GHz):**
```cisco-wlc
(Cisco Controller) > show 802.11b summary
```
**Shows:**
- 802.11b/g/n network status
- Number of APs
- Channels in use

---

**Show Channel and Power Settings for Specific AP:**
```cisco-wlc
(Cisco Controller) > show ap auto-rf 802.11a AP-Floor1-101
```
**Shows:**
- Current channel
- Current transmit power
- Channel assignment method (auto/manual)
- Power assignment method (auto/manual)

---

### 8. Configuration Commands (Basic Examples)

**Note:** WLC CLI configuration is less common than GUI. These examples show syntax.

**Create a WLAN:**
```cisco-wlc
(Cisco Controller) > config wlan create 10 Guest guest-ssid
(Cisco Controller) > config wlan enable 10
```
- Creates WLAN ID 10
- Profile name: Guest
- SSID: guest-ssid
- Enables the WLAN

---

**Disable a WLAN:**
```cisco-wlc
(Cisco Controller) > config wlan disable 10
```

---

**Set WLAN Security to WPA2-PSK:**
```cisco-wlc
(Cisco Controller) > config wlan security wpa akm psk set-key ascii <password> 10
```
- Sets WPA2-PSK for WLAN ID 10
- ASCII key format

---

**Reboot WLC:**
```cisco-wlc
(Cisco Controller) > reset system
```
**Warning:** Disconnects all APs and clients!

---

**Save Configuration:**
```cisco-wlc
(Cisco Controller) > save config
```
**Purpose:** Persist configuration changes to memory

---

## 🔷 Switch Configuration for WLC Deployment

### 1. Basic Switch Configuration for AP Connectivity

**Configure Access Port for Lightweight AP:**
```cisco-ios
SW1(config)# interface gigabitEthernet 0/1
SW1(config-if)# description Lightweight AP - Floor 1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
SW1(config-if)# spanning-tree portfast
SW1(config-if)# spanning-tree bpduguard enable
SW1(config-if)# power inline auto
```

**Explanation:**
- `switchport mode access` - Configures as access port (NOT trunk)
- `switchport access vlan 10` - Assigns to management VLAN 10 (where WLC management interface resides)
- `spanning-tree portfast` - Brings port up immediately (AP needs network quickly)
- `spanning-tree bpduguard enable` - Protects against loops if AP misconfigured
- `power inline auto` - Enables PoE for AP power (if supported)

---

### 2. VLAN Configuration for WLANs

**Create VLANs for Management and WLANs:**
```cisco-ios
SW1(config)# vlan 10
SW1(config-vlan)# name Management
SW1(config-vlan)# vlan 100
SW1(config-vlan)# name Internal-WLAN
SW1(config-vlan)# vlan 200
SW1(config-vlan)# name Guest-WLAN
SW1(config-vlan)# exit
```

**Assign SVIs (for Layer 3 switch acting as gateway):**
```cisco-ios
SW1(config)# interface vlan 10
SW1(config-if)# description Management VLAN
SW1(config-if)# ip address 192.168.1.1 255.255.255.0
SW1(config-if)# no shutdown

SW1(config)# interface vlan 100
SW1(config-if)# description Internal WLAN
SW1(config-if)# ip address 10.0.0.1 255.255.255.0
SW1(config-if)# no shutdown

SW1(config)# interface vlan 200
SW1(config-if)# description Guest WLAN
SW1(config-if)# ip address 10.1.0.1 255.255.255.0
SW1(config-if)# no shutdown
```

---

### 3. Trunk Configuration for WLC Connection

**Configure Trunk Port to WLC:**
```cisco-ios
SW1(config)# interface gigabitEthernet 0/24
SW1(config-if)# description Trunk to WLC
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,100,200
SW1(config-if)# switchport trunk native vlan 10
```

**Explanation:**
- `switchport mode trunk` - Trunk port carries multiple VLANs
- `switchport trunk allowed vlan` - Specifies which VLANs are carried
- `switchport trunk native vlan 10` - Management VLAN is native (untagged)

**Why trunk for WLC?**
- WLC needs access to multiple VLANs (management + all dynamic interface VLANs)
- WLC maps WLANs to VLANs and sends traffic to wired network on appropriate VLAN

---

### 4. DHCP Configuration for APs

**Configure DHCP Pool for Management VLAN (APs get IPs here):**
```cisco-ios
SW1(config)# ip dhcp pool VLAN10
SW1(dhcp-config)# network 192.168.1.0 255.255.255.0
SW1(dhcp-config)# default-router 192.168.1.1
SW1(dhcp-config)# dns-server 8.8.8.8
SW1(dhcp-config)# option 43 ip 192.168.1.100
SW1(dhcp-config)# exit
```

**Explanation:**
- `network` - Defines IP range for DHCP pool
- `default-router` - Gateway for APs
- `dns-server` - DNS for APs (optional)
- `option 43 ip 192.168.1.100` - Tells APs the WLC IP address (critical for discovery!)

---

**Configure DHCP Pools for Wireless Clients:**
```cisco-ios
SW1(config)# ip dhcp pool VLAN100
SW1(dhcp-config)# network 10.0.0.0 255.255.255.0
SW1(dhcp-config)# default-router 10.0.0.1
SW1(dhcp-config)# dns-server 8.8.8.8
SW1(dhcp-config)# exit

SW1(config)# ip dhcp pool VLAN200
SW1(dhcp-config)# network 10.1.0.0 255.255.255.0
SW1(dhcp-config)# default-router 10.1.0.1
SW1(dhcp-config)# dns-server 8.8.8.8
SW1(dhcp-config)# exit
```

---

**Exclude Static IPs from DHCP Pools:**
```cisco-ios
SW1(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10
SW1(config)# ip dhcp excluded-address 10.0.0.1 10.0.0.10
SW1(config)# ip dhcp excluded-address 10.1.0.1 10.1.0.10
```
**Purpose:** Reserve IPs for WLC, switches, routers, servers

---

### 5. NTP Configuration (Important for WLC)

**Configure Switch as NTP Master:**
```cisco-ios
SW1(config)# ntp master 1
```
**Purpose:** WLCs and APs need accurate time for certificates, logging, troubleshooting

---

**Configure Switch to Use External NTP Server:**
```cisco-ios
SW1(config)# ntp server 216.239.35.0
```

---

### 6. Verification Commands (Switch)

**Verify VLAN Configuration:**
```cisco-ios
SW1# show vlan brief
```

**Verify Trunk Configuration:**
```cisco-ios
SW1# show interfaces trunk
```

**Verify PoE Status:**
```cisco-ios
SW1# show power inline
```
**Shows:** Which ports have PoE enabled, power draw, power available

**Verify DHCP Bindings:**
```cisco-ios
SW1# show ip dhcp binding
```
**Shows:** Which devices received IPs from DHCP pools

**Verify DHCP Pool Statistics:**
```cisco-ios
SW1# show ip dhcp pool VLAN10
```

---

## 🔷 Common Troubleshooting Scenarios

### Problem: AP Not Joining WLC

**Diagnostic Steps:**

1. **Check AP has IP address:**
```cisco-ios
SW1# show ip dhcp binding
```
Look for AP's MAC address

2. **Check DHCP Option 43:**
```cisco-ios
SW1# show run | section dhcp
```
Verify `option 43 ip <WLC-IP>` is configured

3. **Check AP can reach WLC:**
```cisco-ios
SW1# show ip arp | include <AP-IP>
SW1# ping <WLC-IP> source vlan 10
```

4. **Check WLC status:**
```cisco-wlc
(Cisco Controller) > show ap join stats summary all
```

5. **Check AP is not blocked:**
```cisco-wlc
(Cisco Controller) > show exclusionlist
```
If AP MAC is listed, remove it:
```cisco-wlc
(Cisco Controller) > config exclusionlist delete <AP-MAC>
```

---

### Problem: Clients Cannot Connect to WLAN

**Diagnostic Steps:**

1. **Check WLAN is enabled:**
```cisco-wlc
(Cisco Controller) > show wlan summary
```
Status should show `Enabled`

2. **Check interface mapping:**
```cisco-wlc
(Cisco Controller) > show wlan <WLAN-ID>
```
Verify WLAN is mapped to correct dynamic interface

3. **Check dynamic interface status:**
```cisco-wlc
(Cisco Controller) > show interface summary
```
Dynamic interface should show `Up`

4. **Check DHCP pool for client VLAN:**
```cisco-ios
SW1# show ip dhcp pool <VLAN-pool>
SW1# show ip dhcp binding
```

---

### Problem: Poor Wireless Performance

**Diagnostic Steps:**

1. **Check client signal strength:**
```cisco-wlc
(Cisco Controller) > show client detail <MAC>
```
Look for RSSI value (should be &gt;-70 dBm)

2. **Check channel utilization:**
```cisco-wlc
(Cisco Controller) > show ap auto-rf 802.11a summary
```

3. **Check for rogue APs:**
```cisco-wlc
(Cisco Controller) > show rogue ap summary
```

4. **Check client load balancing:**
```cisco-wlc
(Cisco Controller) > show ap summary
```
Look for uneven client distribution

---

## 📝 Command Quick Reference

### Top 10 WLC Commands for CCNA

| Command | Purpose |
|---------|---------|
| `show sysinfo` | WLC summary info |
| `show ap summary` | List all APs |
| `show interface summary` | List all interfaces |
| `show wlan summary` | List all WLANs |
| `show client summary` | List all connected clients |
| `show client detail <MAC>` | Detailed client info |
| `show ap join stats summary all` | AP join troubleshooting |
| `config wlan enable <ID>` | Enable WLAN |
| `config wlan disable <ID>` | Disable WLAN |
| `save config` | Save configuration |

### Top 10 Switch Commands for WLC Deployment

| Command | Purpose |
|---------|---------|
| `show vlan brief` | Verify VLANs |
| `show interfaces trunk` | Verify trunk to WLC |
| `show power inline` | Check PoE status for APs |
| `show ip dhcp binding` | See DHCP leases (APs and clients) |
| `show run | section dhcp` | Verify DHCP config (Option 43!) |
| `show ip arp` | Verify IP-to-MAC mappings |
| `ping <WLC-IP>` | Test reachability to WLC |
| `show mac address-table` | Verify AP MACs learned |
| `show spanning-tree interface <int>` | Check STP status on AP ports |
| `debug ip dhcp server events` | Troubleshoot DHCP issues |

---

## 🎯 Exam Tips

**Command Focus for CCNA:**
- You won't be asked to configure WLCs via CLI in the exam
- Focus on **verification commands** (`show` commands)
- Understand **switch configuration** for AP connectivity (access ports, PoE, DHCP Option 43)
- Know **DHCP Option 43** is used to tell APs the WLC IP address
- Remember **CAPWAP uses UDP ports 5246 (control) and 5247 (data)**

**Common Exam Scenarios:**
- Given output from `show ap summary`, identify AP status
- Troubleshoot why APs aren't joining (missing Option 43, wrong VLAN)
- Identify correct switch port configuration for lightweight AP (access port, not trunk)
- Explain why WLC needs trunk port (multiple VLANs for dynamic interfaces)

---

**End of Commands Reference - Topic 1.1.e Controllers**