**Table of Contents**


---





---


#summary Audio

# Introduction #
For the audio effect, we are planning on using the speakers to play music during the spell cast time, when the book receives damage, and during a fail cast time.

# Research #

**Audio Circuit Overview – Method I**
**(Two Line Serial Mode – PWM Output)**

![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/audio%20circuit.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/audio%20circuit.jpg)
![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/audio%20specs.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/audio%20specs.jpg)

**NOTE:  UPON FURTHER RESEARCH ON FORUMS RELATED TO THE OPERATION OF THE DEVICE OPTIMAL VOLTAGE IS 3.55 (V) AND OPERATIONAL CURRENT DRAW IS 100 (mA). THE DEVICE ALSO SUPPORTS SD CARDS UP TO 2 (GB) FORMATTED FOR THE (FAT) FILE SYSTEM.**

NOTE2: DATASHEET DOESN’T SPECIRFY SPEAKER OUTPUT BUT ON THE WEBSITE AT SPARKFUN.COM IT SAYS IT CAN DRIVE A SPEAKER RATED FOR (8 Ohm / 0.5 W).

SD Card Details **![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/sd%20card%20details.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/sd%20card%20details.jpg)
![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/example%20dat%20in.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/example%20dat%20in.jpg)**

**Timing Waveform in Two Line Serial Mode**

![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/timing%20waveform.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/timing%20waveform.jpg)

**Audio Circuit Overview – Method II
(Two Line Serial Mode – PWM Output)**

![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/audio%20circuit%20method%20ii.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/audio%20circuit%20method%20ii.jpg)

For this method we would use a PIC 16F1825 and manually read/write from SD Card using SPI. The rest of the requirements would be almost identical. We chose to go with Method I since the interface with the SD Card is already taken care of, so the cost in time would be less.

## Block Diagram / Flow chart for method I ##

![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/block%20diagram%20method%20i.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/block%20diagram%20method%20i.jpg)
![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/flow%20chart%20method%20i.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/flow%20chart%20method%20i.jpg)

## Block Diagram / Flow chart for method II ##
![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/block%20diagram%20method%20ii.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/block%20diagram%20method%20ii.jpg)
![https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/flow%20chart%20method%20ii.jpg](https://seal-tome-6.googlecode.com/hg/Research/Research%20Audio/flow%20chart%20method%20ii.jpg)

**Choice 1:** [WTV020-SD datasheet](https://dlnmh9ip6v2uc.cloudfront.net/datasheets/Widgets/WTV020SD.pdf) – Audio driver

**Choice 2:** [PIC16f1825 datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/41440C.pdf) – using the PIC to read the audio file

**Choice 3:** [595-TLC7528CDW datasheet](http://www.mouser.com/ds/2/405/slas062e-196033.pdf) – Using a DAC to produce sine waves

**Audio Circuit Overview – Method III
(Two Line Serial Mode – PWM Output)**

Generate audio from stored bit streams located on the PIC directly and play them back with PWM DAC through a speaker. This method seemed incredibly complex with a lower audio quality and similar cost to the other two methods, so we decided to go with Method I instead.



---


---


---



---


[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)