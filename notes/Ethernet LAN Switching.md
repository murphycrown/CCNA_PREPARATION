Layer 2 PDUs(Protocol Data Units) are called frames.The data, the header and the trailer encapsulated by the Layer is called payload,so L2 PDU - an ethernet 
frame contains  L3 PDU - a packet as its payload.Let's take a look at the how the Ethernet frame looks like.

![[ethernet_frame_detailed.png]]

- Fields inside the Ethernet header:
	1. **Preamble**
		- Allows devices to synchronize their clocks to make sure they are ready to receive rest of the frame.	
		- **Length** : 7 bytes
		- **Bit pattern** : 10101010 * 7(times)
	2. SFD (Start Frame Delimiter)
		- Shows the end of the preamble and the beginning of the rest of the frame.
		- **Length** : 1 byte
		- **Bit pattern** : 10101011
	3. Destination
		-  Indicates the destination device's MAC (Media Access Control) address.
		- **Length** : 6 bytes
	4. Source
		-  Indicates the sender device's MAC (Media Access Control) address.
		- **Length** : 6 bytes
	 5. Type / Length
		 - If the value in this field 1500 or less, then it shows the **Length** of the encapsulated packet in bytes.However, if the value is 1536 or greater than that, then it indicates the **TYPE** of the encapsulated packet, and the length of the packet is determined via other methods.
		 - **Length** : 2 bytes
- Field inside the Ethernet trailer:
	1. FCS (Frame Check Sequence)
	- Its main purpose is to detect corrupted data by running the CRC (Cyclic Redundancy Check) algorithm over the received data.
	- **Length** : 4 bytes


- Even though the **Preamble** and **SFD** fields send with every Ethernet header, they usually not considered as part of it.the Ethernet header consists of three fields: **Destination**, **Source**, **Type/Length**.Therefore, the size of the ethernet header + ethernet trailer is 18 bytes.

- The minimum size of an Ethernet frame (Ether header+payload+Ethernet trailer) is 64 bytes.Thus, the minimum size of the L3 PDU (packet) is 46 bytes.However if you send a packet that is less than 46 bytes , padding bytes (zeros) are added to maintain the balance.