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

```

## 🌉 Step 2 – Configure Router-on-a-Stick

Connected to router console:

```bash
enable
configure terminal

interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
exit

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
exit

interface g0/0
 no shutdown
exit

end
write memory

```

## 🌐 Step 3 – Configure OSPF

Connected to router console:

```bash
configure terminal
router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
end
write memory

```

## 🔒 Step 4 – Apply ACLs

Connected to router console:

```bash
configure terminal
access-list 100 deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 100 permit ip any any

interface g0/0.20
 ip access-group 100 in
exit

end
write memory
