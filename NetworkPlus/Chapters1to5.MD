
# OSI Model
## Layer 1: Physical Layer

Layer 1 deals with the physical connections between devices. This includes the transmission of bits on the network along with the physical and electrical characteristics of the network. The physical layer defines the following: 

* How to represent bits on the medium
* Wiring standards for connectors and jacks
* Physical topology
* Synchronizing bits
* Bandwidth usage
* Multiplexing strategy
  
### How to represent bits on the medium

Data on a computer network is represented as a binary expression. Electrical voltage (on copper wiring) or light (carried via fiber-optic cabling) can represent these 1s and 0s. 

There are two fundamental ways digital data can be represented using a signal:
1. Current state modulation
2. State transition modulation

In **current state modulation**, data is represented by the current state (or level) of the signal. Each bit corresponds directly to a particular voltage or signal level. For example, the presence or absence of voltage on a wire portrays a binary 1 or a binary 0.

<img src="images/csm.png" alt="current state modulation" width="70%"/>  

<br>

Alternatively, there is **state transition modulation** where data is represented by changes (transitions) in the signal, not by the voltage level itself. The presence or absence of a transition at a specific time represents a bit. For example, a transition from low to high can be represented by a 1 while a high to low transition can be represented by a 0. 

<img src="images/stm.png" alt="state transition modulation" width="70%"/>

### Synchronizing bits
### Bandwidth usage
### Multiplexing strategy
  
