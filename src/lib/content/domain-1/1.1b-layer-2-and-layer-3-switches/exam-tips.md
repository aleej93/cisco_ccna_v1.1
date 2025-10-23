# Exam Tips: 1.1b Layer 2 and Layer 3 Switches — CCNA v1.1

## 🎯 What the Exam Expects You to Know

For objective **1.1b**, the exam focuses on your understanding of the **role and function** of switches in a network. You need to know:

1. What switches do (connect hosts within a LAN)
2. Key characteristics (many ports, LAN-only connectivity)
3. The difference between Layer 2 and Layer 3 switches
4. When to use a switch vs. a router

---

## 🔥 Common Exam Question Patterns

### Pattern 1: Device Selection Questions

**"Which device should be used to connect 30 computers in an office?"**

✅ **Answer: Switch** - Switches have many ports for connecting hosts in the same LAN

❌ **Not a Router** - Routers connect different networks, not individual hosts

---

### Pattern 2: Switch vs. Router

**"What is the primary difference between a switch and a router?"**

✅ **Switch:** Connects hosts **within** the same LAN  
✅ **Router:** Connects **different** LANs together

**Remember:** Switches have many ports (24+), routers have fewer ports

---

### Pattern 3: Layer 2 vs. Layer 3 Switches

**"What additional capability does a Layer 3 switch have compared to a Layer 2 switch?"**

✅ **Layer 3 switches can perform routing functions**

- Layer 2 = MAC addresses only
- Layer 3 = MAC addresses + IP addresses (routing)

---

### Pattern 4: True/False Statements

**"Which statement about switches is FALSE?"**

Watch for these common **FALSE statements:**

- ❌ "Switches can connect different LANs together" (that's a router)
- ❌ "Switches send data over the Internet" (that's a router)
- ❌ "Switches have fewer ports than routers" (opposite is true)

---

## 💡 Quick Memory Tricks

### The "S" Rule

**Switch = Same**

- Switches connect devices in the **Same** LAN
- **S**ame network, **S**witch

### The "R" Rule

**Router = Remote**

- Routers connect **Remote** networks
- **R**emote networks, **R**outer

### Port Count Rule

- **Switches:** Many ports (think 24-48)
- **Routers:** Few ports (think 2-8)

---

## ⚠️ Common Mistakes to Avoid

### Mistake #1: Confusing Switch and Router Functions

❌ **Wrong:** "Use a switch to connect two offices in different cities"  
✅ **Correct:** "Use a router to connect different LANs"

**Tip:** If the question mentions "different networks" or "Internet," think **router**, not switch.

---

### Mistake #2: Forgetting Layer 3 Switch Capabilities

❌ **Wrong:** "Only routers can make routing decisions"  
✅ **Correct:** "Layer 3 switches can also perform routing"

**Tip:** Layer 3 switches = "multilayer switches" = switching + routing

---

### Mistake #3: Thinking All Switches Are the Same

❌ **Wrong:** "All switches only use MAC addresses"  
✅ **Correct:** "Layer 2 switches use MAC addresses; Layer 3 switches can use IP addresses too"

---

## 🧠 Key Exam Vocabulary

| Term            | Definition         | Exam Tip                   |
| --------------- | ------------------ | -------------------------- |
| **LAN**         | Local Area Network | Switches work within a LAN |
| **Layer 2**     | Data Link Layer    | Uses MAC addresses         |
| **Layer 3**     | Network Layer      | Uses IP addresses, routing |
| **MAC Address** | Hardware address   | Layer 2 switching          |
| **IP Address**  | Network address    | Layer 3 routing            |

---

## 📊 Comparison Table (Memorize This!)

| Feature            | Layer 2 Switch | Layer 3 Switch     | Router             |
| ------------------ | -------------- | ------------------ | ------------------ |
| **OSI Layer**      | Layer 2        | Layer 2 & 3        | Layer 3            |
| **Forwards using** | MAC addresses  | MAC + IP addresses | IP addresses       |
| **Can route?**     | No             | Yes                | Yes                |
| **Typical ports**  | 24-48          | 24-48              | 2-8                |
| **Connects**       | Same LAN       | Same LAN + routing | Different networks |

---

## 🎓 Sample Exam Scenarios

### Scenario 1

**"A company wants to connect 40 computers in their main office. What device should they purchase?"**

**Answer:** A switch (has many ports for LAN connectivity)

---

### Scenario 2

**"A network engineer needs to connect the New York office LAN to the Tokyo office LAN over the Internet. What device is required?"**

**Answer:** A router (connects different LANs)

---

### Scenario 3

**"Which device operates at Layer 2 and uses MAC addresses to forward traffic?"**

**Answer:** A Layer 2 switch

---

### Scenario 4

**"A device needs to perform both switching within a LAN and routing between VLANs. What type of device is this?"**

**Answer:** A Layer 3 switch (multilayer switch)

---

## ✅ Pre-Exam Checklist

Before your exam, make sure you can answer these questions confidently:

- [ ] What is the primary function of a switch?
- [ ] How many ports do switches typically have?
- [ ] What's the difference between Layer 2 and Layer 3 switches?
- [ ] What OSI layer does each type of switch operate at?
- [ ] When would you use a switch vs. a router?
- [ ] What addresses do Layer 2 switches use?
- [ ] What addresses do Layer 3 switches use?
- [ ] Can switches connect different LANs? (No!)
- [ ] Can switches send data over the Internet? (No!)

---

## 🔑 Final Exam Tips

1. **Read carefully:** If a question mentions "different networks" or "Internet," it's asking about routers, not switches

2. **Know the layers:** Layer 2 = MAC addresses, Layer 3 = IP addresses (routing)

3. **Port count matters:** Many ports = switch, few ports = router

4. **Function over features:** Focus on WHAT the device does, not brand names or speeds

5. **Process of elimination:** If unsure, eliminate obviously wrong answers (e.g., "firewall" when asked about connecting hosts)

---

**Remember:** This topic is foundational. Switches are covered in much more detail in Domain 2.0 (VLANs, trunking, STP). For now, focus on understanding their **role and function** in the network.
