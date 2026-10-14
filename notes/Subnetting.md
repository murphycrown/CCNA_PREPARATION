Before reading this article ,review the [[IPv4 addressing]] to understand the topic better.

Subnetting is basically dividing large networks into the small networks.

- IPv4 addresses assigned to the companies by a non-profit organization called IANA (Internet Assigned Numbers Authority) based on their size.
## CIDR (Classless Inter-Domain routing)

 - It is invented my network researchers to prevent the ip addresses being wasted by dividing the network ip addresses into smaller subnets.
 - Even though, it is very  useful because it divides network addresses into fixed-length subnets ,it still wasn't the best way in terms of efficiency.
## VLSM (Variable-Length Subnet Mask)

- This way is the most efficient way when each LAN has different number of hosts.The process of calculating subnets is similar to CIDR, but inhere you must start from the LAN that has the biggest number of hosts to the smallest.
- In VLSM the subnets are not in fixed-length.The subnet decided by the number of devices a LAN has.
 