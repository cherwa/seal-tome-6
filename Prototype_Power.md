**Table of Contents**


---





---


#summary This is the Power Block Prototyping page.

# POWER BLOCK MAIN BLOCK DIAGRAM #
https://seal-tome-6.googlecode.com/hg/power_BlockDiagarm.JPG

This block feeds 3.3V to all the components of the Spelltome.
After a shipping problem with FEDEX, the RECOM option was decided to be used.  See bottom of page for a picture of the device.

---


## POWER BLOCK SCHEMATIC ##

![https://seal-tome-6.googlecode.com/hg/powerSchematic.jpg](https://seal-tome-6.googlecode.com/hg/powerSchematic.jpg)

## POWER BLOCK - FUNCTIONAL LIST ##

  * 5V input from battery at label J1

  * Label J5 is switch in the form of a jumper to turn supply ON/OFF

  * Diode D1 (1N4007) is reverse current protection for regulator R-78B-1.5

  * J2 (Grnd) is Ground Connection for Regulator Output

  * J3 (V+ Power Output) is Positive Voltage Output Connection for Regulator

  * J4 is a single pair of outputs to supply PIC board and functions as a test point (Square indicator is V+)

  * U2 is 5V to 3.3V DC/DC converter (RECOM R-78B-1.5)

  * Voltage is supplied through MiniUSB-B jack to board (Regulated 5V- 1A)



---

## POWER BLOCK – TEST DATA ##

Here you will find data that was collected to verify that the Tome would actually receive enough power to operate.  This regulator is a serious piece of equipment.  As you can see, we varied the load by quite a bit and the current stayed very near 3 Volts and very near 1 amp (see diagram below)

The Seal Tome 6 Power block was tested with 5V input voltage dropped across a Rheostat (1.5 Ohm to 10.6 Ohm value) in series with high wattage Resistor (2.7 Ohm) rated at 1A.  This gave us close to 13 Ohms to drop the power supply’s output voltage across.  The Rheostat is not a precision piece of equipment.  This is why "close to" and "around" is used to describe its value.  The mechanical nature of the device gave some strange readings close to its max and min Resistance values.

The current was limited to 1A from the 5V supply.  The output current and voltage of the R-78B-1.5 was measured as the load was varied from highest value (~13 Ohm) to lowest value (~3.0 Ohm).  The R-78B-1.5 behaved as expected and varied in voltage from 3.2V to 3.32 volts with around .97mA max current output and .26mA minimum output.  The graph below shows the date acquired during the test:

https://seal-tome-6.googlecode.com/hg/Voltage%20output%20vs.%20Current%2012%20Ohm%20load.JPG

|**Increment**|**Voltage Across the Output (Volts)**|**Current Through Load (Amps)**|**Load Value (Ohms)**|
|:------------|:------------------------------------|:------------------------------|:--------------------|
|Step 1       |3.2                                  |0.97                           |3.298969072          |
|Step 2       |3.2                                  |0.92                           |3.47826087           |
|Step 3       |3.22                                 |0.86                           |3.744186047          |
|Step 4       |3.23                                 |0.8                            |4.0375               |
|Step 5       |3.24                                 |0.75                           |4.32                 |
|Step 6       |3.25                                 |0.7                            |4.642857143          |
|Step 7       |3.25                                 |0.68                           |4.779411765          |
|Step 8       |3.26                                 |0.64                           |5.09375              |
|Step 9       |3.27                                 |0.59                           |5.542372881          |
|Step 10      |3.27                                 |0.57                           |5.736842105          |
|Step 11      |3.27                                 |0.54                           |6.055555556          |
|Step 12      |3.28                                 |0.5                            |6.56                 |
|Step 13      |3.28                                 |0.49                           |6.693877551          |
|Step 14      |3.29                                 |0.46                           |7.152173913          |
|Step 15      |3.29                                 |0.44                           |7.477272727          |
|Step 16      |3.29                                 |0.42                           |7.833333333          |
|Step 17      |3.3                                  |0.4                            |8.25                 |
|Step 18	     |3.3	                                 |0.39	                          |8.461538462          |
|Step 19	     |3.3	                                 |0.36	                          |9.166666667          |
|Step 20	     |3.31	                                |0.34	                          |9.735294118          |
|Step 21	     |3.31	                                |0.33	                          |10.03030303          |
|Step 22	     |3.31	                                |0.31	                          |10.67741935          |
|Step 23	     |3.31	                                |0.3	                           |11.03333333          |
|Step 24	     |3.31	                                |0.29	                          |11.4137931           |
|Step 25	     |3.32	                                |0.28	                          |11.85714286          |
|Step 26	     |3.32	                                |0.27	                          |12.2962963           |
|Step 27	     |3.32	                                |0.26	                          |12.76923077          |
|Step 28	     |3.32	                                |0.26	                          |12.76923077          |


---

# POWER SWITCHING BLOCK DIAGRAM AT IR BLOCK #

Below you will find a block diagram for the Power Switching portion of the IR block.

https://seal-tome-6.googlecode.com/hg/powerSwitching_BlockDiagarm1.JPG

---

## BJT POWER SWITCHING SCHEMATIC ##
![https://seal-tome-6.googlecode.com/hg/BJTschematic.jpg](https://seal-tome-6.googlecode.com/hg/BJTschematic.jpg)

## FUNCTIONAL LIST FOR POWER SWITCHING BLOCK ##

The Base of the BJT takes a control signal in and uses this to turn on the Collector - Emitter junction.  This allows the current to flow from the Collector to the Emitter as the BJT is in Saturation mode.


  * BJT is MMBT2222A Fairchild Semiconductor
  * BJT is operated in Saturation Mode i.e. both junctions are forward biased
    * This allows a near short to appear across Vce (actually around .22V drop)
    * This near short allows Ic to flow
  * Applied Voltages:
    * E < B > C
  * J1 is Input from PIC Port B to BASE (3.3V – 25mA max)
    * Current testable inline to header J1
    * Voltage testable across header J1 to header J3 (Emitter Output to Ground Connection)
  * J2 is Input from IR LED Board to Collector of BJT (3.3V – 100mA max)
    * Current testable inline to header J2
    * Voltage testable across header J2 to header J3 (Emitter Output to Ground Connection)
    * Max current based upon 360 degree LED maximum forward current value
  * Upon input to BASE (current > 0), signal turns BJT to ON and passes current through Vc to Ve portion of the BJT (ic).  This allows the IR LEDs to be fired at the frequency in which the signal is applied to the BASE of BJT.
  * A potentiometer has been included to tune the output of the IR LEDs (relative to intensity) by decreasing the applied current Ic.  Nominal values where calculated as follows:
    * BASE current limiting resistance = 132 Ohms
  * This value allows a theoretical 25mA to flow to the BASE of BJT.
    * COLLECTOR current limiting resistance = 31 Ohms
  * This value allows a theoretical 100mA to flow as Ic.

---

## BJT TEST DATA ##

The BJT circuit below has two different resistor values that were of question while building this circuit.  It was known that the BJT's needed to be operated in saturation mode to created the switching necessary in the system.    Theoretically, the voltage drop once the BJT is turned on (i.e. once the base has received current and thus the junction between C and E is made to pass current that adds to the current being passed into the base) is extremely low ~ .02V.  This is seen as a near short but is still a voltage drop.  It was measured to be .022V.

For the BJT to be effective, the Base voltage must be greater than the Collector and the Emitter voltage.  This in fact does happen once the voltage drops occur across the resistor and IR LED.  The base voltage is 3.3V due to the supply from the PIC side and the current was found to be around 16mA.
The voltage across B to E was found to be .796V.
The voltage across C to E was found to be .022V.

The resistor values that were found to keep the nominal operating current available through the LEDs are below:

Small angle resistance:  23 Ohms with a Forward Voltage Drop = 1.5V
Medium angle resistance:  26 Ohms with a Forward Voltage Drop = 1.35V
Large angle resistance:  15 Ohms with a Forward Voltage Drop = 1.6V

These values may be substituted in the circuit for the potentiometers that are found before the IR LEDs and above the Collector port of the BJTs.  The nominal value found for the Base port of the BJT is 31 Ohms.  The value that maximized the current into the base was 33 Ohms.


---


# CONCLUSION #
The amount of power consumed by the Tome was surprising.  We estimated that it would draw around 1 amp with everything on....that means full white bright on the two sets of LEDs and the sound being pumped out of the speakers as well.  We measured somewhere around ??? (TO BE MEASURED WITH FINAL SYSTEM)....We already know that the whole system only draws around 600mA without the audio.  This is surprising but, we are only using certain colors (no white).

# PHOTOS #
https://seal-tome-6.googlecode.com/hg/power_proto0.JPG




---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)