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
- A light source, called the optical transmitter, shines a light into the core
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





