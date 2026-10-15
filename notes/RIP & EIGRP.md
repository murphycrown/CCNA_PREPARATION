## RIP (Routing Information Protocol)

- It is an industry standard protocol.
- It is a distance vector IGP protocol (uses routing by rumor logic to learn or share routes).
- Uses **hop count** as its metric.One router = one hop (bandwidth is irrelevant).
- The maximum **hop count** is 15.Anything more than that is considered unreachable.

- It has three versions:
	1. RIPv1 and RIPv2, used for IPv4.
	2. RIPng (RIP Next Generation)  used for IPv6.

- Uses two message types:
	1. **Request :** RIP asks neighbor routers to send their routing tables.
	2. **Response :** To send the local router's routing table to neighboring routers.

- RIP enabled routers share their routing tables every **30 seconds** by default.

- RIPv1
	1. Only supports classful addresses (Class A, Class B, Class C)
	2. Doesn't support CIDR or VLSM
	3. Doesn't include subnet mask information in advertisements (Response Messages).
- RIPv2
	1. Supports VLSM AND CIDR.
	2. Includes subnet mask information in advertisements.
	3. Messages are multicast to 224.0.0.9
### RIP configuration

1. Use `router rip` command from the Global Configuration Mode to enable RIP.
2. Use `version [2]` to configure RIP version.
3. Use `no auto-summary` to prevent router from converting advertisements into a clasful ip addresses.

4. Use `network [ip-address]` command to configure the ip address.You don't need to configure the subnet mask because command itself is **classful** meaning it automatically converts IP addresses into classful addresses.
	-  `network` command doesn't tells the router which networks to advertise.It tells the router which interfaces to activate RIP on,and then the router will advertise the network prefixes of those interfaces.

5. Use `passive-interface [interface-name]` to configure passive interfaces.
	- If an interfaces connected to the router doesn't have any RIP neighbor, it will be pointless to send RIP advertisement to that interface.That's why we use passive interfaces to reduce unnecessary traffic.

6. Use `default-information originate` command to share the default route with neighboring routers.

7. Use `show ip protocols` to see the detailed information about the protocol is being used.

8. Use `maximum-paths [1]` command to configure the maximum number of paths that a device can use at the same time.

9. Use `distance [120]` command to change the Administrative Distance of a protocol.

## EIGRP (Enhanced Interior Gateway Routing Protocol)

- EIGRP was Cisco proprietary, but Cisco has published online ,so other vendors can implement it on their equipment.
- Considered as an advanced or hybrid distance vector routing protocol.
- Much faster than RIP to reacting changes in the network.
- Does not have the 15 **hop count** limit of RIP.
- Sends messages using multicast address 224.0.0.10.
- EIGRP is the only IGP that can perform unequal-cost load-balancing (by default it perform ECMP load-balancing over 4 paths like RIP).

### EIGRP configuration

1. Type `router eigrp [AS-number]` to configure the EIGRP protocol on the network. 
	- AS (Autonomous System) number must match between routers, or they won't form an adjacency and share route information.
2. Type `no auto-summary` to ensure that the routers advertises actual prefix length instead of classful networks.
3. Use `passive-interface [interface-name]` to configure passive interfaces.
	- If an interfaces connected to the router doesn't have any EIGRP neighbor, it will be pointless to send EIGRP advertisement to that interface.That's why we use passive interfaces to reduce unnecessary traffic.
4. Use `network [172.16.1.0] [0.0.0.15]` to configure the 172.16.1.0/28 network.`[0.0.0.15]` might be a little bit confusing because EIGRP uses **wildcard mask** over normal **subnet mask** .
	- **Wildcard mask** is simply an **inverted** subnet mask.All **0s** in the subnet mask are **1s** in the equivalent wildcard mask.All **0s** in the subnet mask are **1s** in the equivalent wildcard mask.
5. Use `eigrp router-id [1.1.1.1]` command to configure the Router ID.
	- Router ID order of priority:
		1. Manually configuring the Router ID with the command shown above.
		2. Highest IP address on a loopback interface will be configured as the Router ID.
		3. Highest IP address on a physical interfaces will be configured automatically.
6. Use `show ip eigrp neighbors` commands to see the EIGRP neighbors of a router.
7. Use `do show ip eigrp topology` to detailed  version EIGRP topology.
### EIGRP terminology

- By default, EIGRP uses bandwidth and delay to calculate the metric.
- Bandwidth of the slowest link in the topology added by the delay of all links gives us the metric.
- **Feasible Distance** means this router's metric value to the route's destination.
- **Reported Distance** (Advertised Distance) means the neighbor's metric value to the route's destination.
- **Successor** means the route with the lowest metric to the destination (the best route)
- **Feasible Successor** means an alternate route to the destination which meets the **feasibility condition**.Feasibility condition states that a router is considered a **Feasible Successor** if its reported distance is lower than the successor route's feasible distance.
### Unequal-Cost Load-Balancing

- By default, EIGRP uses ECMP(Equal-Cost Multi-Path ).
- Use `variance [number]` command to configure Unequal-Cost Load-Balancing on a router.
	- `variance 2` simply means feasible successor routes with a Feasible Distance up to 2x the successor route's Feasible Distance can be used to load-balance.
	- Note that EIGRP perform unequal-cost load-balancing over feasible successor routes.In order to be used for load-balancing the route must satisfy the feasibility condition.

