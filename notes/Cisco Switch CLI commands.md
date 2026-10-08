######  `show mac address-table` 
Displays the MAC addresses attached to each port.
######  `enable`
Enters the Privileged Exec Mode where you can see status and configs.
###### `show ip interface brief`
Shows the status of all physical interfaces.
###### `clear mac address-table dynamic`
Clears the CAM (Content-Addressable Memory) table of a switch.
###### `clear mac address-table dynamic address [Mac Address]` 
Clears the specific MAC address from CAM(Content Addressable Memory) table.
###### `clear mac address-table dynamic interface [Interface Name]` 
Removes the specific Interface from CAM(Content Addressable Memory) table.
###### `configure terminal`
Enters the Global Configuration Mode where you can change switch-wide settings (create VLANs , set hostname).Short version is `conf t`.
###### `interface [Interface Name]`
Changes settings for a specified port.
###### `switchport mode access`
Enables the Access Mode for the specified range of ports.
###### `switchport access vlan 10`
Binds the access ports specifically to VLAN 10.Any untagged frame coming into this port gets assigned to VLAN 10 inside the switches.
