**Table of Contents**


---





---

# Introduction #
![https://seal-tome-6.googlecode.com/hg/integration/2013-11-11%2018.06.32.jpg](https://seal-tome-6.googlecode.com/hg/integration/2013-11-11%2018.06.32.jpg)
![https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20block%20diagram.png](https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20block%20diagram.png)

For our PIC, we separated the ports to different busses on the breakout board. Along with the busses, we are also sending power form the power board through the pic, to deliver power lines to each port bus.

The port buses are assigned by the following convention:
| Portx(0) | Portx(1) | Portx(2) | Portx(3) | Portx(4) | Portx(5) | Portx(6) | Portx(7) | Portx(8) | Portx(9) |
|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:---------|
| VDD      | VSS      | Regx(0)  | Regx(1)  | Regx(2)  | Regx(3)  | Regx(4)  | Regx(5)  | Regx(6)  | Regx(7)  |
Where "x" represents the different ports on the pic

# Schematics and Layouts #
## Pic Schematic (will pretty-fy later) ##
![https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20pic%20schematic.png](https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20pic%20schematic.png)

## Pic Layout ##
![https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20pic%20layout.png](https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20pic%20layout.png)

## FTDI Chip schematic ##
![https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20ftdi%20schematic.png](https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20ftdi%20schematic.png)

## FTDI Chip Layout ##
![https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20fidi%20layouyt.png](https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/prototype%20fidi%20layouyt.png)


# Main Loop #
![https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/flowchart%20for%20main%20loop.png](https://seal-tome-6.googlecode.com/hg/protyping/pic_proto/flowchart%20for%20main%20loop.png)

The main loop calls the main methods, which calls sub methods/functions:
  * Void **Spell Cool down** (Void) – waits 60 s before calling any other methods.
    * Void **Play audio** (Uint8\_t dataReg) - sends the data reg for audio to play the “spell ready” audio
    * Void **Light LED** (Uint8\_t dataReg) - sends the data reg for the LED display the CD
  * Void **Fail spell cast** (Void) – if the spell fails to cast, reset cooldown and output fail indicators
    * Void **Play audio** (Uint8\_t dataReg) – sends the data reg for audio to play the “spell fail” audio
    * Void **Light LED** (Uint8\_t dataReg) - sends the data reg for the LED display the “spell fail” lights
  * Void **Book damage** (void) – sends the data reg for book damage to sub functions
    * Void **Play audio** (Uint8\_t dataReg) - sends the data reg for audio to play the “book damage” audio
    * Void **Light LED** (Uint8\_t dataReg) - sends the data reg for the LED display the “book damage” lights
  * Void **Spell cast** (void) – sends the page data reg to the sub methods/functions to output the correct indicators, and packets.
    * Void **Play audio** (Uint8\_t pageReg) - sends the page reg for the appropriate page, for the audio to play the correct spell audio
    * Void **Light LED** (Uint8\_t pageReg) - sends the page reg for the appropriate page, for the audio to display the correct lights
    * Void **IR LED** (Uint8\_t pageReg) - sends the page reg for the appropriate page, for the IR to fire the correct packet
    * Void **XBEE** (Void) – Tells the xbee to fire our buff spell

# Hardware IO #
| IO Name | Description of Signal | Expected Range |
|:--------|:----------------------|:---------------|
| Power (input)| From the power block, sends 3.3V up to 1 amp to the PIC breakout board to distribute power to the port busses | 0 - 3.3v       |
| UART (Input/Output) | From the computer to our PIC board. The UART is to help us debug our program if for some reason our program isn’t working as expected. Also helps with debugging hardware that functions off UART | 0 - 3.3v       |
| PORTA[9:0] (output) | All the A registers are grouped into one header, along with power and ground. This is done to encapsulate the hardware more, and make it easier during integration | 0 - 3.3v       |
| PORTB[9:0] (output) | Similar to above but for  B register | 0 - 3.3v       |
| PORTC[9:0] (output) | Similar to above but for  C register | 0 - 3.3v       |
| PORTD[9:0] (output) | Similar to above but for  D register | 0 - 3.3v       |
| PORTE[4:0] (output) | Similar to above but for E register. Port E is only 5 bits, since REG E only has 3 GPIO. | 0 - 3.3v       |



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)