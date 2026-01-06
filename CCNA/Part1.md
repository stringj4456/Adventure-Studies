# Chapter 1: Introduction to TCP/IP Networking

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

<img src="images/ch1/crossover.png" alt="" width="50%"/>  



