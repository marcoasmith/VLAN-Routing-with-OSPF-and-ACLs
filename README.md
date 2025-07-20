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
<img width="400" height="500" alt="ChatGPT Image Jul 19, 2025 at 05_02_31 PM" src="https://github.com/user-attachments/assets/b10a194c-c87d-45f4-93d5-517f92fafd8a" />


## 🔌 Step 1 – Cabling Setup

1. **Use Ethernet Cable 1** to connect:  
   - `fa0/1` on **Switch** → `g0/0` on **Router**

2. **Use Ethernet Cable 2**:  
   - From your **PC1** (for testing) → `fa0/2` on **Switch**

3. **Use Ethernet Cable 3**:  
   - From your **PC2** (for testing) → `fa0/3` on **Switch**

4. **Use the console cable** to connect your PC to the switch or router so you can configure them.

   






## ⚙️ Step 2 – Configure VLANs on Switch
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

## 🌉 Step 3 – Configure Router-on-a-Stick

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

## 🌐 Step 4 – Configure OSPF

Connected to router console:

```bash
configure terminal
router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
end
write memory

```

## 🔒 Step 5 – Apply ACLs

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

```

## ✅ Conclusion

In this project, we successfully built a small routed network using a Cisco 2960 switch and a Cisco 2900 router.

✔️ Step 1: We configured VLANs on the switch and assigned ports to each VLAN.

✔️ Step 2: We set up Router‑on‑a‑Stick on the router, creating sub‑interfaces for inter‑VLAN routing.

✔️ Step 3: We enabled and configured OSPF to advertise our VLAN networks dynamically.

✔️ Step 4: We applied ACLs to control traffic between VLANs and restrict access as needed.


Through these steps, we demonstrated key networking skills:

-VLAN segmentation and trunking

-Router sub‑interface configuration for inter‑VLAN routing

-Dynamic routing with OSPF

-Traffic filtering using standard and extended ACLs

This project shows how a router and switch can work together to build a scalable and secure network.


<img width="740" height="721" alt="Screenshot 2025-07-19 at 5 20 46 PM" src="https://github.com/user-attachments/assets/a74fbcb1-eba5-4057-a261-64b5f3267383" />
