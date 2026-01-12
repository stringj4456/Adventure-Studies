# Chapter 2: Fundamentals of Ethernet LANs

**Same-layer interaction**: The two computers use a protocol to communicate with the same layer on another computer. The protocol defines a header that communicates what each computer wants to do

**Adjacent-layer interaction**: On a single computer, one lower layer provides a service to the layer just above. The software or hardware that implements the higher layer requests that the next lower layer perform the needed function

## Transmitting Data Using Twisted Pairs
- To send data, the two devices follow some rules called an **encoding scheme**
  - The idea works a lot like when two people talk using the same language
  - The speaker says some words in a particular language, and the listener, because she speaks the same language, can understand the spoken words
- With an encoding scheme, the transmitting node changes the electrical signal over time, while the other node, the receiver, using the same rules, interprets those changes as either 0s or 1s
- For example, 10BASE-T uses an encoding scheme that encodes a binary 0 as a transition from higher voltage to lower voltage during the middle of a 1/10,000,000th-of-a-second interval
- Note that in an actual UTP cable, the wires will be twisted together, instead of being parallel
- Twisting the wire pairs together helps cancel out most of the EMI, so most networking physical links that use copper wires use twisted pairs
- EMI between wire pairs in the same cable is called **crosstalk**

## Breaking Down a UTP Ethernet Link
- The term **Ethernet link** refers to any physical cable between two Ethernet nodes
- The 10BASE-T and 100BASE-T standards require two pairs of wires, while the 1000BASE-T standard requires four pairs
- Each wire has a color-coded plastic coating, with the wires in a pair having a color scheme
- For example, for the blue wire pair, one wire’s coating is all blue, while the other wire’s coating is blue and-white striped
- Many Ethernet UTP cables use an RJ-45 connector on both ends
- The RJ-45 connector has eight physical locations into which the eight wires in the cable can be inserted, called pin positions, or simply pins
- Some Cisco switches include physical ports whose port hardware (the transceiver) can be changed later, after you purchase the switch
- An example of this is SFP and SFP+

## Straight Through Cable Pinout
- 10BASE-T and 100BASE-T use two pairs of wires in a UTP cable, one for each direction, as shown in Figure 2-9
- The figure shows four wires, all of which sit inside a single UTP cable that connects a PC and a LAN switch
- In this example, the PC on the left transmits using the top pair, and the switch on the right transmits using the bottom pair

<img src="images/ch1/transmit.png" alt="" width="50%"/>  

- As a rule, Ethernet NIC transmitters use the pair connected to pins 1 and 2; the NIC receivers use a pair of wires at pin positions 3 and 6
- LAN switches, knowing those facts about what Ethernet NICs do, do the opposite:
  - Their receivers use the wire pair at pins 1 and 2, and their transmitters use the wire pair at pins 3 and 6
- The switch effectively reverses the transmit and receive logic of the endpoint device
- To make the preceding logic work, the UTP cable must use a **straight-through cable** pinout convention
- An Ethernet straight through cable connects the wire at pin 1 on one end of the cable to pin 1 at the other end of the cable; the wire at pin 2 needs to connect to pin 2 on the other end of the cable; pin 3 on one end connects to pin 3 on the other, and so on
- Figure 2-10 shows the concept of straight-through pinout with two pairs—one pair at pins 1,2 and another at pins 3,6, as used by 10BASE-T and 100BASE-T:

<img src="images/ch1/straight-through.png" alt="" width="50%"/>  

- A straight-through cable works correctly when the nodes use opposite pairs for transmitting data
- However, when connecting two devices that transmit on the same pins, you then need another type of cabling pinout called a crossover cable pinout
- The crossover cable pinout crosses the pair at the transmit pins on each device to the receive pins on the opposite device
- Figure 2-11 shows this:

<img src="images/ch1/crossover.png" alt="" width="52%"/>

## Choosing the Right Cable Pinouts
- The key is to know whether a device acts like a PC NIC, transmitting at pins 1 and 2, or like a switch, transmitting at pins 3 and 6. Then, just apply the following logic: 
  - Crossover cable: If the endpoints transmit on the same pin pair 
  - Straight-through cable: If the endpoints transmit on different pin pairs
- Table 2-3 lists the devices and the pin pairs they use, assuming that they use 10BASE-T and 100BASE-T

<img src="images/ch1/table.png" alt="" width="50%"/>

- Figure 2-12 shows a campus LAN in a single building. In this case, several straight-through cables are used to connect PCs to switches. In addition, the cables connecting the switches require crossover cables:

<img src="images/ch1/campus.png" alt="" width="50%"/>

## Automatic Rewiring with Auto-MDIX
- If the link needs a crossover cable, but the installer connected a straight-through cable, this feature can sense the incorrect pinout, and then redirect the electrical signals to the correct pairs to compensate so that the link works
- The Ethernet standard calls this feature automatic medium-dependent interface crossover (auto-MDIX)
- Auto-MDIX allows sites to use straight-through pinouts on all cables
- On the links that need a crossover pinout, the auto-MDIX on the switch port will sense the use of the straight-through pinout and then internally swap the pairs used by the transceiver to make the link work

## UTP Cabling Pinouts for 1000BASE-T
- 1000BASE-T requires four wire pairs and it also uses more advanced electronics that allow both ends to transmit and receive simultaneously on each wire pair
- The wiring pinouts for 1000BASE-T work almost identically to the earlier standards, adding details for the additional two pairs
- The straight-through cable for 1000BASE-T uses the four wire pairs to create four circuits, but the pins need to match
- It uses the same pinouts for two pairs as do the 10BASE-T and 100BASE-T standards, and it adds a pair at pins 4 and 5 and another pair at pins 7 and 8, as shown in Figure 2-13

<img src="images/ch1/1000base.png" alt="" width="50%"/>

- 1000BASE-T (Gigabit Ethernet) uses straight-through cable pinout for some links but crossover cables in other cases
- The Gigabit Ethernet crossover cable crosses pairs A and B in the figure (the pairs at pins 1,2 and 3,6) and also pairs C and D (the pair at pins 4,5 with the pair at pins 7,8)

## Fiber Cabling Transmission Concepts
- Fiber-optic cabling uses glass as the medium through which light passes, varying that light over time to encode 0s and 1s
- Fiber-optic cables use fiberglass, which allows a manufacturer to spin a long thin string (fiber) of flexible glass
- A fiber-optic cable holds the fiber in the middle of the cable, allowing the light to pass through the glass
- Figure 2-14 shows a cutout with the components of a fiber cable for perspective

<img src="images/ch1/fiber.png" alt="" width="50%"/>

- The three outer layers of the cable protect the interior of the cable and make the cables easier to install and manage, while the inner cladding and core work together to create the environment to allow transmission of light over the cable
- A light source, called the **optical transmitter**, shines a light into the core
- Light can pass through the core; however, light reflects off the cladding back into the core
- Figure 2-15 shows an example with a light-emitting diode (LED) transmitter. You can see how the cladding reflects the light back into the core as it travels through the core: 

<img src="images/ch1/mmf.png" alt="" width="50%"/>

- The figure shows the normal operation of a **multimode fiber**, characterized by the fact that the cable allows for multiple angles (modes) of light waves entering the core
- In contrast, **single-mode fiber** uses a smaller-diameter core, around one-fifth the diameter of common multimode cables
- To transmit light into a much smaller core, a laser-based transmitter sends light at a single angle (hence the name single-mode)

<img src="images/ch1/smf.png" alt="" width="50%"/>

- Multimode improves the maximum distances over UTP, and it uses less expensive transmitters as compared with single-mode
- To transmit between two devices, you need two cables, one for each direction
- Note that the transmit port on one device connects to a cable that connects to a receive port on the other device, and vice versa with the other cable

## Using Fiber with Ethernet
- To use fiber with Ethernet switches, you need to use a switch with either built-in ports that support a particular optical Ethernet standard, or a switch with modular ports that allow you to change the Ethernet standard used on the port

<img src="images/ch1/fiberstandards.png" alt="" width="50%"/>

- Although distance might be the first criterion to consider when thinking about whether to use UTP or fiber cabling, a few other tradeoffs exist as well
- UTP wins again on cost, because the cost goes up as you move from UTP, to multimode, and then to single-mode, due to the extra cost for the transmitters like the SFP and SFP+ modules
- UTP has some negatives, however. First, UTP might work poorly in some electrically noisy environments such as factories, because UTP can be affected by electromagnetic interference (EMI)
- Also, UTP cables emit a faint signal outside the cable, so highly secure networks may choose to use fiber, which does not create similar emissions, to make the network more secure

<img src="images/ch1/cablecompare.png" alt="" width="50%"/>

## Ethernet Data Link Protocols
- The Ethernet data-link protocol defines the Ethernet frame: an Ethernet header at the front, the encapsulated data in the middle, and an Ethernet trailer at the end
- Ethernet actually defines a few alternate formats for the header, with the frame format shown in Figure 2-18 being commonly used today:

<img src="images/ch1/ethheader.png" alt="" width="50%"/>

- Table 2-6 lists the fields in the header and trailer and a brief description for reference:

<img src="images/ch1/fields.png" alt="" width="50%"/>

## Ethernet Addressing
- Ethernet addresses, also called Media Access Control (MAC) addresses, are 6-byte long (48-bit-long) binary numbers
- Most MAC addresses represent a single NIC or other Ethernet port, so these addresses are often called a unicast Ethernet address
- Before a manufacturer can build Ethernet products, it must ask the IEEE to assign the manufacturer a universally unique 3-byte code, called the **organizationally unique identifier (OUI)**
- The manufacturer agrees to give all NICs (and other Ethernet products) a MAC address that begins with its assigned 3-byte OUI
- The manufacturer also assigns a unique value for the last 3 bytes, a number that manufacturer has never used with that OUI

<img src="images/ch1/mac.png" alt="" width="50%"/>

- In addition to unicast addresses, Ethernet also uses group addresses
- The IEEE defines two general categories of group addresses for Ethernet:
  - **Broadcast address**: Frames sent to this address should be delivered to all devices on the Ethernet LAN. It has a value of FFFF.FFFF.FFFF
  - **Multicast addresses**: Frames sent to a multicast Ethernet address will be copied and forwarded to a subset of the devices on the LAN that volunteers to receive frames sent to a specific multicast address

## Identifying Network Layer Protocols with the Ethernet Type Field 
- The Ethernet Type field, or EtherType, sits in the Ethernet data-link layer header, but its purpose is to directly help the network processing on routers and hosts
- Basically, the Type field identifies the type of network layer (Layer 3) packet that sits inside the Ethernet frame
- The original host has a place to insert a value (a hexadecimal number) to identify the type of packet encapsulated inside the Ethernet frame
- IEEE manages a list of EtherType values, so that every network layer protocol that needs a unique EtherType value can have a number
- The sender just has to know the list (Anyone can view the list; just go to www.ieee.org and search for EtherType)
- For example, a host can send one Ethernet frame with an IPv4 packet and the next Ethernet frame with an IPv6 packet. Each frame would have a different Ethernet Type field value, using the values reserved by the IEEE, as shown in Figure 2-20:

<img src="images/ch1/ethertype.png" alt="" width="50%"/>

## Error Detection with FCS
- The Ethernet Frame Check Sequence (FCS) field in the Ethernet trailer—the only field in the Ethernet trailer—gives the receiving node a way to compare results with the sender, to discover whether errors occurred in the frame
- The sender applies a complex math formula to the frame before sending it, storing the result of the formula in the FCS field
- The receiver applies the same math formula to the received frame
- The receiver then compares its own results with the sender’s results. If the results are the same, the frame did not change; otherwise, an error occurred and the receiver discards the frame
- Ethernet defines that the errored frame should be discarded, but Ethernet does not attempt to recover the lost frame

## Sending in Modern Ethernet LANs Using Full Duplex
- **Half duplex**: The device must wait to send if it is currently receiving a frame; in other words, it cannot send and receive at the same time
- **Full duplex**: The device does not have to wait before sending; it can send and receive at the same time

## Using Half Duplex with LAN Hubs
- LAN hubs forward data using physical layer standards rather than data-link standards and are therefore considered to be Layer 1 devices
- When an electrical signal comes in one hub port, the hub repeats that electrical signal out all other ports (except the incoming port)
- The downside of using LAN hubs is that if two or more devices transmitted a signal at the same instant, the electrical signals collide and become garbled
- To prevent these collisions, the Ethernet nodes must use half-duplex logic instead of full-duplex logic
- Half-duplex logic tells the nodes that if someone else is sending, wait before sending
- Nodes that use half-duplex logic actually use a relatively well-known algorithm called carrier sense multiple access with collision detection (CSMA/CD)
- The algorithm takes care of the obvious cases but also the cases caused by unfortunate timing
- How CSMA/CD works:
  1. A device with a frame to send listens until the Ethernet is not busy
  2. When the Ethernet is not busy, the sender begins sending the frame
  3. The sender listens while sending to discover whether a collision occurs; collisions might be caused by many reasons, including unfortunate timing. If a collision occurs, all currently sending nodes do the following:
     - They send a jamming signal that tells all nodes that a collision happened
     - They independently choose a random time to wait before trying again, to avoid unfortunate timing
     - The next attempt starts again at Step 1
- For all links between PCs and switches, or between switches, use full duplex
- However, for any link connected to a LAN hub, the connected LAN switch and NIC port should use half duplex

# Leased Line WANS
- To connect LANs using a WAN, the internetwork uses a router connected to each LAN, with a WAN link between the routers
- For the WAN link, the enterprise’s network engineer must do some planning and then order some kind of WAN link from a WAN service provider
- That provider installs the WAN link between the two routers, as shown in Figure 3-1:

<img src="images/ch1/leasedline.png" alt="" width="50%"/>

- The leased line service, a physical layer service, delivers bits in both directions, at a predetermined speed, using full-duplex logic
- The leased line uses two pairs of wires, one pair for each direction of sending data, which allows full-duplex operation

<img src="images/ch1/leasedline2.png" alt="" width="50%"/>

- To create a leased line, some physical path must exist between the two routers on the ends of the link
- The physical cabling must leave the customer buildings where each router sits; however, the telco does not simply install one cable between the two buildings
- Instead, it uses what is typically a large and complex network that creates the appearance of a cable between the two routers
- Figure 3-3 shows a conceptual view of a small part of the telco network
- Telcos put their equipment in buildings called central offices (COs). The telco installs cables from the CO to most every other building in the city, expecting to sell services to the people in those buildings one day
- The telco would then configure its switches to use some of the capacity on each cable to send data in both directions, creating the equivalent of a crossover cable between the two routers

<img src="images/ch1/leasedline3.png" alt="" width="50%"/>

- The term leased line emphasizes the fact that the telco leases the use of the leased line to a customer, but the customer does not permanently own the line
- Many names exist for leased lines including:
  - **Leased circuit, Circuit**: The words line and circuit are often used as synonyms in telco terminology; circuit makes reference to the electrical circuit between the two endpoints
  - **Serial link, Serial line**: The words link and line are also often used as synonyms. Serial in this case refers to the fact that the bits flow serially and that routers use serial interfaces
  - **Point-to-point link, Point-to-point line**: These terms refer to the fact that the topology stretches between two points, and two points only (Some older leased lines allowed more than two devices)
  - **T1**: This specific type of leased line transmits data at 1.544 megabits per second (1.544 Mbps)
  - **WAN link, Link**: Both of these terms are very general, with no reference to any specific technology
  - **Private line**: This term refers to the fact that the data sent over the line cannot be copied by other telco customers, so the data is private

## Data-Link Details of Leased Lines 
- A leased line provides a Layer 1 service
- Routers on the ends of the line use one of two data-link protocols: High Level Data Link Control (HDLC) or Point-to-Point Protocol (PPP)
- All data-link protocols perform a similar role: to control the correct delivery of data over a physical link of a particular type
- For example, the Ethernet data-link protocol uses a destination address field to identify the correct device that should receive the data and an FCS field that allows the receiving device to determine whether the data arrived correctly
- Figure 3-4 shows the HDLC frame format as an example, with Table 3-3 that follows describing the fields
- However, note that HDLC and PPP have a similar frame format, although the newer PPP (defined in the 1990s) has more features and functions (plus additional optional headers) than the older HDLC (defined in the 1970s)

<img src="images/ch1/hdlc.png" alt="" width="45%"/>

<img src="images/ch1/hdlc2.png" alt="" width="50%"/>

## How Routers Use a WAN Data Link
- Leased lines connect to routers, and routers focus on delivering packets to a destination host
- However, routers physically connect to both LANs and WANs, with those LANs and WANs requiring that data be sent inside data-link frames
- The TCP/IP network layer focuses on forwarding IP packets from the sending host to the destination host. The underlying LANs and WANs just act as a way to move the packets to the next router or end-user device
- Figure 3-6 shows some of the data-link layer logic used by the hosts and routers
- Basically, three separate data-link layer steps encapsulate the packet, inside a data-link frame, over three hops through the internetwork: from PC1 to R1, from R1 to R2, and from R2 to PC2

<img src="images/ch1/routewan.png" alt="" width="52%"/>

- Following the steps in the figure, again for a packet sent by PC1 to PC2’s IP address: 
  1. To send the IP packet to Router R1 next, PC1 encapsulates the IP packet in an Ethernet frame that has the destination MAC address of R1
  2. Router R1 de-encapsulates (removes) the IP packet from the Ethernet frame, encapsulates (inserts) the packet into an HDLC frame using an HDLC header and trailer, and forwards the HDLC frame to Router R2 next
  3. Router R2 de-encapsulates (removes) the IP packet from the HDLC frame, encapsulates (inserts) the packet into an Ethernet frame that has the destination MAC address of PC2, and forwards the Ethernet frame to PC2
- In summary, a leased line with HDLC creates a WAN link between two routers so that they can forward packets for the devices on the attached LANs
- The leased line itself provides the physical means to transmit the bits, in both directions
- The HDLC frames provide the means to encapsulate the network layer packet correctly so that it crosses the link between routers
- By today’s standards, leased-line WAN links are slow, with the fastest leased line speeds in the tens of megabits per second (Mbps)

## Ethernet as a WAN Technology
- Today, many WAN service providers (SP) offer WAN services that take advantage of Ethernet
- SPs offer a wide variety of these Ethernet WAN services, with many different names. But all of them use a similar model, with Ethernet used between the customer site and the SP’s network, as shown in Figure 3-7

<img src="images/ch1/ethwan.png" alt="" width="52%"/>

- The customer connects to an Ethernet link using a router interface
- The (fiber) Ethernet link leaves the customer building and connects to some nearby SP location called a point of presence (PoP)
- Inside the SP’s network, the SP uses any technology that it wants to create the specific Ethernet WAN services

## Ethernet WANs That Create a Layer 2 Service 
- The most basic Ethernet WAN service, one that works much like an Ethernet crossover cable—just over a WAN. In other words: 
  - Logically, behaves like a point-to-point connection between two routers
  - Physically, behaves as if a physical fiber Ethernet link existed between the two routers 
- Common Ethernet WAN service names:
  - **Ethernet WAN**: A generic name to differentiate it from an Ethernet LAN
  - **Ethernet point-to-point link**: A term that emphasizes the topology of a typical Ethernet WAN link that has exactly two endpoints: the routers on the two ends of the link
  - **Ethernet Line Service (E-Line)**: A term from the Metro Ethernet Forum (MEF) for the kind of point-to-point Ethernet WAN service shown throughout this book
  - **Ethernet over MPLS (EoMPLS)**: A term that refers to Multiprotocol Label Switching (MPLS), a technology that can be used to create the Ethernet service for the customer
- If you can imagine two routers, with a single Ethernet link between the two routers, you understand what this particular Ethernet WAN service does, as shown in Figure 3- 8
- In this case, the two routers, R1 and R2, connect with an Ethernet WAN service instead of a serial link
- The routers use Ethernet interfaces, and they can send data in both directions at the same time
- Physically, each router actually connects to some SP PoP, as shown earlier in - Figure 3-7, but logically, the two routers can send Ethernet frames to each other over the link

<img src="images/ch1/ethwan2.png" alt="" width="55%"/>

## How Routers Route IP Packets Using Ethernet WAN Links
- WANs, by their very nature, give IP routers a way to forward IP packets from a LAN at one site, over the WAN, and to another LAN at another site
- The routing logic works the same whether the WAN link happens to be a serial link or an Ethernet WAN link, with the encapsulation details being slightly different
- With an Ethernet WAN link, the link uses Ethernet for both Layer 1 and Layer 2 functions, so the routers encapsulate using the familiar Ethernet header and trailer, as shown in the middle of Figure 3-9

<img src="images/ch1/ethwan3.png" alt="" width="52%"/>

- The figure shows the same three routing steps as shown with the serial link in the earlier Figure 3-6
- In this case, all three routing steps use the same Ethernet (802.3) protocol, however note that each frame’s data-link header and trailer are different
- Each router discards the old data-link header/trailer and adds a new set, as described in these steps:
  1. To send the IP packet to Router R1 next, PC1 encapsulates (inserts) the IP packet in an Ethernet frame that has the destination MAC address of R1. 
  2. Router R1 de-encapsulates (removes) the IP packet from the Ethernet frame and encapsulates (inserts) the packet into a new Ethernet frame, with a new Ethernet header and trailer. The destination MAC address is R2’s G0/0 MAC address, and the source MAC address is R1’s G0/1 MAC address. R1 forwards this frame over the Ethernet WAN service to R2 next
  3. Router R2 de-encapsulates (removes) the IP packet from the Ethernet frame, encapsulates (inserts) the packet into an Ethernet frame that has the destination MAC address of PC2, and forwards the Ethernet frame to PC2

## How Network Layer Routing Uses LANs and WANs 
- The following list summarizes the major steps in a router’s internal network layer routing for each packet beginning with the frame arriving in a router interface: 
  1. Use the data-link Frame Check Sequence (FCS) field to ensure that the frame had no errors; if errors occurred, discard the frame
  2. Assuming that the frame was not discarded at Step 1, discard the old datalink header and trailer, leaving the IP packet
  3. Compare the IP packet’s destination IP address to the routing table, and find the route that best matches the destination address. This route identifies the outgoing interface of the router and possibly the next-hop router IP address
  4. Encapsulate the IP packet inside a new data-link header and trailer, appropriate for the outgoing interface, and forward the frame
- Figure 3-11 works through an example of a packet sent by PC1 to PC2, followed by a detailed analysis of each device’s routing logic:

<img src="images/ch1/routing.png" alt="" width="50%"/>

## The IP Header
<img src="images/ch1/ipheader.png" alt="" width="50%"/>

## How IP Routing Protocols Help IP Routing 
- The best method for routers to know all the useful routes is to configure the routers to use the same IP routing protocol
- If you enable the same routing protocol on all the routers in a TCP/IP internetwork, with the correct settings, the routers will send routing protocol messages to each other
- As a result, all the routers will learn routes for all the IP networks and subnets in the TCP/IP internetwork
- All the routing protocols use the same general steps for learning routes:
  1. Each router, independent of the routing protocol, adds a route to its routing table for each subnet directly connected to the router
  2. Each router’s routing protocol tells its neighbors about the routes in its routing table, including the directly connected routes and routes learned from other routers
  3. Each router’s routing protocol listens to messages from neighboring routers and learns routes, with the next-hop router of that route typically being the neighbor from which the route was learned
- Note that at the final step, routers may have to choose between multiple routes to reach a single subnet
- When that happens, routers place the best currently available route to reach a subnet (based on a measurement called a metric) into the routing table
- Figure 3-13 shows an example of how a routing protocol works

<img src="images/ch1/routingprotocol.png" alt="" width="50%"/>

- Below lists out the steps for the above image
  - Subnet 150.150.4.0 exists as a subnet at the bottom of the figure, connected to Router R3
  - R3 adds a connected route for 150.150.4.0 to its IP routing table; this happens without help from the routing protocol
  - R3 sends a routing protocol message, called a routing update, to R2, causing R2 to learn about subnet 150.150.4.0
  - R2 adds a route for subnet 150.150.4.0 to its routing table
  - R2 sends a similar routing update to R1, causing R1 to learn about subnet 150.150.4.0
  - R1 adds a route for subnet 150.150.4.0 to its routing table. The route lists R1’s own Serial0 as the outgoing interface and R2 as the next-hop router IP address (150.150.2.7)

## The Address Resolution Protocol
- TCP/IP defines the Address Resolution Protocol (ARP) as the method by which any host or router on a LAN can dynamically learn the MAC address of another IP host or router on the same LAN
- ARP defines a protocol that includes the ARP Request, which is a message that makes the simple request “if this is your IP address, please reply with your MAC address”
- ARP also defines the ARP Reply message, which indeed lists both the original IP address and the matching MAC address
- The figure shows the ARP Request sent by router R3, on the left of the figure, as a LAN broadcast
- All devices on the LAN will then process the received frame
- On the right, at Step 2, host PC2 sends back an ARP Reply, identifying PC2’s MAC address

<img src="images/ch1/arp.png" alt="" width="50%"/>

- Hosts and routers remember the ARP results, keeping the information in their ARP cache or ARP table
- A host or router only needs to use ARP occasionally, to build the ARP cache the first time
- Each time a host or router needs to send a packet encapsulated in an Ethernet frame, it first checks its ARP cache for the correct IP address and matching MAC address
- Hosts and routers will let ARP cache entries time out to clean up the table, so occasional ARP Requests can be seen
- You can see the contents of the ARP cache on most PC operating systems by using the **arp -a** command from a command prompt

## Accessing the IOS XE CLI
- To create IOS XE, Cisco took IOS and modernized the internal software architecture
- IOS XE, often referred to simply as XE, has features to improve uptime and the ability to maintain devices without requiring rebooting (reloading) the device
- For the purposes of CCNA, almost everything you see with commands and the CLI applies to older IOS-based switches as well as newer switches that use IOS XE
- The switch CLI can be accessed through three popular methods: the console, Telnet, and Secure Shell (SSH)
- The console is a physical port built specifically to allow access to the CLI
- Console access requires both a physical connection between a PC (or other user device) and the switch’s console port, as well as some software on the PC
- Figure 4-3 depicts the options

<img src="images/ch1/console.png" alt="" width="50%"/>

## Cabling the Console Connection
- The physical console connection, both old and new, uses three main components: the physical console port on the switch, a physical serial port on the PC, and a cable that works with the console and serial ports
- Most PCs today use a familiar standard USB connector for the console connection (often a USB mini-B connector on the switch)
- In the simplest form, you can use any USB port on the PC, with a USB cable, connected to the USB console port on the switch or router
 
<img src="images/ch1/consoleconnect.png" alt="" width="50%"/>

- The case on the far left in the figure shows an older console connection, typical of how you would have connected to a switch over ten years ago
- Before PCs used USB ports, they used serial ports for serial communications
- The PC serial port had a D-shell connector (roughly rectangular) with nine pins (often called a DB-9)
- The console port looks like any Ethernet RJ-45 port (but is typically colored in blue and with the word console beside it on the switch)
- The older-style cabling used a standard RJ-45 to DB-9 converter plug and a UTP rollover cable with RJ-45 connectors on each end
- The rollover pinout uses eight wires, rolling the wire at pin 1 to pin 8, pin 2 to pin 7, pin 3 to pin 6, and so on
- The center case in the figure shows a variation that you might use on occasion that combines the cabling concepts from the left and right cases in the figure
- You use the USB port on your PC but the RJ-45 console port on the switch
- In fact, for some very old switch models, the switch has only an RJ-45 console port but no USB console port, requiring this kind of console cabling
- In this case, you need a USB converter plug that converts from the older rollover console cable (with RJ-45 connectors) to a USB connector
- When using the USB options, you typically also need to install a software driver so that your PC’s OS knows that the device on the other end of the USB connection is the console of a Cisco device

## Configuring a Terminal Emulator 
- After the PC is physically connected to the console port, a terminal emulator software package must be installed and configured on the PC
- The terminal emulator software treats all data as text. It accepts the text typed by the user and sends it over the console connection to the switch
- Similarly, any bits coming into the PC over the console connection are displayed as text for the user to read
- The emulator must be configured to use the PC’s serial port to match the settings on the switch’s console port settings
- The default console port settings on a switch are as follows
  - 9600 bits/second
  - No hardware flow control 
  - 8-bit ASCII
  - No parity bits
  - 1 stop bit
- Note that the last three parameters are referred to collectively as 8N1

## User and Enable (Privileged) Modes
- All three CLI access methods covered so far (console, Telnet, and SSH) place the user in an area of the CLI called user EXEC mode
- User EXEC mode, sometimes also called **user mode**, allows the user to look around but not break anything
- Cisco IOS supports a more powerful EXEC mode called privileged mode (also known as **enable mode**)
- If the command prompt ends with a **>**, the user is in user mode; if it ends with a **#**, the user is in enable mode
- The commands that can be used in either user mode or enable mode are called EXEC commands

## Password Security for CLI Access from the Console
- Simple passwords can be configured at two points in the login process from the console: when the user connects from the console, and when any user moves to enable mode (using the **enable** EXEC command)
- The command **show running-config** lists the current configuration in the switch
- Use **hostname** ***hostname*** to set the switches hostname
- Use **enable secret** ***password*** to define the password that all users must use to reach enable mode
- Use **password** ***password*** to define the password the console user must type when prompted
- **line console 0** is the command that identifies the console, basically meaning “these next commands apply to the console only”
- The **login** command tells IOS to perform simple password checking (at the console)
- Remember, by default, the switch does not ask for a password for console users

## CLI Help Features
- Table 4-3 summarizes command-recall help options available at the CLI
- Note that, in the first column, **command** represents any command. Likewise, **parm** represents a command’s parameter
- For example, the third row lists command **?**, which means that commands such as **show ?** and **copy ?** would list help for the show and copy commands, respectively

<img src="images/ch1/help1.png" alt="" width="50%"/>

- When you enter the ?, the Cisco IOS CLI reacts immediately; that is, you don’t need to press the Enter key or any other keys
- When ? is entered in user mode, the commands allowed in user mode are displayed, but commands available only in enable mode (not in user mode) are not displayed
- Cisco IOS stores the commands that you enter in a history buffer, storing ten commands by default
- The CLI also allows you to move backward and forward in the historical list of commands and then edit the command before reissuing it
- Table 4-4 lists the commands used to manipulate previously entered commands

<img src="images/ch1/help2.png" alt="" width="50%"/>

## The debug and show Commands
- The **show** command has a large variety of options, and with those options, you can find the status of almost every feature of Cisco IOS
- Essentially, the show command lists the currently known facts about the switch’s operational status
  - Ex. **show mac address-table dynamic**
- The **debug** command also tells the user details about the operation of the switch
- However, while the show command lists status information at one instant of time—more like a photograph— the debug command acts more like a live video camera feed
- Once you issue a debug command, IOS remembers, issuing messages over time as events continue to occur
- Any switch user can choose to receive those messages, with the switch sending the messages to the console by default

## Configuring Cisco IOS Software
- Configuration mode accepts configuration commands—commands that tell the switch the details of what to do and how to do it
- User and privileged modes accept EXEC commands, which return output, or possibly take an action like reloading the switch, but commands in these modes do not change any configuration settings
- Commands entered in configuration mode update the active configuration file
- These changes to the configuration occur immediately each time you press the Enter key at the end of a command
- Figure 4-11 illustrates the navigation among configuration mode, user EXEC mode, and privileged EXEC mode

<img src="images/ch1/modes.png" alt="" width="50%"/>

## Configuration Submodes and Contexts
- When using configuration mode, you move from the initial mode—global configuration mode—into subcommand modes
- Context-setting commands move you from one configuration subcommand mode, or context, to another
- These context-setting commands tell the switch the topic about which you will enter the next few configuration commands
- The **interface** command is one of the most commonly used context-setting configuration commands
- For example, the CLI user could enter interface configuration mode by entering the **interface FastEthernet 0/1** configuration command
- Asking for help in interface configuration mode displays only commands that are useful when configuring Ethernet interfaces
- Commands used in this context are called subcommands—or, in this specific case, interface subcommands
- Consider Example 4-4, which shows the following:
  - Movement from enable mode to global configuration mode by using the **configure terminal** EXEC command
  - Use of a **hostname Fred** global configuration command to configure the switch’s name. Using a global command from global configuration mode leaves you in global configuration mode
  - Movement from global configuration mode to console line configuration mode (using the **line console 0** command). The **line** command is another of the small set of context-setting commands that move you to another submode
  - Setting the console’s simple password to hope (using the **password hope** line subcommand). Using a subcommand while in that submode leaves the command prompt in that submode
  - Movement from console configuration mode to interface configuration mode (using the **interface ***type number***** command). The interface command is another of the small set of context-setting commands that move you to another submode
  - Setting the speed to 100 Mbps for interface Fa0/1 (using the **speed 100** interface subcommand)
  - Movement from interface configuration mode back to global configuration mode (using the **exit** command)

<img src="images/ch1/ex4.png" alt="" width="50%"/>

- Table 4-5 shows the most common command prompts in configuration mode, the names of those modes, and the context-setting commands used to reach those modes

<img src="images/ch1/table45.png" alt="" width="50%"/>

- Figure 4-12 shows most of the navigation between global configuration mode and the four configuration submodes listed in Table 4-5

<img src="images/ch1/table412.png" alt="" width="50%"/>

- Generally, Cisco uses global commands for settings that apply to the entire switch and subcommands that apply to one component or feature

## Storing Switch Configuration Files
- To store information that must be retained when the switch loses power or is reloaded, Cisco switches use several types of more permanent memory, none of which has any moving parts
- The following list details the four main types of memory found in Cisco switches, as well as the most common use of each type:
  - **RAM**: Sometimes called DRAM, for dynamic random-access memory, RAM is used by the switch just as it is used by any other computer: for working storage. The running (active) configuration file is stored here 
  - **Flash memory**: Either a chip inside the switch or a removable memory card, flash memory stores fully functional Cisco IOS images and is the default location where the switch gets its Cisco IOS at boot time. Flash memory also can be used to store any other files, including backup copies of configuration files
  - **ROM**: Read-only memory (ROM) stores a bootstrap (or boothelper) program that is loaded when the switch first powers on. This bootstrap program then finds the full Cisco IOS image and manages the process of loading Cisco IOS into RAM, at which point Cisco IOS takes over operation of the switch
  - **NVRAM**: Nonvolatile RAM (NVRAM) stores the initial or startup configuration file that is used when the switch is first powered on and when the switch is reloaded 
- Figure 4-13 summarizes this same information in a briefer and more convenient form

<img src="images/ch1/figure413.png" alt="" width="50%"/>

- Cisco IOS stores the collection of configuration commands in a configuration file
- Switches use multiple configuration files—one file for the initial configuration used when powering on, and another configuration file for the active, currently used running configuration as stored in RAM
- Table 4-6 lists the names of these two files, their purpose, and their storage location

<img src="images/ch1/config.png" alt="" width="50%"/>

- Essentially, when you use configuration mode, you change only the running-config file
- If you want to keep the configuration, you have to copy the running-config file into NVRAM, overwriting the old startup-config file


























