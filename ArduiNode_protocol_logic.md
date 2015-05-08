# ArduiNode  protocol #
CAPITALIZED words refer to #defines in the arduiNode source code.

## Beacon ##
Every node with a valid id (!=0) sends beacon frames in regular intervals. These frames contain the nodes ID and the HTM (hops to master). They are addressed to BROADCASTADDR with the default of 255.

## Routing ##
Routing is done from the slave nodes to the master node (base station). Every node has a routing table with NODE\_TABLE\_SIZE entries which contains the ID and HTM and is sorted smallest HTM first. If a node has something to send it takes the first entry of this table as destination node. If the node does not respond to communication attempts PKTRETRY times the entry is deleted from the node table.

The master node acts as a base station, all packets in the network are routed to this node, as its the data sink. At the moment its not possible to route packets to slaves using multi hop, addressing individual slaves within the range of the master node is possible but experimental. Refer to the arduiNode functions page for more information on that.

## Master vs Slave nodes ##
Besides routing, there are some more differences between the two node types:
  * Master nodes always send BEACONs, slave only if they have a valid ID.
  * Only master nodes allocate new IDs.
  * If a DATA packet arrives at a slave node it will try to forward it to a node which is nearer to the master or the master itself. A master node will not forward DATA.