# Lab: Router-on-a-Stick – VLAN 10 & 20 Communication

## 🎯 Objective
Simulate inter-VLAN routing between two VLANs (10 and 20) using Router-on-a-Stick configuration.

## 🧰 Topology
![router on a stick 1](https://github.com/user-attachments/assets/e63bbcaf-5d07-4f43-86dd-68b24e8ad9f4)


- VLAN 10 – Office One: PC1 (10.10.0.2), PC2 (10.10.0.3)
- VLAN 20 – Office Two: PC3 (10.20.0.2)
- Router G0/0 connected to switch via trunk
- Inter-VLAN routing handled via subinterfaces on router

## ⚙️ Configuration Overview
- VLANs created on switch: 10 and 20
- Access ports assigned to correct VLANs
- Trunk port set on link between router and switch
- Subinterfaces created for VLAN 10 and 20 with proper encapsulation (`dot1Q`)

## ❌ Issues Encountered & Fixes
- ❗ **Forgot `switchport mode access`** on access ports → PCs weren’t getting VLAN assignment  
  ✔️ Fixed by setting mode to access on Fa1/1, Fa2/1, Fa3/1
- ❗ **VLAN description error** — tried to use a space in the name  
  ✔️ Learned to use quotes or no spaces
- ❗ **Incorrect VLAN assignment** — Fa2/1 assigned to VLAN 20 instead of VLAN 10  
  ✔️ Reassigned correctly after testing ping failures

## ✅ Result
- All PCs could ping across VLANs
- Subinterfaces and trunk port functioned as expected

## 🧠 Lessons Learned
- Always verify port-to-VLAN assignments
- Trunking is essential for RoaS
- Use `ipconfig` and `ping` during testing to catch config errors
