## DTP (Dynamic Trunking Protocol)

The table below represents which port mode can interact with others and can form a trunk or stay as an access port.

| **Administrative Mode** | **Trunk** | **Dynamic Desirable** | **Access** | **Dynamic Auto** |
| ----------------------- | --------- | --------------------- | ---------- | ---------------- |
| **Trunk**               | Trunk     | Trunk                 | X          | Trunk            |
| **Dynamic Desirable**   | Trunk     | Trunk                 | Access     | Trunk            |
| **Access**              | X         | Access                | Access     | Access           |
| **Dynamic Auto**        | Trunk     | Trunk                 | Access     | Access           |
- If the switch uses DTP protocol to form a trunk with other switches, you can disable trunk negotiating by simply typing `swtichport nonegotiate` 
## VTP (VLAN Trunking Protocol)

VTP allows you to configure VLANs on a central VTP server switch, do the other switches (VTP clients) can synchronize their VLAN database to the server.It is recommended that you do not use it.

There are 3 VTP modes:  server, client, transparent

1. **Server mode**
	- Switches operate in a server mode by default.
	- VTP servers can add, delete and modify VLANs.
	- VLAN database is stored in non-volatile ram (NVRAM) by default.
	- VTP server increase their **revision number** every time they delete , modify or add VLANs.
	- **Revision number** is used by switches to determine the newest version of the VLAN database.
	- VTP servers can also function as a VTP client meaning they can synchronize their VLAN database to another server with a higher revision number.

2. **Client mode**
	- Cannot modify, add or delete VLANs.
	- VTP clients do not store the VLAN database in NVRAM (in VTPv3 they do)
	- VTP clients synchronize their VLAN database to a server with a higher revision number in their **VTP domain**.
	- VTP clients can advertise their VLAN database and forward VTP advertisements to other VTP clients ober their trunk ports.

3. **Transparent mode**
	- The switches in that mode do not sync their VLAN database.
	- They maintain their own VLAN database in NVRAM, but it won't be advertised to other switches.
	- This mode only allows to forward VTP advertisements to switches that are in the same domain as it.

## VTP CLI commands

![[show_vtp_status.png]]

- **Maximum VLANs supported locally** is 1005 ,because VTPv1 and VTPv2 doesn't support extended VLAN range.
- Use `vtp domain [domain-name]` to change the switch's domain name.

![[vtp_domain.png]]

- If we add, modify or delete VLANs , the revision number increases respectively.
![[increasing_revision_number.png]]

- There are two things that resets the revision number to 0:

	1. Changing domain name to an unused domain
	![[revision_number_reset.png]]

	2. Changing VTP mode to transparent.
	 - Use `vtp mode` command to change VTP operating mode.
	
	![[vtp_mode_transparent.png]]


- Use `vtp version` command to change VTP versions.

- VTPv2 is not much different than VTPv1.The major difference is that VTPv2 introduces support for Token Ring VLANs.If you use Token Ring VLANs you must enable VTPv2. Otherwise, there is no reason to use VTPv2.
- Token Ring is a very old technology, so there is no reason to use VTPv2.
