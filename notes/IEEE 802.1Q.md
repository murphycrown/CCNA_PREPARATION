IEEE 802.1Q is a standard that defines how the frames should be tagged while travelling through the trunk link.It also commonly known as Dot1Q. The length of the 802.1Q tag is 32 bit (4 bytes).

![[IEEE802.1Q_detailed.png]]

The 802.1Q tag inserted to an Ethernet frame after the source mac address.As we see from the picture , it consist of two fields:

- **TPID(Tag Protocol Identifier)**
	- Used for identifying that the frame is 802.1Q-tagged and always set to the value of **0x8100**.
	- **Length** : 16 bit (2 bytes)
- TCI (Tag Control Information)
	- Used for carrying the specific metadata within VLAN
	- **Length** : 16 bit (2 bytes)
	- It consists of three fields:
		- **PCP (Priority Code Point)**
			- Used for Class of Service (CoS) which prioritizes the important traffic during the congestion.
			- **Length**: 3 bit
		- **DEI (Drop Eligible Indicator)** 
			- It indicates that the package can be dropped (1)  or not (0) if the network is congested.It is set to 0 by default.
			- **Length** : 1 bit
		- **VID (VLAN Identifier)**
			- Identifies the VLAN the frame belongs to.
			- **Length**: 12 bits
			- Because this field is 12 bits, it shows that there are $$2^{12} = 4096$$ possible VLANs.



## 802.1Q (tagged) frame detailed inspection

Here is the captured tagged frame from wireshark. Let's analyze it.

```
Ethernet II, Src: 0c:7c:bd:44:00:00 (0c:7c:bd:44:00:00), Dst: CDP/VTP/DTP/PAgP/UDLD (01:00:0c:cc:cc:cc)
    Destination: CDP/VTP/DTP/PAgP/UDLD (01:00:0c:cc:cc:cc)
    Source: 0c:7c:bd:44:00:00 (0c:7c:bd:44:00:00)
    Type: 802.1Q Virtual LAN (0x8100)
    [Stream index: 0]
802.1Q Virtual LAN, PRI: 0, DEI: 0, ID: 1
    0. .... .... .... = Priority: Best Effort (default) (0)
    ...0 .... .... .... = DEI: Ineligible
    .... 0000 0000 0001 = ID: 1
    Length: 44


```

- **Type: 802.1Q Virtual LAN (0x8100)** : indicates that the package has been wrapped with 802.1Q VLAN tag header.This tells your NIC that instead of  a normal payload type after the source MAC address , the frame contains 4-byte 802.1Q VLAN tag header. The hex value `0x8100` is the standard EtherType identifier for VLAN tagging.

- **PRI : 0 (Priority / CoS - Class of Service)** : It is a 3 bit field used for Quality of Service (QoS) packet prioritization (IEEE 802.1p).0 means **Best Effort**  which tells the switch to deliver the package normally.We can think of it as shipping label.It helps switches to decide which packages they should send first.

- **DEI: 0 (Drop Eligible Indicator)** : it is a 1 bit field that acts as a congestion-control flag telling network devices whether a packet is expandable if the switch or router  experiences a heavy congestion and runs out of buffer space.
	- **0 (Ineligible)** means the packet can't be dropped preferentially.It has a standard protection during traffic jam.
	- **1 (Eligible)** means the packet has a low importance and can be dropped by the switch's queue management during heavy congestion.

- **ID: 1 (VLAN ID)**: A 12 bit field identifies the spesific VLAN number attached to this frame.A value of **1** means VLAN 1 (assigned by default on Cisco swiches).