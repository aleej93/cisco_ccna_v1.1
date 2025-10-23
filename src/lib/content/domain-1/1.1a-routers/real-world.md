# 🌍 Real-World: Routers

**Quick real-world examples of where and why routers matter.**

---

## 🏠 Home Network

Your home Wi-Fi router connects your devices (phones, laptops, smart TVs) to the Internet. It assigns private IP addresses (192.168.x.x) to your devices and translates them to your ISP's public IP.

**Real example:** When you stream Netflix, your router forwards packets from your TV to Netflix servers across the Internet.

---

## 🏢 Corporate Branch Office

A company with offices in New York (192.168.1.0/24) and London (192.168.2.0/24) uses routers at each location to connect to a VPN over the Internet.

**Real example:** An employee in NY sends an email to London - the router forwards it across the company's WAN.

---

## 🌐 Internet Service Provider (ISP)

ISPs use high-capacity routers to forward traffic between customers and the rest of the Internet. These routers handle millions of packets per second.

**Real example:** When you visit google.com, your packets pass through multiple ISP routers before reaching Google's data center.

---

## 🏥 Hospital Network

Hospitals segment their network into VLANs (patient records, medical devices, guest Wi-Fi) and use routers or Layer 3 switches to allow controlled communication between them.

**Real example:** A doctor's workstation (VLAN 10) accesses the patient database server (VLAN 20) through inter-VLAN routing.

---

## ☁️ Cloud Data Center

Cloud providers like AWS use routers to connect virtual networks (VPCs) and route traffic between customers, availability zones, and the Internet.

**Real example:** Your web app in AWS us-east-1 communicates with a database in us-west-2 via AWS's internal routing.

---

**💡 Key Takeaway:** Routers are everywhere - from your home to the global Internet. They're the backbone of network connectivity.
