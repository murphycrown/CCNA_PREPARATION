**ARP (Address Resolution Protocol)** plays an important role in local area networks (LANs). To build a Layer 2 frame, a sending host needs the destination MAC address, which is where ARP comes into play. It provides the ability to broadcast a request to the entire network to discover a specific target's MAC address. Because ARP operates at Layer 2.5, its messages are encapsulated directly within Ethernet frames.

Imagine **Host A (192.168.1.1)** wants to communicate with **Host B (192.168.1.2)**, but does not have Host B's MAC address in its table:

- **Step 1:** Host A constructs a frame, setting the destination MAC address to `FF:FF:FF:FF:FF:FF` (Layer 2 Broadcast). Inside this frame, it encapsulates an ARP Request containing `Source IP: 192.168.1.1` and `Target IP: 192.168.1.2`.

- **Step 2:** Host A transmits this broadcast frame across the local network.

- **Step 3:** Every connected device's NIC receives the frame, recognizes the broadcast MAC address, and passes the payload up to the Operating System.

- **Step 4:** Non-target devices drop the request. Host B's OS inspects the Target IP field, confirms it matches its own IP address, and crafts a unicast ARP response frame containing its MAC address.

- **Step 5:** Host A receives the response frame and updates its ARP table with the target MAC address of `192.168.1.2`.

You can see an example walkthrough from Cisco Packet Tracer in [[ARP_ICMP_FLOW.canvas]].