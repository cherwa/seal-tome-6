**Table of Contents**


---





---

# Introduction #

![https://seal-tome-6.googlecode.com/hg/integration/2013-11-11%2018.06.32.jpg](https://seal-tome-6.googlecode.com/hg/integration/2013-11-11%2018.06.32.jpg)


# Details #

The Pic boards is used to connect all the sub-components together. The ports are assigned as follow:
| Port | Assigned Ports | Description |
|:-----|:---------------|:------------|
| PORTB[0](0.md) & PORTB[2:5] | Photo-transistor | These are assigned to the photo-transistor input. This is done so that we can use an interrupt pin for the photo-transistor. PORT[1](1.md) is skipped so that we can use it for other interrupt pins |
| PORTB[1](1.md) | IR Receive     | Receives all IR packets, interrupts, and detects to see if is a heal or damage. |
| PORTC[2:0] | IR Send        | Sends the IR packet to each beam angle |
| PORTC[7:6] | XBEE           | DOUT and DIN I/O for XBEE |
| PORTD[3:0] | RGB LED Driver | Output lines to control health, and LED visual drivers |
| PORTE[2:0] | Audio Driver   | Output lines to control audio |

# main.c program: #
```
/******************************************************************************/
/* Files to Include                                                           */
/******************************************************************************/
#if defined(__XC)
    #include <xc.h>        /* XC8 General Include File */
#elif defined(HI_TECH_C)
    #include <htc.h>       /* HiTech General Include File */
#elif defined(__18CXX)
    #include <p18cxxx.h>   /* C18 General Include File */
#endif

#if defined(__XC) || defined(HI_TECH_C)

#include <stdint.h>        /* For uint8_t definition */
#include <stdbool.h>       /* For true/false definition */

#endif

#include "system.h"        /* System funct/params, like osc/peripheral config */
#include "user.h"          /* User funct/params, such as InitApp */
#include "AUDIO.h"
#include "LED.h"
#include "ir_xbee.h"

#define _XTAL_FREQ 16000000  //define frequency
/******************************************************************************/
/* User Global Variable Declaration                                           */
/******************************************************************************/
/* i.e. uint8_t <variable_name>; */
uint8_t spellReg = 0;
uint8_t startSpellFlag = 0;
uint8_t cd = 0;
uint8_t bookClose = 0;
uint8_t primeCount = 0;
uint8_t cdTime = 0;
//defs

/******************************************************************************/
/* Main Program                                                               */
/******************************************************************************/
void delay10ms(uint8_t i)
{
    for (int j = 0; j < i; j ++)
    {
        __delay_ms(10);
    }
}

void coolDown (void)
{
    for (cd; cd < 60; cd ++)
    {
        if (cd >= 0 && cd < 10)  //cd just started
        {
            LED_R = 0x01;
            updateLeds();
        }
        else if (cd >= 10 && cd < 20)  //cd 10 sec
        {
            LED_R = 0x03;
            updateLeds();
        }
        else if (cd >= 20 && cd < 30)  //cd 20 sec
        {
            LED_R = 0x07;
            updateLeds();
        }
        else if (cd >= 30 && cd < 40)  //cd 30 sec
        {
            LED_R = 0x0f;
            updateLeds();
        }
        else if (cd >= 40 && cd < 50)  //cd 40 sec
        {
            LED_R = 0x1f;
            updateLeds();
        }
        else if (cd >= 50 && cd < 59)  //cd 50 sec
        {
            LED_R = 0x3f;
            updateLeds();
        }
        else                        //cd ready
        {
            LED_R = 0x00;
            LED_G = 0x3f;
            updateLeds();
        }
        delay10ms(cdTime);
    }
    INTCONbits.INT0IE = 1;  //enable interupt
}
void startSpell(void)
{
    //INTCONbits.INT0IE = 0;  //disable book open int
    INTCON2bits.INTEDG0 = 1;    //detect rising edge of interrupt
    bookClose = 0;
    // need to update
    for(primeCount = 0; primeCount < 10; primeCount ++)
    {

        LED_R = 0xff;   //red
        LED_G = 0x00;
        LED_B = 0x00;
        updateLeds();
        delay10ms(15);

        LED_R = 0x00;   //green
        LED_G = 0xff;
        LED_B = 0x00;
        updateLeds();
        delay10ms(15);

        LED_R = 0x00;   //blue
        LED_G = 0x00;
        LED_B = 0xff;
        updateLeds();
        delay10ms(15);
    }
    INTCONbits.INT0IE = 0;  //disable book open int
    cd = 0;
    startSpellFlag = 0;
    if (bookClose == 0)
    {
        if ((spellReg == 0x01))// && ((~PORTB & 0x1f) == 0x01))
        {
            ATRIGGER(0);
            irDamage(1);
            delay10ms(5);
            for(int i = 0; i < 10; i++)  //Damage AOE
            {
                LED_R = 0xff;   //red + 2 yellow
                LED_G = 0x21;
                LED_B = 0x00;
                updateLeds();
                delay10ms(10);

                LED_R = 0xff;   //red + 2 yellow
                LED_G = 0x12;
                LED_B = 0x00;
                updateLeds();
                delay10ms(10);

                LED_R = 0xff;   //red + 2 yellow
                LED_G = 0x0c;
                LED_B = 0x00;
                updateLeds();
                delay10ms(10);

                LED_R = 0xff;   //red
                LED_G = 0x00;
                LED_B = 0x00;
                updateLeds();
                delay10ms(10);
            }
            ATRIGGER(STOP);
        }
        else if ((spellReg == 0x03))// && ((~PORTB & 0x1f) == 0x03))  //damage single
        {
            ATRIGGER(1);
            irDamage(0);
            delay10ms(5);
            for(int i = 0; i < 5; i++)
            {
                LED_R = 0x30;   //cyan blue magenta
                LED_G = 0x03;
                LED_B = 0x3f;
                updateLeds();
                delay10ms(15);

                LED_R = 0x18;   //cyan blue magenta 2
                LED_G = 0x21;
                LED_B = 0x3f;
                updateLeds();
                delay10ms(15);

                LED_R = 0x0c;   //blue magenta cyan
                LED_G = 0x30;
                LED_B = 0x3f;
                updateLeds();
                delay10ms(15);

                LED_R = 0x06;   //blue magenta cyan 2
                LED_G = 0x18;
                LED_B = 0x3f;
                updateLeds();
                delay10ms(15);

                LED_R = 0x03;   //magenta cyan blue
                LED_G = 0x0c;
                LED_B = 0x3f;
                updateLeds();
                delay10ms(15);

                LED_R = 0x21;   //magenta cyan blue 2
                LED_G = 0x06;
                LED_B = 0x3f;
                updateLeds();
                delay10ms(15);
            }
        }
        else if ((spellReg == 0x07))// && ((~PORTB & 0x1f) == 0x07))  //healing 360
        {
            ATRIGGER(1);
            irHeal(2);
            delay10ms(5);
            for(int i = 0; i < 8; i++)
            {
                LED_R = 0x00;   //green + 2 cyan
                LED_G = 0xff;
                LED_B = 0x09;
                updateLeds();
                delay10ms(20);

                LED_R = 0x00;   //green + 2 cyan
                LED_G = 0xff;
                LED_B = 0x12;
                updateLeds();
                delay10ms(20);

                LED_R = 0x00;   //green + 2 cyan
                LED_G = 0xff;
                LED_B = 0x24;
                updateLeds();
                delay10ms(20);
            }
            ATRIGGER(STOP);
        }
        else if ((spellReg == 0x0f))// && ((~PORTB & 0x1f) == 0x0f))   //healing single
        {
            ATRIGGER(1);
            irHeal(0);
            delay10ms(5);
            for(int i = 0; i < 2; i++)
            {
                LED_R = 0x00;   //green + 0 cyan
                LED_G = 0xff;
                LED_B = 0x00;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 1 cyan 1
                LED_G = 0xff;
                LED_B = 0x20;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 1 cyan 2
                LED_G = 0xff;
                LED_B = 0x10;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 1 cyan 3
                LED_G = 0xff;
                LED_B = 0x08;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 1 cyan 4
                LED_G = 0xff;
                LED_B = 0x04;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 1 cyan 5
                LED_G = 0xff;
                LED_B = 0x02;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 1 cyan 6
                LED_G = 0xff;
                LED_B = 0x01;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 2 cyan 1
                LED_G = 0xff;
                LED_B = 0x21;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 2 cyan 2
                LED_G = 0xff;
                LED_B = 0x11;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 2 cyan 3
                LED_G = 0xff;
                LED_B = 0x09;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 2 cyan 4
                LED_G = 0xff;
                LED_B = 0x05;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 2 cyan 5
                LED_G = 0xff;
                LED_B = 0x03;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 3 cyan 1
                LED_G = 0xff;
                LED_B = 0x23;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 3 cyan 2
                LED_G = 0xff;
                LED_B = 0x13;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 3 cyan 3
                LED_G = 0xff;
                LED_B = 0x0b;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 3 cyan 4
                LED_G = 0xff;
                LED_B = 0x07;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 4 cyan 1
                LED_G = 0xff;
                LED_B = 0x27;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 4 cyan 2
                LED_G = 0xff;
                LED_B = 0x17;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 4 cyan 3
                LED_G = 0xff;
                LED_B = 0x0f;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 5 cyan 1
                LED_G = 0xff;
                LED_B = 0x2f;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green + 5 cyan 2
                LED_G = 0xff;
                LED_B = 0x1f;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green
                LED_G = 0xff;
                LED_B = 0x00;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //cyan
                LED_G = 0xff;
                LED_B = 0x3f;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //green
                LED_G = 0xff;
                LED_B = 0x00;
                updateLeds();
                delay10ms(10);

                LED_R = 0x00;   //cyan
                LED_G = 0xff;
                LED_B = 0x3f;
                updateLeds();
                delay10ms(10);
            }
            ATRIGGER(STOP);
        }
        else if ((spellReg == 0x1f))// && ((~PORTB & 0x1f) == 0x1f))   //buff
        {
            ATRIGGER(1);
            Xbee_senddata();
            delay10ms(10);
            delay10ms(5);
            for(int i = 0; i < 5; i++)
            {
                LED_R = 0x00;   //green
                LED_G = 0xff;
                LED_B = 0x00;
                updateLeds();
                delay10ms(20);
                LED_R = 0xff;   //yellow
                LED_G = 0xff;
                LED_B = 0x00;
                updateLeds();
                delay10ms(20);

            }
            ATRIGGER(STOP);
        }
        else                    //bad spell
        {
            ATRIGGER(1);

            delay10ms(5);
            for(int i = 0; i < 5; i++)
            {
                LED_R = 0x2a;   //half red
                LED_G = 0x00;
                LED_B = 0x00;
                updateLeds();
                delay10ms(50);

                LED_R = 0x15;   //other half red
                LED_G = 0x00;
                LED_B = 0x00;
                updateLeds();
                delay10ms(50);
            }
            ATRIGGER(STOP);
        }
    }
    else    //book close
    {
        ATRIGGER(1);

        delay10ms(5);
        for(int i = 0; i < 5; i++)
        {
            LED_R = 0x00;   //half blue
            LED_G = 0x00;
            LED_B = 0x2a;
            updateLeds();
            delay10ms(50);

            LED_R = 0x00;   //other half blue
            LED_G = 0x00;
            LED_B = 0x15;
            updateLeds();
            delay10ms(50);
        }
        ATRIGGER(STOP);
    }
    INTCON2bits.INTEDG0 = 0;    //reset to falling edge
    LED_R = 0x00;   //all off
    LED_G = 0x00;
    LED_B = 0x00;
    updateLeds();
    delay10ms(50);
    ATRIGGER(STOP);
    bookClose = 0;
}

void main(void)
{
    OSCCON = 0b01110010; // set up internal 16 MHz clock
    /* Configure the oscillator for the device */
    ConfigureOscillator();

    /* Initialize I/O and Peripherals for application */
    InitApp();

    //initilize audio
    AINIT();

    /* TODO <INSERT USER APPLICATION CODE HERE> */

    //turns off analog
    ADCON0 = 0x00;
    ADCON1 = 0x0f;
    ADCON2 = 0x00;

    ANCON0 = 0x00;
    ANCON1 = 0x00;

    //set inputs and outputs
    TRISC = 0x00; // set as output
    TRISB = 0xff; //set RB0 as input for int
    TRISD = 0x00;
    PORTC = 0x00; //initilize

    PORTD = 0x00; //initilize portd


    // set up interrupts
    INTCONbits.INT0IE = 0; //disable Interrupt 0 (RB0 as interrupt)
    INTCON3bits.INT1IE = 1; //enable Interrupt 0 (RB1 as interrupt)

    INTCON2bits.INTEDG0 = 0; //cause RB0 interrupt at falling edge
    INTCON2bits.INTEDG1 = 0; //cause RB1 interrupt at falling edge

    INTCONbits.INT0IF = 0; //reset RB0 interrupt flag
    INTCON3bits.INT1IF = 0; //reset RB1 interrupt flag

    INTCONbits.GIE = 1;     //enables all unmask interurpt
    INTCONbits.PEIE = 1;
    ei();     // This is like fliping the master switch to enable interrupt


    //initialize led to blank
    LED_R = 0x00;
    LED_G = 0x00;
    LED_B = 0x00;
    updateLeds();
    startSpellFlag = 0;
    cd = 0;
    //xbee tris bits config
    //seting tris to high sets as input, set to low sets as output
    TRISC = 0;// x04; //c0 c1 as out, c2 as in
    //TRISCbits.TRISC2 = 1; //Ouput of IR receiver inputs into PIC
    TRISCbits.TRISC7 = 1; //XBee input
    TRISCbits.TRISC6 = 0; //XBee output

    //XBee Configuration
    TXSTA1bits.CSRC = 0; //
    TXSTA1bits.TX9 = 0;  //8-bit transmission
    TXSTA1bits.TXEN = 1; //Transmit
    TXSTA1bits.SYNC = 0; //Asynch
    TXSTA1bits.SENDB = 0; //no send sync break
    TXSTA1bits.BRGH = 1; //

    RCSTA1bits.SPEN = 1; //Serial port
    RCSTA1bits.RX9 = 0;  //receiving 8-bits
    RCSTA1bits.CREN = 1; //Receive

    BAUDCON1bits.RXDTP = 0; //Rx not inverted
    BAUDCON1bits.TXCKP = 0; //Default transmit, high
    BAUDCON1bits.BRG16 = 0; //8-bit baud rate
    //BAUDCON1bits.WUE = 0; //Rx rising edge detected

    SPBRGH1 = 0;
    SPBRG1 = 103;

    tomeHealth = 100;
    updateHealthIndication();

    bookClose = 0;

    if (RB6 == 0)
    {
        cdTime = 5;
    }
    else
    {
        cdTime = 100;
    }

    while(1)
    {
        //irDamage(0);
        //delay10ms(500);
        
        coolDown();
        if (startSpellFlag == 1)
        {
            startSpell();
        }
        updateHealthIndication();
    }

}

```



---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)