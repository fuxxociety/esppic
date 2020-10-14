# ESPPIC - An ESP-based PIC programmer




## NOTE -- This is a fork of Mats' original project.  [Go to SmallRoomLabs for the real thing](https://github.com/SmallRoomLabs/esppic).
## Help for compile and load.

### The PIC micro

   Before anything else at all  ...your PIC __MUST__ have Low Voltage Programming (LVP) enabled.  ESPPIC will _not_ work at all (ie:- won't even read, let alone   program memory) if LVP is not set.  Any modern PIC processors which you buy from a reliable source should come with this configured, but if you're using a device from a previous project, it's very likely that it won't be.

   The only way to set LVP in a PIC which doesn't have it enabled is to use a "high voltage" programmer (ie:- PicKit2/3) to program it.  There is no way round this (but you can build yourself a cheap HV programmer very easily, depending upon the contents of your spares box).

#### How can I tell if I don't have LVP enabled?

   If your ESP boots and displays the ESPPIC page, but the dump memory link (bottom LH side of the page) comes back with all zeros in the memory section and all zeros in the DEV-ID field, then there's a good chance that the LVP bit isn't set (this is, of course, assuming that your wiring to the PIC is all correct).

### Compile & Load

   * Use PlatformIO.  It has much more functionality than the Arduino IDE.
   * Once you've initialized the project (ie:- pio init --board=esp12e), edit the platformio.ini file to add the following lines to enable the LittleFS filesystem and automagically install the WebSockets library:-  
```C
   board_build.filesystem = littlefs  
   lib_deps = links2004/WebSockets@^2.2.1  
```
   * Copy the "assets" directory to "data" in the platformIO project directory (-not- the /src directory).  This makes the web content for the ESP available to the uploadfs command. 
   * Use "pio build -t upload" to compile and upload to your target board.  There will be several warnings during the compile; this is expected.
   * Use "pio build -t uploadfs" to load the web-pages from the "data" directory to the LittleFS filesystem on the ESP8266.





![ESP with PIC](https://github.com/SmallRoomLabs/esppic/raw/master/images/esppic-bare-S.jpg "NodeMCU and a PIC16F1705")

## Status
  * v0.1 - Can flash/read code & configs to a PIC16F1705. The code flashed is hardcoded as hex data in an array of strings in the esp code. 

  * v0.2 - Implemented web interface, can upload files. Read and flash config from web.
