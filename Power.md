**Table of Contents**


---





---


#summary Power\_Block_&_Functional\_Hardware\_Switching

# Introduction #
The sorcerer's Spelltome is powered by a 5V battery and is rechargeable.  The 5V supply is "Bucked" down to 3.3V and distributed to multiple paths for each component within the system.

---

# Research #

## Supply: ##
The Sorcerer’s Spelltome is powered by a 5V usb portable and rechargeable power supply (Anker Astro).  This power source is capable of delivering 5.6A for an hour.  As an alternate selection (Anker Astro Mini) can supply 3 Amps for an hour.  Both of these supplies are basically portable cell phone chargers.<br />

---


## Power Regulation for Electrical Components ##
1 3.3V switching “Buck” regulator will be used to supply the Audio, RGB driver and LEDs, as well as the Xbee communication device.  1 3.3V switching “Buck” regulator will be used to supply the packaging, the PIC microprocessor, as well as the IR LED’s group of BJTs.  This is a total of TWO regulators to split the duty of regulating the 5V supply into two groups.<br />
The Texas Instruments LM2852YMXA-3.0/NOPB will be the first choice.  This regulator has a 1.5MHz switching frequency.  This is the more efficient option but will require more components to get it incorporated into our system.  This option will require three extra capacitors and an inductor.  A second 3.3V switching regulator of the same<br />
The second choice will be the Texas Instruments TPS78633DCQ.  This regulator is of the Low-Drop-Out type.  We will lose efficiency but will be gaining a less complex component as well as a less noisy circuit.<br />
The third choice will be the TPS78633KTTT.  This design is of the less efficient type.  It is an LDO with 7mV Load Regulation.<br />
Just as a backup, we have decided to include another option.  This option is the RECOM R-78B3.3-1.5L.  This is a Switching type of Regulator.  It is quite a bit more expensive but, they have been proven to be quite reliable and resilient to changes in load as well as input.<br />

### The following table table shows the differences between the options: ###

|Regulator|Type|Dropout(V)|Load Regulation|Line Regulation|Output Current|Output Voltage|Price $ |
|:--------|:---|:---------|:--------------|:--------------|:-------------|:-------------|:-------|
|LM2852YMXA3.0/NOPB|Switching at 1.5MHz|N/A       |8mV            |N/A            |1.5A          |3.3V          |3.77    |
|TPS78633DCQ | LDO|.51V @ 1.5A|7mV            |5% / Volt      |1.5A          |3.3V          |3.72    |
|TPS78633KTTT | LDO|.51V @ 1.5A|7mV            |5% / Volt      |1.5A          |3.3V          |3.73    |
|R-78B3.3-1.5L|Switching|N/A       |N/A            |N/A            |1.5A          |3.3V          |$11.64  |

---


## Power Switching for Electrical Components ##
The IR LEDs will be controlled with an NPN BJT device.  Each LED will have one NPN transistor allowing current to flow through it.  The Bipolar Junction Transistor device will serve as a current substitution so that the Tome’s microprocessor is not used as a current sink or source.  The appropriate section found within this data sheet will show the connections required for the LEDs to function properly with the supplied data transmission packets.  Packaging alternates have been shown but the surface mount approach will save space.  The current limiting resistors (potentiometers) have been included to dial the system in for maximum intensity.<br />
First Transistor option used for switching:  BJT (NPN) MMBT2222A (SMD package).  The cost for this device is $0.18 cents per piece.<br />
The second option will be to use the NXP PBSS4130PANP (SMD package).  This transistor is quite a bit more expensive at $.48 per piece.  This will not be a very wise choice to make for our switching needs due to the price.<br />
There does seem to be a difference in the switching time for the devices by a difference of 5 nano seconds.  The cheaper option is faster at switching on by 5 nano seconds but slower at switching off by 5 nano seconds.  Even with these things considered, these factors will not be a limiting situation in our data transmission or packet scheme.  We will be transmitting a packet at a frequency of 56kHz.  This is well beyond the limits of the switching time for the BJTs.<br />

### Circuit For Switching ###
![https://seal-tome-6.googlecode.com/hg/switchingCircuits.jpg](https://seal-tome-6.googlecode.com/hg/switchingCircuits.jpg)

---

## References: ##

**Amazon.com for the Portable Power Battery Banks**<br />
5600mAh (Anker): <br />
http://www.amazon.com/Portable-External-Flashlight-Thunderbolt-Incredible/dp/B005K7192G/ref=pd_sim_cps_6

**3000mAh Ultra-Compact External Battery Backup Charger:**<br />http://www.amazon.com/Ultra-Compact-Lipstick-Sized-Sensation-ThunderBolt-Blackberry/dp/B005NF5NTK/ref=sr_1_fkmr0_3?ie=UTF8&qid=1381174868&sr=8-3-fkmr0&keywords=portable+power+supply6000mAh

**Texas Instruments (Understanding the Terms and Definitions of LDO Voltage Regulators)**<br />
http://www.ti.com/lit/an/slva079/slva079.pdf

**Wikipedia (Voltage Regulator)**<br />
http://en.wikipedia.org/wiki/Voltage_regulator

**Texas Instruments (Linear and Switching Voltage Regulator Fundamental part 1)**<br />
http://www.ti.com/lit/an/snva558/snva558.pdf

**Analog Devices (Understanding how voltage regulators work)**<br />
http://www.analog.com/en/content/ta_fundamentals_of_voltage_regulators/fca.html

**Dimension Engineering (A Beginner’s guide to Switching Regulators)**<br />
http://www.dimensionengineering.com/info/switching-regulators



---


---


---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)