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


















