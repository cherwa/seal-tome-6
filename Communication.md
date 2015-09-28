**Table of Contents**


---





---


#summary Communication

# Introduction #
The spell tome will be using infrared emitters (IR LEDs) to fire spells, an infrared receiver to register incoming signals from other users, and an XBee to communicate with the MAGE server when sending player buffs. The tome will have a variety of spells for the user to choose from, including two less-than-10 degree spread spells, a 55 to 65 degree spread spell, and 360 degree spread spell. These different angle spreads will be accomplished by choosing the appropriate beam angle for each IR LED. <br />

# Research #
## IR Receiver ##
The MIRP system requires that any IR receivers used need to have a carrier frequency of 56 kHz to properly register the action between users, so any receivers researched need to have the corresponding carrier frequency. Additionally, the minimum irradiance of the receiver should ideally be small. <br />

Listed below are the different infrared receivers that could be used for the spell tome. Based primarily on what previous groups have successfully used, and the 56 kHz frequency restriction, we have decided to use the TSOP6256TR receiver. If a larger data transmission rate is required, then the TSOP6156TR receiver will be used, which otherwise has the same specs as the TSOP6256TR receiver. Otherwise, the TSOP32256 or the TSOP2156 receiver will be used (based on the situation), which are cheaper than the TSOP6256TR receiver and have a smaller supply current.<br />
![https://seal-tome-6.googlecode.com/hg/General%20images/IR%20Receiver.png](https://seal-tome-6.googlecode.com/hg/General%20images/IR%20Receiver.png)

## IR LED (< 10 degree spread) ##
For the less-than-10 degree spread, any IR emitter considered needs to have a beam angle of less than 10 degrees. Additionally, to ensure that the outputted signal from the IR LED is strong enough and far-reaching enough to be properly registered by other users, the radiant intensity of the possible emitters needs to be as large as possible. <br />

The infrared emitter that the team will use for the less-than-10 degree spread spell will be the SFH 4545, which has the proper beam angle, a low price, and a high radiant intensity. The SFH4045 emitter, which also possesses the proper beam angle but has a much lower radiant intensity, will act as the fallback.<br />
![https://seal-tome-6.googlecode.com/hg/General%20images/IRLeds10deg.png](https://seal-tome-6.googlecode.com/hg/General%20images/IRLeds10deg.png)

## IR LED (55 to 65 degree spread) ##
With the 55 to 65 degree spread, any IR emitter considered should have a beam angle between the given boundaries. As explained in the less-than-10 degree spread IR LED, the radiant intensity needs to be as large as possible. <br />

The IR LED that the group wishes to use for the 55-to-65 degree spread spell will be the VSMB3940X01-GS08, which has the appropriate beam angle, a comparatively higher radiant intensity, and a lower cost. Next in line will be the SFH 4244-Z, then the SFH 4247-Z (ranked in descending order of radiant intensity).<br />
![https://seal-tome-6.googlecode.com/hg/General%20images/IRLeds55deg.png](https://seal-tome-6.googlecode.com/hg/General%20images/IRLeds55deg.png)

## IR LED (360 degree spread) ##
For the 360-degree spread spell, the team wishes to use an array of SMD infrared emitters placed inside the spell tome. The high radiant intensity signals from these LEDs will be manipulated by the plexiglass walls of the tome to output the 360-degree spell. For this case, the team will use the IR91-21C/TR7 emitter, which has a large radiant intensity for a surface-mount LED for a reasonable cost. However, if this plexiglass scheme fails, then an array of high radiant intensity through-hole IR emitters (IR333C/H0/L10) will be placed on the tome’s spine, instead.<br />
![https://seal-tome-6.googlecode.com/hg/General%20images/IRLeds360deg.png](https://seal-tome-6.googlecode.com/hg/General%20images/IRLeds360deg.png)

## Xbee ##
As the MAGE server uses the Zigbee firmware, any XBee considered needs to be a Series 1 (the Series 2 and 2B are not compatible with the Series 1 firmware). <br />
The group will use a 1mW Series 1 XBee to communicate with the MAGE server. While the Series 1 Pro XBee’s do have a higher output power and a longer range, the regular Series 1 XBee’s have a much lower cost and will still get the job done. The antenna used will either be a wire or PCB, depending on the situation. <br />

Choice 1:<br />
TSOP6256TR datasheet - IR receiver <br />
http://www.vishay.com/docs/82463/tsop62.pdf <br />

SFH 4545 datasheet – 10o IR LED<br />
http://www.mouser.com/ds/2/311/FH4545_Pb_free-226127.pdf <br />

VSMB3940X01-GS08 datasheet – 55 o – 65 o IR LED <br />
http://www.mouser.com/ds/2/427/vsmb3940-247521.pdf <br />

IR91-21C/TR7 datasheet – 360o IR LED<br />
http://www.mouser.com/ds/2/143/IR91_21C_TR7_datasheet-50806.pdf <br />

XBee Series 1 datasheet - XBee<br />
http://www.digi.com/products/wireless-wired-embedded-solutions/zigbee-rf-modules/point-multipoint-rfmodules/xbee-series1-module#specs <br />

Choice 2:<br />
TSOP32256 datasheet – IR receiver<br />
http://www.mouser.com/ds/2/427/tsop322-254180.pdf <br />

SFH 4045 datasheet – 10o IR LED<br />
http://www.mouser.com/ds/2/311/FH4045_Pb_free-226084.pdf <br />

SFH 4244-Z datasheet – 55 o – 65 o IR LED<br />
http://www.mouser.com/ds/2/311/FH4244_Pb_free-34815.pdf <br />

IR333C/H0/L10 datasheet – 360o IR LED<br />
http://www.mouser.com/ds/2/143/IR333_H0_L10_datasheet-26899.pdf <br />

Choice 3:<br />
SFH 4247-Z datasheet – 55 o – 65 o IR LED<br />
http://www.mouser.com/ds/2/311/FH4247_Pb_free-54646.pdf <br />



---


---


---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)