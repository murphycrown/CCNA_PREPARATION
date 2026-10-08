A multilayer switch is capable of both switching and routing.You can create routes and assign IP addresses on it ,just like a router.Its invention purpose is mainly about the speed, because a lot of network going through from a switch to a router can cause network congestion and delays.
- To enable ip routing on multilayer switches we use `ip rounting` command.Use the `no switchport` command to turn the port from a switchport to a routed port.Now, you will be able to assign ip addresses to each port.
- In this topology, we only need router when we want to communicate with an IP address outside out network.Therefore, we configure router as a default route on a Multilayer switch: `ip address 0.0.0.0 0.0.0.0 [ip-address-of-router]`
## Configuring SVI (Switched Virtual Interfaces)
- The SVI port is used by the switches for inter-vlan routing.
	1.  Type `interface vlan[vlan-number]`
	2. Type `no shutdown`. SVI ports are disables by default.
	3. Use `ip address [ip-address] [subnet-mask]` to specify ip address.
	4. Use `show ip interface brief` command to verify.

If the ports state is down/down ,then it means you did something wrong while configuring.

- Conditions for SVIs to up/up when we type `show interfaces status` command.
	1. The VLAN must exist on a switch.
	2. The switch must have at least one access port in the VLAN in an up/up state or one trunk port that allows the VLAN that is an up/up state.
	3. The VLAN mustn't be shutdown.
	4. The SVI mustn't be shutdown.