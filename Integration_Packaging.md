**Table of Contents**


---





---

# Introduction #


![http://wiki.seal-tome-6.googlecode.com/hg-history/26356b01ea9810df1d54a739cef96874ddf8bcf1/2013-11-11%2018.08.02.jpg](http://wiki.seal-tome-6.googlecode.com/hg-history/26356b01ea9810df1d54a739cef96874ddf8bcf1/2013-11-11%2018.08.02.jpg)




# Program #

```
      // snipit from "interrupts.c"
      /* Determine which flag generated the interrupt */
      if((INTCONbits.INT0IF == 1) && (PORTBbits.RB0 == 0)) 
      {
 
          for (int i =0; i < 5 ; i ++)                            //.5 second delay
          {
              __delay_ms(25);
              __delay_ms(25);
              __delay_ms(25);
              __delay_ms(25);
          }
          INTCONbits.INT0IF =0; /* Clear Interrupt Flag 1 */
          spellReg = ((~PORTB & 0x3c)>> 1) + (~PORTB & 0x01);    //Checks which pins are high on PORTB to determine the spell. Sets result to spellReg.
          startSpellFlag = 1;                                    //Flag used to initialize spell
      }
      else if((INTCONbits.INT0IF == 1) && (PORTBbits.RB0 == 1))  //Checks for book close interrupt. 
      {
          bookClose = 1;
          INTCONbits.INT0IF =0;
          primeCount = 9;
      }

```


---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)