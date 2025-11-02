# Routers
* Although a router is considered to be a Layer 3 device it has the capability to consider high-layer traffic parameters, such as quality of service (QoS) settings, in making forwarding decisions
* Routers do not forward broadcast packets by default. This means that each port on a router automatically creates a separate broadcast domain
* Each port also creates a separate collision domain
* What is a collision domain? A collision domain represents an area on a LAN on which there can be only one transmission at a time
* Thanks to the elimination of legacy hubs and bridges in the modern network, our networks today feature microsegmentation
* This means we eliminate the possibility of frame collisions by automatically creating tiny collision domains for each port
* Figure 2-1 shows how each port on a router is a separate collision domain and a separate broadcast domain:
  * Notice this figure also shows two Layer 2 switches
  * These devices do not automatically create broadcast domains by default, but they do help microsegment the network
  * Each port on the switch represents a collision domain just like a router
 
  <img src="images/router.png" alt="Routers" width="45%"/>

