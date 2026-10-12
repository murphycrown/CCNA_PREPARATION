sVLAN (Virtual Local Area Networks) belongs to Layer 2 of the OSI model. Imagine you have a company and this company has two different departments like Sales and IT. These departments are separated into to rooms randomly. Your job is to design a network where both Sales and IT department's  members can communicate with each other privately. If you have one switch in each room you need long data cables to connect all IT departments in one switch and Sales departments to another. This is not a cost-effective way and creates a very complex network structure.That's where VLAN comes in. Instead of running extra cables between rooms, you simply create VLANs on your switches and assign each port to its respective departments (e.g., VLAN 10 for IT , VLAN 20 for Sales) . This way you create a simple private network for one department.This creates logically isolated private networks across the same physical hardware.

There are 4096 possible VLANs (range from 0 - 4095), but first (0) and last (4095) VLANs are reserved and can't be used.There the actually range of usable VLANs are 1 - 4094
## Configuring VLANs on a switch
You can see the well known Cisco commands and their usage from [[Cisco Switch CLI commands]]
1. Type `enable` to enter the Privileged exec model
2. Type `configure terminal` to enter the Global Configuration Model
3. Type `vlan 10` to create a new VLAN.
4. Type `name Subnet10(or the name you prefer)` to customize the name of your VLAN.
5. Type `exit` to exit from VLAN configuration.
6. Repeat the step 3, 4 and 5 if you need to create two or more VLANs.
7. Type `interface range fa0/1 - 2` to select the ports.
8. Type `switchport mode access` to enable Access Mode
9. Type `switchport access vlan [number]` assign to VLAN

Configuring trunk link:
1. Type `interface range fa0/1 - 2` to select the ports.
2. Type `switchport mode trunk` to enable Trunk Mode.However, in some switches you might need to configure the encapsulation type with `switchport trunk encapsulation dot1q` before enabling Trunk Mode.Read [[IEEE 802.1Q]] to learn more about the IEEE 802.1Q.
3. Use `show interfaces trunk` command to confirm that the trunk interface is working.
4. Use `switchport trunk allowed vlan` command to specify which VLANs should be allowed in this trunk port.It has some options:
	![[show_trunk_allowed_vlan_options.png]]
5. Use `show interfaces trunk` command to verify.
6. It is best to change native VLAN to an unused VLAN for security purposes.`switchport trunk native vlan [number]` is used for changing the native VLAN.

You can see an example of how the ARP request travels through the VLAN in 
![[VLAN_ARP_FLOW.canvas]]
## ROAS (Router on a Stick)

When we connect a router to a switch we use one physical interfaces, so what if we have 2 or more networks connected to the switch.How can we configure these networks on the router.To do this we divide one physical interface into three separate logical sub interfaces.

1. Type `enable` to enter the Privileged exec model
2. Type `configure terminal` to enter the Global Configuration Mode.
3.  Type `interface g0/0` to select the physical interface.
4. Type `no shutdown` to change the port state from *down* to *up*.
5. Use `interface g0/0.10` to create a new interface for VLAN 10.Remember that the sub interface number doesn't have to match the VLAN, but it is highly recommended.
6. Type `encapsulation dot1q [vlan_number]` .It tells the router to tag every frame coming to this sub interface with specific VLAN number.
7. Finally, assign the ip address to the interface by using `ip address [address] [subnet mask]`.
8. Do the same for each network.

### Assigning Native VLANs on a router

There are two methods of configuring the Native VLAN on a router:

1. Use `encapsulation dot1q [vlan-number] native` command to configure native VLANs on subinterfaces.
2. Configure the IP address for the native VLAN on the routers physical interface.For example 
	 - `interface g0/0`
	 - `ip address 192.168.1.0 255.255.0.0`
	