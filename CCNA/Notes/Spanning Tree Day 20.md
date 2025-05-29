# Spanning Tree Protocol (STP) – Overview #
- Classic STP is defined by IEEE 802.1D.   
- STP is enabled by default on all switches from all vendors.   
- STP prevents Layer 2 loops by placing redundant ports into a blocking state. 
- STP interfaces act as backups and can switch to forwarding if an active link fails.   
- Forwarding state: Interface behaves normally (sends/receives all traffic).   
- Blocking state: Interface only processes STP BPDUs (Bridge Protocol Data Units).   
# Broadcast Storms & MAC Address Flapping #
- Broadcast Storm   
- A broadcast storm occurs when too many broadcast packets (e.g., ARP) flood the network.   
- These frames loop endlessly between switches if STP is not in place, multiplying with each loop.   
- Consequences:   
- Network slowdowns   
- Devices crashing   
- Loss of connectivity   
- MAC Address Flapping   
- Happens when the same source MAC address is received on multiple switch ports repeatedly.   
- The switch keeps updating its MAC address table back and forth, causing instability.   
# BPDU Behavior #
- STP-enabled switches send/receive Hello BPDUs on all interfaces.   
- Default Hello timer: Every 2 seconds.   
- If a switch receives a Hello BPDU on an interface, it knows that interface is connected to another switch.   
- Routers, PCs, and other endpoints do not send BPDUs.   

# Root Bridge Election #
- Switches use the Bridge ID field in the BPDU to elect the root bridge.   
- Lowest Bridge ID wins.   
- Bridge ID = Bridge Priority + MAC Address.   
- Default bridge priority = 32768.   
- If priorities tie, lowest MAC address wins.   
- All ports on the root bridge are designated ports and are in the forwarding state.   
- Every collision domain must have one designated port (forwarding).   
# Root Bridge Election Rules #
- Lowest Bridge Priority. 
- If tied: Lowest MAC Address.
# STP Port Roles #
### Root Port: ###
- One per non-root switch. 
- The port with the best path (lowest cost) to the root bridge. 
- Do not count the cost of the receiving interface — only the sending side.
#### Root Port Selection Criteria (in order) #####
- Lowest Root Path Cost 
- Lowest neighbor Bridge ID (MAC address) 
- Lowest neighbor Port ID (interface number) 
### Designated Port: ### 
- One per collision domain. 
- Forwards traffic toward the root. 
- If two switches connect in a domain, the switch with the lowest root cost gets the designated port. 
#### Designated Port Selection Criteria (in order): ##### 
- Lowest Root Path Cost 
- Lowest Bridge ID 
- Blocking Port: 
### The non-designated port in a collision domain. ###
- It does not forward data traffic, only listens for BPDUs. 
# STP Path Cost by Link Speed # 
| Link Speed | STP Cost |
|------------|----------|
| 10 Mbps    | 100      |
| 100 Mbps   | 19       |
| 1 Gbps     | 4        |
| 10 Gbps    | 2        |


# STP Convergence 
- When a switch first powers on, it assumes it’s the root bridge. 
- It gives up this role only when it receives a superior BPDU (with a lower Bridge ID). 
### After convergence: 
- Only the root bridge generates BPDUs. 
- Other switches simply forward BPDUs.

# Bridge Priority Details 
- Default priority: 32768 
- In VLAN 1, default = 32769 (32768 + 1) 
- Bridge Priority is added to an Extended System ID (based on VLAN ID) to create the final Bridge ID. 
- You can only configure bridge priority in multiples of 4096: 
### Valid values: 
0, 4096, 8192, 12288, 16384, 20480, 24576, 28672, 
32768, 36864, 40960, 45056, 49152, 53248, 57344, 61440 

# Cisco-Specific: PVST (Per-VLAN Spanning Tree) 
- Cisco switches use PVST, which runs a separate STP instance per VLAN. 
- Each VLAN can have different forwarding/blocking interfaces. 

# CLI Commands # 

> Symbol Reference:
> - `>` = Privileged EXEC mode  
> - `#` = Global Configuration mode

> - `#` Show Spanning-tree  > **Note:**  shows how many VLANs are participating in STP.
> - `#`show spanning-tree vlan > **Note:** can specify the specific VLAN that is participating in STP.  
> - `#`show spanning-tree detail > **Note:**  shows more information.  
> - `#`show spanning-tree summary > **Note:**  lists each vlan & and shows how many interfaces are in each STP state.
