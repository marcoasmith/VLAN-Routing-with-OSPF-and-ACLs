# VLAN-Routing-with-OSPF-and-ACLs
# 🚀 Cisco VLAN + OSPF + ACL Lab

## 📌 Overview
This project demonstrates how to configure a **Cisco 2960 switch** and a **Cisco 2900 router** to create VLANs, enable inter‑VLAN routing (router‑on‑a‑stick), run OSPF, and apply ACLs for access control.

It’s written step‑by‑step so even a beginner can follow along.  
✅ VLANs  
✅ OSPF  
✅ ACLs  
✅ Tested with a Mac (VLAN10) and Windows PC (VLAN20)

---

## 🖥 Equipment
- Cisco 2960 Switch  
- Cisco 2900 Router  
- Console cable + USB adapter  
- Ethernet cables  
- One Mac and one Windows PC  
- PuTTY (Windows) / Terminal (Mac)

---

## 🗺 Topology


---

## ⚙️ Step 1 – Configure VLANs on Switch
Connected to switch console:

```bash
enable
configure terminal

vlan 10
 name SALES
exit

vlan 20
 name HR
exit

interface fa0/2
 switchport mode access
 switchport access vlan 10
exit

interface fa0/3
 switchport mode access
 switchport access vlan 20
exit

interface fa0/1
 switchport mode trunk
exit

write memory


