#include "p16F628a.inc"    
 __CONFIG _FOSC_INTOSCCLK & _WDTE_OFF & _PWRTE_OFF & _MCLRE_ON & _BOREN_OFF & _LVP_OFF & _CPD_OFF & _CP_OFF    

RES_VECT  CODE    0x0000            ; processor reset vector
    
    BCF PORTA,0		;reset
    MOVLW 0x01
    MOVWF PORTB
    
    BSF PORTA,1		;exec
    CALL time
    BCF PORTA,1
    CALL time
  
    GOTO    START                   ; go to beginning of program
; TODO ADD INTERRUPTS HERE IF USED
MAIN_PROG CODE                      ; let linker place main program

i EQU 0x20
j EQU 0x21
x equ 0x30
y equ 0x31
z equ 0x32
a equ 0x33 

START
    
    
    MOVLW 0x07
    MOVWF CMCON
    BCF STATUS, RP1
    BSF STATUS, RP0 
    CLRF TRISB
    CLRF TRISA
    BCF STATUS, RP0
    
    BCF PORTA,1
    BCF PORTA,0
    
INITLCD
    BCF PORTA,0		;reset
    MOVLW 0x01
    MOVWF PORTB
    
    BSF PORTA,1		;exec
    CALL time
    BCF PORTA,1
    CALL time
    
    MOVLW 0x0C		;first line
    MOVWF PORTB
    
    BSF PORTA,1		;exec
    CALL time
    BCF PORTA,1
    CALL time
         
    MOVLW 0x3C		;cursor mode
    MOVWF PORTB
    
    BSF PORTA,1		;exec
    CALL time
    BCF PORTA,1
    CALL time
    
    
INICIO	  
   
    CALL first     
    GOTO INICIO


first
    BCF PORTA,0		;command mode
    CALL time
    
    
    MOVLW 0x8F		;LCD position
    MOVWF PORTB
    CALL e
    
    BSF PORTA,0		;data mode
    CALL time
    
    MOVLW 'C'
    MOVWF PORTB
    CALL e
    
    MOVLW 'A'
    MOVWF PORTB
    CALL e
   
    MOVLW 'R'
    MOVWF PORTB
    CALL e

    MOVLW 'L'
    MOVWF PORTB
    CALL e
    
    MOVLW 'O'
    MOVWF PORTB
    CALL e
    
    MOVLW 'S'
    MOVWF PORTB
    CALL e
    
    MOVLW ' '
    MOVWF PORTB
    CALL e
   
    MOVLW 'M'
    MOVWF PORTB
    CALL e

    MOVLW 'A'
    MOVWF PORTB
    CALL e
    
    MOVLW 'N'
    MOVWF PORTB
    CALL e
    
    MOVLW 'U'
    MOVWF PORTB
    CALL e
    
    MOVLW 'E'
    MOVWF PORTB
    CALL e
   
    MOVLW 'L'
    MOVWF PORTB
    CALL e

    BCF PORTA,0		;command mode
    CALL time
    
    MOVLW 0xCF		;LCD position
    MOVWF PORTB
    CALL e
    ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
    BSF PORTA,0		;data mode
    CALL time
    
    MOVLW 'S'
    MOVWF PORTB
    CALL e
    
    MOVLW 'A'
    MOVWF PORTB
    CALL e
   
    MOVLW 'N'
    MOVWF PORTB
    CALL e

    MOVLW 'C'
    MOVWF PORTB
    CALL e
    
    MOVLW 'H'
    MOVWF PORTB
    CALL e
    
    MOVLW 'E'
    MOVWF PORTB
    CALL e
    
    MOVLW 'Z'
    MOVWF PORTB
    CALL e
   
    MOVLW ' '
    MOVWF PORTB
    CALL e

    MOVLW 'V'
    MOVWF PORTB
    CALL e
    
    MOVLW 'A'
    MOVWF PORTB
    CALL e
    
    MOVLW 'L'
    MOVWF PORTB
    CALL e

    MOVLW 'E'
    MOVWF PORTB
    CALL exec
    
    MOVLW 'N'
    MOVWF PORTB
    CALL e

    MOVLW 'C'
    MOVWF PORTB
    CALL exec
    
    MOVLW 'I'
    MOVWF PORTB
    CALL e
    
    MOVLW 'A'
    MOVWF PORTB
    CALL e
    
    BCF PORTA,0		;command mode
    CALL time
    
    MOVLW 0x18		;LCD position
    MOVWF PORTB
    CALL e
    ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
    BSF PORTA,0		;data mode
    CALL time
    
   
    
   
    RETURN
    
    

e

    BSF PORTA,1		;exec
    CALL time
    BCF PORTA,1
    CALL time
    RETURN
    
time
    CLRF i
    MOVLW d'10'
    MOVWF j
loop    
    MOVLW d'80'
    MOVWF i
    DECFSZ i
    GOTO $-1
    DECFSZ j
    GOTO loop
    RETURN

    

   
			
    END
