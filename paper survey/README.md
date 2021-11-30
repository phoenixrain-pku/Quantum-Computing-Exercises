# Paper Survey Collection

Update on 2021/11/4:

1. https://oa.upm.es/46651/1/INVE_MEM_2016_254845.pdf

   This work, *Quantum-Aware Software Defined Networks*, gives a brief QKD architecture using SDN. So it is more likely an end-to-end model.

2. https://www.osti.gov/servlets/purl/1471920

   This work, *Software-defined Quantum Network Switching*, designs  a quantum SDN protocol. It separates the quantum part and classical part on each switch. When establishing a connection, it classically confirms there exists a quantum path (handshake), and then begins quantum transmission, and classically closes the connection.
   
   The external controller is present to reconfigure the classical switch, and during the quantum transmission process, the classical switch cannot be reconfigured.
   
   But this work only models the architecture and gives some constraints. The detailed protocols and algorithms can be considered much more.
   
3. https://dl.acm.org/doi/pdf/10.1145/3387514.3405853

   This work, *Concurrent Entanglement Routing for Quantum Networks: Model and Designs*, designs a new entanglement routing algorithm based on quantum network features. It compares itself with SDN, and mentioned that the quantum network topology  is not reliable because links may arbitrarily fail. Hence, more robust algorithms are required. I think it truly emphasizes importance on robustness in routing, so maybe a controller who always gains global information, is much more needed.



I think these tasks can be considered more detailly:

1. What layers should be edited, or even replaced, on the classical network stack? What layers should we focus on? 

   + It's evident that the physical layer should be replaced, but we don't need to care about it. 

   + The link layer is responsible for error correlation and data packaging. There is a transmission between the raw data and data frames. What additional quantum information should be added, and how to add?

   + The network layer is responsible for transmission between different hosts. In this layer, we design some protocols, and do network management such as congestion control. There are many issues to be discussed here. I'm mostly interested in the routing algorithm. 

     In quantum network, a quantum path can only be shared by one pair each time, so routing becomes much more difficult. I prefer to make the controller responsible for path calculation and allocation in the whole network, and use classical protocols such as OpenFlow to achieve this.

   + The transport layer is responsible for transmission between different processes. I think we can discuss how to achieve TCP, reliably transfer information among processes.

   + The application layer offers different service for clients, like mail service or web service. This may help to prevent mails from being copied or retransmission. But is this important?
   
2. What can the controller do?

   I prefer to make it be the hub of all information, including nodes and paths status. Therefore, every switch can interact with the controller, instead of interact with its neighbors. This allows dynamic network, and to add a new node we can just let it classically connect to the controller.

   Additionally, I think the controller can be responsible for entanglement establishment. Once two nodes want to begin communicating, the controller can establish a entanglement between them, by directly distribute entangled pairs, or using entanglement swapping technique. However, the controller is only responsible for routing and distributing. It cannot gain any information from the two nodes.

   However, the balance between distribution and clustering is not easy to discuss. So the responsibility of the controller and other switches should be considered more seriously.

