
# Spanning Tree Protocol (STP) Port States


###  1. Port Roles and Stable States
- Root Ports (RP) and Designated Ports (DP)  
- Always remain in the Forwarding state during stable topology.  
- Participate in normal network operation.  
### Non-Designated Ports
- Always remain in the Blocking state during stable topology.  
- Used to prevent loops.  
### 2. Transitional Port States
#### Transitional states occur when an interface is:
- Activated  
- Recovering from a topology change  
- Moving from a blocking to forwarding state  
### The two transitional states are:  
##### a. Listening State  
- Default duration: 15 seconds (set by the forward delay timer).  
##### Functions:  
- Receives/sends only STP BPDUs.  
- Does not send/receive regular traffic.  
- Does not learn MAC addresses.  
#### b. Learning State  
Default duration: 15 seconds (same forward delay timer).  
##### Functions:
- Receives/sends STP BPDUs.  
- Learns MAC addresses from incoming traffic.  
- Does not send/receive normal traffic yet.  
### 3. Blocking State
Applied to Non-Designated Ports.
Purpose: Loop prevention.
#### Characteristics:
- Effectively disabled for normal data traffic.  
- Receives STP BPDUs only.  
- Does not forward traffic.  
- Does not learn MAC addresses.  
- Remains in place unless a topology change triggers a transition.  
### 4. Forwarding State
- Applied to Root Ports and Designated Ports after completing transitions.  
- Full participation in network operations:  
- Sends and receives STP BPDUs.  
- Sends and receives normal traffic.  
- Learns MAC addresses.  

### STP Path Cost by Link Speed 
| Port State  | Forwards Traffic | Learns MACs | Sends/Receives BPDUs | Duration              |
|-------------|------------------|-------------|-----------------------|------------------------|
| Blocking    | No               | No          | Yes                   | Indefinite (until change) |
| Listening   | No               | No          | Yes                   | 15 seconds (default)  |
| Learning    | No               | Yes         | Yes                   | 15 seconds (default)  |
| Forwarding  | Yes              | Yes         | Yes                   | Ongoing (stable)      |
| Disabled  | NO/NO              | NO         | NO                   | Stable      |

### Spanning Tree Timers
| Stp Timer  |Purpose  |Duration  |
|----------|-------|--------|
| Hello  | How often the root bridge sends hello BPDUs  | 2sec  |
| Forward Delay  | How long the switch will stay in the listening and Learning states (each state is 15 seconds = total of 30 seconds)  |15 sec  |
| Max Age  | How long an interface will wait after ceasing to receive Hello BDPUs to change the STP topology  | 20 sec (10*hello)

### Spanning Tree Protocol (STP) – Timers, Features, and Configuration

### 1. STP Timers

- Hello Timer  
  How often the root bridge sends Hello BPDUs.  
  Default: 2 seconds

- Forward Delay  
  Time a port stays in the Listening and Learning states.  
  Default: 15 seconds (each) → total 30 seconds

- Max Age  
  Time an interface waits after BPDUs stop arriving before reevaluating STP.  
  Default: 20 seconds (usually 10 × Hello Timer)

- If BPDUs are received before Max Age expires → no change.  
- If no BPDUs are received and Max Age expires → reevaluate STP.  
  Blocking → Listening → Learning → Forwarding  
  Total transition time ≈ 50 seconds  
- Forwarding to Blocking happens immediately.  
- Blocking to Forwarding must pass through Listening and Learning.


### 2. PortFast and BPDU Guard

#### PortFast
- Immediately transitions the port to the Forwarding state.
- Skips Listening and Learning states.
- Only use on ports connected to end devices.
- Never enable on switch-to-switch links.

#### BPDU Guard
- Disables a PortFast-enabled port if it receives a BPDU.
- Prevents loops from misconfigurations.
- To re-enable, shut and unshut the interface.



### 3. Optional STP Features (STP Toolkit)

| Feature     | Function                                                              |
|-------------|-----------------------------------------------------------------------|
| BPDU Guard  | Disables PortFast-enabled ports if BPDUs are received                 |
| Root Guard  | Prevents a port from becoming root if superior BPDUs are received     |
| Loop Guard  | Prevents Forwarding if BPDUs stop arriving (protects against loops)   |



### 4. STP Types

| STP Variant   | Encapsulation Support              |
|---------------|------------------------------------|
| PVST          | Cisco proprietary – ISL only       |
| PVST+         | Cisco extended – supports 802.1Q   |
| Standard STP  | MAC address: 0180.c200.0000        |

---

# CLI Commands 

> Symbol Reference:
> - `#` = Privileged EXEC mode  
> - `(config) #` = Global Configuration mode
> - `(Config-if) #` Confiuration interface mode

> - `(config) #` spanning-tree portfast default 
> - `(Config-if) #` Spanning-tree portfast 
> - `(Config-if) #`spanning-tree bpduguard enable 
> - `(config) #` spanning-tree portfast bpduguard default (this enables BPDU Guard on all portfast-enabled interfaces 
> - `(config) #`spanning-tree mode ? 
> - `(config) #`spanning-tree mode pvst 
> - `(config) #`spanning-tree vlan 1 root primary (this configs the primary root bridge by setting the priority to 24576. If another switch has that it sets it lower to 4096, so less than the other switch's priority) 
> - `(config) #`spanning-tree vlan 1 root secondary (sets the secondary root bridge) 
> - `(Config-if) #`spanning-tree vlan 1 cost  (example: spanning-tree vlan 1 cost 200) 
> - `(Config-if) #`spanning-tree vlan 1 port-priority  
> - `(config) #`do show spanning-tree 

