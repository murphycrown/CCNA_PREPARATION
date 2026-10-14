Image below shows the output of `show interface status` command in switches.

![[switch_interface_status.png]]

- **Duplex**

	 ![[switch_show_duplex.png]]
	 
	- **half-duplex** means device cannot send and receive data at the same time
	- **full-duplex** means device can send and receive data at the same time.
	- **auto** means device automatically negotiates itself.

- **Speed**

	![[switch_show_speed.png]]

	- Here you can specify different speed options based on the cable type you are using, if you don't specify anything device automatically negotiates the speed for you.

## Configuring interfaces

 1. Use `enable` and then `configure terminal` command to enter the global configuration mode.
 
 2. Unlike routers, switches do not shutdown the interfaces by default.It can sound like a good feature, but it lowers the level of security of our network.Therefore, it is best practice to keep them disabled by default.
 
	 - Determine the range of network interfaces you don't use.
	
	 -  Specify the interface range by using `interface range [interface_name]0/[number] - [number]` 
	
	 - Type `shutdown` to disable all interfaces that you don't use.
	
3. Specify the interface you want to configure by using `interface [interface_name]0/[number]`

4. set `speed [max-speed]`.`[max-speed]` value can change depending on the cable, but you can check the maximum speed by simply typing `speed?`

5. Now, we want our interface to be capable of transmitting and receiving data at the same time.We use `duplex full` command to establish full-duplex transmission.

6. Finally, assign a description to the interface to remember which device it is connected.Use `description [device_name]` to keep it simple and understandable.
7. 