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

## Speaker Datasheet ##

![https://seal-tome-6.googlecode.com/hg/protyping/Audio/Speaker%20Datasheet.png](https://seal-tome-6.googlecode.com/hg/protyping/Audio/Speaker%20Datasheet.png)

## Block Diagram / Flow Chart ##

![https://seal-tome-6.googlecode.com/hg/protyping/Audio/Block%20Diagram.png](https://seal-tome-6.googlecode.com/hg/protyping/Audio/Block%20Diagram.png)



![https://seal-tome-6.googlecode.com/hg/protyping/Audio/Flow%20Chart.png](https://seal-tome-6.googlecode.com/hg/protyping/Audio/Flow%20Chart.png)

**Choice 1:** [WTV020-SD datasheet](https://dlnmh9ip6v2uc.cloudfront.net/datasheets/Widgets/WTV020SD.pdf) – Audio driver



---


---

Tome Links

---

_[Main Block Programming](MainBlock.md)_<br />[Power](Power.md)<br />[Visuals](Visuals.md)<br />[Packaging](Packaging.md)<br />[Audio](Audio.md)<br />[Communication](Communication.md)<br />_[Back to The Tome's Main Page](Sorcerers_Spelltome_Wiki_Main.md)_


---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)