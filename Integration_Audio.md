**Table of Contents**


---





---

# Introduction #

Add your content here.


# Details #

## AUDIO.h code: ##
```
/*
 * File:   AUDIO.h
 * Author: Nik
 *
 * Created on November 1, 2013, 6:03 PM
 */

#ifndef AUDIO_H
#define	AUDIO_H

// predefined macros
#define INPUT           1
#define OUTPUT          0
#define _XTAL_FREQ      16000000         //define frequency for the delay functions

// audio commands and files
#define STOP            0xFFFF

// prototypes
void AINIT();
void ACLK(unsigned char state);
void ADATA(unsigned char state);
void ARST(unsigned char state);
void ATRIGGER(unsigned int file);

// definitions
void AINIT() {
    TRISEbits.TRISE0 = OUTPUT;              // CLK
    TRISEbits.TRISE1 = OUTPUT;              // DATA
    ACLK(1);                                // Set ACLK to HIGH
    ADATA(1);                               // set ADATA to HIGH
}

void ACLK(unsigned char state) {
    if(state == 1)
        LATEbits.LATE0 = 1;

    if(state == 0)
        LATEbits.LATE0 = 0;
}

void ADATA(unsigned char state) {
    if(state == 1)
        LATEbits.LATE1 = 1;

    if(state == 0)
        LATEbits.LATE1 = 0;
}

void ATRIGGER(unsigned int file) {
    int i = 15;
    int A[16];
    for(; i >= 0; i--) {
       A[i] = file & 1;
       file >>= 1;
    }

    ACLK(0);
    ADATA(A[0]);

    // delay 20 ms
    __delay_ms(20);
    
    for(i = 1; i < 16 ; i++) {
        ACLK(1);
        __delay_us(200);    // delay 200 us

        ACLK(0);
        ADATA(A[i]);
        __delay_us(200);    // delay 200 us
    }
    ACLK(1);
    ADATA(1);
}

#endif	/* AUDIO_H */


```


---



---

[Home](MainPage.md)

[Research Home](Research.md)

[Prototype Home](prototype.md)

[Integration Phase I Home](Integration.md)