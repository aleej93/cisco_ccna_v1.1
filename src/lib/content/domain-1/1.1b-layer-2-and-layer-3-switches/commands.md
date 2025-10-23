# Commands: 1.1b Layer 2 and Layer 3 Switches — CCNA v1.1

## 🎯 Overview

While this topic (1.1b) focuses on understanding the **role and function** of switches, you'll need to know basic switch CLI navigation for the CCNA exam. This reference covers the **Cisco IOS CLI hierarchy** and fundamental commands.

---

## 📊 Cisco IOS CLI Hierarchy

```
┌─────────────────────────────────────────────────────────────┐
│                    USER EXEC MODE                            │
│  Prompt: Switch>                                             │
│  Access: Basic monitoring commands only                      │
│  Commands: show, ping, traceroute (limited)                  │
└─────────────────────────────────────────────────────────────┘
                            ↓ enable
                            ↑ disable / exit
┌─────────────────────────────────────────────────────────────┐
│                  PRIVILEGED EXEC MODE                        │
│  Prompt: Switch#                                             │
│  Access: All show commands, debugging, file management       │
│  Commands: show (all), debug, copy, reload, etc.             │
└─────────────────────────────────────────────────────────────┘
                   ↓ configure terminal
                   ↑ exit / end / Ctrl+Z
┌─────────────────────────────────────────────────────────────┐
│                GLOBAL CONFIGURATION MODE                     │
│  Prompt: Switch(config)#                                     │
│  Access: Configure device-wide settings                      │
│  Commands: hostname, ip, vlan, interface, line, etc.         │
└─────────────────────────────────────────────────────────────┘
         ↓                    ↓                    ↓
         ↓                    ↓                    ↓
┌────────────────┐  ┌────────────────┐  ┌──────────────────┐
│ INTERFACE      │  │  LINE          │  │  VLAN            │
│ CONFIG MODE    │  │  CONFIG MODE   │  │  CONFIG MODE     │
├────────────────┤  ├────────────────┤  ├──────────────────┤
│ Switch(config- │  │ Switch(config- │  │ Switch(config-   │
│ if)#           │  │ line)#         │  │ vlan)#           │
├────────────────┤  ├────────────────┤  ├──────────────────┤
│ Configure      │  │ Configure      │  │ Configure        │
│ specific       │  │ console/VTY/   │  │ VLAN settings    │
│ interface      │  │ AUX lines      │  │                  │
└────────────────┘  └────────────────┘  └──────────────────┘
         ↑                    ↑                    ↑
         └────────────────────┴────────────────────┘
                      exit (goes up one level)
                      end or Ctrl+Z (returns to #)
```

---

## 🔑 CLI Mode Summary Table

| Mode                 | Prompt                 | Access Command              | Purpose                      | Exit Command        |
| -------------------- | ---------------------- | --------------------------- | ---------------------------- | ------------------- |
| **User EXEC**        | `Switch>`              | (initial login)             | Basic monitoring             | `exit` (logout)     |
| **Privileged EXEC**  | `Switch#`              | `enable`                    | Full monitoring & management | `disable` or `exit` |
| **Global Config**    | `Switch(config)#`      | `configure terminal`        | Device-wide configuration    | `exit` or `end`     |
| **Interface Config** | `Switch(config-if)#`   | `interface <type> <number>` | Configure specific interface | `exit`              |
| **Line Config**      | `Switch(config-line)#` | `line <type> <number>`      | Configure console/VTY access | `exit`              |
| **VLAN Config**      | `Switch(config-vlan)#` | `vlan <number>`             | Configure VLAN settings      | `exit`              |

---

## ⚙️ Basic Switch Commands

### Accessing the Switch

#### Console Cable Connection

```
(Physical connection via console cable)
Press Enter to access the CLI
```

#### Entering Privileged EXEC Mode

```cisco-ios
Switch> enable
Switch#
```

**Explanation:**

- The `enable` command moves you from User EXEC mode to Privileged EXEC mode
- You may be prompted for a password if one is configured

---

### Viewing Switch Information

#### Show Device Information

```cisco-ios
Switch# show version
```

**Explanation:**

- Displays IOS version, uptime, hardware information, and configuration register
- Useful for verifying switch model and software version

#### Show Running Configuration

```cisco-ios
Switch# show running-config
```

**Explanation:**

- Displays the current active configuration (in RAM)
- Shows all configured settings on the switch

#### Show Interface Status

```cisco-ios
Switch# show interfaces status
```

**Explanation:**

- Shows a summary of all interfaces: status, VLAN, duplex, speed, type
- Quickly see which ports are up/down and their configuration

#### Show Specific Interface

```cisco-ios
Switch# show interfaces gigabitethernet 0/1
```

**Explanation:**

- Displays detailed information about a specific interface
- Replace `gigabitethernet 0/1` with your interface name

#### Show MAC Address Table

```cisco-ios
Switch# show mac address-table
```

**Explanation:**

- Displays the switch's MAC address table
- Shows which MAC addresses are learned on which ports

---

### Basic Switch Configuration

#### Enter Global Configuration Mode

```cisco-ios
Switch# configure terminal
Switch(config)#
```

**Explanation:**

- Enters Global Configuration mode from Privileged EXEC mode
- Shortcut: `conf t`

#### Set Hostname

```cisco-ios
Switch(config)# hostname SW1
SW1(config)#
```

**Explanation:**

- Changes the switch hostname (appears in the prompt)
- Helps identify the device in the network

#### Configure Interface

```cisco-ios
SW1(config)# interface gigabitethernet 0/1
SW1(config-if)#
```

**Explanation:**

- Enters interface configuration mode for GigabitEthernet 0/1
- Shortcut: `int gi0/1`

#### Enable an Interface

```cisco-ios
SW1(config-if)# no shutdown
```

**Explanation:**

- Administratively enables the interface (brings it up)
- Interfaces are shut down by default on some models
- Shortcut: `no shut`

#### Set Interface Description

```cisco-ios
SW1(config-if)# description Connected to PC1
```

**Explanation:**

- Adds a description to the interface
- Helpful for documentation and troubleshooting

#### Assign Interface to VLAN (Layer 2)

```cisco-ios
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
```

**Explanation:**

- Configures the interface as an access port
- Assigns the port to VLAN 10
- Covered in detail in Domain 2.0

---

### Saving Configuration

#### Save Running Config to Startup Config

```cisco-ios
SW1# copy running-config startup-config
```

**Explanation:**

- Saves the current configuration to NVRAM
- Configuration persists after reboot
- Shortcut: `copy run start` or `write memory` / `wr`

---

### Layer 3 Switch Configuration

#### Enable IP Routing (Layer 3 Switch Only)

```cisco-ios
SW1(config)# ip routing
```

**Explanation:**

- Enables routing functionality on a Layer 3 switch
- Required for inter-VLAN routing
- Only available on Layer 3 switches

#### Create a Switched Virtual Interface (SVI)

```cisco-ios
SW1(config)# interface vlan 10
SW1(config-if)# ip address 192.168.10.1 255.255.255.0
SW1(config-if)# no shutdown
```

**Explanation:**

- Creates a virtual interface for VLAN 10
- Assigns an IP address for Layer 3 routing
- Used as the default gateway for hosts in VLAN 10

#### Configure Routed Port (Layer 3 Switch Only)

```cisco-ios
SW1(config)# interface gigabitethernet 0/1
SW1(config-if)# no switchport
SW1(config-if)# ip address 10.1.1.1 255.255.255.0
SW1(config-if)# no shutdown
```

**Explanation:**

- Converts a switch port to a routed port (Layer 3 interface)
- `no switchport` disables Layer 2 switching on the port
- Behaves like a router interface

---

## 🔍 Verification Commands

### Check Interface Status

```cisco-ios
SW1# show ip interface brief
```

**Explanation:**

- Shows a summary of all interfaces with IP addresses and status
- Quick way to verify Layer 3 configuration

### Verify VLAN Configuration

```cisco-ios
SW1# show vlan brief
```

**Explanation:**

- Displays all VLANs and which ports are assigned to them
- Covered in detail in Domain 2.0

### Check Routing Table (Layer 3 Switch)

```cisco-ios
SW1# show ip route
```

**Explanation:**

- Displays the routing table (Layer 3 switches only)
- Shows all known networks and how to reach them

---

## 🎓 CLI Navigation Tips

### Quick Shortcuts

- **Tab:** Auto-complete commands
- **?:** Context-sensitive help
- **Ctrl+Z or `end`:** Return to Privileged EXEC mode from any config mode
- **Up Arrow:** Recall previous command
- **Ctrl+A:** Move cursor to beginning of line
- **Ctrl+E:** Move cursor to end of line

### Getting Help

```cisco-ios
Switch# show ?
```

**Explanation:**

- Lists all available options for the `show` command

```cisco-ios
Switch# sh?
```

**Explanation:**

- Lists all commands starting with "sh"

---

## 📌 Important Notes for CCNA

1. **For Objective 1.1b:** You need to understand switch roles and functions, not memorize all commands
2. **Configuration commands** are covered extensively in Domain 2.0 (VLANs, trunking, etc.)
3. **Layer 3 switch commands** (IP routing, SVIs) are important for later topics
4. **Focus on understanding the CLI hierarchy** - this is fundamental for all Cisco devices

---

## 🔗 Related Topics

- **Domain 2.0:** VLAN configuration, trunking, EtherChannel, STP
- **Domain 3.0:** Routing configuration on Layer 3 switches
- **Domain 4.0:** DHCP relay on Layer 3 switches
- **Domain 5.0:** Port security, DHCP snooping, DAI on switches

---

## ✅ Key Takeaways

- **User EXEC mode (>):** Basic monitoring only
- **Privileged EXEC mode (#):** Full monitoring and management
- **Global Config mode (config)#:** Device-wide configuration
- **Sub-config modes (config-if)#, etc.:** Specific configuration contexts
- **Always save your config!** Use `copy run start`
- **Layer 3 switches** can route between VLANs using SVIs or routed ports

---

**Remember:** This is a CLI reference to support your understanding of switches. The CCNA exam focuses on conceptual knowledge for this objective. Detailed switch configuration is covered in Domain 2.0 and beyond!
