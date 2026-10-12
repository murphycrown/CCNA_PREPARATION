### Ethernet Standards (Copper)

| Speed    | Common Name      | IEEE Standard | Informal Name | Maximum Length |
| :------- | :--------------- | :------------ | :------------ | :------------- |
| 10 Mbps  | Ethernet         | 802.3i        | 10BASE-T      | 100 m          |
| 100 Mbps | Fast Ethernet    | 802.3u        | 100BASE-T     | 100 m          |
| 1 Gbps   | Gigabit Ethernet | 802.3ab       | 1000BASE-T    | 100 m          |
| 10 Gbps  | 10 Gig Ethernet  | 802.3an       | 10GBASE-T     | 100 m          |
- **BASE-T** : BASE refers to baseband signalling and T means twisted pair.
### UTP cables

UTP (Unshielded Twisted Pair)  cables have no metallic shields which can make them vulnerable to electrical interference.They consists of cables that are twisted to each other which protects them against EMI (Electromagnetic interference).
#### 10BASE-T and 100BASE-T
10BASE-T AND 100BASE-T use 2 pairs (4 wires) to transmit (Tx) and receive (Rx) data.The table below shows which devices use which pins of the 10BASE-T (Ethernet) or the 100BASE-T(Fast Ethernet) cables.

| **Device Type** | **Transmit (Tx) Pins** | **Receive (Rx) Pins** |
| --------------- | ---------------------- | --------------------- |
| **Router**      | 1 and 2                | 3 and 6               |
| **Firewall**    | 1 and 2                | 3 and 6               |
| **PC**          | 1 and 2                | 3 and 6               |
| **Switch**      | 3 and 6                | 1 and 2               |
- UTP copper cables have two types: straight-through and crossover.
	1. **Straight-through** cables connects pin on one end straight to the pin on the other end.They are useful for connecting devices that use different pins for transmitting and receiving data.
	2. **Crossover** cables don't connect one pain straight to the same pin on the other end.They connect pin 1 to pin 3 and pin 2 to pin 6.They are used for connecting devices that use same pins for transmitting and receiving data.
- **Full-Duplex transmission** means that both device can send and receive data at the same time.
##### AUTO MDI-X
Even though, it is important to use the right cable while connecting devices, modern devices solve this problem by adopting a feature called AUTO MDI-X.AUTO MDI-X allows devices to detect which pins their neighbor transmitting data on and adjust which pins they use to transmit ans receive data.So, if we connect two switches that support AUTO MDI-X with straight-through copper cable, they can communicate with each other without any issue.
#### 1000BASE-T AND 10GBASE-T
1000BASE-T and 10GBASE-T cables use all 4 pairs to transmit and receive data.The pins are paired as follows: 1 and 2, 3 and 6 ,4 and 5, 7 and 8.In Gigabit Ethernet and 10 Gigabit Ethernet cables each pair is bidirectional meaning they are not specifically dedicated for receiving or transmitting data.That's what enables them to operate in much higher speed.
### Fiber-Optic cables
Fiber-Optic cables send lights over glass fibers.They have two connector in each end,one to transmit and another to receive data.
![[fiber-optic.jpg]]Fiber-optic cables consist of 4 parts:
1. fiberglass core where the light is sent
2. cladding that reflects light
3. coating - a protective buffer
4. Strength member - prevents the cable to snap easily under tension
5. Outer jacket - protects the inner layers from the environment
- Instead of using RJ-45 ports, Fiber-optic cables use SFP(Small Form-Factor Pluggable) ports .
There are two types of fiber-optic cables: single-mode and multimode.
#### Multimode fiber-optic cables
* In Multimode cables, diameter of fiberglass core is wider than single-mode cables.It allows multiple angles(modes) of light waves to enter the core
- the length of multimode cables are longer than UTP cables ,but shorter than single-mode cables.
- They are cheaper than single-mode fiber due to cheaper LED-based SFP transmitters.
#### Single-Mode fiber-optic cables
- Fiberglass core diameter is narrower than multimode fibers.
- Light enters at a single angle(mode) from a laser-based transmitter.
- the length of single-mode cables are longer than both UTP and multimode cables.
- They are more expensive than multimode fiber due to laser-based SFP transmitters.
### Fiber-Optic Cable Standards

| Informal Name   | IEEE Standard |  Speed  | Cable Type               |          Maximum Length |
| :-------------- | :-----------: | :-----: | :----------------------- | ----------------------: |
| **1000BASE-LX** |    802.3z     | 1 Gbps  | Multimode or Single-Mode | 550 m (MM)<br>5 km (SM) |
| **10GBASE-SR**  |    802.3ae    | 10 Gbps | Multimode                |                   400 m |
| **10GBASE-LR**  |    802.3ae    | 10 Gbps | Single-Mode              |                   10 km |
| **10GBASE-ER**  |    802.3ae    | 10 Gbps | Single-Mode              |                   30 km |
