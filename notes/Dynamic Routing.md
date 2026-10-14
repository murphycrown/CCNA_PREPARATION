- Network route is a route to a network or subnet ( mask length < /32 )
- Host route is a route to a specific host ( mask length = /32 )

Instead of manually configuring routes, we can configure a Dynamic Routing protocol on routers.In addition, configuring dynamic routing ensures that, in case of a physical failure, routers will adapt their routing tables and remove the corresponding routes.

- Categories of dynamic routing protocols:
	1. **IGP** (Interior Gateway Protocol) used to share routes within a single **autonomous system (AS)**
	2. **EGP** (External Gateway Protocol) used to share routes between different **autonomous system (AS)**
- Algorithm types for each protocol that are used to determine the best route:
- **IGP** algoritms:
	1. **Distance vector** used by :
		1. **RIP (Routing Information Protocol)** 
		2. **EIGRP (Enhanced Interior Gateway Routing Protocol)**.
	2. **Link State** used by:
		1. **OSPF (Open Shortest Path First)**
- **EGP** algorithm:
	1. **Path Cost** used by:
		1. **BGP (Border Gateway Protocol)**

- Criteria for choosing the the best route:

1. AD (Administrative Distance) is determined by the Dynamic Routing Protocol that is used.Each protocol has different AD value and the lower one is preferred.

| **Route protocol/type** | **AD** | **Route protocol/type** | **AD** |
| ----------------------- | ------ | ----------------------- | ------ |
| Directly connected      | 0      | IS-IS                   | 115    |
| Static                  | 1      | RIP                     | 120    |
| External BGP (eBGP)     | 20     | EIGRP (external)        | 170    |
| EIGRP                   | 90     | Internal BGP (iBGP)     | 200    |
| IGRP                    | 100    | Unusable route          | 255    |
| OSPF                    | 110    |                         |        |
2. **Metric** determines the cost of reaching the route ( like in the STP).All protocols use different metrics to find the total cost. Lower cost is preferred.

| IGP       | Metric                                         | Explanation                                                                                                                                                                    |
| :-------- | :--------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **RIP**   | Hop count                                      | Each router in the path counts as one 'hop'. The total metric is the total number of hops to the destination. **Links of all speeds are equal.**                               |
| **EIGRP** | Metric based on bandwidth & delay (by default) | Complex formula that can take into account many values. By default, the bandwidth of the **slowest link in the route** and the total delay of all links in the route are used. |
| **OSPF**  | Cost                                           | The cost of each link is calculated based on bandwidth. The total metric is the total cost of each link in the route.                                                          |
| **IS-IS** | Cost                                           | The total metric is the total cost of each link in the route. The cost of each link is **not** automatically calculated by default. All links have a cost of 10 by default.    |

- If all criteria are satisfied, the traffic will be load balanced over both routes and this is called **ECMP(Equal Cost Multi-Path)**.