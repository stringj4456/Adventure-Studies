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

# Switches
* Layer 2 switches dynamically learn the MAC addresses attached to various ports by looking at the source MAC addresses on frames coming into a port
* Initially, however, a switch is unaware of what MAC addresses reside off which ports (unless MAC addresses have been statically configured)
* Therefore, when a switch receives a frame destined for a MAC address not yet present in the switch’s MAC address table, the switch floods that frame out all the switch ports except the port on which the frame was received
* Similarly, broadcast frames (that is, frames with destination MAC address FFFF.FFFF.FFFF) are always flooded out of all switch ports except the port on which the frame was received
* The reason broadcast frames are always flooded is that no endpoint will have MAC address FFFF.FFFF.FFFF, which means that the FFFF.FFFF.FFFF MAC address will never be learned in a switches MAC address table
  
<br>

* If PC1 does not already have the server’s MAC address in its Address Resolution Protocol (ARP) cache, PC1 can send an ARP request in an attempt to learn the server’s MAC address, as shown in Figure 2-2
  
  <img src="images/arp1.png" alt="ARP" width="50%"/>
* When switch SW1 sees PC1’s ARP request enter port Gigabit 0/1, PC1’s MAC address AAAA.AAAA.AAAA is added to switch SW1’s MAC address table
* Also, because the ARP request is a broadcast, its destination MAC address is FFFF.FFFF.FFFF
* Because the MAC address FFFF.FFFF.FFFF is not known to switch SW1’s MAC address table, switch SW1 floods a copy of the incoming frame out all switch ports other than the port on which the frame was received, as shown in Figure 2-3

  <img src="images/arp2.png" alt="ARP" width="50%"/>
* When switch SW2 receives the ARP request over its Gig 0/1 trunk port, the source MAC address AAAA.AAAA.AAAA is added to switch SW2’s MAC address table, as illustrated in Figure 2-4
* Also, using behavior similar to that of switch SW1, switch SW2 floods the broadcast

  <img src="images/arp3.png" alt="ARP" width="50%"/>
* The server receives the ARP request and responds with an ARP reply, as shown in Figure 2-5
* Unlike the ARP request, however, the ARP reply frame is not a broadcast frame. The ARP reply, in this example, has a destination MAC address AAAA.AAAA.AAAA, which makes the ARP reply a unicast frame

  <img src="images/arp4.png" alt="ARP" width="50%"/>
* Upon receiving the ARP reply from the server, switch SW2 adds the server’s MAC address BBBB.BBBB.BBBB to its MAC address table, as shown in Figure 2-6
* Also, the ARP reply is only sent out port Gig 0/1 because switch SW1 knows that the destination MAC address AAAA.AAAA.AAAA is available off port Gig 0/1

  <img src="images/arp5.png" alt="ARP" width="50%"/>
* When receiving the ARP reply in its Gig 0/2 port, switch SW1 adds the server’s MAC address BBBB.BBBB.BBBB to its MAC address table
* Also, like switch SW2, switch SW1 now has an entry in its MAC address table for the frame’s destination MAC address AAAA.AAAA.AAAA
* Therefore, switch SW1 forwards the ARP reply out port Gig 0/1 to the endpoint of PC1, as illustrated in Figure 2-7

  <img src="images/arp6.png" alt="ARP" width="50%"/>
* After receiving the server’s ARP reply, PC1 knows the MAC address of the server
* Therefore, PC1 can now properly construct an SSH segment destined for the server
* Because PC1 learned the server’s MAC address as a result of its earlier ARP request and stored that result in its local ARP cache, the transmission of subsequent Telnet segments does not require additional ARP requests
* However, if unused for a period of time, entries in a PC’s ARP cache can time out
* Therefore, the PC would have to broadcast another ARP frame if it needed to send traffic to the same destination IP address
* The sending of the additional ARP frames adds a small amount of delay when reestablishing a session with that destination IP address

<br>

* As shown in Figure 2-12, each port on a switch represents a separate collision domain
* Also, all ports on a switch belong to the same broadcast domain, with one exception: when the ports on a switch have been divided into separate virtual LANs (VLANs)
* Remember that each VLAN represents a separate broadcast domain, and for traffic to travel from one VLAN to another, that traffic must be routed by a Layer 3 device
<img src="images/coll1.png" alt="Collision/Broadcast Domain" width="35%"/>

* Whereas a Layer 2 switch makes forwarding decisions based on MAC address information, a multilayer switch can make forwarding decisions based on upper-layer information
* Some literature refers to a multilayer switch as a Layer 3 capable switch because of the switch’s capability to make forwarding decisions like a router
* The term multilayer switch is more accurate, however, because many multilayer switches have policy-based routing features that allow upper-layer information (for example, application port numbers) to be used in making forwarding decisions
<img src="images/coll2.png" alt="Collision/Broadcast Domain" width="45%"/>

* As on a Layer 2 switch, each port on a multilayer switch represents a separate collision domain; however, a characteristic of a multilayer switch (and a router) is that it can become a boundary of a broadcast domain
* Although all ports on a Layer 2 switch belong to the same broadcast domain, if configured as such, all ports on a multilayer switch can belong to different broadcast domains

# IDS vs IPS
* Because the analyzed traffic does not flow through the IDS device, the IDS device is considered to be **passive**, and the IPS device is considered to be **active**
* Although an IDS device can also communicate with a security appliance or a router to prevent subsequent attack packets, the initially offending traffic reaches its destination
* Conversely, an IPS device can drop the traffic inline, thus preventing even the first malicious packet from reaching its intended target
<img src="images/idsips.png" alt="IDS/IPS" width="45%"/>

# IDS/IPS Device Categories
* IDS and IPS devices can be categorized based on how they detect malicious traffic
* Consider the following approaches to detecting malicious traffic:
  * Signature-based detection
  * Policy-based detection
  * Anomaly-based detection
  
* **Signature Based Detection**
  * The primary method used to detect and prevent attacks using IDS or IPS technologies is signature based
  * A signature could be a string of bytes that, in a certain context, triggers detection
  * For example, attacks against a web server typically take the form of URLs. Therefore, URLs could be searched for a certain string that would identify an attack against a web server
  * As another example, the IDS or IPS device could search for a pattern in the MIME header of an email message
* **Policy Based Detection**
  * With a policy-based approach, the IDS/IPS device needs a specific declaration of the security policy
  * For example, you could write a network access policy that identifies which networks can communicate with other networks. The IDS/IPS device could then recognize out-of-profile traffic that does not conform to the policy and report that activity
  * Policy-based detection could also identify unencrypted channels and plaintext credentials and insecure protocols such as Telnet, SNMPv1, SNMPv2, HTTP, FTP, SLIP, and TFTP
	
* **Anomaly Based Detection**
  * This approach is prone to false positives because a normal condition is difficult to measurably define
  * However, there are a couple of options for detecting anomalies:
    * **Statistical anomaly detection**: 
      * This approach involves watching network traffic patterns over a period of time and dynamically building a baseline
      * Then, if traffic patterns significantly vary from the baseline, an alarm can be triggered
    * **Nonstatistical anomaly detection**:
      * This approach allows an administrator to define what traffic patterns are supposed to look like
      * However, imagine that Microsoft releases a large update for its Windows 10 OS, and your company has hundreds of computers that are configured to automatically download that service pack. If multiple employees turn on their computers at approximately the same time tomorrow morning, and multiple copies of the service pack simultaneously start to download, the IDS/IPS device might consider that traffic pattern to be significantly outside the baseline
      * As a result, the nonstatistical anomaly detection approach could lead to a false positive
      * However, an anomaly-based IPS may be able to indicate abnormal behavior, compared to the baseline of normal activity, which could assist you in discovering a new type of attack that is being used against your network

# Load Balancer
* A load balancer is a network device or software component that distributes incoming network traffic across multiple servers, systems, or resources in a network, ensuring optimal utilization of resources, high availability, and improved performance
* Load balancers operate at the application layer (Layer 7) or transport layer (Layer 4) of the OSI model and use various algorithms, such as round-robin, least connections, or weighted distribution, to evenly distribute incoming requests or connections among the backend servers
* The load balancer can also check the health of the nodes periodically and intelligently prevent the forwarding of web requests to servers that are sickly

# Proxy Servers
* Some clients are configured to forward their packets, which are seemingly destined for the Internet, to a proxy server
* The proxy server receives the client’s request, and on behalf of that client (that is, as that client’s proxy), the proxy server sends the request out to the Internet
* When a reply is received from the Internet, the proxy server forwards the response on to the client
<img src="images/proxy.png" alt="Proxy Server" width="45%"/>

* Because all requests going out to the Internet are sourced from the proxy server, the IP addresses of network devices inside the trusted network are hidden from the Internet
* Many proxy servers perform content caching and thus can save bandwidth:
  * For example, without a proxy server, if multiple clients all visited the same website, the same graphics from the home page of the website would be downloaded multiple times (one time for each client visiting the website)
  * However, with a proxy server performing content caching, when the first client navigates to a website on the Internet, and the Internet-based web server returns its content, the proxy server not only forwards this content to the client requesting the web page but also stores a copy of the content on its hard drive
  * Then, when a subsequent client points its web browser to the same website, after the proxy server determines that the page has not changed, the proxy server can locally serve up the content to the client, without having to once again consume Internet bandwidth to download all the graphic elements from the Internet-based website 
* Some proxy servers can perform content filtering to restrict clients from accessing certain URLs
* A reverse proxy receives requests on behalf of a server or servers and replies back to the clients on behalf of those servers
* Reverse proxies can also be used with load-balancing and caching to better utilize a group of servers providing scalability and high availability

# Network Attached Storage (NAS)
* A NAS device is a specialized type of storage device that is designed to provide centralized storage and file sharing capabilities to multiple users and devices within a network
* Unlike traditional storage solutions that are directly attached to individual computers, NAS devices connect to a local area network or wide area network, allowing them to be accessed by any device connected to the network
* NAS devices typically consist of one or more hard drives configured in a Redundant Array of Independent Disks (RAID) array for data redundancy and increased reliability

# Storage Area Networks (SAN)
* A storage area network (SAN) is a high-speed, very specialized network that is designed to store massive amounts of data and make that data available quickly when clients and/or servers request it
* Originally, Fibre Channel was the technology that ruled the SAN space
* Unlike Ethernet, Fibre Channel is designed for very low-latency, guaranteed lossless connectivity
* In contrast, with UDP in an Ethernet environment, it is easy to contend with packet loss and delays. This is not the case in a SAN environment
* To make SANs even more accessible and flexible, they began to be created to support Internet Small Computer System Interface (iSCSI)
* With iSCSI, which is an IP-based technology for network storage, a client using the storage is referred to as an initiator, and the system providing the iSCSI storage is called the iSCSI target
* Networks supporting iSCSI are often configured to support larger-than-normal frame sizes, referred to as jumbo frames
* Converging different forms of traffic on a network extended to SAN and LAN traffic is thanks to a remarkable invention: Fibre Channel over Ethernet (FCoE)
* Just like it sounds, this technology allows Ethernet to encapsulate Fibre Channel frames and carry them over a high-speed Ethernet infrastructure
* Modifications were made to the Ethernet standards for FCoE to provide the level of service required in the SAN for Fibre Channel
* Ethernet needs to be truly high speed in order to have a chance at providing FCoE services. In the Cisco implementation, 10-Gbps Ethernet is required for FCoE

# Controllers
* Access points tend to come in two major types: autonomous and lightweight 
* Lightweight access points do not have the control plane intelligence built in to perform their functions for the network
* These devices are controlled by controllers, or more formally known as wireless LAN controllers (WLCs)
* WLCs are specialized network devices that permit the central control and management of large numbers of lightweight access points
* WLCs simplify the administration of your access points, and they can also assist you dramatically in the monitoring and ongoing maintenance of the wireless infrastructure

# Content Delivery Network (CDN)
* A content delivery network (CDN) is a sophisticated infrastructure composed of multiple servers distributed across various geographic locations, strategically positioned to deliver web content and digital media to users with optimal speed and reliability
* For example, when a user requests access to content hosted on a web server, the CDN automatically identifies the user’s location and routes the request to the nearest server within its network
* By serving content from servers near the user, CDNs can significantly reduce latency and minimize the time it takes for content to reach the end-user device, enhancing the overall user experience
* CDNs can also help mitigate the risk of server overload and improve scalability by distributing the load of content delivery across multiple servers
* This distributed architecture enables CDNs to handle high volumes of traffic efficiently, particularly during peak usage periods or sudden spikes in demand 
* CDNs can also offer advanced caching mechanisms that store copies of frequently accessed content on edge servers, further optimizing performance and reducing the strain on the servers of origin

# Quality of Service
* While the main concern of your network is to ensure that data packets reach their rightful destinations, it is the job of quality of service (QoS) to ensure that packets do not suffer from long delays (latency) or, worse, dropped packets
* Through the use of QoS technologies, you can identify which traffic types need to be sent first, how much bandwidth to allocate to various traffic types, which traffic types should be dropped first in the event of congestion, and how to make the most efficient use of the relatively limited bandwidth of an IP WAN
* Three categories of quality issues:
  * **Delay**:
    * Delay is the time required for a packet to travel from source to destination
    * You might have witnessed delay on the evening news when the news anchor is talking via satellite to a foreign news correspondent
    * Because of the satellite delay, the conversation begins to feel unnatural
  * **Jitter**:
    * Jitter is the uneven arrival of packets
    * For example, imagine a VoIP conversation where packet 1 arrives at a destination router. Then, 20 ms later, packet 2 arrives. After another 70 ms, packet 3 arrives, and then packet 4 arrives 20 ms behind packet 3
    * This variation in arrival times (that is, variable delay) is not due to dropped packets, but the jitter might be interpreted by the listener as dropped packets
  * **Drops**:
    * Packet drops occur when a link is congested and a router’s interface queue overflows
    * Some types of traffic, such as UDP traffic carrying voice packets, are not retransmitted if packets are dropped
* As a packet travels from source to destination, its effective bandwidth is the bandwidth of the slowest link along that path






















