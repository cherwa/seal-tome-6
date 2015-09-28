**Table of Contents**


---





---


![http://wiki.seal-tome-6.googlecode.com/hg/block.png](http://wiki.seal-tome-6.googlecode.com/hg/block.png)

# Phototransitor Schematic #

![http://wiki.seal-tome-6.googlecode.com/hg/schematic2.png](http://wiki.seal-tome-6.googlecode.com/hg/schematic2.png)



---

# Block Inputs/Outputs & Testpoints #

> ## Inputs ##

| **Input Name** | **Description of Signal** | **Expected Range** |
|:---------------|:--------------------------|:-------------------|
| J1- Pin 1      | Voltage Input             | 3.3V               |
| Phototransistor X5 | Light level determines how much current is passed through the phototransistor | No/Low Light level - Moderate/High Light level |
| Phototransistor X4 | Light level determines how much current is passed through the phototransistor | No/Low Light level - Moderate/High Light level |
| Phototransistor X3 | Light level determines how much current is passed through the phototransistor | No/Low Light level - Moderate/High Light level |
| Phototransistor X2 | Light level determines how much current is passed through the phototransistor | No/Low Light level - Moderate/High Light level |
| Phototransistor X1 | Light level determines how much current is passed through the phototransistor | No/Low Light level - Moderate/High Light level |


> ## Outputs ##

| **Output Name** | **Description of Signal** | **Expected Range** |
|:----------------|:--------------------------|:-------------------|
| J1 - Pin 3 (Interrupt Pin) | Output from phototransistor will be close to VDD (read as 1) when light level is high enough and will be close to Ground (read as 0) when light level is low enough. This pin will trigger the interrupt if read as high. | _No/low light:_ Less than .3 Volts, _Moderate/high light:_ Greater than 3 Volts|
| J1 - Pin 4      | Output from phototransistor will be close to VDD (read as 1) when light level is high enough and will be close to Ground (read as 0) when light level is low enough. | _No/low light:_ Less than .3 Volts, _Moderate/high light:_ Greater than 3 Volts|
| J1 - Pin 5      | Output from phototransistor will be close to VDD (read as 1) when light level is high enough and will be close to Ground (read as 0) when light level is low enough. | _No/low light:_ Less than .3 Volts, _Moderate/high light:_ Greater than 3 Volts|
| J1 - Pin 6      | Output from phototransistor will be close to VDD (read as 1) when light level is high enough and will be close to Ground (read as 0) when light level is low enough. | _No/low light:_ Less than .3 Volts, _Moderate/high light:_ Greater than 3 Volts|
| J1 - Pin 7      | Output from phototransistor will be close to VDD (read as 1) when light level is high enough and will be close to Ground (read as 0) when light level is low enough. | _No/low light:_ Less than .3 Volts, _Moderate/high light:_ Greater than 3 Volts|

> ## Functions ##

> ### Page Selection Function ###
> Depending on which phototransistors are exposed to light, the Page selection function returns a value that tells the rest of the program which spell to execute. This is done through the use of a global variable that the other parts of the program will use. If a phototransistor is exposed to light, it will be read as a 1, otherwise it will be read as a 0. The spell that’s cast depends on how many transistors are exposed to light. Due to the nature of the setup, a phototransistors shouldn’t turn on unless the previous one is on. (i.e. Pin 7 can’t read a 1 unless Pin 6 reads a 1, Pin 6 can’t read a 1 unless Pin 5 reads a 1, etc…)

![http://wiki.seal-tome-6.googlecode.com/hg/phototransistor%20flowchart.png](http://wiki.seal-tome-6.googlecode.com/hg/phototransistor%20flowchart.png)
<img src='http://wiki.seal-tome-6.googlecode.com/hg/phototransistor%20flowchart2.1.png' align='right' title='Flowchart 2' />

> ### Input Parameters ###

| **Control[4:0] (Pin 7, Pin 6, Pin 5, Pin 4, Pin 3)** | **Return Value (Global Variable)** |
|:-----------------------------------------------------|:-----------------------------------|
| 00000                                                | Book is Closed (GV = 0)            |
| 00001                                                | Open to page 1 (GV = 1)            |
| 00011                                                | Open to page 2 (GV = 2)            |
| 00111                                                | Open to page 3 (GV = 3)            |
| 01111                                                | Open to page 4 (GV = 4)            |
| 11111                                                | Open to page 5 (GV = 5)            |
| XXXXX (anything else)                                | Treat as closed (GV = 0)           |

> ## Testpoints ##

| **Test Point** | **Description of Signal and Measurement Conditions** | **Range of Values** |
|:---------------|:-----------------------------------------------------|:--------------------|
| TP - VDD       | Voltage Input. Should always be on and always be supplying a constant voltage. | VDD - 3.3V          |
| TP - X5        | Depending on the amount of light hitting the phototransistor, the amount of current allowed through it changes. This affects the voltage that the corresponding pin reads off of the pull-down resistor. | GND to VDD ≈ (0, to 3.3V) |
| TP - X4        | Depending on the amount of light hitting the phototransistor, the amount of current allowed through it changes. This affects the voltage that the corresponding pin reads off of the pull-down resistor. | GND to VDD ≈ (0, to 3.3V) |
| TP - X3        | Depending on the amount of light hitting the phototransistor, the amount of current allowed through it changes. This affects the voltage that the corresponding pin reads off of the pull-down resistor. | GND to VDD ≈ (0, to 3.3V) |
| TP - X2        | Depending on the amount of light hitting the phototransistor, the amount of current allowed through it changes. This affects the voltage that the corresponding pin reads off of the pull-down resistor. | GND to VDD ≈ (0, to 3.3V) |
| TP - X1        | Depending on the amount of light hitting the phototransistor, the amount of current allowed through it changes. This affects the voltage that the corresponding pin reads off of the pull-down resistor. | GND to VDD ≈ (0, to 3.3V) |


---


# Packaging #

To make sure that all the individual components would fit comfortably within our book, a simple AutoCAD Inventor model was made. With this model we are able to plan out the optimal layout and have a rough idea of what our finished product might look like.

http://wiki.seal-tome-6.googlecode.com/hg/book%20assembly2.bmp



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)