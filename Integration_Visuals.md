# Introduction #

Add your content here.


# Details #

# LED.h code: #
```
/* 
 * File:   LED.h
 * Author: Michael Oatman
 *
 * Created on November 1, 2013, 7:49 PM
 */

#ifndef LED_H
#define	LED_H

// globals
uint8_t LED1byte1 = 0;
uint8_t LED1byte2 = 0;
uint8_t LED1byte3 = 0;
uint8_t LED2byte1 = 0;
uint8_t LED2byte2 = 0;
uint8_t LED2byte3 = 0;
uint8_t LED1bright1 = 127;
uint8_t LED1bright2 = 127;
uint8_t LED1bright3 = 127;
uint8_t LED2bright1 = 64;
uint8_t LED2bright2 = 64;
uint8_t LED2bright3 = 64;

uint8_t LED_R = 0;
uint8_t LED_G = 0;
uint8_t LED_B = 0;

uint8_t tomeHealth = 100;

// defs
#define Sin PORTDbits.RD0
#define SClk PORTDbits.RD1
#define Lat PORTDbits.RD2
#define Blnk PORTDbits.RD3
#define ON 1
#define OFF 0


//function delclarations
void bitChange(void);
void setBrightness();
void updateLeds();
void delay2( int value);
void updateHealthIndication();

// functions
    void delay2(int value)
    {
    for(int i = 0; i < value; i++)
        __delay_ms(10);
    }


    void updateHealthIndication()
    {
        if(tomeHealth > 80)
        {
            LED2byte1 = 0;
            LED2byte2 = 32 + 4;
            LED2byte3 = 64 + 8 + 1;
            updateLeds();
        }

        else if (tomeHealth > 60)
        {
            LED2byte1 = 0;
            LED2byte2 = 32;
            LED2byte3 = 64 + 8 + 1;
            updateLeds();
        }

        else if (tomeHealth > 40)
        {
            LED2byte1 = 0;
            LED2byte2 = 0;
            LED2byte3 = 64 + 128 + 8 + 16 + 2 + 1;
            updateLeds();
        }

        else if (tomeHealth > 20)
        {
            LED2byte1 = 0;
            LED2byte2 = 0;
            LED2byte3 = 128 + 16;
            updateLeds();
        }

        else if (tomeHealth > 0)
        {
            LED2byte1 = 0;
            LED2byte2 = 0;
            LED2byte3 = 128;
            updateLeds();
        }

        else if (tomeHealth == 0 || tomeHealth > 100)
        {
            LED1byte1 = 128 + 64;
            LED1byte2 = 255;
            LED1byte3 = 255;
            updateLeds();
            delay2(2);

            LED1byte1 = 0;
            LED1byte2 = 0;
            LED1byte3 = 0;
            updateLeds();
            delay2(2);

            LED1byte1 = 128 + 64;
            LED1byte2 = 255;
            LED1byte3 = 255;
            updateLeds();
            delay2(2);

            LED1byte1 = 0;
            LED1byte2 = 0;
            LED1byte3 = 0;
            updateLeds();
            delay2(2);

            LED1byte1 = 128 + 64;
            LED1byte2 = 255;
            LED1byte3 = 255;
            updateLeds();
            delay2(2);

            LED1byte1 = 0;
            LED1byte2 = 0;
            LED1byte3 = 0;
            updateLeds();
        }
    }




void setBrightness()
{
        SClk  = 0;
	Sin = 1;
	SClk = 1;


	Sin = 0;
        SClk = 0;
	SClk = 1;

        SClk = 0;
	SClk = 1;

	SClk = 0;
	SClk = 1;

	uint8_t currentByte = LED1bright1;

	for(uint8_t i = 0; i < 7; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

        currentByte = LED1bright2;

	for(uint8_t i = 0; i < 7; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}


        currentByte = LED1bright3;

	for(uint8_t i = 0; i < 7; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

        Sin = 1;

        SClk = 0;
        SClk = 1;

        Sin = 0;

        SClk = 0;
        SClk = 1;

        SClk = 0;
        SClk = 1;

        SClk = 0;
        SClk = 1;

        currentByte = LED2bright1;

	for(uint8_t i = 0; i < 7; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

        currentByte = LED2bright2;

	for(uint8_t i = 0; i < 7; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}


        currentByte = LED2bright3;

	for(uint8_t i = 0; i < 7; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}


        SClk = 0;


        Blnk = 1;
	Lat = 1;
        Sin = 0;
	Lat = 0;
        Blnk = 0;

}
void bitChange(void)
{
    LED1byte1 = ((LED_R & 0x01) <<6) + ((LED_G & 0x01) <<7);
    LED1byte2 = ((LED_B & 0x01)) + ((LED_R & 0x02)) + ((LED_G & 0x02) << 1) + ((LED_B & 0x02) << 2) +
            ((LED_R & 0x04) << 2) + ((LED_G & 0x04) << 3) + ((LED_B & 0x04) << 4) + ((LED_R & 0x08) << 4);
    LED1byte3 = ((LED_G & 0x08) >> 3) + ((LED_B & 0x08) >> 2) + ((LED_R & 0x10) >> 2) + ((LED_G & 0x10) >> 1) +
            ((LED_B & 0x10)) + ((LED_R & 0x20)) + ((LED_G & 0x20) << 1) + ((LED_B & 0x20) << 2);
}

void updateLeds()
{
    bitChange();
        SClk = 0;
	Sin = 0;
	SClk = 1;

	uint8_t currentByte = LED1byte1;

	for(uint8_t i = 0; i < 8; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

	currentByte = LED1byte2;

	for(uint8_t i = 0; i < 8; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

	currentByte = LED1byte3;

	for(uint8_t i = 0; i < 8; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

        Sin = 0;
        SClk = 0;
        SClk = 1;

        currentByte = LED2byte1;

	for(uint8_t i = 0; i < 8; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

	currentByte = LED2byte2;

	for(uint8_t i = 0; i < 8; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

	currentByte = LED2byte3;

	for(uint8_t i = 0; i < 8; i++)
	{
		Sin = (currentByte & 1);
                SClk = 0;
		SClk = 1;
		currentByte = currentByte >> 1;
	}

        SClk = 0;

        Blnk = 1;
	Lat = 1;
        Sin = 0;
	Lat = 0;
        Blnk = 0;
        setBrightness();
}


#endif	/* LED_H */

```


---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)