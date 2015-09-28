**Table of Contents**


---





---

# IR Emitters and Receiver #

![https://seal-tome-6.googlecode.com/hg/integration/2013-11-11%2018.07.46.jpg](https://seal-tome-6.googlecode.com/hg/integration/2013-11-11%2018.07.46.jpg) <br />

## <u>Code</u> ##
### 56 kHz Signal ###
```
void ir56k_cycle(){
    LATCbits.LATC0 = 1;
        __delay_us(9);
    LATCbits.LATC0 = 0;
        __delay_us(5);
        Nop();
}
```

### IR Damage Packet ###
```
void irDamage(){
    int i;
    for(i = 0; i < 10; i++)
        ir56k_cycle();
    for(i = 0; i < 140; i++)
        __delay_us(14);
    for(i = 0; i < 20; i++)
        ir56k_cycle();
    for(i = 0; i < 130; i++)
        __delay_us(14);
    for(i = 0; i < 20; i++)
        ir56k_cycle();
    for(i = 0; i < 130; i++)
        __delay_us(14);
    for(i = 0; i < 150; i++)
        ir56k_cycle();
}
```

### IR Heal Packet ###
```
void irHeal(){
    int i;
    for(i = 0; i < 10; i++)
        ir56k_cycle();
    for(i = 0; i < 140; i++)
        __delay_us(14);
    for(i = 0; i < 30; i++)
        ir56k_cycle();
    for(i = 0; i < 120; i++)
        __delay_us(14);
    for(i = 0; i < 30; i++)
        ir56k_cycle();
    for(i = 0; i < 120; i++)
        __delay_us(14);
    for(i = 0; i < 150; i++)
        ir56k_cycle();
}
```

### IR Receive ###
```
//code snipit form "interrupts.c"
else if(INTCON3bits.INT1IF == 1)  //ir receive
      {
          //INTCON3bits.INT1IF = 0;
          heal =0;
          damage =0;
          
          for (int i =0; i < 25; i ++)     //wait around 150 cycles 2.50 ms
          {
              __delay_us(25);
              __delay_us(25);
              __delay_us(25);
              __delay_us(25);
          }
          if (PORTBbits.RB1 == 0)   //pass first packet
          {
              PORTCbits.RC4 = ~PORTCbits.RC4;
              for (int i = 0; i < 2 ; i ++) //loop twice for both middle packet
              {
                  for (int i =0; i < 3; i ++)     //wait around 20 cycles .3 ms
                  {
                      __delay_us(25);
                      __delay_us(25);
                      __delay_us(25);
                      __delay_us(25);
                  }
                  if (PORTBbits.RB1 == 0)   //check if still 0
                  {
                      PORTCbits.RC5 = ~PORTCbits.RC5;
                      
                      for (int i =0; i < 2 ; i ++)      //see if 0 after 10 cycles .20 ms
                      {
                          __delay_us(25);
                          __delay_us(25);
                          __delay_us(25);
                          __delay_us(25);
                      }
                      
                      if (PORTBbits.RB1 == 1)   // damage
                      {
                          PORTDbits.RD7 = ~PORTDbits.RD7;
                          damage ++;
                      }
                      else // heal
                      {
                          PORTDbits.RD6 = ~PORTDbits.RD6;
                          heal ++;
                      }
                      for (int i =0; i < 19 ; i ++) //delay 1.9 ms
                      {
                          __delay_us(25);
                          __delay_us(25);
                          __delay_us(25);
                          __delay_us(25);
                      }
                  }
              }
              for (int i =0; i < 2 ; i ++) //delay .2 ms
              {
                  __delay_us(25);
                  __delay_us(25);
                  __delay_us(25);
                  __delay_us(25);
              }
              if (PORTBbits.RB1 == 0)
              {
                  
                  for (int i =0; i < 23 ; i ++) //delay 150 cycles 2.3 ms
                  {
                      __delay_us(25);
                      __delay_us(25);
                      __delay_us(25);
                      __delay_us(25);
                  }
                  if (PORTBbits.RB1 == 0)
                  {
                      if (heal == 2)
                      {
                          PORTDbits.RD5 = ~PORTDbits.RD5;
                          tomeHealth += 1;
                      }
                      else if(damage == 2)
                      {
                          PORTDbits.RD4 = ~PORTDbits.RD4;
                          tomeHealth -=1;
                      }
                  }
              }
          }
          INTCON3bits.INT1IF = 0;
      }
```

---


# XBee #

![https://seal-tome-6.googlecode.com/hg/integration/2013-11-11%2018.07.20.jpg](https://seal-tome-6.googlecode.com/hg/integration/2013-11-11%2018.07.20.jpg) <br />

## <u>Code</u> ##
```
void xbeetransmit()
{
    TRISC = 0;// x04; //c0 c1 as out, c2 as in
    TRISCbits.TRISC2 = 1; //Ouput of IR receiver inputs into PIC
    TRISCbits.TRISC7 = 1; //XBee input
    TRISCbits.TRISC6 = 0; //XBee output


    TXSTA1bits.TX9 = 0;  //8-bit transmission
    TXSTA1bits.TXEN = 1; //Transmit
    TXSTA1bits.SYNC = 0; //Asynch
    TXSTA1bits.SENDB = 0; //no send sync break
    TXSTA1bits.BRGH = 0; 

    RCSTA1bits.SPEN = 1; //Serial port
    RCSTA1bits.RX9 = 0;
    RCSTA1bits.CREN = 1; //Single reception

    BAUDCON1bits.RXDTP = 0;
    BAUDCON1bits.TXCKP = 0;
    BAUDCON1bits.BRG16 = 0;

    SPBRG1 = 26;

    unsigned char delim = 0x7E;
    unsigned char length_high = 0x00;
    unsigned char length_low = 0x09;
    unsigned char api = 0x01;
    unsigned char frame = 0x01;
    unsigned char dest_16h = 0x00;
    unsigned char dest_16l = 0x00;
    unsigned char disable = 0x00;
    unsigned char b = 'B';
    unsigned char u = 'U';
    unsigned char f1 = 'F';
    unsigned char f2 = 'F';
    volatile unsigned char checksum = 0xff - ((api+frame+dest_16h+dest_16l+disable+b+u+f1+f2)&0xFF);

    OSCCON = 0b01110010; // set up internal 16 MHz clock

   while(1)
{
       TXSTA1bits.TXEN = 1;
       TXREG1 = delim;

       //Length
       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = length_high;

       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = length_low;

       //Frame Type
       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = api;

       //Frame ID
       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = frame;

       //64-bit Destination Address
       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = dest_16h;

       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = dest_16l;


       //Broadcast Radius
       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = disable;


       //Payload
       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = b;


       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = u;


       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = f1;


       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = f2;


       while(TXSTA1bits.TRMT == 0);
       TXSTA1bits.TXEN = 1;
       TXREG1 = checksum;


       while(TXSTA1bits.TRMT == 0);
       for(int i = 0;i < 10; i++) {
           __delay_ms(25);
           __delay_ms(25);
       }
}

```


---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)