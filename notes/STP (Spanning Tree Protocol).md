- STP is a Layer 2 protocol.

- Classic Spanning Tree Protocol's IEEE 802.1D

- Switches from all vendors run STP by default.

- STP prevents Layer 2 loops by placing redundant ports in a blocking state.In other words, disabling the interface.These interfaces act as backups, meaning they can only enter the forwarding state if actively running interfaces are failing.
	1. Interfaces in a **forwarding state** behaves normally.They send and receive all the traffic.
	2. Interfaces in a blocking state only send or receive STP messages( called BPDUs=Bridge Protocol Data Units)
	
- By selecting which ports are forwarding and which ports are blocking, STP creates a single path to or from each point in the network.This prevents Layer 2 loops.

- STP enabled switches configured to send or receive **Hello BPDUs** out of all interfaces and the default timer is 2 seconds.If a switch receives this BPDU , it knows that it is connected to a switch.

- There is a set process that STP uses to determine which ports should be forwarding and which should be blocking.

- A switch use one field in the STP BPDU - the **Bridge ID**, field to select a root bridge for the network.The switch with the lowest **Bridge ID** becomes the root bridge.

- All ports on the root bridge are put in a forwarding state, and other switches in the topology must have a path to reach the root bridge.All ports are on the root bridge are considered as **designated ports** (forwarding).

- **Bridge ID** inside an STP BPDU has two fields:

![[BRIDGE_ID.png]]


- VLAN ID is included because Cisco switches use a version of STP called **PVST** (Per-VLAN Spanning Tree).PVST runs a separate STP 'instance' in each VLAN, so in each VLAN different interfaces can be forwarding or blocking.

	 1. **Bridge Priority**
	    -  Set to 32768 by default (is there is no VLAN configured )
		- Length: 16 bits
	2. **MAC address**
		- Length: 48 bits

## STP protocol from a switch's perspective

1. When a switch is powered on, it assumes it is the root bridge
2. It only gives up its position if it receives a superior BPDU (with a lower **Bridge ID**)
3. Once the topology has converged and all the switches agree on the root bridge, only the root bridge sends BPDUs.
4. All ports are on the root bridge are considered as **designated ports** (forwarding state).
5. The ports connected to root ports will become designated ports (forwarding state).
6. Other switches in the network will forward the root bridge's BPDUs , but they won't generate their own original BPDUs.
7. Each remaining switch will select one of its interfaces to be its root port. The interface with the lowest **root cost** will be the **root port**.Root ports are also in a forwarding state.

Each interface in the network has an associated STP cost:

| Speed    | STP Cost |
| :------- | :------- |
| 10 Mbps  | 100      |
| 100 Mbps | 19       |
| 1 Gbps   | 4        |
| 10 Gbps  | 2        |
7. If the switch's interfaces has the same cost switch will choose the interface connected to the switch with lowest **Bridge ID**. 
8. If the **Bridge ID** also same, then it chooses the port connected to the interface in the neighbor switch with the lowest port ID.
Each interface of a switch has default STP **port ID** consists of port priority of 128 and a unique port number.

**Root port selection:**
- Lowest root cost
- Lowest neighbor Bridge ID
- Lowest neighbor port ID

9. Each remaining collision domain will select one interface to be a designated port.A designated port is selected according the same rules as a root port and after the process the other switch will make its port non-designated (blocking state).
## CLI commands for STP

- `show spanning-tree` shows the port states for each VLAN. You can even specify a VLAN number.
	![[show_spanning_tree.png]]

	- **Spanning tree enables protocol** means that we are using the classic STP (actually it is Cisco's PVST, but it means it is in a classic mode rather than newer Rapid STP).
	- **Root ID** displays the information about the root bridge of this spanning tree.
	- **Bridge ID** displays the information about this switch.

- `show spanning-tree detail` shows more detailed information

- `show spanning-tree summary` shows the summary of the spanning tree.

	![[show_spanning_tree_summary.png]]
	
- `spanning-tree mode [mode-name]` configure the STP mode.

	![[spanning_tree_mode.png]]
	
### STP load-balancing

- If we have multiple VLANs in our topology, blocking the same interface in each VLAN is a waste of interface bandwidth.That's why we specify different root bridges for each VLAN to save bandwidth.
- We manually configure the root bridge by manipulating the priority of a switch.Use `spanning-tree vlan 1 root primary` to configure a current switch as a root bridge. This command sets the **Bridge Priority** to 24576, but if another switch already has a priority lower than 24576, it sets this switch's priority to 4096 less than the other switch's priority.

	 ![[spanning_tree_vlan_1_root_primary.png]]
	 
- If we want to configure secondary root bridge as a backup.We use a command similar to primary root bridge's: `spanning-tree vlan 1 root secondary`.

	![[spanning_tree_vlan_1_root_secondary.png]]

### Configuring STP Port Settings

![[stp_port_settings.png]]

- **cost** gives us an opportunity to change the default cost of the interface.We use this device to change the selection process of blocking and designated ports and it ranges from 200 million.
- **port-priority** also act as a tie-breaker like cost field in the selection of blocking and designated ports.We can manually configure it by using the command that is shown above.It ranges from 0 to 240 (default value is 128 ).

## STP Port States

| STP Port State | Stable/Transitional |
| :------------- | :------------------ |
| Blocking       | Stable              |
| Listening      | Transitional        |
| Learning       | Transitional        |
| Forwarding     | Stable              |
- **Root/Designated Ports**
	- Root/Designated ports remain stable in a **Forwarding state**.

- **Listening State** 
	- Only **Designated** or **Root ports** enter the Listening State.

	- The Listening state is 15 seconds long by default.This is determined by the **Forward Delay** timer.

- **Blocking Ports**
	- Non-designated ports remain stable in a **Blocking state**.
	
	- Interfaces in a blocking state are effectively disabled to prevent loops.
	
	- Interfaces in a blocking state do not send or receive regular network traffic.They receive STP BPDUs, but they can't forward it.
	
	- Interfaces in a blocking state do not learn MAC addresses.

- Listening/Learning are transitional states which are passed through when an interface is activated, or when a blocking port must change its state to a Forwarding state due to a change in network topology.

| STP Port State | Send/Receive BPDUs | Frame forwarding (regular traffic) | MAC address learning | Stable/Transitional |
| :------------- | :----------------- | :--------------------------------- | :------------------- | :------------------ |
| Blocking       | NO/YES             | NO                                 | NO                   | Stable              |
| Listening      | YES/YES            | NO                                 | NO                   | Transitional        |
| Learning       | YES/YES            | NO                                 | YES                  | Transitional        |
| Forwarding     | YES/YES            | YES                                | YES                  | Stable              |
| Disabled       | NO/NO              | NO                                 | NO                   | Stable              |
