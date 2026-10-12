## STP PortFast

Portfast allows a port to move immediately to the **Forwarding state** ,by passing **Listening**, **Learning** states.It can only be enabled if the port is connected to the end host. Otherwise, it can cause a Layer 2 loop.

### Enabling Portfast

Portfast can be enabled in an interface level.

![[stp_portfast.png]]

As seen from the output, portrast only takes effect if the port is in an access mode.

- Use the `spanning-tree portfast default`  in the Global Configuration Mode to enable portfast in all access ports.

- In some scenarios (like ROAS) , we might want to enable portfast on a trunk link.We can enable it  using the command `spanning-tree portfast trunk` on an interface.

- However, we are taking a huge risk by using portfast because if an employee change the end host with a switch he may accidentally create a Layer 2 loop.
## STP BPDU Guard

We use another feature called BPDU Guard to prevent Portfast-enabled interfaces from causing a Layer 2 loop.
## Enabling BPDU Guard

Enabling BPDU Guard is quite similar to port fast

![[stp_bpdu_guard.png]]

- Use the `spanning-tree portfast bpduguard default`  in the Global Configuration Mode to enable BPDU Guard on all Portfast-enabled interface.
Here is what happens we connect switch to a port where both Portfast and BPDU Guard features are enabled.

![[stp_bpdu_guard_disable_ports.png]]

<<<<<<< HEAD
BPDU Guard puts the port in a **ErrDisable** state and disables it immediately.
- **ErrDisable** is a Cisco switch feature that disables a port under certain conditions, such as BPDU Guard violation.
- You can enable the port again with two ways:
1. use the `shutdown` and `no shutdown` commands.

![[enable_bpdu_guard_disabled_port.png]]

2. **ErrDisable Recovery** is feature that automatically re-enables the err-disabled ports after a certain period of time.
	- `show errdisable recovery` used for showing the status of this feature.
	
		![[show_errdisable_recovery.png]]
		
	- `errdisable recovery cause bpduguard ` used for enabling the feature.

		![[errdisable_recovery_cause_bpduguard.png]]
## STP BPDU FILTER

As we know from the STP, the switch keep sending BPDUs to a device even if it is an host device.This is completely unnecessary , and it uses bandwidth and processing power even if it is minimal.In addition, BPDUs contains information about our LAN topology, so it is a big problem in terms of security.We use a feature called **BPDU Filter** to prevent an interface from sending BPDUs.
- Unlike BPDU Guard, it doesn't disables the port when it receives a BPDU.

- **BPDU filter** can be enabled in two ways:
	1. `spanning-tree bpdufilter enable` used to configure a specific interface.
		- The port simply ignores any BPDU it receives which disable STP on the port.
	2. `spanning-tree portfast bpdufilter default` enables BPDU Filter on all portfast-enabled ports.
		- When we enable the feature with this command,the ports do not send BPDUs, but if they receive BPDUs, they just operate as a normal STP port.
## STP ROOT Guard
Root Guard ensures that the switch stays the root bridge even if a new switch with a lower bridge ID connects to the network.
- Use `spanning-tree guard root` to enable from the interface configuration mode.
## STP LOOP Guard
We use LOOP Guard to protect the network from loops by blocking a port if it unexpectedly stops receiving BPDUs.
- Use `spanning-tree guard loop` to enable LOOP Guard from interface configuration mode.
- Use `spanning-tree loopguard default` from the global configuration mode to enable it for all ports.
- Use `spanning-tree guard none` to disable the feature from the specific port if needed.

BPDU Guard disables the port instantly and change its state to administratively shutdown.To enable the port again, we use the `shutdown` and `no shutdown` commands.

![[enable_bpdu_guard_disabled_port.png]]

