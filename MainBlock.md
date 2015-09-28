**Table of Contents**


---





---


#summary Main Block

# Introduction #
https://seal-tome-6.googlecode.com/hg/Research/Research%20Pic/Pic%2044%20pin.JPG
The Pic we picked for our team is the PIC18f45k80, which is an 8 bit 44 pin pic. We chose an 8 bit pic because we felt the scope of the project wasn’t complex enough to justify a 16 bit. Also because it has the necessary GPIO’s and functions we need. These functions and GPIO’s are listed as:
  * 1 UART (2 pins)
  * 3 interrupts (3 pins)
  * 2 ADC (2 pins)
  * 24 GPIO (24 pins)
  * PICIT3 pins (3 pins)
  * Total pins 34 pins

Along with our PIC we would also be using a FTDI chip for UART communication. The FTDI chip we will be using is the FT232R. This chip allows us to debug the PIC if we receive an unexpected outcome. This chip is connected via USB to a computer, where we can read and write the data to the PIC.
https://seal-tome-6.googlecode.com/hg/Research/Research%20Pic/Tables%20for%2044%20pin.JPG

# Research #
https://seal-tome-6.googlecode.com/hg/Research/Research%20Pic/Breakout%20board%20flow.JPG
We plan build the prototype in multiple separate breakout boards then reconnect them to the PIC. To make integration easier for us, we separated the ports, assigning one port to the particular breakout board. We assign ports by giving priority to the breakout boards that require specific pins, such as interrupts and I2C.

## Recommended Connections ##
![https://seal-tome-6.googlecode.com/hg/Research/Research%20Pic/reccomended%20connections.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Pic/reccomended%20connections.jpg)
**Required Connections**

  * C1-C6: 0.1uF, 20V ceramic
  * C7: 10uf, 20v ceramic/tantalum
  * [R1](https://code.google.com/p/seal-tome-6/source/detail?r=1): 10k ohm
  * [R2](https://code.google.com/p/seal-tome-6/source/detail?r=2): 100 ohm to 470 ohm

The jumper (JP) is connected during operation and is removed during programming and debugging operations.

**Note 1:** Connecting ENVREG to VDD will enables the regulator. Connecting ENVREG to VSS will disable the regulator.
**Note 2:** Example is shown for 64 pin pic18F66K80. Only two of these are present in the 44 pin pic.

## FTDI Chip ##
![https://seal-tome-6.googlecode.com/hg/Research/Research%20Pic/ftdi%20chip.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Pic/ftdi%20chip.jpg)

The FTDI chip will be wired as below. The chip allows for multiple configurations, and the one we chose was to have the chip powered VIA an external USB cable. The PIC is powered by a separate source, but we’ve also allowed for the pic to also be powered with the same USB port with a jumper pin. Along with wiring the FTDI chip to the USB port, we will also be wiring up LED’s to the TX and RX of the chip, so that we know when data is being transferred. The LED’s are connected to the CBUS [4:0] bus. TX and RX is connected to CBUS [2](2.md), CBUS [3](3.md) respectively.

https://seal-tome-6.googlecode.com/hg/Research/Research%20Pic/Ftdi%20requiered%20connections.JPG
**First choice:**
[PIC18f45k80 44 pin Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/39977f.pdf) – This PIC gives us the necessary pins and function for our project.
FT232R Datasheet – We are choosing this FTDI chip since it is fairly easily to setup, and does allow for us to setup LED’s to let us know if TX and RX is working. This will also help when using Canbus and communicating with the Xbee.

**Second choice:**
[PIC18f45k80 64 pin Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/39977f.pdf) – If we need more GPIO pins than expected we will upgrade to a pic from the same family so that our code remains the same.  Although this is our second choice, we rather not work with this pic, as it is very difficult to solder on the breakout board.
Our second choice for our FTDI chip is to not use it if we can’t get it working. Our FTDI chip is fairly simple, and only purpose is to help debug. But if we can’t get it working we will be removing it.



---


---

Tome Links

---

_[Main Block Programming](MainBlock.md)_<br />[Power](Power.md)<br />[Visuals](Visuals.md)<br />[Packaging](Packaging.md)<br />[Audio](Audio.md)<br />[Communication](Communication.md)<br />_[Back to The Tome's Main Page](Sorcerers_Spelltome_Wiki_Main.md)ges_



---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)