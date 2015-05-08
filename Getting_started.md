# Basic use of arduiNode #

## Installation ##
### needed libraries ###
You will need the latest arduiNode lib.. <sup>_</sup>
  * Download the latest arduinode.xx.zip and unpack it to ARDUINO\_DIR/libraries/
  * You'll also need the protothreads library which is also in **Downloads** as arduino library repack. Unpack it to ARDUINO\_DIR/libraries/
  * Restart your arduino IDE after that.

### test program ###
Flash one controller with the arduiNode\_MASTER sketch and another one with arduiNode\_SLAVE. All sketches are part of the arduiNode library. They are situated in /examples.
> Connect the master node to your serial port and open the serial console. You can now (hopefully) observe the communication. Slave node sends data (0xAA 0xBB 0xCC 0xDD 0xEE) every 3s, the master receives and displays it. It also sums the data up, as an easy example how to access the data buffer.


## Hardware ##
### Controller ###
I use boarduinos with atmega168 chips from adafruit for testing. The code should work on all arduino flavours out there. If you encounter any problems with other atmega chips, please let me know!

### Communication ###
At the moment communication works with infra red or the rfm12 wireless transceiver modules from HopeRF.
#### IR ####
There is an ir-receiver (TSOP31236 36kHz) and an ir led for that purpose on board.

  * The output pin of the receiver is connected to arduino's pin d7
  * The IR led is wired to d3 via a matching resistor.
  * The status led is wired to d8. It blinks on tx and rx.
  * These 2 pins can't be changed for the moment.

#### RFM12 ####
RFM12 communication now works fine, connect the module as follows:

> | **RFM12** | **arduino** |
|:----------|:------------|
> |nSEL|d10 (SS)|
> |SDI|d11 (MOSI)|
> |SDO|d12 (MISO)|
> |SCK|d13 (SCK)|
> |SDOnIRQ|d2|
> |nIRFSK/DATA/nFFS|VCC|


## Debug output ##
The library file **main.h** contains some compile options. By default the option CONNECTDEBUGMODUS is set to 1 (=true). This will output a lot of detailed communication insights. However it will also increase the code size by a lot.. So if later on you don't need it anymore, you can turn it of. Simply set the '1' to a '0'. There are also some other debug options which are for development.