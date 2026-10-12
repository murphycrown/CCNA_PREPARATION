We can think of a network as a combination of devices. Let's look at one of the basic examples of a network. We can make a network by simply connecting two devices (e.g., computers, laptops) together with cables.
We can illustrate how data is transferred between two devices  in several ways:
## **Sending raw data frames**

We will use Docker to demonstrate the data frame transmission between two devices.
#### Step 1 
Create a Docker network and a container that uses this network.
#### Step 2 
Grab the MAC address from the Docker container and use `Scapy` to create a frame and send it.
```python
from scapy.all import Ether, Raw, sendp

# Craft a raw Ethernet frame
frame = Ether(src="de:cd:86:d2:49:3d", dst="d2:dd:fc:9d:4e:49") / Raw(load="Hello directly over Layer 2!")

# Send out a specific physical interface (e.g., eth0)
sendp(frame, iface="br-f53a8d33b467")

```

#### Step 3 
Execute the code and watch the frame from the container using `tcpdump`.
![[Pasted image 20260729195952.png]]
As seen in the output, the frame sent from our host machine arrived successfully inside the container.