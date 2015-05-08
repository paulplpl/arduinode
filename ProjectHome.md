# Overview #
**arduinode** is a protocol for a wireless sensor net. Communication is handled in the background, neighbor nodes find each others and span the net. Some of its core features are: multi hop packet routing, dynamic id allocation, collision avoidance and rebroadcasting of lost messages. **[Introduction blog post on arduiNode](http://harteware.blogspot.com/2011/10/presenting-arduinode-wireless-sensor.html)**<br>

<h1>News</h1>
The new rfm12 driver is now fully integrated into arduiNode and everything works great most of the time.. The only problems at the moment are packet collisions, but these should be gone soon. I plan to release version 1.0 till end of the month. Please drop me an email to the mail address found in the header files if you have any comment!<br>
<br>
<h1>Hardware</h1>
For the communication channel you can choose between two options:<br>
<ul><li>infra red<br>
</li><li>radio</li></ul>

See the "Getting Started" article in the wiki for more details on how to connect the communication hardware to the arduino.<br>
<br>
<br>
<h1>Installation</h1>
Download arduinode.xx.zip and unpack it to ARDUINO_DIR/libraries/<br>
Restart your arduino IDE after that. Now you can access the library and the two examples.<br>
You'll also need the <b>protothreads</b> library which you can also download <a href='http://code.google.com/p/arduinode/downloads/detail?name=pt.zip'>here</a> as arduino library repack.<br>
<br>
<h1>Use it</h1>
Obviously you'll need at least two nodes for testing ;)<br>
Flash one controller with the <b>arduiNode_MASTER</b> sketch and another one with <b>arduiNode_SLAVE</b>. Connect the master node to your serial port and open the serial console. You can now (hopefully) observe the communication.<br>
Slave node sends data (0xAA 0xBB 0xCC 0xDD 0xEE) every 3s, the master receives and displays it. It also sums the data up, as an easy example howto access the data buffer.