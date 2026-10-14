EtherChannel group multiple physical interfaces together to act as a single logical interface.Traffic passing through the EtherChannel will be load balanced among the physical interfaces in the group.An algorithm is used to define which traffic will use which interface.

- Use `show etherchannel load-balance` to see the current load balancing method
- To change the current configuration, use `port-channel load-balance [src-dst-mac]`
There are three methods of EtherChannel configuration on Cisco switches:
 1. PAgP(Port Aggregation Protocol)
	 - Dynamically negotiates the creation/maintenance of the EtherChannel (like DTP).
2. LACP(Link Aggregation Control Protocol)
	- It is an industry standard protocol (IEEE 802.3ad).It basically does the same thing as PAgP.LACP is widely used because it can be used to form an EtherChannel with switches from other vendors.
3. Static EtherChannel
	- This protocol is not used to determine whether an EtherChannel should be formed.
	- Interfaces are statically configured to form an EtherChannel.
	- This is not widely used because you want the switches to dynamically maintain the EtherChannel in case of a physical failure of the physical interfaces.

Up to 8 interfaces can be formed into a single EtherChannel.LACP allows up to 16 interfaces,but only 8 interfaces will be active.The others will be in  standby mode, waiting for an active interface to fail.

- Use `channel-group [1] mode [desirable]` to configure the EtherChannel mode.
- Use `channel-protocol [lacp]` command to manually configure the EtherChannel protocol.
- Member interfaces in an Ether channel must have
	1. Same duplex (full/half)
	2. Same speed
	3. Same switchport mode (access/trunk)
	4. Same allowed VLANs or Native VLANs for trunk interfaces.
- If an interfaces configuration doesn't match with the others, it will be excluded from the EtherChannel.
- Use `show etherchannel summary` to verify the EtherChannel configuration.
- `show ether-channel port-channel` can be used for more detailed status check.
## Configuring EtherChannel on multilayer switches

1. Select the range `interface range g0/0 - 2`
2. Configure routed ports using `no switchport` command.
3. Use `channel-group 1 mode active`