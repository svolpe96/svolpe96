# Lab: Scaled Router-on-a-Stick – VLANs 10, 20, 30, 40

## 🎯 Objective
Simulate a scaled-up router-on-a-stick setup using 4 VLANs across two switches, with centralized inter-VLAN routing on the router.

## 🧰 Topology
![scaled-up version of router on a stick](https://github.com/user-attachments/assets/81facc41-ef0d-4af2-bd2e-38a36d51d0b3)

- 1 Router (Router1)
- 2 Switches (SW1 and SW2)
- 8 PCs total:
  - VLAN 10 (10.10.0.0/24): PC1, PC2
  - VLAN 20 (10.20.0.0/24): PC7, PC8
  - VLAN 30 (10.30.0.0/24): PC5, PC6
  - VLAN 40 (10.40.0.0/24): PC3, PC4
- SW1 and SW2 connected together
- SW1 trunked to Router1 on g0/0
- Static IPs assigned to each PC and router subinterfaces

## ⚙️ Configuration Overview
- VLANs 10, 20, 30, 40 created on both switches with appropriate names
- Switchports assigned to access mode and correct VLANs
- Trunk link set between:
  - SW1 <-> Router (g0/0)
  - SW1 <-> SW2
- Router subinterfaces configured:
  - g0/0.10 – 10.10.0.1/24
  - g0/0.20 – 10.20.0.1/24
  - g0/0.30 – 10.30.0.1/24
  - g0/0.40 – 10.40.0.1/24

## ❌ Issues Encountered & Fixes
- ❗ PCs in different VLANs couldn't ping each other  
  ✔️ After a long troubleshooting session, realized the trunk between **SW2 and the router was missing**  
  ✔️ Enabled trunking on the correct SW2 interface and inter-VLAN routing started working

## ✅ Result
- All PCs could ping each other across VLANs
- Every PC could successfully ping the router's subinterface for their VLAN
- Inter-VLAN routing fully functional

## 🧠 Lessons Learned
-  Always double-check **trunking configurations** between switches and routers
-  Planning ahead helps when scaling — naming VLANs and organizing ports avoids confusion
-  Simple mistakes like a missing trunk can break the entire network, even if configs seem fine
