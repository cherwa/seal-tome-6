**Table of Contents**


---





---


#summary Visuals

# Introduction #

For the visual effects, we are planning on using LED’s to shine through a sheet of plexi glass. This Plexi glass will be cut up to direct the light at specific angels. During the cool down different edges of the book will illuminate to indicate the time before you can cast a spell.

![http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/BDVis.png](http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/BDVis.png)

# Research #

For the Visual effect, we will be choosing the TLC5652 RGB LED Driver. This driver can control up to 8 RGB LEDs with the following control lines:

•	Serial IN 1 and 2

•	Serial Clock

•	Latch

•	Blank

We will be using 2 RGB driver. One for the Spell cool down, and cast animation, and one for the health. This may however drop down to one, if the number of RGB LEDs we need are low enough that we just need to use one driver. This all depends on how we plan to implement the visual effects.
For the LED, we are deciding on a surface mount RGB LED, model PLCC6 3. This LED is small enough (5x6mm) and bright enough, with an average of 500 Milli-Candela for each RGB light (typical LED is about 50 mcd) for our applications.

| Parameter |	Value | Units |
|:----------|:------|:------|
| Pins needed | 5     | N/A   |
| RGB LEDs Needed | 11    | N/A   |
| Max Forward Current for LEDs | 50    | mA    |
| Max Supply Current for LEDs from driver | 45 (R and G) and 35 (B) | mA    |
| Recommended Supply Current | 35 (R and G) and 26.2 (B) | mA    |
| Supply Voltage Range | -0.3 to 6.0 | V     |
| Recommended Supply Voltage | 3.3   | V     |
| Max Current Needed by System | 0.65  | A     |
| Max Power Needed by System | 2.31  | W     |
| RIref     | 1.4   | kΩ    |


# Function Flowcharts #


![http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCUpdateVis.png](http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCUpdateVis.png)

All LED updating will be done with one function, and any time an LED is turned on or off by a function (by or-ing the bit into the right variable) that is completely linear as this flowchart demonstrates. Note that since there are multiple LED drivers, this is done for both LED drivers in parallel. It has no input, however, for each LED there are 3 global bytes that contain the on/off information for each LED.

![http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCHealthVis.png](http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCHealthVis.png)

This function is called every time the health changes and at startup. It determines which of the health LEDs are to be lit and of which color.



# Alternative Approaches #

![http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/BDAltVis.png](http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/BDAltVis.png)


The first approach before we considered the LED driver approach was driving all the LEDs with BJTs. This was one of the most basic approaches we could have taken, but we decided against it for a few reasons. Firstly, it took too many pins, since each health LED had to be driven separately. Secondly, it was reinventing the wheel that LED drivers provided, and the hunt for the right BJTs might be complicated. Lastly, we would not have the flexibility to make the health LEDs different colors with this method.

![http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCAltVis.png](http://seal-tome-6.googlecode.com/hg/Research/Research%20Visual/FCAltVis.png)


This is the flowchart we would have used for this. Like the serial communication flowchart, it is completely linear, but much more basic since it is simply parallel communication.



# Data Sources #

Texas Instruments, “24-Channel, Constant-Current LED Driver with Global Brightness Control and LED Open-Short Detection,” TLC5952 datasheet, May 2009

https://www.dropbox.com/s/67y9bmsiw0q6v8q/LED%20Driver%20sbvs129.pdf

This is the datasheet for the LED driver our group has decided to use. After looking into it, we have decided it fits the requirements of our project, and we only need to find compatible parts.


CREE, “Cree® PLCC6 3 in 1 SMD LED CLP6C-FKB,” CLP6C-FKB datasheet, 2011

https://www.dropbox.com/s/6wwb2y0nofn3b1g/CLP6CFKB%28933%29.pdf

This is the datasheet for the LEDs our group has decided to use in conjunction with the LED driver. This reference is useful because it notifies us the current rating for the LEDs, the brightness, and the size, all of which fit well with our LED driver and project requirements. The LEDs also have six pins, and no common anode or cathode, and thus are more flexible than those with a common anode or cathode.



Microchip, “28/40/44/64-Pin, Enhanced Flash Microcontrollers with ECAN™ and nanoWatt XLP Technology,” PIC18F66K80 FAMILY datasheet, Nov. 2011

This is the datasheet for the PIC family we have chosen, and more specifically, we have decided on the 44 pin. This datasheet is useful to me because it notifies me if the microcontroller we chose is compatible or not with the LED driver that I am researching. From this I can gather that it does have the outputs to support the LED driver, and has enough left over for the other sections of this project.



D. Crunkilton (June 2005). Serial-in/serial-out shift register. [Online](Online.md). Available FTP: http://www.allaboutcircuits.com Directory: /vol\_4/chpt\_12/ File: 2.html

This source instructed me on how to use a shift register alongside a serial clock. The source was needed not only for future reference when it comes to integration, but was also needed for verification that the chosen LED driver could work with our chosen MCU.



Santais (October 5, 2009). Writing your first programme.. [Online](Online.md). Available: http://picstart.blogspot.com/2009/10/writing-your-first-programme.html

This source gave me information on some of the conventions of pic programming and enough information to write my part of the program. I am not the main PIC programmer and my code will most certainly be reviewed by my peers, but it is important to know the conventions of PIC programming either way.





China Young Sun LED Technology CO., LTD., “YSL-R596CR3G4B5C-C10 RED/GREEN/BLUE Triple Color LED,” YSL-R596CR3G4B5C-C10 datasheet, No Date Given

These RGB LEDs would have been a nice low power option, but ultimately there were a few factors that made us decide against them. Their common cathode design makes them less flexible when it comes to LED drivers, and they are not flat, so they would not fit well under the acrylic.



Texas Instruments, “16 CHANNEL LED DRIVER WITH DOT CORRECTION AND GRAYSCALE PWM CONTROL,” TLC5940 datasheet, October 2007

Very similar in design to our LED driver of choice, we almost chose this LED driver because of its availability in a breadboard ready form, which would make prototyping and testing it much easier. There were a few reasons that made us decide it was not fit for our purposes. The absolute maximum of current per channel is 120 mA compared to 45 mA for the driver we chose, which suggests this driver was meant for higher power applications. This driver has fewer pins than the TLC5952 as well, which means we would have to buy and solder more of them, which adds more overhead. Finally, this chip has programmable memory, which ultimately we would not use and would go to waste because of our design to have everything controlled from the PIC itself. This is definitely a workable alternative to our choice, but we feel it has too few output channels and just seems to be designed for higher power applications.





---


---


---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)

