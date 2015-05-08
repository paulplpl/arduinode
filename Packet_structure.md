## packet types ##
Communication is packet orientated. Different packet types are used for different purposes.
The type of a packet is represented as the forth byte of every packet.
Possible packets and their corresponding numbers are:
  * RTS     0
    * Ready To Send: before a node sends data to another node, it first sends a RTS demand.
  * CTS     1
    * Clear To Send: if the node is ready to accept data it responds with a CTS packet.
  * ACK     2
    * Acknowledgement: if a node received all data bytes of a data transmission, it responds with an ACK.
  * PING    3
    * not implemented
  * DATA    5
    * n bytes of payload are routed from the sending nodes to the master node. The rxbuffer[ ] has to be big enough to hold the data + header bytes
  * BEACON  7
    * is send out periodically, contains the nodes ID (= fromAdress) and HTM(= Hops To Master)
  * INID    8
    * I Need ID: the nodes request for a UID to identify itself in the network. A new key in form of a timestamp is generated every time the node receives a beacon until the node has a valid ID. The key is the 8 bit value of millis() at this time. This key is used to identify the nodes INID request. So if multiple nodes need ID's at the same time, the chance of 2 nodes getting the same ID is greatly reduced. Each node rebroadcasting an INID packet, adds its own ID to the packet. These ID's are needed for the ANID response route.
  * ANID
    * Allocated new ID: the master node's response to an INID  demand. Like the INID packet it contains the node key and the ID's of all the nodes located on the way back to the id-requesting node. If a node which needs an ID receives such a packet and the key corresponds to its, it takes the new ID.



## packet format ##
This is the packet format used by arduinode.
<b>rxbuff [ ]</b> refers to the index of the rx buffer.

|<b>Packet type</b>|
|:-----------------|
|<b>Rts</b>|length|toAddr|fromAddr|RTS|
|<b>Cts</b>|length|toAddr|fromAddr|CTS|
|<b>Ack</b>|length|toAddr|fromAddr|ACK|
|<b>BEACON</b>|length|toAddr|fromAddr|BEACON|HTM|
|<b>DATA</b>|length|toAddr|fromAddr|DATA|payload|payload|payload|payload|...|
|<b>INID</b>|length|toAddr|fromAddr|INID|nodeKey|ID(a)|ID(b)|ID(n)|
|<b>ANID</b>|length|toAddr|fromAddr|ANID|newID|nodeKey|ID(a)|ID(b)|ID(n)|
|<b>rxbuff [ ]</b>|0 |1 |2 |3 |4 |5 |6 |7 |8 |