**Table of Contents**


---





---


#summary IR & XBee Communication (Prototype Phase).
<a href='http://tinypic.com?ref=11rgghx'><img src='http://i42.tinypic.com/11rgghx.png' alt='Image and video hosting by TinyPic' border='0'>
<br />
<h1><b>IR Emitters</b></h1>

<a href='http://tinypic.com?ref=2njvh5l'><img src='http://i40.tinypic.com/2njvh5l.png' alt='Image and video hosting by TinyPic' border='0'><br />

Each of the LEDs in the circuit has their own break-out board (and are attached by socket-header connections), and can be removed/interchanged at any time (for testing purposes). Surface-mount potentiometers (with a resistance range of several hundred Ohms) have been placed with each different angle LED array, so that the current through the LEDs can be altered in order to find maximum radiant intensity and, therefore, maximum transmission range. <br />

<a href='http://tinypic.com?ref=15zrx1x'><img src='http://i44.tinypic.com/15zrx1x.png' alt='Image and video hosting by TinyPic' border='0'><br />

<h2><b>void ir56k_cycle()</b></h2>
Generates a 56kHz square wave, which will be used to generate properly-formatted IR packets.<br>
<br>
<h2><b>void irDamage()</b></h2>
Generates IR packets corresponding to a damage signal.<br>
<br>
<h2><b>void irHeal()</b></h2>
Generates IR packets corresponding to a heal signal.<br>
<br />

<h1><b>XBee</b></h1>

<a href='http://tinypic.com?ref=144jkl'><img src='http://i43.tinypic.com/144jkl.png' alt='Image and video hosting by TinyPic' border='0'><br />

The XBee has been placed into a pair of sockets and mounted on a break-out board. Only four pins (Vs, TX, RX, and GND) will be connected to the socket on the outside. <br />


<h1><b>IR Receiver (TSOP6256)</b></h1>

<a href='http://tinypic.com?ref=2w2pr8x'><img src='http://i40.tinypic.com/2w2pr8x.png' alt='Image and video hosting by TinyPic' border='0'><br />

The receiver has been placed into a pair of sockets and mounted on a break-out board. Pins 1, 3, and 4  are connected to the lone socket on the left (not including Pin 2). <br />

<a href='http://tinypic.com?ref=kc87b'><img src='http://i39.tinypic.com/kc87b.png' alt='Image and video hosting by TinyPic' border='0'><br />

<h1><b>Inputs</b></h1>

<table><thead><th> </th><th>Input Name </th><th> Description of Signal </th><th> Expected Range </th></thead><tbody>
<tr><td>IR LEDs</td><td> Power (LED1 & LED2) </td><td> 56kHz signal from the PIC that powers the IR LED </td><td> 3.3V @ 25mA    </td></tr>
<tr><td>IR LEDS</td><td> Power (LED Array)</td><td> 56kHz signal from the PIC that powers the IR LED </td><td> 3.3V @ 25mA    </td></tr>
<tr><td>XBee</td><td> Vs (XBee) </td><td> Power the XBee        </td><td> 3.3V           </td></tr>
<tr><td>XBee</td><td> Rx (XBee) </td><td> Data transfer between PIC and XBee </td><td> 3.3V           </td></tr>
<tr><td>Receiver</td><td> Vs (TSOP6256) </td><td> Power the receiver    </td><td> 3.3V           </td></tr>
<br />
<br /></tbody></table>

<h1><b>Outputs</b></h1>

<table><thead><th> </th><th>Output Name </th><th> Description of Signal </th><th> Expected Range </th></thead><tbody>
<tr><td>IR LEDs</td><td> MIRP       </td><td> Output from the IR LEDs when powered with the manipulated 56kHz square wave signal </td><td> IR packets with a range of 15 feet (when being powered by the BJTs) </td></tr>
<tr><td>XBee</td><td> Player Buff</td><td> When prompted, the XBee will send a "player buff" to the MAGE server </td><td>                </td></tr>
<br />
<br /></tbody></table>

<a href='http://tinypic.com?ref=2ia62b6'><img src='http://i40.tinypic.com/2ia62b6.png' alt='Image and video hosting by TinyPic' border='0'><br />

An IR packet is composed of 600 cycles of 56kHz square wave bursts. One cycle corresponds to one period (approximately 18 microseconds). An “ON” signal is defined as the 56kHz burst, and an “OFF” signal is defined as no 56kHz signal.<br>
<br>
<a href='http://tinypic.com?ref=2daymg0'><img src='http://i40.tinypic.com/2daymg0.png' alt='Image and video hosting by TinyPic' border='0'><br />

This is the general formatting of each IR packet being sent with the IR LEDs. Every packet must start with ten “ON” cycles, and end with 150 “ON” cycles. For a damage packet, 20 “ON” and 130 “OFF” cycles are generated in the Data Envelope and the Redundant Data region. For a heal pack, 30 “ON” and 120 “OFF” cycles are generated in the Data Envelope and the Redundant Data region. Every packet ends with 150 straight “ON” cycles.<br>
<br />

<h1><b>Test-point</b></h1>
<table><thead><th>T.P.</th><th>Description of Signal and Measurement Conditions</th><th>Range of Values</th></thead><tbody>
<tr><td>Output from PIC to IR LED</td><td>The output from the PIC should be a manipulated 56kHz square wave signal. Plug an oscilloscope input to the output of the PIC to measure and examine the signal.</td><td> Damage/Heal Signal</td></tr></tbody></table>

<hr />
<a href='MainPage.md'>Home</a>

<a href='Research.md'>Research Home</a>

<a href='prototype.md'>Prototype Home</a>

<a href='Integration.md'>Integration Phase I Home</a>