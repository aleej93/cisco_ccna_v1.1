# CCNA 200-301 v1.1 | Domain 1.0: Network Fundamentals

## Topic 1.1.d Access Points - Commands Reference

---

## 📌 IMPORTANT NOTE

Access Points are typically managed through a **Wireless LAN Controller (WLC)** GUI or via the WLC CLI. Individual AP configuration is uncommon in lightweight architectures. However, you should understand verification commands and basic concepts.

For the CCNA exam, **focus on understanding concepts** rather than memorizing AP-specific commands, as the exam emphasizes controller-based management.

---

## 🖥️ WIRELESS LAN CONTROLLER (WLC) - Web GUI

Most AP configuration is done through the WLC web interface. Key navigation paths:

### Access Point Configuration

```
WLC GUI Path:
WIRELESS → Access Points → All APs
- View all registered APs
- See AP name, MAC, IP, status, clients, mode
```

### Configure AP Mode

```
WLC GUI Path:
WIRELESS → Access Points → All APs → [Select AP] → General
- AP Mode dropdown: Local, FlexConnect, Monitor, Sniffer, etc.
- Apply changes
```

### View CAPWAP Status

```
WLC GUI Path:
WIRELESS → Access Points → All APs
- Look for "Status" column showing:
  - Registered (AP successfully joined WLC)
  - Not Joined (AP cannot reach WLC)
```

---

## 🖥️ WLC CLI COMMANDS (Lightweight AP Management)

### Show All Access Points

```cisco-wlc
(Cisco Controller) > show ap summary

AP Name              Slots  AP Model         Ethernet MAC    Location
-------------------- ------ ---------------- --------------- ----------------
AP01                 2      AIR-CAP3702I-A-K 00:1A:2B:3C:4D:5E Building-A
AP02                 2      AIR-CAP2702I-A-K 00:1A:2B:3C:4D:5F Building-B
AP03                 2      AIR-CAP3702I-A-K 00:1A:2B:3C:4D:60 Building-C
```

**What this shows:**

- All APs registered with the WLC
- AP names, MAC addresses, model numbers
- Location information (if configured)

---

### Show Specific AP Details

```cisco-wlc
(Cisco Controller) > show ap config general AP01

Cisco AP Identifier.............................. 1
Cisco AP Name.................................... AP01
AP Mode.......................................... Local
...
Primary Cisco Switch Name........................ WLC-Primary
Primary Cisco Switch IP Address.................. 10.1.1.10
Secondary Cisco Switch Name...................... WLC-Secondary
Secondary Cisco Switch IP Address................ 10.1.1.11
...
AP Up Time....................................... 5 days, 3 hrs, 22 mins
```

**What this shows:**

- Current AP mode (Local, FlexConnect, Monitor, etc.)
- Which WLC the AP is registered to
- Uptime and status information

---

### Show AP Join Statistics (CAPWAP Troubleshooting)

```cisco-wlc
(Cisco Controller) > show ap join stats summary all

AP Name: AP01
  Number of CAPWAP Discovery Request Messages... 3
  Number of CAPWAP Join Request Messages........ 2
  Number of CAPWAP Join Response Success........ 1
  ...
  Join Error History:
    Join Timestamp............................... May 12 10:45:32
    Join Priority................................ 1
    Join Result.................................. Success
```

**What this shows:**

- CAPWAP discovery and join process
- Troubleshooting failed AP registrations
- Historical join attempts

---

### Change AP Mode

```cisco-wlc
(Cisco Controller) > config ap mode local AP01
```

**What this does:**

- Changes AP01 to Local mode (default mode providing BSS for clients)

**Other mode options:**

```cisco-wlc
config ap mode flexconnect AP01    # FlexConnect mode
config ap mode monitor AP01         # Monitor mode (rogue detection)
config ap mode sniffer AP01         # Sniffer mode (packet capture)
config ap mode bridge AP01          # Bridge/Mesh mode
config ap mode rogue-detector AP01  # Rogue Detector mode
config ap mode se-connect AP01      # Spectrum Expert mode
```

---

### Show CAPWAP Tunnel Status

```cisco-wlc
(Cisco Controller) > show capwap client rcb

CAPWAP Client RCB Table:
Entry for AP: AP01
State: RUN
...
CAPWAP Control Tunnel:
  Source IP: 192.168.10.50 (AP)
  Destination IP: 10.1.1.10 (WLC)
  Source Port: 45812
  Destination Port: 5246

CAPWAP Data Tunnel:
  Source IP: 192.168.10.50 (AP)
  Destination IP: 10.1.1.10 (WLC)
  Source Port: 45813
  Destination Port: 5247
```

**What this shows:**

- CAPWAP Control tunnel (UDP 5246) status
- CAPWAP Data tunnel (UDP 5247) status
- Verifies AP-to-WLC communication

---

### Show Client Summary per AP

```cisco-wlc
(Cisco Controller) > show client summary

MAC Address       AP Name   WLAN  Status
----------------- --------- ----- --------------
aa:bb:cc:dd:ee:01 AP01      10    Associated
aa:bb:cc:dd:ee:02 AP01      20    Associated
aa:bb:cc:dd:ee:03 AP02      10    Associated
```

**What this shows:**

- Which clients are connected to which APs
- WLAN/SSID assignments
- Client association status

---

## 🖥️ AUTONOMOUS AP CLI COMMANDS

If working with an autonomous AP (less common in modern deployments):

### Access Autonomous AP CLI

```cisco-ios
# Via Console Cable:
Username: Cisco
Password: Cisco
AP>

# Or via SSH/Telnet:
ssh admin@192.168.1.1
```

---

### Show AP Configuration

```cisco-ios
AP# show running-config

!
hostname AP01
!
interface Dot11Radio0
 ssid CompanyWiFi
 encryption mode ciphers aes-ccm
!
interface GigabitEthernet0
 description Uplink to Switch
!
```

**What this shows:**

- Complete AP configuration
- SSIDs, VLANs, security settings
- Interface configurations

---

### Show Wireless Client Associations

```cisco-ios
AP# show dot11 associations

802.11 Client Stations on Dot11Radio0:

SSID [CompanyWiFi] :

MAC Address    IP address      Device        State
-------------- --------------- ------------- -----
aabb.ccdd.ee01 192.168.10.101 laptop        Assoc
aabb.ccdd.ee02 192.168.10.102 phone         Assoc
```

**What this shows:**

- Clients associated with this autonomous AP
- Client MAC and IP addresses
- Association state

---

### Configure SSID on Autonomous AP

```cisco-ios
AP# configure terminal
AP(config)# dot11 ssid CorpWiFi
AP(config-ssid)# vlan 10
AP(config-ssid)# authentication open
AP(config-ssid)# authentication key-management wpa version 2
AP(config-ssid)# wpa-psk ascii MySecurePassword123
AP(config-ssid)# exit
AP(config)# interface Dot11Radio0
AP(config-if)# ssid CorpWiFi
AP(config-if)# end
AP# write memory
```

**What this does:**

- Creates SSID "CorpWiFi"
- Assigns SSID to VLAN 10
- Configures WPA2-PSK security
- Applies SSID to the radio interface
- Saves configuration

---

## 🖥️ SWITCH COMMANDS (AP Connectivity)

### Verify AP Connected to Switch

```cisco-ios
Switch# show cdp neighbors

Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
AP01             Gig1/0/5          165              T     AIR-CAP37 Gig0
```

**What this shows:**

- AP connected via CDP (Cisco Discovery Protocol)
- Which switch port the AP is on (Gig1/0/5)
- AP model (AIR-CAP3702)

---

### Show PoE Status for AP

```cisco-ios
Switch# show power inline GigabitEthernet1/0/5

Interface Admin  Oper       Power   Device              Class Max
--------- ------ ---------- ------- ------------------- ----- ----
Gi1/0/5   auto   on         15.4    Cisco AP            3     30.0

Interface  Power  Voltage  Current
           (Watts)(Volts)  (Amps)
---------- ------ -------- --------
Gi1/0/5    15.4   53.2     0.290
```

**What this shows:**

- AP is receiving PoE (Power over Ethernet)
- Power draw: 15.4W
- Inline power is functioning correctly

---

### Configure Switch Port for Lightweight AP

```cisco-ios
Switch# configure terminal
Switch(config)# interface GigabitEthernet1/0/5
Switch(config-if)# description Lightweight-AP01
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 100
Switch(config-if)# power inline auto
Switch(config-if)# spanning-tree portfast
Switch(config-if)# end
Switch# write memory
```

**What this does:**

- Configures **access port** (not trunk - lightweight APs use access ports)
- Assigns to VLAN 100 (management VLAN where WLC is reachable)
- Enables PoE to power the AP
- Enables PortFast for faster port activation
- Saves configuration

**Why access port?**  
Lightweight APs tunnel all traffic to the WLC via CAPWAP. They don't need trunk ports because they don't locally switch VLANs.

---

### Configure Switch Port for Autonomous AP

```cisco-ios
Switch# configure terminal
Switch(config)# interface GigabitEthernet1/0/10
Switch(config-if)# description Autonomous-AP02
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,99
Switch(config-if)# power inline auto
Switch(config-if)# spanning-tree portfast trunk
Switch(config-if)# end
Switch# write memory
```

**What this does:**

- Configures **trunk port** (autonomous APs locally bridge VLANs)
- Allows VLANs 10, 20 (SSIDs), and 99 (management)
- Enables PoE
- Enables PortFast for trunk
- Saves configuration

**Why trunk port?**  
Autonomous APs locally switch traffic to different VLANs based on SSID. They need trunk ports to carry multiple VLANs.

---

## 🖥️ TROUBLESHOOTING COMMANDS

### AP Cannot Join WLC - Check Reachability

```cisco-ios
# From switch or router, test connectivity to WLC:
Switch# ping 10.1.1.10

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.1.10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5)
```

**What this checks:**

- Network connectivity between AP and WLC
- If ping fails, check routing, VLANs, firewalls

---

### Check CAPWAP Ports Open (Firewall Troubleshooting)

```bash
# On a Linux/Windows machine, test if CAPWAP ports are reachable:
nmap -p 5246,5247 -sU 10.1.1.10

PORT     STATE         SERVICE
5246/udp open|filtered capwap-control
5247/udp open|filtered capwap-data
```

**What this checks:**

- UDP ports 5246 and 5247 are not blocked by firewall
- Critical for CAPWAP communication

---

### WLC Debug for AP Join Issues

```cisco-wlc
(Cisco Controller) > debug capwap events enable
(Cisco Controller) > debug capwap errors enable

# Watch real-time output as AP attempts to join
# Look for:
#   - Discovery messages
#   - Join requests
#   - Authentication failures
#   - Certificate issues

# To disable debugging:
(Cisco Controller) > debug capwap events disable
(Cisco Controller) > debug capwap errors disable
```

**What this does:**

- Real-time logging of CAPWAP events
- Identifies why APs fail to join WLC

---

## 📋 COMMAND SUMMARY TABLE

| **Task**                                 | **Command**                        | **Device**    |
| ---------------------------------------- | ---------------------------------- | ------------- |
| Show all APs                             | `show ap summary`                  | WLC           |
| Show AP details                          | `show ap config general <AP-name>` | WLC           |
| Change AP mode                           | `config ap mode <mode> <AP-name>`  | WLC           |
| Show CAPWAP tunnels                      | `show capwap client rcb`           | WLC           |
| Show clients per AP                      | `show client summary`              | WLC           |
| Verify AP on switch                      | `show cdp neighbors`               | Switch        |
| Check PoE status                         | `show power inline <interface>`    | Switch        |
| Configure access port for lightweight AP | `switchport mode access`           | Switch        |
| Configure trunk port for autonomous AP   | `switchport mode trunk`            | Switch        |
| Ping WLC from network                    | `ping <WLC-IP>`                    | Switch/Router |

---

## 🎯 KEY EXAM NOTES

1. **Lightweight APs connect to access ports** (not trunks)
2. **Autonomous APs connect to trunk ports**
3. **CAPWAP uses UDP ports 5246 (control) and 5247 (data)**
4. **Control tunnel is encrypted by default**
5. **Data tunnel is NOT encrypted by default**
6. **APs receive power via PoE (802.3af or 802.3at)**
7. **Most configuration is done on WLC, not individual APs**

---

## 🔗 RELATED TOPICS

- **1.1.e Controllers** - Deep dive into WLC configuration
- **1.1.h Power over Ethernet (PoE)** - How APs receive power
- **Wireless Security** - WPA2, WPA3, 802.1X authentication

---

**Last Updated:** Based on CCNA 200-301 v1.1 Official Exam Topics  
**Command Depth:** Exam-focused - Emphasis on verification and troubleshooting
