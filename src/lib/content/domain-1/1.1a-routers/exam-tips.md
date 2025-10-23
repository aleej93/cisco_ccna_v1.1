# 🎯 Exam Tips: Routers

**Quick strategies to ace router questions on the CCNA 200-301 exam.**

---

## 📌 Question Patterns to Expect

### 1️⃣ **Longest Prefix Match Questions**
**Most common router question type on the exam.**

**Example format:**
> *"A router has the following routes in its table. Which interface will be used for a packet destined to 192.168.10.25?"*

**How to answer:**
1. Write out each route and determine if the destination IP falls within that subnet
2. If multiple routes match, choose the one with the **longest prefix** (/27 beats /24, /24 beats /16, etc.)
3. Remember: *More specific = longer prefix = higher number after the /*

**Common trap:** Don't assume administrative distance matters here! Once routes are in the table, **only prefix length matters** for forwarding decisions.

---

### 2️⃣ **Layer Identification Questions**

**Example format:**
> *"At which OSI layer does a router make forwarding decisions?"*

**Quick answer:** Layer 3 (Network Layer)

**Key points:**
- Routers use **IP addresses** (Layer 3)
- Switches use **MAC addresses** (Layer 2)
- Don't confuse Layer 3 switches with regular routers (both operate at Layer 3, but used differently)

---

### 3️⃣ **Broadcast Domain Questions**

**Example format:**
> *"How many broadcast domains are in this topology?"*

**Rule:** Each router interface = new broadcast domain

**Quick tip:** Count router interfaces, not switch ports. Switches don't break up broadcast domains (unless they're VLANs, which you'll learn later).

---

### 4️⃣ **Default Gateway Questions**

**Example format:**
> *"A PC with IP 192.168.1.100/24 wants to reach 8.8.8.8. What device does it send the packet to first?"*

**Answer:** The default gateway (router's IP address on that subnet)

**Watch for:** Questions asking "what happens next" — trace the packet hop by hop.

---

## ⚠️ Common Mistakes to Avoid

### ❌ Mistake #1: Confusing AD with Prefix Length
**Wrong thinking:** "OSPF has AD 110 and RIP has AD 120, so OSPF route always wins."

**Correct thinking:** 
- **AD** is used to decide which routes *enter* the routing table
- **Prefix length** is used to decide which route is *used* after they're in the table

**Exam trap:** They'll give you multiple matching routes from different protocols and ask which one is used. Answer: **Longest prefix match**, not lowest AD.

---

### ❌ Mistake #2: Forgetting to Check if IP is in Range
**Example:** 
- Route: 192.168.1.0/30 (covers .1, .2, .3)
- Destination: 192.168.1.5

**Wrong:** Assume it matches because "192.168.1" is the same

**Correct:** Do the math! 192.168.1.5 is **NOT** in the /30 range, so this route doesn't match at all.

**Exam tip:** If you're not sure, quickly calculate: /30 = 4 addresses total (network, 2 hosts, broadcast)

---

### ❌ Mistake #3: Router vs Switch Confusion
**Exam loves to test this!**

| **Routers** | **Switches** |
|------------|-------------|
| Connect **different** networks | Connect devices **within** same network |
| Layer 3 (IP addresses) | Layer 2 (MAC addresses) |
| Separate broadcast domains | Forward broadcasts |
| Fewer interfaces | Many interfaces |

**Exam trap:** "Which device connects the Sales VLAN to the Marketing VLAN?" Answer: Router or Layer 3 switch (not a regular switch).

---

### ❌ Mistake #4: Misunderstanding "Connected" Routes
**Key point:** Routers automatically add *directly connected* networks to the routing table when the interface is up.

**Exam question style:**
> *"Which routes are added to the routing table without any configuration?"*

**Answer:** Connected routes (marked with "C" in `show ip route`)

**Don't say:** Static routes, OSPF routes, default routes (all require configuration)

---

## 🧠 Memory Aids

### **Route Selection Order (for forwarding):**
1. **Longest** prefix match first
2. If tied, **lowest** AD
3. If tied, **lowest** metric

**Mnemonic:** "**L**ongest **A**lways **M**atters" (LAM)

---

### **Administrative Distance Values (memorize these!):**
- **Connected:** 0
- **Static:** 1
- **EIGRP:** 90
- **OSPF:** 110
- **RIP:** 120

**Exam tip:** Lower AD = more trustworthy. Connected routes always win.

---

## 📋 Quick Reference for Exam Day

### **Router Interface Commands to Know:**
```
show ip route               # View routing table
show ip interface brief     # Check interface status
```

### **Reading `show ip route` Output:**
```
D    192.168.10.0/24 [90/2170112] via 10.1.1.2
^    ^               ^  ^         ^
|    |               |  |         └─ Next-hop IP
|    |               |  └─────────── Metric
|    |               └────────────── Administrative Distance
|    └────────────────────────────── Network prefix
└─────────────────────────────────── Route source (D=EIGRP, O=OSPF, R=RIP, S=Static, C=Connected)
```

**Exam loves this format!**

---

## ⏱️ Time-Saving Tips

1. **Don't overthink:** If a question asks "which route is used," check prefix length first. 90% of the time, that's your answer.

2. **Eliminate obviously wrong answers:** If the destination IP doesn't even fall within a route's range, cross it out immediately.

3. **Draw it out:** For topology questions, quickly sketch the network. Visualizing helps avoid mistakes.

4. **Use process of elimination:** Even if unsure, eliminate 2-3 wrong answers to improve your odds.

---

## 🔥 High-Yield Exam Facts

✅ Routers separate broadcast domains  
✅ Each router interface is usually in a different network  
✅ Longest prefix match is the #1 rule for forwarding  
✅ Default route is 0.0.0.0/0 (matches everything)  
✅ Routers decrement TTL; switches don't  
✅ Routers rewrite Layer 2 headers at each hop  

**Expect 8-12 router-related questions on the exam.**

---

## 💡 Final Exam Day Advice

- **Read carefully:** Cisco is known for tricky wording. Watch for words like "not," "except," "best," "first."
- **Trust your prep:** If you understand longest prefix match and broadcast domains, you'll handle most router questions.
- **Flag and move on:** If stuck, flag the question and return to it later. Don't waste time on one question.

---

**Good luck! 🚀 You've got this!**