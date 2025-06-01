# Lab: Router-on-a-Stick 1

## 🎯 Objective
Simulate inter-VLAN routing between two VLANs (Office One and Office Two)

## 🧰 Topology
![router on a stick 1](https://github.com/user-attachments/assets/75209799-4b75-47b5-8c33-2a9a3c63fdc2)


- R1 (Router) and SW1 (Switch)
- 3 PCs:
  - PC1, PC2 in VLAN 10 (Office One)
  - PC3 in VLAN 20 (Office Two)
- Subinterfaces on R1 for VLANs 10 and 20
- SW1 trunked to R1 via g0/1
- End devices statically assigned IPs based on VLAN subnet

## ⚙️ Configuration Overview
- Set hostnames for R1 and SW1
- Set passwords using MD7 encryption (`service password-encryption`, password = `hello`)
- Set R1 interface `g0/1` IP to `10.0.0.1/8`
- Created VLAN 10 and 20 on SW1 with proper names and descriptions
- Assigned switch ports to VLANs
- Configured router-on-a-stick using:
  - `g0/1.10` → VLAN 10
  - `g0/1.20` → VLAN 20
- Enabled trunking on SW1
- Assigned static IPs to PCs based on their VLANs
- Verified connectivity by pinging PC3 and the gateway

## ❌ Issues Encountered & Fixes
- ❗ Trouble setting up VLANs  
  ✔️ Forgot `switchport mode access` — fixed on appropriate ports  
- ❗ Issue naming VLANs (Cisco IOS doesn’t allow spaces)  
  ✔️ Used underscores or no spaces in VLAN names  
- ❗ PC2 was placed in the wrong VLAN  
  ✔️ Moved from VLAN 1 to VLAN 10 by correcting the port assignment  
- ❗ Couldn't ping the router at first  
  ✔️ Fixed by setting up router-on-a-stick properly with encapsulation and correct IPs

## ✅ Result
- Successful inter-VLAN communication
- PCs in VLAN 10 and VLAN 20 can ping each other
- Default gateway pinged successfully from PC3
- Router and switch fully configured with hostnames and passwords

## 🧠 Lessons Learned
- Always set `switchport mode access` when assigning ports to VLANs
- VLAN names cannot have spaces in Cisco IOS — use underscores or short labels
- Subinterfaces need matching encapsulation IDs and active physical interfaces
- It's easy to place a PC in the wrong VLAN — verify port-to-VLAN mappings
