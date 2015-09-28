**Table of Contents**


---





---


#summary This is the Visuals Prototyping page

# Spell Tome Lighting Block #

## Block Diagram ##


![http://seal-tome-6.googlecode.com/hg/protyping/led/RGB%20proto%20BD.png](http://seal-tome-6.googlecode.com/hg/protyping/led/RGB%20proto%20BD.png)



This is the block diagram for the lightning block. All signals are highlighted in white, and all test points are labeled as TP# and are in bold black.





## Health Schematic ##


![http://seal-tome-6.googlecode.com/hg/protyping/led/Health%20Schematic.png](http://seal-tome-6.googlecode.com/hg/protyping/led/Health%20Schematic.png)



This is the schematic for the health portion of the lighting block. All inputs are under the J1 header and all eleven test points are displayed.









## Cooldown Schematic ##


![http://seal-tome-6.googlecode.com/hg/protyping/led/Cooldown%20Schematic.png](http://seal-tome-6.googlecode.com/hg/protyping/led/Cooldown%20Schematic.png)



This is the schematic for the cooldown portion of the lighting block. All inputs are under the J1 header. This schematic is functionally exactly the same as the health schematic, but there is one more LED and it is separated into two boards, which connect at vias.

## Function List ##


### void updateLeds() ###
Description: This is the main function used to update the LEDs. It sends in all serial data of the LEDs to the driver. It technically has no inputs, but it uses 3 global bytes (per LED driver in use) to store the LED on/off information.
Inputs: None (other than the global bytes)
Return Values: None



![http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCUpdateVis.png](http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCUpdateVis.png)



This is the flowchart for the updateLeds() function.

### void updateBrightness() ###
Description: Very similar to the updateLeds() function, this function also uses global bytes that store brightness data for red, green and blue. It sends the data using the same serial method as updateLeds(), but instead of the first bit being low, it is high to indicate brightness value.
Inputs: None (other than the global bytes)
Return Values: None


The flowchart for updateBrightness() is functionally the same as the flowchart for updateLeds(), other than the differences detailed in the description.


### void updateHealthIndication() ###
Description: This function is called whenever the global health value is changed. It compares the current health value to the maximum health value, and comes up with a percentage. Depending on this percentage, a certain amount of LEDs are lit up. Its input is the global byte of current health value.
Inputs: None (other than the global bytes)
Return Values: None


![http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCHealthVis.png](http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCHealthVis.png)



This is the flowchart of the updateHealth() function.






## Inputs ##

|Input Name|Description of Signal|Expected Range|Measured Range|
|:---------|:--------------------|:-------------|:-------------|
|Sin       |This is the serial input that is communicated from the PIC microprocessor to the LED driver. As a digital input, its switching characteristics resemble that of a square wave.|0 – 3.3V      |0 – 3.32 V    |
|SClk      |This is the serial clock used for the shift register on the LED driver. The shift register shifts on the rising edge of this signal. As a digital input, its switching characteristics resemble that of a square wave.|0 – 3.3V      |0 – 3.31 V    |
|Latch     |This is the serial latch used for the shift register on the LED driver. On the rising edge of this signal, the values in the shift register will be transferred either to RGB on/off data or brightness data, depending on the state of the MSB in the shift register. As a digital input, its switching characteristics resemble that of a square wave.|0 – 3.3V      |0 – 3.31 V    |
|Blank     |This input has the ability to turn off all inputs for the LED driver whenever its input is high. As a digital input, its switching characteristics resemble that of a square wave.|0 – 3.3V      |0 – 3.31 V    |
|Vcc/VLED  |This input is the voltage (source) used to power both the LED driver and the LEDs themselves.|3.3 – 3.3 V   |3.27 – 3.34V  |
|GND       |This is the common ground for the system.|0 V           |0 V           |






## Outputs ##

|Output Name|Description of Signal|Expected Range|Measured Value|
|:----------|:--------------------|:-------------|:-------------|
|Iref       |This is the reference current used to determine the output current on every channel of the RGB LEDs.|0.8 – 0.85 mA |1.13 mA       |
|Light      |This is the light that is output by each LED.|Red: 560 – 1120 mcd Green: 1120 – 2240 mcd Blue: 280 – 560 mcd|Unable to measure|



Example updateLeds() output for the following global variables:
LED1Byte1 = 10000000
LED1Byte2 = 10100010
LED1Byte3 = 01001001

Output: Green 5, Blue 4, Green 3, Blue 2, Green 2, Green 1 and Green 0 are all turned on, all other LEDs are turned off.







## Test Points ##

|T.P. Name|Description of Signal and measurement conditions|Range of Values|
|:--------|:-----------------------------------------------|:--------------|
|TP1      |This test point is the current that has passed through the red LED and is heading back to the driver. This was used to determine the voltage across the red LED and the current passing through it. It was also used to test the voltage at the current sink.|21-25 mA/2.27 V through red, 0.5 V at current sink|
|TP2      |This test point is the current that has passed through the green LED and is heading back to the driver. This was used to determine the voltage across the green LED and the current passing through it. It was also used to test the voltage at the current sink.|23-27 mA/3.33 through green,0.17 V at current sink|
|TP3      |This test point is the current that has passed through the blue LED and is heading back to the driver. This was used to determine the voltage across the blue LED and the current passing through it. It was also used to test the voltage at the current sink.|16-21 mA/3.31 V through blue,0.22 V at current sink|
|TP4      |This was the test point used at Vcc/VLED.       |3.27 – 3.34V   |
|TP5      |This was the test point used at ground.         |0 V            |
|TP6      |This was the test point used at Sin.            |0 – 3.32 V     |
|TP7      |This was the test point used at SClk            |0 – 3.31 V     |
|TP8      |This was the test point used at Latch.          |0 – 3.31 V     |
|TP9      |This was the test point used at Blank.          |0 – 3.31 V     |
|TP10     |This was another test point used at Vcc/VLED.   |3.27 – 3.34V   |
|TP11     |This was the test point used at Iref, to measure the output current and voltage at that point|1.8 V  at Iref, 1.13 mA|



Max Current with 6 LEDs on white, max brightness: 334 mA

Spell Warm-up time: 10 s

Spell Cool-down time: 60 s



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)