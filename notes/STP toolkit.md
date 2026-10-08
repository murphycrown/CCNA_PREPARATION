## STP PortFast

Portfast allows a port to move immediately to the **Forwarding state** ,by passing **Listening**, **Learning** states.It can only be enabled if the port is connected to the end host. Otherwise, it can cause a Layer 2 loop.

### Enabling Portfast

Portfast can be enabled in an interface level.

![[stp_portfast.png]]

As seen from the output, portrast only takes effect if the port is in an access mode.

- Use the `spanning-tree portfast default`  in the Global Configuration Mode to enable portfast in all access ports.
- However, we are taking a huge risk by using portfast because if an employee change the end host with a switch he may accidentally create a Layer 2 loop.
## STP BPDU Guard

We use another feature called BPDU Guard to prevent Portfast-enabled interfaces from causing a Layer 2 loop.
## Enabling BPDU Guard

Enabling BPDU Guard is quite similar to port fast

![[stp_bpdu_guard.png]]

- Use the `spanning-tree portfast bpduguard default`  in the Global Configuration Mode to enable BPDU Guard on all Portfast-enabled interface.
Here is what happens we connect switch to a port where both Portfast and BPDU Guard features are enabled.

![[stp_bpdu_guard_disable_ports.png]]

BPDU Guard disables the port instantly and change its state to administratively shutdown.To enable the port again, we use the `shutdown` and `no shutdown` commands.

![[enable_bpdu_guard_disabled_port.png]]