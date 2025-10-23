# Real-World Scenarios: 1.1.e Controllers

**Exam Objective:** *Domain 1.1.e — Explain the role and function of network components: Controllers*

---

## 🌐 Overview

This document presents realistic scenarios where Wireless LAN Controllers (WLCs) are deployed in various environments. Each scenario includes business requirements, technical solutions, cost considerations, and lessons learned.

---

## 📊 Scenario 1: Small Retail Store (50 Employees)

### Business Requirements

**Company:** Fashion retail store with one location  
**Size:** 5,000 sq ft retail floor  
**Users:** 50 employees + 100-200 daily customers  
**Budget:** Limited (~$15,000 for wireless)  
**IT Staff:** No dedicated IT staff, managed by outsourced MSP

**Wireless Needs:**
- Employee devices (tablets, mobile POS systems)
- Guest WiFi for customers
- Security cameras (IP-based)
- Digital signage displays

---

### Technical Solution

**Deployment Model:** Cisco Mobility Express

**Hardware:**
- **6x Cisco Catalyst 9120 APs** (indoor, dual-band)
- **1x Cisco Catalyst 1000 switch** (24-port, PoE+)
- One AP designated as "master" running WLC software

**Why Mobility Express?**
- ✅ No separate WLC hardware needed (saves ~$5,000)
- ✅ Supports up to 100 APs (far exceeds need)
- ✅ Simple web-based management
- ✅ Perfect for single-site deployments

**Network Design:**

```
Internet
   |
  ISR
   |
Catalyst 1000 Switch (PoE+)
   |
   |-- AP1 (Master - runs WLC) [Access Port, VLAN 10]
   |-- AP2 [Access Port, VLAN 10]
   |-- AP3 [Access Port, VLAN 10]
   |-- AP4 [Access Port, VLAN 10]
   |-- AP5 [Access Port, VLAN 10]
   |-- AP6 [Access Port, VLAN 10]

VLANs:
- VLAN 10: Management (192.168.10.0/24) - APs
- VLAN 100: Employee (10.10.100.0/24) - Employee WiFi
- VLAN 200: Guest (10.10.200.0/24) - Customer WiFi
```

**WLANs Configured:**
1. **"EmployeeNet"** - WPA2-Enterprise with RADIUS (for employees)
2. **"GuestWiFi"** - WPA2-PSK with daily password rotation (for customers)
3. **"Cameras"** - WPA2-PSK (for security cameras, hidden SSID)

---

### Cost Breakdown

| Item | Quantity | Unit Price | Total |
|------|----------|------------|-------|
| Cisco Catalyst 9120 APs | 6 | $800 | $4,800 |
| Cisco Catalyst 1000-24P Switch | 1 | $1,500 | $1,500 |
| CAT6A Cabling (per drop) | 6 | $150 | $900 |
| Installation Labor | - | - | $3,000 |
| **Total** | | | **$10,200** |

**Annual Costs:**
- Cisco DNA Essentials (management): $1,200/year
- Internet bandwidth upgrade: $600/year
- **Total Annual:** $1,800/year

---

### Implementation Timeline

**Week 1:** Site survey, cable routing planning  
**Week 2:** Cable installation, switch mounting  
**Week 3:** AP installation, initial configuration  
**Week 4:** Testing, security hardening, employee training

**Total Time:** 4 weeks

---

### Outcome

**Results After 6 Months:**
- ✅ 100% wireless coverage across retail floor
- ✅ Average 50 concurrent clients during business hours
- ✅ Guest WiFi used by 80% of customers (increased dwell time)
- ✅ Zero downtime due to wireless issues
- ✅ POS transactions 30% faster with mobile devices

**Lessons Learned:**
- Mobility Express worked perfectly for single location
- Outsourced MSP could manage via cloud with no on-site visits
- Guest portal increased customer engagement (email collection)
- Hidden SSID for cameras reduced unauthorized device attempts

---

## 🏢 Scenario 2: Mid-Size Office Building (300 Employees)

### Business Requirements

**Company:** Marketing agency, 3-floor office building  
**Size:** 30,000 sq ft total  
**Users:** 300 employees + 20-30 daily visitors  
**Budget:** Moderate (~$75,000 for wireless)  
**IT Staff:** 2-person IT team (generalists)

**Wireless Needs:**
- Employee laptops and smartphones
- Conference room wireless (high density)
- Guest WiFi (isolated from corporate)
- IoT devices (printers, smart displays)
- High availability (SLA requirement)

---

### Technical Solution

**Deployment Model:** Unified WLC (Dedicated Appliance)

**Hardware:**
- **40x Cisco Catalyst 9130 APs** (high density, Wi-Fi 6)
- **2x Cisco 9800-40 WLCs** (high availability, up to 2000 APs each)
- **2x Cisco Catalyst 9300 switches** (distribution layer, PoE+, stacking)

**Why Unified WLC?**
- ✅ High availability with redundant WLCs (N+1 architecture)
- ✅ Supports 2000 APs per WLC (room for growth)
- ✅ Advanced features (rogue AP detection, CleanAir)
- ✅ Better performance for 300+ concurrent clients

**Network Design:**

```
Internet
   |
Firewall (ASA)
   |
   |-------- Core Switch (Catalyst 9300) --------
   |                    |                         |
WLC-1 (Primary)    WLC-2 (Standby)    Distribution Switches
[Trunk Port]       [Trunk Port]              |
                                     Access Layer Switches
                                              |
                                         40x APs
                                     [Access Ports]

VLANs:
- VLAN 10: Management (192.168.10.0/24)
- VLAN 100: Corporate (10.100.0.0/16)
- VLAN 200: Guest (10.200.0.0/24)
- VLAN 300: IoT (10.300.0.0/24)
```

**WLANs Configured:**
1. **"CorpWiFi"** - WPA2-Enterprise (802.1X with RADIUS)
2. **"GuestNet"** - Web authentication (captive portal)
3. **"IoT-Devices"** - WPA2-PSK (hidden SSID, MAC filtering)

**High Availability:**
- WLC-1 and WLC-2 configured in **SSO (Stateful Switchover)**
- APs join both WLCs (primary and secondary)
- If WLC-1 fails, APs automatically switch to WLC-2
- Client sessions maintained during failover

---

### Cost Breakdown

| Item | Quantity | Unit Price | Total |
|------|----------|------------|-------|
| Cisco Catalyst 9130 APs | 40 | $1,200 | $48,000 |
| Cisco 9800-40 WLCs | 2 | $12,000 | $24,000 |
| Cisco Catalyst 9300 Switches | 2 | $8,000 | $16,000 |
| Cabling & Patch Panels | - | - | $10,000 |
| Installation & Configuration | - | - | $15,000 |
| RADIUS Server (VM) | 1 | $0 (FreeRADIUS) | $0 |
| **Total** | | | **$113,000** |

**Note:** Over budget by $38,000, but justified by:
- HA requirement (prevents downtime)
- Future scalability (can add 1960 more APs)
- Advanced security features

**Annual Costs:**
- Cisco DNA Advantage: $18,000/year
- Support contracts: $8,000/year
- **Total Annual:** $26,000/year

---

### Implementation Timeline

**Month 1:** Design review, hardware procurement  
**Month 2:** Infrastructure prep (cabling, rack space)  
**Month 3:** WLC deployment, AP installation (Floors 1-2)  
**Month 4:** AP installation (Floor 3), testing, cutover  
**Month 5:** Monitoring, optimization, documentation

**Total Time:** 5 months

---

### Outcome

**Results After 1 Year:**
- ✅ 99.95% uptime (only 4 hours downtime in 12 months)
- ✅ Average 350 concurrent clients during peak hours
- ✅ Seamless roaming between floors (VoIP calls maintained)
- ✅ Conference rooms support 50+ clients simultaneously
- ✅ 60% reduction in help desk wireless tickets

**Lessons Learned:**
- HA was critical - WLC-1 failed once due to power supply, WLC-2 took over seamlessly
- Conference room APs needed high-density mode for large meetings
- Guest WiFi captive portal captured 500+ email addresses per month
- RADIUS integration with Active Directory simplified user management
- Dynamic channel assignment eliminated manual RF planning

---

## 🏫 Scenario 3: University Campus (5,000 Students)

### Business Requirements

**Organization:** Mid-size university, 10 buildings  
**Size:** 500,000 sq ft total  
**Users:** 5,000 students + 500 faculty/staff  
**Budget:** Large (~$800,000 for wireless)  
**IT Staff:** 15-person IT department (dedicated wireless team)

**Wireless Needs:**
- Campus-wide WiFi coverage (indoor and outdoor)
- Dormitory wireless (high density, 24/7)
- Classroom wireless (lecture capture, online exams)
- Guest WiFi for visitors and conferences
- Eduroam support (inter-university roaming)
- Extreme high availability (academic calendar-driven)

---

### Technical Solution

**Deployment Model:** Unified WLC (Multi-Controller Cluster)

**Hardware:**
- **500x Cisco Catalyst 9130/9136 APs** (mix of indoor and outdoor)
- **4x Cisco 9800-CL WLCs** (virtual, on UCS servers)
- **Redundant data center** (primary and secondary site)
- **Cisco ISE (Identity Services Engine)** for authentication

**Why Unified WLC Cluster?**
- ✅ Supports 6,000 APs (allows growth)
- ✅ Campus-wide seamless roaming
- ✅ Redundancy across multiple WLCs
- ✅ Centralized management for all buildings

**Network Design:**

```
Internet (10 Gbps fiber)
   |
Border Routers (Redundant)
   |
   |-------- Core Switches (Catalyst 9500) --------
   |                                                |
Primary Data Center                    Secondary Data Center
  - WLC-1 (Virtual)                      - WLC-3 (Virtual)
  - WLC-2 (Virtual)                      - WLC-4 (Virtual)
  - Cisco ISE Primary                    - Cisco ISE Secondary
   |                                                |
   |----------- Distribution Layer Switches -------|
                      |
            Building Access Switches
                      |
                 500x APs
             [Access Ports, PoE+]

VLANs:
- VLAN 10: Management (10.10.0.0/16)
- VLAN 100: Student (10.100.0.0/16)
- VLAN 200: Faculty (10.200.0.0/16)
- VLAN 300: Guest (10.300.0.0/24)
- VLAN 400: Eduroam (10.400.0.0/16)
- VLAN 500: IoT (10.500.0.0/24)
```

**WLANs Configured:**
1. **"UniSecure"** - WPA2-Enterprise (students/faculty, ISE auth)
2. **"UniGuest"** - Web authentication (self-registration portal)
3. **"Eduroam"** - WPA2-Enterprise (inter-university roaming)
4. **"UniIoT"** - WPA2-PSK (IoT devices, hidden SSID)

**Special Features:**
- **Mobility groups** for inter-WLC roaming
- **Fast roaming (802.11r)** for VoIP and video
- **Client load balancing** across 500 APs
- **BandSelect** (prefer 5GHz for capable clients)
- **CleanAir** for RF interference detection

---

### Cost Breakdown

| Item | Quantity | Unit Price | Total |
|------|----------|------------|-------|
| Cisco Catalyst 9130 APs (Indoor) | 400 | $1,200 | $480,000 |
| Cisco Catalyst 9136 APs (Outdoor) | 100 | $1,500 | $150,000 |
| Cisco 9800-CL WLCs (Virtual) | 4 | $25,000 | $100,000 |
| Cisco ISE Appliances | 2 | $35,000 | $70,000 |
| Cisco Catalyst 9500 Core Switches | 4 | $40,000 | $160,000 |
| Distribution/Access Switches | - | - | $250,000 |
| Fiber & Copper Cabling | - | - | $150,000 |
| Installation & Professional Services | - | - | $200,000 |
| **Total** | | | **$1,560,000** |

**Budget Overrun:** $760,000 (justified by critical importance)

**Annual Costs:**
- Cisco DNA Advantage: $200,000/year
- Support contracts: $150,000/year
- ISE licensing: $50,000/year
- **Total Annual:** $400,000/year

---

### Implementation Timeline

**Phase 1 (3 months):** Design, procurement, data center setup  
**Phase 2 (6 months):** Building 1-5 deployment (academic buildings)  
**Phase 3 (4 months):** Building 6-10 deployment (dorms, rec center)  
**Phase 4 (2 months):** Outdoor coverage, optimization  
**Phase 5 (1 month):** Testing, documentation, training

**Total Time:** 16 months (summer break targeted for minimal disruption)

---

### Outcome

**Results After 2 Years:**
- ✅ 99.99% uptime (99.99% SLA met)
- ✅ Average 4,500 concurrent clients during peak (9am-5pm)
- ✅ 8,000+ devices registered via NAC (students average 1.6 devices each)
- ✅ Seamless roaming across entire campus (VoIP, video calls maintained)
- ✅ Eduroam supports 200+ visiting students/faculty per semester
- ✅ 95% reduction in wireless-related help desk tickets

**Key Metrics:**
- **Peak concurrent clients:** 6,200 (during finals week)
- **Average throughput per user:** 15 Mbps
- **Client satisfaction:** 4.7/5 (up from 2.8/5 before upgrade)
- **Network capacity:** 60% utilized (room for 3,000 more clients)

**Lessons Learned:**
- Phased deployment was critical to avoid disrupting classes
- Summer break installations prevented student complaints
- Dorms required high-density APs (80+ clients per AP)
- Outdoor APs needed weatherproofing and lightning protection
- Guest WiFi captive portal required legal terms acceptance
- ISE integration with AD reduced manual account management by 90%
- 802.11r fast roaming was essential for lecture hall transitions
- Client load balancing prevented overcrowding on popular APs

---

## 🏭 Scenario 4: Manufacturing Plant (200 Workers)

### Business Requirements

**Company:** Automotive parts manufacturer  
**Size:** 200,000 sq ft factory floor + 20,000 sq ft offices  
**Users:** 200 workers (factory and office)  
**Budget:** Moderate (~$100,000 for wireless)  
**IT Staff:** 1 network engineer, 2 help desk technicians

**Wireless Needs:**
- Warehouse wireless scanners (inventory management)
- Forklift-mounted tablets
- Office wireless (standard productivity)
- Ruggedized APs (harsh factory environment)
- Real-time location tracking (RTLS)

---

### Technical Solution

**Deployment Model:** Embedded WLC (in Catalyst switches)

**Hardware:**
- **30x Cisco Catalyst 9130 APs** (industrial-rated, IP67 for factory)
- **20x Cisco Catalyst 9120 APs** (standard for offices)
- **2x Cisco Catalyst 9300 switches** (with embedded WLC)
- **RTLS system** (tags for asset tracking)

**Why Embedded WLC?**
- ✅ No separate WLC hardware (saves rack space)
- ✅ WLC functionality built into switches
- ✅ Lower cost than dedicated appliance
- ✅ Sufficient capacity (&lt;200 APs)

**Network Design:**

```
Internet
   |
Firewall
   |
Core Switch (Catalyst 9500)
   |
   |---- Catalyst 9300-1 (Embedded WLC, Factory) ----
   |                    |
   |              30x Industrial APs
   |              [Access Ports, PoE+]
   |
   |---- Catalyst 9300-2 (Embedded WLC, Office) ----
                        |
                  20x Office APs
                  [Access Ports, PoE+]

VLANs:
- VLAN 10: Management (192.168.10.0/24)
- VLAN 100: Factory Devices (10.100.0.0/24)
- VLAN 200: Office WiFi (10.200.0.0/24)
- VLAN 300: RTLS (10.300.0.0/24)
```

**WLANs Configured:**
1. **"FactoryWiFi"** - WPA2-Enterprise (scanners, tablets)
2. **"OfficeWiFi"** - WPA2-Enterprise (employee laptops)
3. **"RTLS"** - Hidden SSID for asset tracking tags

**Special Considerations:**
- Industrial APs rated for -40°F to +185°F
- High power PoE+ (30W per AP)
- RF planning for metal surfaces (high reflectivity)
- Redundant power supplies for critical APs

---

### Cost Breakdown

| Item | Quantity | Unit Price | Total |
|------|----------|------------|-------|
| Cisco Catalyst 9130 APs (Industrial) | 30 | $2,000 | $60,000 |
| Cisco Catalyst 9120 APs (Office) | 20 | $800 | $16,000 |
| Cisco Catalyst 9300 Switches (Embedded WLC) | 2 | $15,000 | $30,000 |
| RTLS System (Tags + Software) | 1 | $20,000 | $20,000 |
| Installation & Mounting (Factory) | - | - | $25,000 |
| **Total** | | | **$151,000** |

**Budget Overrun:** $51,000 (justified by RTLS cost)

**Annual Costs:**
- Cisco DNA Essentials: $12,000/year
- RTLS subscription: $5,000/year
- Support: $8,000/year
- **Total Annual:** $25,000/year

---

### Implementation Timeline

**Month 1:** RF site survey (factory floor challenging)  
**Month 2:** Infrastructure prep (conduit, high mounting)  
**Month 3:** AP installation (factory, nights/weekends)  
**Month 4:** Office AP installation, WLC configuration  
**Month 5:** RTLS integration, testing, training

**Total Time:** 5 months

---

### Outcome

**Results After 1 Year:**
- ✅ 100% factory floor coverage (despite metal surfaces)
- ✅ Inventory accuracy improved from 85% to 98%
- ✅ Forklift efficiency up 20% (real-time tablet updates)
- ✅ RTLS tracked 500+ assets in real-time
- ✅ Zero AP failures (industrial-rated withstood harsh environment)

**Key Metrics:**
- **Concurrent devices:** 150 (100 scanners + 50 laptops)
- **Uptime:** 99.8% (minimal downtime for maintenance)
- **RTLS accuracy:** Within 10 feet (sufficient for warehouse)

**Lessons Learned:**
- RF site survey revealed metal surfaces required more APs than estimated
- High mounting (25 feet) avoided forklift damage
- Industrial APs justified higher cost (standard APs failed in pilot)
- Redundant power to critical APs prevented production delays
- RTLS tags needed battery monitoring system (batteries last ~2 years)

---

## 🏥 Scenario 5: Hospital (500 Beds)

### Business Requirements

**Organization:** Regional hospital, 10-story building  
**Size:** 750,000 sq ft  
**Users:** 1,500 staff + 1,000 patients/visitors  
**Budget:** Large (~$1,200,000 for wireless)  
**IT Staff:** 20-person IT team (dedicated clinical engineering)

**Wireless Needs:**
- Electronic Medical Records (EMR) access
- Medical devices (infusion pumps, monitors)
- VoIP phones for staff
- Patient/visitor WiFi (isolated)
- Real-time location (RTLS) for equipment and patients
- Mission-critical uptime (life safety)

---

### Technical Solution

**Deployment Model:** Unified WLC (N+N+1 Redundancy)

**Hardware:**
- **600x Cisco Catalyst 9130AXI APs** (healthcare-rated, Wi-Fi 6E)
- **6x Cisco 9800-80 WLCs** (ultra-high capacity, geo-redundant)
- **Cisco ISE** for NAC (network access control)
- **Cisco DNA Center** for network automation

**Why N+N+1 WLC Architecture?**
- ✅ Mission-critical uptime requirement
- ✅ 6 WLCs: 2 in primary data center, 2 in secondary, 2 in disaster recovery site
- ✅ Any 2 WLCs can handle full load
- ✅ Geographic redundancy (sites 50 miles apart)

**Network Design:**

```
Internet (Redundant 10G links)
   |
   |-------- Core Network (Redundant) --------
   |                |                          |
Primary DC     Secondary DC           DR Site (50 miles)
WLC-1, WLC-2   WLC-3, WLC-4          WLC-5, WLC-6
Cisco ISE-1    Cisco ISE-2           Cisco ISE-3
   |                |                          |
   |----------- Hospital Floor Switches ------|
                      |
                 600x APs
             [Access Ports, PoE++]

VLANs:
- VLAN 10: Management (10.10.0.0/16)
- VLAN 100: Medical Devices (10.100.0.0/16)
- VLAN 200: Staff WiFi (10.200.0.0/16)
- VLAN 300: VoIP (10.300.0.0/16)
- VLAN 400: Patient/Guest (10.400.0.0/24)
- VLAN 500: RTLS (10.500.0.0/24)
```

**WLANs Configured:**
1. **"HospitalSecure"** - WPA3-Enterprise (staff, EMR access)
2. **"MedicalDevices"** - WPA2-Enterprise (infusion pumps, monitors)
3. **"VoIP"** - WPA2-Enterprise with 802.11r (staff phones)
4. **"PatientWiFi"** - Web authentication (patients/visitors)
5. **"RTLS"** - Hidden SSID for asset/patient tracking

**Special Features:**
- **Fast roaming (802.11r)** for VoIP calls
- **Priority QoS** for medical devices
- **Client exclusion** for misbehaving devices
- **Rogue AP detection** (security requirement)
- **Spectrum analysis (CleanAir)** to avoid RF interference with medical equipment

---

### Cost Breakdown

| Item | Quantity | Unit Price | Total |
|------|----------|------------|-------|
| Cisco Catalyst 9130AXI APs (Wi-Fi 6E) | 600 | $1,800 | $1,080,000 |
| Cisco 9800-80 WLCs | 6 | $35,000 | $210,000 |
| Cisco ISE Appliances | 3 | $35,000 | $105,000 |
| Cisco DNA Center | 1 | $50,000 | $50,000 |
| Core/Distribution/Access Switches | - | - | $500,000 |
| Fiber Infrastructure | - | - | $200,000 |
| Installation & Professional Services | - | - | $400,000 |
| **Total** | | | **$2,545,000** |

**Budget Overrun:** $1,345,000 (approved due to life-safety criticality)

**Annual Costs:**
- Cisco DNA Advantage: $300,000/year
- Support contracts: $200,000/year
- ISE licensing: $75,000/year
- **Total Annual:** $575,000/year

---

### Implementation Timeline

**Phase 1 (6 months):** Design, regulatory approval, procurement  
**Phase 2 (12 months):** Floors 1-5 deployment (careful patient care coordination)  
**Phase 3 (10 months):** Floors 6-10 deployment  
**Phase 4 (2 months):** Outdoor/parking areas, redundancy testing  
**Phase 5 (2 months):** Go-live, staff training, optimization

**Total Time:** 32 months (longest due to strict regulatory requirements)

---

### Outcome

**Results After 3 Years:**
- ✅ 99.999% uptime (only 5 minutes downtime in 3 years, planned)
- ✅ 2,500 concurrent devices during peak hours
- ✅ EMR system access 3 seconds faster on average
- ✅ VoIP calls maintain quality during roaming (no dropped calls)
- ✅ RTLS tracks 5,000+ assets and 1,000+ patients
- ✅ Zero medical device RF interference incidents
- ✅ Patient satisfaction with WiFi: 4.8/5

**Key Metrics:**
- **Concurrent clients:** 3,200 (peak during visiting hours)
- **Medical devices:** 800 (infusion pumps, monitors, etc.)
- **VoIP phones:** 400 (staff communication)
- **Uptime:** 99.999% (5-nines)

**Lessons Learned:**
- Redundancy investment was justified - WLC failures occurred twice, seamless failover
- Healthcare-rated APs required for antimicrobial coating and cleanability
- RF survey in hospital was challenging due to medical equipment EMI
- 802.11r fast roaming was essential for VoIP (doctors on the move)
- Patient WiFi required bandwidth shaping to prevent network saturation
- RTLS accuracy within 3 feet met clinical requirements
- ISE integration with hospital AD simplified credentialing for staff
- Rogue AP detection caught 15+ unauthorized APs in 3 years

---

## 📈 Comparative Analysis

### Cost Per User by Deployment Type

| Deployment | Users | Total Cost | Cost Per User |
|------------|-------|------------|---------------|
| **Retail (Mobility Express)** | 50 | $10,200 | $204 |
| **Office (Unified WLC)** | 300 | $113,000 | $377 |
| **University (Unified Cluster)** | 5,500 | $1,560,000 | $284 |
| **Manufacturing (Embedded WLC)** | 200 | $151,000 | $755 |
| **Hospital (N+N+1 WLC)** | 2,500 | $2,545,000 | $1,018 |

**Key Insights:**
- Mobility Express = lowest cost per user (simple deployment)
- Manufacturing = high cost per user (industrial-rated equipment)
- Hospital = highest cost per user (mission-critical uptime)
- University = best scalability (most users for lowest per-user cost)

---

### Deployment Model Selection Guide

| Factor | Mobility Express | Embedded WLC | Unified WLC | Cloud-Based |
|--------|------------------|--------------|-------------|-------------|
| **Max APs** | &lt;100 | &lt;200 | 6,000+ | Unlimited |
| **Cost** | $ | $$ | $$$$ | $$$ (subscription) |
| **Complexity** | Low | Medium | High | Low |
| **Best For** | Small sites | Branch offices | Large campus | Multi-site |
| **Redundancy** | Low | Medium | High | High |
| **Management** | GUI | GUI | GUI/CLI | Cloud Portal |

---

## 🔧 Common Troubleshooting Scenarios

### Issue 1: APs Not Joining WLC

**Symptoms:**
- APs stuck in "Discovering" state
- APs reboot continuously

**Common Causes:**
1. ❌ Missing DHCP Option 43
2. ❌ No IP connectivity between AP and WLC
3. ❌ Firewall blocking CAPWAP ports (UDP 5246/5247)
4. ❌ AP and WLC software version mismatch

**Resolution Steps:**
1. Verify AP has IP address: `show ip dhcp binding`
2. Check DHCP Option 43: `show run | include option 43`
3. Test connectivity: `ping <WLC-IP> source vlan <mgmt-vlan>`
4. Check WLC logs: `show ap join stats summary all`
5. Verify firewall permits UDP 5246/5247

---

### Issue 2: Poor Wireless Performance

**Symptoms:**
- Slow client speeds
- Frequent disconnections
- High latency

**Common Causes:**
1. ❌ Channel interference (co-channel or adjacent-channel)
2. ❌ Overloaded AP (too many clients)
3. ❌ Weak signal strength (RSSI &lt; -75 dBm)
4. ❌ Incorrect QoS settings

**Resolution Steps:**
1. Check channel utilization: `show ap auto-rf 802.11a summary`
2. Review client distribution: `show ap summary` (check Clients column)
3. Verify client RSSI: `show client detail <MAC>` (should be &gt; -70 dBm)
4. Enable load balancing: WLC &gt; Wireless &gt; 802.11a/b &gt; Load Balancing

---

### Issue 3: Clients Cannot Obtain IP Addresses

**Symptoms:**
- Clients associate but no Internet access
- Limited connectivity messages
- Self-assigned IPs (169.254.x.x)

**Common Causes:**
1. ❌ DHCP server unreachable
2. ❌ DHCP pool exhausted
3. ❌ Incorrect VLAN mapping (WLAN to dynamic interface)

**Resolution Steps:**
1. Check DHCP pool: `show ip dhcp pool <pool-name>`
2. Verify DHCP bindings: `show ip dhcp binding`
3. Test DHCP from WLC virtual interface: `test dhcp vlan <client-vlan>`
4. Verify WLAN-to-VLAN mapping: `show wlan <ID>` (check Interface/Interface Group)

---

## 🎓 Career Application

### Wireless Engineer Role

**Skills Needed:**
- WLC deployment and configuration
- RF planning and site surveys
- Troubleshooting CAPWAP issues
- Security policy implementation (WPA2/WPA3, 802.1X)

**Typical Tasks:**
- Design wireless networks for various environments
- Configure WLCs and lightweight APs
- Optimize RF coverage and capacity
- Integrate with AAA servers (ISE, RADIUS)
- Monitor and troubleshoot wireless performance

**Career Path:**
1. Network Engineer → Wireless Engineer → Senior Wireless Architect
2. Certifications: CCNA Wireless → CCNP Enterprise (wireless focus) → CCIE Wireless

---

### Network Operations Center (NOC) Analyst

**WLC-Related Tasks:**
- Monitor WLC health and AP status
- Respond to alerts (AP down, high client density)
- Perform basic troubleshooting (AP not joining, clients can't connect)
- Escalate complex issues to wireless team

**Key Metrics to Monitor:**
- WLC CPU and memory utilization
- Number of joined APs
- Client count per AP
- Failed authentication attempts

---

## 🏁 Summary

**Key Takeaways:**

1. **Deployment Model Selection is Critical**
   - Mobility Express: &lt;100 APs, single site
   - Embedded WLC: &lt;200 APs, branch offices
   - Unified WLC: Large campus, high capacity
   - Cloud-based: Multi-site, simplified management

2. **Cost Considerations**
   - Hardware cost is only 40-60% of total
   - Installation and professional services add significant cost
   - Annual licensing can exceed initial hardware cost over 5 years

3. **Redundancy Requirements Vary**
   - Retail: Limited redundancy acceptable
   - Enterprise: N+1 redundancy recommended
   - Mission-critical: N+N+1 or higher

4. **Real-World Challenges**
   - RF planning in challenging environments (metal, concrete)
   - Integration with existing systems (AD, ISE, RADIUS)
   - User expectations for seamless roaming
   - Security and compliance requirements

---

**End of Real-World Scenarios - Topic 1.1.e Controllers**