# Music-Machine
arduino mega 2560 (atmega 2560) Music Machine

/*
  MUSIC MACHINE
  Creator: Nathan Semianiw
*/

//MATRIX KEYPAD CONSTANTS AND VARIABLES
#define KEYPAD_COL_PORT PORTC// Port Register for Pins Keypad Columns are connected too
#define KEYPAD_COL_DIRECTION DDRC// Data Direction Register for Pins Keypad columns are Connected too 
#define KEYPAD_COL_PIN PINC// Pin Register for Pins Keypad Columns are Connected too

#define COL1 PC0// Pin that Column 1 of Keypad is Connected too (Pin 37 of Arduino mega 2560)
#define COL2 PC1// Pin that Column 2 of Keypad is Connected too (Pin 36 of Arduino mega 2560) 
#define COL3 PC2// Pin that Column 3 of Keypad is Connected too (Pin 35 of Arduino mega 2560) 
#define COL4 PC3// Pin that Column 4 of Keypad is Connected too (Pin 34 of Arduino mega 2560) 

#define KEYPAD_ROW_PORT PORTD// Port Register for Pins Keypad Rows are Connected too
#define KEYPAD_ROW_DIRECTION DDRD// Data Direction Register for Pins Keypad Rows are Connected too
#define KEYPAD_ROW_PIN PIND// Pin register for Pins keypad Rows are Connected too 

#define ROW1 PD0// Pin that Row 1 of Keypad is Connected too (Pin 21 of Arduino mega 2560)(INT0)
#define ROW2 PD1// Pin that Row 2 of Keypad is Connected too (Pin 22 of Arduino mega 2560)(INT1) 
#define ROW3 PD2// Pin that Row 3 of Keypad is Connected too (Pin 23 of Arduino mega 2560)(INT2) 
#define ROW4 PD3// Pin that Row 4 of Keypad is Connected too (Pin 24 of Arduino mega 2560)(INT3) 
//NOTE: THE ROWS OF THE 4X4 MATRIX BE CONNECTED TO EXTERNAL INTERUPPT PINS!

//LCD SCREEN CONSTANTS AND VARIABLES
#define LCD_DATA_PORT PORTA// Port Register for LCD DATA Pins (D0-D7) are connected too
#define LCD_DATA_DIRECTION DDRA// Data Direction Register for Pins LCD DATA Pins (D0-D7) are connected too
#define LCD_DATA_PIN PINA// Pin Register for Pins LCD DATA Pins (D0-D7) are Connected too

#define D0 PA0// Pin that D0 of LCD Display is connected too (Pin of Arduino Mega 2560)
#define D1 PA1// Pin that D1 of LCD Display is connected too (Pin of Arduino Mega 2560)
#define D2 PA2// Pin that D2 of LCD Display is connected too (Pin of Arduino Mega 2560)
#define D3 PA3// Pin that D3 of LCD Display is connected too (Pin of Arduino Mega 2560)
#define D4 PA4// Pin that D4 of LCD Display is connected too (Pin of Arduino Mega 2560)
#define D5 PA5// Pin that D5 of LCD Display is connected too (Pin of Arduino Mega 2560)
#define D6 PA6// Pin that D6 of LCD Display is connected too (Pin of Arduino Mega 2560)
#define D7 PA7// Pin that D7 of LCD Display is connected too (Pin of Arduino Mega 2560)

#define LCD_CONTROL_PORT PORTG// Port Register for LCD CONTROL Pins (RS,R/W,E) are connected too
#define LCD_CONTROL_DIRECTION DDRG// Data Direction Register for Pins LCD DATA Pins (RS,R/W,E) are connected too
#define LCD_CONTROL_PIN PING// Pin Register for Pins LCD CONTROL Pins (RS,R/W,E) are Connected too

#define RS PG0// Pin that RS of LCD Display is connected too (Pin of Arduino Mega 2560)
#define RW PG1// Pin that R/W of LCD Display is connected too (Pin of Arduino Mega 2560)
#define ENABLE PG2// Pin that E of LCD Display is connected too (Pin of Arduino Mega 2560)

// Initalization Data of LCD Display
#define FUNCTION_SET B00111000; //8 Bit interface, 2 lines enabled, 5x8 Text
#define ENTRY_MODE_SET B00000110; //Set entry mode, cursor/blink moves to right, No display shift
#define DISPLAY_ONOFF B00001100; // Display on, cursor off , blink 

#define NUMBER_OF_CUSTOM_CHARACTERS 2// Number of Custom Characters being Loaded into LCD Display

//BUZZER CONSTANTS AND VARIABLES
#define BUZZER_PORT PORTH// Port Register that the Buzzer is Connected too
#define BUZZER_DIRECTION DDRH// Data Direction Register that the Buzzer is Connected too
#define BUZZER_PIN PINH// Pin Register that theBuzzer is Connected too
#define BUZZER_SIGNAL PH3// Pin that the Buzzer is Connected too (OC4A)(PWM)

#define CLOCK_FREQUENCY 16000000.00 // Timer/Counter Clock Frequency
#define TIMER4_PRESCALER 256 // Timer/Counter 4 Prescaler

//10 SEGEMENT DISPLAY CONSTANTS AND VARIABLES
#define LED_0to7_PORT PORTL// Port Register for LED's 0 to 7(Except LED_3) of 10-Segement Display Pins are Connected too
#define LED_0to7_DIRECTION DDRL// Data Direction Register for LED's 0 to 7(Except LED_3) of 10-Segement Display Pins are Connected too
#define LED_0to7_PIN PINL// Pin Register for LED's 0 to 7(Except LED_3) of 10-Segement Display Pins are Connected too

#define LED_0 PL0// Pin that LED_0 of the 10-Segment Display is Connected too (Pin 49 of Arduino Mega 2560)
#define LED_1 PL1// Pin that LED_1 of the 10-Segment Display is Connected too (Pin 48 of Arduino Mega 2560)
#define LED_2 PL2// Pin that LED_2 of the 10-Segment Display is Connected too (Pin 47 of Arduino Mega 2560)
#define LED_4 PL4// Pin that LED_4 of the 10-Segment Display is Connected too (Pin 45 of Arduino Mega 2560)
#define LED_5 PL5// Pin that LED_5 of the 10-Segment Display is Connected too (Pin 44 of Arduino Mega 2560)
#define LED_6 PL6// Pin that LED_6 of the 10-Segment Display is Connected too (Pin 43 of Arduino Mega 2560)
#define LED_7 PL7// Pin that LED_7 of the 10-Segment Display is Connected too (Pin 42 of Arduino Mega 2560)

#define LED_8to9_PORT PORTB// Port Register for LED's 8 to 9(Including LED_3) of 10-Segement Display Pins are Connected too
#define LED_8to9_DIRECTION DDRB// Data Direction Register for LED's 8 to 9(Including LED_3) of 10-Segement Display Pins are Connected too
#define LED_8to9_PIN PINB// Pin Register for LED's 8 to 9(Including LED_3) of 10-Segement Display Pins are Connected too

#define LED_3 PB1// Pin that LED_3 of the 10-Segment Display is Connected too (Pin 52 of Arduino Mega 2560)
#define LED_8 PB2// Pin that LED_8 of the 10-Segment Display is Connected too (Pin 51 of Arduino Mega 2560)
#define LED_9 PB3// Pin that LED_9 of the 10-Segment Display is Connected too (Pin 53 of Arduino Mega 2560)

//SERVO MOTORS
#define SERVO_PORT PORTB// Port Register that Servo 1 and Servo 2 are connected too
#define SERVO_DIRECTION DDRB// Data Direction Register that Servo 1 and Servo 2 are connected too
#define SERVO_PIN PINB// Pin Register that Servo 1 and Servo 2 are connected too
#define SERVO1 PB5// Pin that Servo 1 is connected too (Pin 11 of Arduino Mega 2560)(OC1A)(PWM)
#define SERVO2 PB6// Pin that Servo 2 is connected too (Pin 12 of Arduino Mega 2560)(OC1B)(PWM)

#define DRUM_DELAY 90
#define SERVO1_HOME 110 //OCR1A value for stick 1 home position
#define SERVO2_HOME 112 //OCR1B value for stick 2 home position
#define SERVO1_HIT 120 //OCR1A Value for Stick 1 to Hit Drum
#define SERVO2_HIT 123 //OCR1B Value for Stick 2 to Hit Drum

int custom_character[NUMBER_OF_CUSTOM_CHARACTERS][8] = {{0b00000000, 0b00000100, 0b00000100, 0b00000100, 0b00011111, 0b00001110, 0b00000100, 0b00000000},
  {0b00000000, 0b00000100, 0b00001110, 0b00011111, 0b00000100, 0b00000100, 0b00000100, 0b00000000}
};

char tune[][16] = {{"JAMES BOND"},// Name of Tune 1
  {"FINAL COUNTDOWN"},// Name of Tune 2
  {"STAR WARS"},// Name of Tune 3
  {"CUSTOM TUNE 1"}// Name of Tune 4
};

int C[] = {0, 0, 0, 0, 262, 523, 1047, 2093};// Keyboard Frequency Values for Note C {C0,C1,C2,C3,C4,C5,C6,C7}
int CS[] = {0, 0, 0, 0, 277, 554, 1109, 2217};// Keyboard Frequency Values for Note C {CS0,CS1,CS2,CS3,CS4,CS5,CS6,CS7}
int D[] = {0, 0, 0, 0, 294, 587, 1175, 2349};// Keyboard Frequency Values for Note C {D0,D1,D2,D3,D4,D5,D6,D7}
int DS[] = {0, 0, 0, 0, 311, 622, 1245, 2489};// Keyboard Frequency Values for Note C {DS0,DS1,DS2,DS3,DS4,DS5,DS6,DS7}
int E[] = {0, 0, 0, 0, 330, 659, 1319, 2637};// Keyboard Frequency Values for Note C {E0,E1,E2,E3,E4,E5,E6,E7}
int F[] = {0, 0, 0, 0, 349, 698, 1397, 2794};// Keyboard Frequency Values for Note C {F0,F1,F2,F3,F4,F5,F6,F7}
int FS[] = {0, 0, 0, 0, 370, 740, 1480, 2960};// Keyboard Frequency Values for Note C {FS0,FS1,FS2,FS3,FS4,FS5,FS6,FS7}
int G[] = {0, 0, 0, 0, 392, 784, 1568, 3136};// Keyboard Frequency Values for Note C {G0,G1,G2,G3,G4,G5,G6,G7}
int GS[] = {0, 0, 0, 0, 415, 831, 1661, 3322};// Keyboard Frequency Values for Note C {GS0,GS1,GS2,GS3,GS4,GS5,GS6,GS7}
int A[] = {0, 0, 0, 0, 440, 880, 1760, 3520};// Keyboard Frequency Values for Note C {A0,A1,A2,A3,A4,A5,A6,A7}
int AS[] = {0, 0, 0, 0, 466, 932, 1865, 3729};// Keyboard Frequency Values for Note C {AS0,AS1,AS2,AS3,AS4,AS5,AS6,AS7}
int B[] = {0, 0, 0, 0, 494, 988, 1976, 3951};// Keyboard Frequency Values for Note C {B0,B1,B2,B3,B4,B5,B6,B7}

//TUNE 1 NOTES- First Value in Each Array is Number of Notes in the Tune
int tune_buzzer[3][100] = {
  //TUNE 1 BUZZER NOTES - JAMES BOND
  { 38, E[6], F[6], F[6], F[6], F[6], E[6], E[6], E[6], E[6],
    G[6], G[6], G[6], G[6], E[6], E[6], E[6], DS[7], D[7], B[6],
    A[6], B[6], E[6], G[6], DS[7], D[7], G[6], B[6], B[6], FS[7],
    F[7], B[6], D[7], AS[7], A[7], F[7], A[7], DS[7], D[7]
  },
  //TUNE 2 BUZZER NOTES - FINAL COUNTDOWN
  { 53, G[5], B[5], A[5], B[5], E[5], 0, 0, C[6], B[5],
    C[6], B[5], A[5], 0, 0, C[6], B[5], C[6], E[5], FS[5],
    0, A[5], G[5], A[5], G[5], FS[5], A[5], G[5], 0, B[5],
    A[5], B[5], E[5], 0, 0, C[6], B[5], C[6], B[5], A[5],
    0, 0, B[5], A[5], B[5], E[5], FS[5], 0, A[5], G[5],
    A[5], G[5], FS[5], A[5]
  },
  //TUNE 3 BUZZER NOTES - STAR WARS
  { 38, A[6], A[6], A[6], F[6], C[7], A[6], F[6], C[7], A[6],
    0, E[7], E[7], E[7], F[7], C[7], GS[6], F[6], CS[6], A[6],
    0, A[7], A[6], A[6], A[7], GS[7], G[6], FS[7], F[7], FS[7],
    0, AS[6], DS[7], D[7], CS[7], C[7], C[6], C[7], 0
  }
};

int tune1_led[][53][10] = {
  //TUNE 1 LED SEQUENCE - JAMES BOND
  { {1, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 1, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 1, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 1, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 1, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
    {1, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 1, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 1, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 1, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 1, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 1, 0},
    {0, 0, 0, 0, 0, 0, 0, 1, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 0, 0, 0, 0},
    {0, 0, 0, 0, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 1, 0, 0, 0, 0, 0, 0},
    {0, 0, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 1, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 1, 1, 1, 1, 1, 1, 1}
  },
  //TUNE 2 LED SEQUENCE - FINAL COUNTDOWN
  { {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 1, 1, 1, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 1, 1, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 0, 0, 0},
    {0, 0, 0, 0, 1, 1, 0, 0, 0, 0},
    {0, 0, 0, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 1, 1, 0, 0, 0, 0, 0, 0},
    {0, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 1, 1, 1, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 1, 1},
    {0, 0, 0, 0, 1, 1, 1, 0, 0, 0},
    {0, 0, 1, 1, 1, 0, 0, 0, 0, 0},
    {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 1, 1, 1, 1, 1, 1, 1}
  },
  // TUNE 3 LED SEQUENCE - STAR WARS
  { {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0,0, 0, 1, 1, 1, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0,0},
    {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 1, 1, 1, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 1, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 1, 1},
    {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 1, 1},
    {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 1, 1},
    {0, 0, 0, 0, 0, 0, 1, 1, 0,0},
    {0, 0, 0, 0, 1, 1, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 1, 1, 0, 0, 0, 0, 0, 0},
    {1, 1, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 1, 1, 1, 1},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 1, 1, 1, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {1, 1, 1, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
  }
};

int dur[][100] = {
  //TUNE 1 NOTE DELAY - JAMES BOND
  { 180, 90, 90, 180, 360, 180, 180, 180, 180, 90,
    90, 180, 360, 180, 180, 180, 180, 720, 180, 180,
    1440, 180, 360, 180, 360, 180, 180, 180, 180, 360,
    180, 360, 180, 360, 180, 360, 180, 480
  },
  //TUNE 2 NOTE DELAY - FINAL COUNTDOWN
  { 472, 118, 118, 472, 472, 472, 236, 118, 118, 236,
    236, 472, 472, 236, 118, 118, 472, 472, 472, 472,
    118, 118, 236, 236, 236, 236, 472, 472, 118, 118,
    472, 472, 236, 472, 118, 118, 236, 236, 472, 236,
    472, 118, 118, 472, 472, 472, 472, 118, 118, 236,
    236, 236, 236
  },
  //TUNE 3 NOTE DELAY - STAR WARS
  { 500, 500, 500, 350, 150, 500, 350, 150, 650, 500,
    500, 500, 500, 350, 150, 500, 350, 150, 650, 500,
    500, 300, 150, 500, 325, 175, 125, 125, 250, 325,
    250, 500, 325, 175, 125, 125, 250, 500
  }
};


//ISR Variables
volatile int button = 0;// Variable to Store Value of Button Pressed on 4x4 Matrix Keypad
volatile int seq = 1;// Variable For Cycling through Keypad Columns 
volatile int buzzer_manual = 0;// Variable to Activate(1) and Deactivate(0) Buzzer in Manual Mode
volatile int drum_manual = 0;// Variable to Activate (1) and Deactivate(0) Drum in Manual Mode
volatile int LED_manual = 0;// Variable to Activate(1) and Deactivate(0) 10-Segment Display in Manual Mode
volatile int octave = 0;// Variable to Store Octave Value Selected



// Menu Selection Variables
int main_menu = 0;// Variable for Program to Cycle Through the Main Menu
volatile int menu_level = 0;// Variable for Program to Cycle through Menu Levels
int tune_menu = 0;// Variable for Program to Cycle through Tune Menu
int module_menu = 0;// Variable for Program to Cycle through Module Menu
int freestyle_menu = 0;// Variable for Program to Cycle through Freestyle Menu
int mode_menu = 0;// Variable for Program to Cycle through Mode Menu


int stick = 0;// Variable for Program to Switch Between Activation of SERVO motors ((1)-SERVO 1, (2)-SERVO 2))
int print_flag = 1;// Variable for Program to Print(1) or Not Print(0) Strings to LCD Display

int module[] = {1, 1, 1}; // {drum,buzzer,led_bar}

char module_names[][16] = {
  {"DRUM"},// Module 1 Name
  {"BUZZER"},// Module 2 Name
  {"10-SEG DISPLAY"}// Module 3 Name
};

volatile int temp_custom_buzzer[200];// Variable for Temporaily Storing the Custom Tune Notes, Before it is Saved to EEPROM
volatile int temp_custom_dur[200];// Variable for Temporaily Storing the Custom Tune Duration, Before it is Saved to EEPROM
volatile int temp_note_count = 0;// Variable for Temporaily Storing the Number of Notes in the Custom Tune, Before it is Saved to EEPROM

int note_count = 0;// Variable EEPROM Stores the Number of Notes in Custom Tune
int custom_buzzer[200];// Variable EEPROM Stores Buzzer Notes (Frequency) in Custom Tune
int custom_dur[200];// Variable EEPROM Stores Duration of Each Note of Custom Tune

volatile int record = 0;// Variable For Program to Turn Recording ON(1) and OFF(0)
volatile signed int count = 0;// Variable for Counting (every 1ms) the Duration of the Break and Note
volatile int note = 0;// Variable for Storing Note Pressed when Recording a Tune
int EEPROM_flag = 1;// Variable for the program to know if EEPROM has Already Be Read or the EEPROM Values have Changed

int hiByte, loByte;// Variables for Storing Upper and Lower Bytes of 16 Bit Value 

char number[10];// Variable for Storing the conversion From an Integer to a Character

void setup() {
  //LCD DISPLAY
  LCD_DATA_DIRECTION |= (1 << D0) | (1 << D1) | (1 << D2) | (1 << D3) | (1 << D4) | (1 << D5) | (1 << D6) | (1 << D7); // Set Pins Connected to D0 to D7 to Output Pins
  LCD_CONTROL_DIRECTION |= (1 << RS) | (1 << RW) | (1 << ENABLE); // Set Pins Connected to RS, R/W and E to Output Pins

  //MATRIX KEYPAD INTERUPTS
  KEYPAD_COL_DIRECTION |= (1 << COL1) | (1 << COL2) | (1 << COL3) | (1 << COL4);// Set Pins Connected to Column 1 to Column 4 to Output Pins
  KEYPAD_ROW_PORT |= (1 << ROW1) | (1 << ROW2) | (1 << ROW3) | (1 << ROW4);// Enable Pull-up Resistors on Keypad Row Pins

  EICRA = 0b10101010;// Falling Edge of INT0,INT1,INT2 and INT3 Generates an Interrupt
  EIMSK = 0b00001111;// Enable INT0,INT1,INT2 and INT3 Interrupts

  // MATRIX KEYPAD PIN CYCLING INTERUPT - Interupts every 5ms
  TCCR3A = (1 << COM3A0); //Normal mode toggle OC1A on compare match
  TCCR3B = (1 << CS32) | (1 << CS10); //Set Prescaler clkio/1024
  TCCR3C = 0b00000000; //TCCR3C =0
  TIMSK3 = (1 << OCIE3A); //Enable Timer/Counter3, Output Compare A Match Interrupt
  OCR3A = 0xFFFF; //High byte of FFFF
  TCNT3 = 0xFFB2; // 65458

  // RECORD MODE TIMER/COUNTER INTERUPT - Interupts every 1ms
  TCCR5A = (1 << COM3A0); //Normal mode toggle OC1A on compare match
  TCCR5B = 0b00000000; //Set Prescaler to No Clock Source (Timer/Counter Stopped)
  TCCR5C = 0b00000000; //TCCR5C =0
  TIMSK5 = (1 << OCIE3A); //Enable Timer/Counter5, Output Compare A Match Interrupt
  OCR5A = 0xFFFF; //High byte of FFFF
  TCNT5 = 0xFF14; // 65300

  // SERVO MOTORS
  SERVO_DIRECTION |= (1 << SERVO1) | (1 << SERVO2); // Set Pins Connected to SERVO 1 and SERVO 2 to Output Pins
  TCCR1A = (1 << COM1A1) | (1 << COM1B1) | (1 << WGM11); //Fast PWM Mode 14, Output Compare Mode 2 for channel A and B
  TCCR1B = (1 << WGM13) | (1 << WGM12) | (1 << CS12); //Fast PWM mode 14, prescaler clkio/256
  OCR1A = SERVO1_HOME; //Drive SERVO1 to Home Position
  OCR1B = SERVO2_HOME; //Drive SERVO2 to Home Position
  ICR1 = 1250; //Load 1250 for TOP Value
  TCNT1 = 0; //Load 0 for BOTTOM Value

  // 10-SEGEMENT DISPLAY
  LED_0to7_DIRECTION |= (1 << LED_0) | (1 << LED_1) | (1 << LED_2) | (1 << LED_4) | (1 << LED_5) | (1 << LED_6) | (1 << LED_7);// Set Pins Connected to LEDs as Output Pins
  LED_8to9_DIRECTION |= (1<<LED_3) | (1 << LED_8) | (1 << LED_9);// Set Pins Connected to LEDs as Output Pins

  // BUZZER
  BUZZER_DIRECTION = (1 << BUZZER_SIGNAL);// Set Pin Connected to Buzzer an Output Pin
  TCCR4A = (1 << COM4A1) | (1 << WGM41);// Fast PWM Mode 14, Output Compare Mode 2 for Channel A
  TCCR4B = (1 << WGM43) | (1 << WGM42) | (1 << CS42);// Fast PWM Mode 14, Prescaler clkio/256
  OCR4A = 0;// Load 0 for COMP Value (No Sound)
  ICR4 = 0;// Load 0 For TOP Value (No Sound)
  TCNT4 = 0;// Load 0 for BOTTOM Value

  lcd_setup();// Call lcd Setup Routine

  custom_char(); // Load Custom Charaters into LCD CGRAM

  lcd_clear();//Clear Lcd Display
  lcd_setCursor(5, 0);// Set Cursor to First Line and Increment 5 Positions to the Right
  lcd_print("MUSIC");//Print the String ("MUSIC") to the LCD Display
  lcd_setCursor(4, 1);// Set the Cursor to the Second line and Increment 4 Positions to the Right
  lcd_print("MACHINE");// Print the String ("MACHINE") to the LCD Display
  _delay_ms(2000); // 2000ms(1s) Delay
  lcd_clear();// Clear the Lcd Display
  lcd_setCursor(7, 0);// Set the Cursor to the First Line and Increment 7 Positions to the Right
  lcd_print("BY");// Print the String ("BY") to the LCD Display
  lcd_setCursor(0, 1);// Set the Cursor to the Second Line and Increment 0 Positions to the Right
  lcd_print("NATHAN SEMIANIW");// Print the String ("NATHAN SEMIANIW") to he LCD Display
  _delay_ms(1000);// 1000ms(1s) Delay
}

void loop() {
  //MAIN MENU - CURSOR ON SELECT A TUNE
  print_flag = 1;// print_flag set to 1
  while (main_menu == 0 & menu_level == 0)
  {
    if (print_flag == 1)// Only Prints to LCD if Print_flag==1
    {
      lcd_clear();// Clear LCD Display
      lcd_setCursor(0, 0); // Set Cursor on the First Line and Incremented 0 Times to the Right
      lcd_print("PLAY A TUNE <");// Print "PLAY A TUNE <" to LCD Display
      lcd_setCursor(0, 1); // Set Cursor on the Second Line and Incremented 0 Times to the Right
      lcd_print("CREATE A TUNE");// Print "CREATE A TUNE" to LCD Display
      print_flag = 0;// print_flag set to 0
    }
    switch (button)// Performs a Function if Button is pressed
    {
      case 2:// Up (Button 2 on Keypad
        main_menu = 1;// Moves Cursor(<) Down to Next line
        button = 0;// Set button to 0
        break;// Breaks Out of Switch Case

      case 10:// Down (Button 8 on Keypad)
        main_menu = 1;// Set main_menu to 1 (Moves Cursor(<) Down to CREATE A TUNE)
        button = 0;// Set button to 0
        break;// Breaks Out of Switch Case

      case 6:// Enter (Button 5 on Keypad)
        menu_level++;// Increments Menu Level by 1
        button = 0;// Set button to 0
        print_flag = 1; // Set print_flag to 1
        break;// Breaks Out of Switch Case
    }
    // TUNE MENU
    while (menu_level >= 1)
    {
      if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
      {
        lcd_clear();// Clear LCD Display
        lcd_setCursor(5, 0); // Set Cursor to First Line and Increment 5 Positions to the Right
        lcd_print("TUNE"); // Print string ("TUNE") to LCD Display
        lcd_setCursor(10, 0);// Set Cursor to First line and Increment 10 to the Right
        itoa(tune_menu + 1, number, 10); // Convert From an Integer to a ASCII Charcter
        lcd_print(number);// Print Character to LCD Screen
        lcd_setCursor((16 - (strlen(tune[tune_menu]))) / 2, 1);
        lcd_print(tune[tune_menu]); // Print Tune Name to LCD Display
        lcd_setCursor(15, 0);// Set Cursor to First Line and Increment 15 Positions to the Right
        lcd_print_custom(2);// Print Custom (UP ARROW) Character to LCD Display
        lcd_setCursor(15, 1);// Set Cursor to Second Line and Increment 15 Positions to the Right
        lcd_print_custom(1);// Print Custom (DOWN ARROW) Character to LCD Display
        print_flag = 0;// Set print_flag to 0
      }
      switch (button)
      {
        case 2:// UP (Button 2 of Keypad)
          if (tune_menu == 0)// Enters loop if User Presses Button 2 of Keypad When LCD Displaying TUNE 1
          {
            tune_menu = 3;// Set tune_menu to 3
          }
          else
          {
            tune_menu--;// Decrement tune_menu by 1
          }
          button = 0;// set button to 0
          print_flag = 1;// Set print_flag to 1
          break;

        case 6:// Enter (Button 5 of Keypad)
          menu_level++;// Increment menu_level by 1
          print_flag = 1;// Set print_flag to 1
          button = 0;// Set button to 0
          break;

        case 10:// Down (Button 8 of Keypad)
          if (tune_menu == 3)
          {
            tune_menu = 0;// Set button to 0
          }
          else {
            tune_menu++;// Increment tune_menu by 1
          }
          button = 0;// Set button to 0
          print_flag = 1;// Set print_flag to 1
          break;

        case 16:// Return/Exit (Button D of Keypad)
          menu_level--;// Decrement menu_level by 1
          tune_menu = 0;// Set tune_menu to 0
          print_flag = 1;// Set print_flag to 1
          button = 0;// Set button to 0
          break;
      }
      // MODULE MENU - USER CAN TURN MODULES ON AND OFF
      while (menu_level >= 2) 
      {
        if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
        {
          lcd_clear();// Clear LCD Display 
          lcd_setCursor(15, 0);// Set Cursor to First Line and Increment 15 Positions to the Right
          lcd_print_custom(2);// Print Custom (UP ARROW) Character to LCD Display
          lcd_setCursor(15, 1);// Set Cursor to the Second Line and Increment 15 Positions to the Right
          lcd_print_custom(1);// Print Custom  (DOWM ARROW) to LCD Display
          if (module_menu == 3)
          {
            lcd_setCursor(0, 0);// Set Cursor to Home Position
            lcd_print("PRESS (5)");// Print String ("PRESS (5)") to LCD Display
            lcd_setCursor(0, 1);// Set Cursor to Second Line and Increment 0 Positions to the Right
            lcd_print("TO PLAY TUNE");// Print String ("TO PLAY A TUNE") to LCD Display
          }
          else
          {
            lcd_setCursor((14 - (strlen(module_names[module_menu]))) / 2, 0);
            lcd_print(module_names[module_menu]); // Print String (Module Name) to LCD Display
            if (module[module_menu] == 0)// Enters if Module is Deactivated
            {
              lcd_setCursor(1, 1);// Set Cursor to Second Line and Increment 1 Position to the Right
              lcd_print("-DEACTIVATED-");// Print String ("-DEACTIVATED-") to LCD Display
            }
            else
            {
              lcd_setCursor(2, 1);// Enters if Module is Activated
              lcd_print("-ACTIVATED-");// Print String ("-ACTIVATED-") to LCD Display
            }
          }
          print_flag = 0;// Set print_flag to 0
        }
        switch (button)
        {
          case 2:// UP (Button 2 of Keypad)
            if (module_menu == 0)
            {
              module_menu = 3;// Set module_menu to 3
            }
            else
            {
              module_menu--;// Decrement module_menu by 1
            }
            print_flag = 1;// Set print_flag to 1
            button = 0;// Set button to 0
            break;

          case 6:// Enter (Button 5 of Keypad)
            if (module_menu == 3)
            {
              menu_level++;// Increment module_menu by 1
            }
            else
            {
              module[module_menu] ^= 1;// Set Module to the Inverse of the Current State
            }
            print_flag = 1;// Set print_flag to 1
            button = 0;// Set button to 0
            break;
          case 10:// Down (Button 8 of Keypad)
            if (module_menu == 3)
            {
              module_menu = 0;// Set module_menu to 0
            }
            else
            {
              module_menu++;// Increment module_menu by 1
            }
            print_flag = 1;// Set print_flagto 1
            button = 0;// Set button to 0
            break;

          case 16:// Return/Exit (Button D of Keypad)
            menu_level--;// Decrement menu_level by 1
            print_flag = 1;// Set print_flag to 1
            module[0] = 1; // Set Drum to 1 (ACTIVATED)
            module[1] = 1;// Set Buzzer to 1 (ACTIVATED)
            module[2] = 1;// Set 10-Segment Display to 1 (ACTIVATED)
            module_menu = 0;// Set module_menu to 0
            button = 0;// Set button to 0
            break;
        }
        //PLAYS SELECTED TUNE
        while (menu_level >= 3)
        {
          if (tune_menu == 3)
          {
            note_count = EEPROM_read(0);// Store the Value in the First EEPROM Address to note_count
            if (EEPROM_flag == 1)// Enters Loop if EEPROM Hasn't Been Read or EEPROM DATA has been Modified
            {
              lcd_clear();//Clear LCD Display
              lcd_print("LOADING...");// Print String ("LOADING...") to LCD Display
              for (int i = 0; i < note_count; i++)
              {
                cli();// Disable Global Interrupts
                hiByte = EEPROM_read((i * 2) + 1);// Read the Hi Byte of the 16 Bit Value (Tune Note)
                loByte = EEPROM_read((i * 2) + 2);// Read the Low Byte of the 16 Bit Value (Tune Note)
                custom_buzzer[i] = hiByte;// Store 8 Bit hiByte Value in custom_buzzer
                custom_buzzer[i] = (custom_buzzer[i]) << 8 | loByte;// Bit Shift custom_buzzer Value to the Left 8 Positions and Mask with loByte (Turns two 8 Bit Values to one 16 Bit)
                hiByte = EEPROM_read((i * 2) + 1 + (note_count * 2));// Read the Hi Byte of the 16 Bit Value (Note Duration)
                loByte = EEPROM_read((i * 2) + 2 + (note_count * 2));// Read the Low Byte of the 16 Bit Value (Note Duration)
                custom_dur[i] = hiByte;// Store 8 Bit hiByte Value in custom_dur
                custom_dur[i] = (custom_dur[i]) << 8 | loByte;// Bit Shift custom_dur Value to the Left 8 Positions and Mask with loByte (Turns two 8 Bit Values to one 16 Bit)
                sei();// Enable Global Interrupts
              }
              _delay_ms(500);// Delay to Allow user to see String On LCD Screen
              EEPROM_flag = 0;// Set EEPROM_flag to 0
            }
            lcd_clear();// Clear LCD Display
            lcd_print("NOW PLAYING...");// Print String ("NOW PLAYING...") to LCD Display
            stick = 0;// Set stick to 0
            for (int i = 0; i < note_count ; i++) 
            {
              if (stick == 0 & custom_buzzer[i] > 0) 
              {
                drum_stick(1, 0);// Enable SERVO 1
                stick = 1;// Set stick to 1
              }
              else if (stick == 1 & custom_buzzer[i] > 0) 
              {
                drum_stick(0, 1);// Enable SERVO 2
                stick = 0;// Set stick to 0
              }
              else 
              {
                drum_stick(0, 0);// Disable SERVO 1 and SERVO 2
              }
              buzzer(custom_buzzer[i], custom_dur[i]);// Play Tune (buzzer(TUNE NOTE, NOTE DURATION)

              if (button == 16) // Return/Exit (Button D of Keypad)
              {
                button = 0;// Set Button to 0
                break;
              }
            }
            menu_level = 2;// Set menu_level to 2
          }
          else
          {
            lcd_clear();// Clear LCD Display
            lcd_print("NOW PLAYING...");// Print String ("NOW PLAYING...") to LCD Display
            stick = 0;// Set stick to 0
            for (int i = 0; i < tune_buzzer[tune_menu][0] ; i++) 
            {
              if (stick == 0 & tune_buzzer[tune_menu][i] > 0) 
              {
                drum_stick(1, 0);// Enable SERVO 1
                stick = 1;// Set stick to 1
              }
              else if (stick == 1 & tune_buzzer[tune_menu][i] > 0) 
              {
                drum_stick(0, 1);// Enable SERVO 2
                stick = 0;// Set Stick to 0
              }
              else 
              {
                drum_stick(0, 0);// Disable SERVO 1 and SERVO 2
              }
              led_display(tune1_led[tune_menu][i][0], tune1_led[tune_menu][i][1], tune1_led[tune_menu][i][2], tune1_led[tune_menu][i][3], tune1_led[tune_menu][i][4], tune1_led[tune_menu][i][5], tune1_led[tune_menu][i][6], tune1_led[tune_menu][i][7], tune1_led[tune_menu][i][8], tune1_led[tune_menu][i][9]);
              buzzer(tune_buzzer[tune_menu][i + 1], dur[tune_menu][i]);// Play Tune (buzzer(TUNE NOTE, NOTE DURATION)
              if (button == 16) // Return/Exit (Button D of Keypad)
              {
                button = 0;// Set button to0
                break;
              }
            }
            led_display(0, 0, 0, 0, 0, 0, 0, 0, 0, 0);// Set All LED's LOW
            menu_level = 2;// Set menu_level to 2
          }
        }
      }
    }
  }


  //MAIN MENU - CURSOR ON CREATE A TUNE
  print_flag = 1;// Set print_flag to 1
  while (main_menu == 1 & menu_level == 0)
  {
    mode_menu = 0;// Set Mode_menu to 0
    if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
    {
      lcd_clear();// Clear LCD Display
      lcd_setCursor(0, 0); // Set Cursor to Home Position
      lcd_print("PLAY A TUNE");// Print String ("PLAY A TUNE") to LCD Display
      lcd_setCursor(0, 1); // Set Cursor on the Second Line and Incremented 0 Times to the Right
      lcd_print("CREATE A TUNE <");// Print Strinf ("CREATE A TUNE") to LCD Display
      print_flag = 0;// Set print_flag to 0
    }
    switch (button)
    {
      case 2:// Up (Button 2 of Keypad)
        main_menu = 0;// Set main_menu to 0
        button = 0;// Set butto to 0
        break;

      case 6:// Enter (Button 5 of Keypad)
        menu_level++;// Increments menu_level by 1
        button = 0;// Set button to 0
        break;

      case 10:// Down (Button 8 of Keypad)
        main_menu = 0;// Set main_menu to 0
        button = 0;// Set button to 0
        break;
    }

    //SELECT A MODULE MENU
    while (menu_level >= 1) // INCREMENTS TO THE NEXT MENU LEVEL
    {
      print_flag = 1;// Set print_flag to 1
      // MANUAL MODE
      while (mode_menu == 0 & menu_level >= 1)
      {
        if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
        {
          lcd_clear();// Clear LCD Display
          lcd_setCursor(0, 0);// Set Cursor to Home Position
          lcd_print("FREESTYLE MODE <");// Print String ("FREESTYLE MODE <") to LCD Display
          lcd_setCursor(0, 1);// Set Cursor to Second Line and Increment 0 Positions to the Right
          lcd_print("RECORD MODE");// Print String ("RECORD MODE") to LCD Display
          print_flag = 0;// Set print_flag to 0
        }
        switch (button)
        {
          case 2:// Up (Button 2 of Keypad)
            mode_menu = 1;// Set mode_menu to 1
            button = 0;// Set button to 0
            break;

          case 6:// Enter (Button 5 of Keypad)
            menu_level++;// Increment menu_level by 1
            button = 0;// Set button to 0
            print_flag = 1;// Set print_flag to 1
            break;

          case 10:// Down (Button 8 of Keypad)
            mode_menu = 1;// Set mode_menu to 1
            button = 0;// Set button to 0
            break;

          case 16:// Return/Exit (Button D of Keypad)
            menu_level--;// Decrement menu_level by 1
            button = 0;// Set button to 0
            print_flag = 1;// Set print_flag to 1
            break;
        }
        // FREESTYLE MENU
        while (menu_level >= 2)
        {
          while (freestyle_menu == 0 & menu_level >= 2)
          {
            if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
            {
              lcd_clear();// Clear LCD Display
              lcd_setCursor(0, 0);// Set Cursor to Home Position
              lcd_print("DRUMS <");// Print String ("DRUMS <") to LCD Display
              lcd_setCursor(0, 1);// Set cursor to Second Line and Increment 0 Positions to the Right
              lcd_print("BUZZER");// Print String ("BUZZER") to LCD Display
              lcd_setCursor(15, 0);// Set Cursor to Second Line and Increment 15 Positions to the Right
              lcd_print_custom(2);// Print Custom (UP ARROW) Character to LCD Display
              lcd_setCursor(15, 1);// Set Cursor to Second Line and Increment 15 Positions to the Right
              lcd_print_custom(1);// Print Custom (DOWM ARROW) Character to LCD Display
              print_flag = 0;// Set print_flag to 0
            }
            switch (button)
            {
              case 2:// Up (Button 2 of Keypad)
                freestyle_menu = 2;// Set freestyle_menu to 2
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                break;

              case 6:// Enter (Button 5 of Keypad)
                menu_level++;// Increment menu_level by 1
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                break;

              case 10:// Down (Button 8 of Keypad)
                freestyle_menu++;// Increment freestyle_menu by 1
                button = 0;// Set Button to 0
                print_flag = 1;// Set print_flag to 1
                break;

              case 16:// Return/Exit (Button D of Keypad)
                menu_level--;// Decrement menu_level by 1
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                break;
            }
            while (menu_level >= 3)
            {
              if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
              {
                lcd_clear();// Clear LCD Display
                lcd_setCursor(0, 0);// Set Cursor to Home Position
                lcd_print("(4)-LEFT STICK");//Print String ("(4)-LEFT STICK") to LCD Display
                lcd_setCursor(0, 1);// Set Cursor to Second Line and Increment 0 Positions to the Right
                lcd_print("(6)-RIGHT STICK");// Print String ("(6)-RIGHT STICK") to LCD Display
                print_flag = 0;// Set print_flag to 0
              }
              drum_manual = 1;// Set drum_manual to 0 (Activate Drum in Manual Mode)
              if (button == 16)// Return/Exit (Button D of Keypad)
              {
                menu_level--;// Decrement menu_level by 1
                button = 0;// Set button to 0
                drum_manual = 0;// Set drum_manual to 0 (Disable DRUM in Manual Mode)
                print_flag = 1;// Set print_flag to 1
                break;
              }
            }
          }
          while (freestyle_menu == 1 & menu_level >= 2)
          {
            if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
            {
              lcd_clear();// Clear LCD Display
              lcd_setCursor(0, 0);// Set Cursor to Home Position
              lcd_print("DRUMS");// Print String ("DRUMS") to LCD Display
              lcd_setCursor(0, 1);// Set Cursor to Second Line and Increment 0 Positions to the Right
              lcd_print("BUZZER <");// Print String ("BUZZER <") to LCD Display
              lcd_setCursor(15, 0);// Set Cursor to First Line and Increment 15 Positions to the Right
              lcd_print_custom(2);// Print Custom (UP ARROW) to LCD Display
              lcd_setCursor(15, 1);// Set Cursor to Second Line and Increment 15 Positions to the Right
              lcd_print_custom(1);// Print Custom (DOWN ARROW) Character to LCD Display
              print_flag = 0;// Set print_flag to 0
            }
            switch (button)
            {
              case 2:// Up (Button 2 of Keypad)
                freestyle_menu--;// Decrement freestyle_menu by 1
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                break;

              case 6:// Enter (Button 5 of Keypad)
                menu_level++;// Increment menu_level by 1
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                break;

              case 10:// Down (Button 8 of Keypad)
                freestyle_menu++;// Increment freestyle_menu
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                break;

              case 16:// Return/Exit (Button D of Keypad)
                menu_level--;// Decrement menu_level by 1
                button = 0;// Set Button to 0
                print_flag = 1;// Set print_flag to 1
                freestyle_menu = 0;// Set freestyle_menu to 0
                break;
            }
            // OCTAVE SELECTION
            while (menu_level >= 3)
            {
              octave_selection();// Call ocatve Selection Routine
              while (menu_level >= 4)
              {
                if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
                {
                  lcd_clear();// Clear LCD Diplay
                  lcd_setCursor(1, 0);// Set Cursor to First Line and Increment 1 Position to the Right
                  lcd_print("PRESS A BUTTON");// Print String ("PRESS A BUTTON") to LCD Display
                  lcd_setCursor(2, 1);// Set Cursor to Second Line and Increment 2 Positions to the Right
                  lcd_print("BETWEEN 1-9");// Print String ("BETWEEN 1-9") to LCD Display
                  print_flag = 0;// Set print_flag to 0
                }
                buzzer_manual = 1;// Set buzzer_manual to 1 (Activate Buzzer in Manual Mode)
                if (button == 16)// Return/Exit (Button D of Keypad)
                {
                  menu_level--;// Decrement menu_level
                  button = 0;// Set button to 0
                  print_flag = 1;// Set print_flag to 1
                  buzzer_manual = 0;// Set buzzer_manual to 0 (Deactivate Buzzer in Manual Mode)
                  octave = 0;// Set Octave to 0
                }
              }
            }
          }
          while (freestyle_menu == 2 & menu_level >= 2)
          {
            if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
            {
              lcd_clear();// Clear LCD Display
              lcd_setCursor(0, 0);//Set Cursor to Home Position
              lcd_print("10-SEGEMENT <");//Print String ("10-SEGEMENT <") to LCD Display
              lcd_setCursor(0, 1);// Set Cursor to Second Line and Increment 0 Positions to the Right
              lcd_print("DISPLAY");// Print String ("DISPLAY") to LCD Display
              lcd_setCursor(15, 0);// Set Cursor to Second line and Increment 15 Positions to the Right
              lcd_print_custom(2);// Print Custom (UP ARROW) Character to LCD Display
              lcd_setCursor(15, 1);// Set Cursor to Second Line and Increment 15 Positions to the Right
              lcd_print_custom(1);// Print Custom (DOWN ARROW) Character to LCD Display
              print_flag = 0;// Set print_flag to 0
            }
            switch (button)
            {
              case 2:// Up (Button 2 of Keypad)
                freestyle_menu--;// Decrement freestyle_menu by 1
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                break;

              case 6:// Enter (Button 5 of Keypad)
                menu_level++;// Increment menu_level by 1
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                break;

              case 10:// Down (Button 8 of Keypad)
                freestyle_menu = 0;// Set freestyle_menu to 0
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 0
                break;

              case 16:// Return/Exit (Button D of Keypad)
                menu_level--;// Decrement menu_level by 1
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 
                freestyle_menu = 0;// Set freestyle_menu to 0
                break;
            }
            while (menu_level >= 3)
            {
              if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
              {
                lcd_clear();// Clear LCD Display
                lcd_setCursor(1, 0);// Set Cursor to First Line and Increment 1 Position to the Right
                lcd_print("PRESS A BUTTON");// Print String ("PRESS A BUTTON") to LCD Display
                lcd_setCursor(2, 1);// Set Cursor to Second Line and Increment 2 Positions to the Right
                lcd_print("BETWEEN 0-9");// Print String ("BETWEEN 0-9") to LCD Display
                print_flag = 0;// Set print_flag to 0
              }
              LED_manual = 1;// Set LED_manul to 0 (Activate 10-SEGMENT DISPLAY in Manual Mode)
              if (button == 16)//Return/Exit (Button D on Keypad)
              {
                menu_level--;// Decrement menu_level by 1
                button = 0;// Set button to 0
                print_flag = 1;// Set print_flag to 1
                LED_manual = 0;// Set LED_manual to 0 (Deactivate 10-SEGMENT DISPLAY in Manual Mode)
              }
            }
          }
        }
      }
      print_flag = 1;// Set print_flag to 1

      // RECORD MODE
      while (mode_menu == 1 & menu_level >= 1)
      {
        if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
        {
          lcd_clear();// Clear LCD Display
          lcd_setCursor(0, 0);// Set Cursor to Home Position
          lcd_print("FREESTYLE MODE");// Print String ("FREESTYLE MODE") to LCD Display
          lcd_setCursor(0, 1);// Set Cursor to Second Line and Increment 0 Positions to the Right
          lcd_print("RECORD MODE <");// Print String ("RECORD MODE <") to LCD Display
          print_flag = 0;// Set print_flag to 0
        }
        switch (button)
        {
          case 2:// Up (Button 2 on Keypad)
            mode_menu = 0;// Set mode_menu to 0
            button = 0;// Set button to 0
            break;

          case 6:// Enter (Button 5 on Keypad)
            menu_level++;// Increment menu_level by 1
            button = 0;// Set Button to 0
            print_flag = 1;// Set print_flag to 1
            break;

          case 10:// Down (Button 8 on Keypad)
            mode_menu = 0;// Set mode_menu to 0
            button = 0;// Set button to 0
            break;

          case 16:// Return/Exit (Button D on Keypad)
            menu_level--;// Decrement menu_level by 1
            button = 0;// Set button to 0
            break;
        }
        // BUZZER-RECORD A TUNE
        while (menu_level >= 2)
        {
          temp_note_count = 0; // Set temp_note_count to 0 (Clear stored values in Temp Memory)
          if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
          {
            lcd_clear();// Clear LCD Display
            lcd_print("BUZZER <");// Print String ("BUZZER <") to LCD Display
            print_flag = 0;// Set Print_flag to 0
          }
          switch (button)
          {
            case 6:// Enter (Button 5 on Keypad)
              menu_level++;// Increment menu_level by 1
              button = 0;// Set button to 0
              print_flag = 1;// Set print_flag to 1
              break;

            case 16:// Return/Exit (Button D on Keypad)
              menu_level--;// Decrement menu_level by 1
              button = 0;// Set button to 0
              print_flag = 1;// Set print_flag to 1
              break;
          }
          // SELECT AN OCTAVE
          while (menu_level >= 3)
          {
            octave_selection();
            // CREATE THE TUNE TO STORE IN EEPROM
            while (menu_level >= 4)
            {
              if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
              {
                lcd_clear();// Clear LCD Display
                lcd_setCursor(0, 0);// Set Cursor to Home Position
                lcd_print("(A)-REC (B)-PLAY");// Print String ("(A)-REC (B)_PLAY") to LCD Display
                lcd_setCursor(0, 1);// Set Cursor to Second Line and Increment 0 Positions to the Right
                lcd_print("(C)-CLR (#)-SAVE");// Print String ("(C)-CLR (#)-SAVE") to LCD SCREEN
                print_flag = 0;// Set print_flag to 0
              }
              buzzer_manual = 1;// Set buzzer_manual to 1 (Activate Buzzer in Manual Mode)
              switch (button)
              {
                case 4:// Record/Stop Recording (Button A on KeyPad)
                  if (record == 0)// Enters if User Presses 'A' to Record A Tune
                  {
                    lcd_clear();// Clear LCD Display
                    lcd_print("RECORDING...");// Print String ("RECORDING...") to LCD SCREEN
                    record = 1;// Set record to 1 (Start Recoring of Tune)
                    TCCR5B = (1 << CS30) | (1 << CS31); //Set prescaler clkio/64 (TURN TIMER/COUNTER 5 ON)
                    count = 0;// Set Duration Count to 0
                  }
                  else if (record == 1)// Enters if User Presses 'A' to Stop Recording Tune
                  {
                    lcd_clear();// Clear LCD Display
                    lcd_setCursor(3, 0); // Set the Cursor to the First line and Increment 3 Positions to the Right
                    lcd_print("RECORDING");// Print String ("RECORDING") to LCD Screen
                    lcd_setCursor(4, 1); // Set the Cursor to the Second Line and Increment 4 Positions to the Right
                    lcd_print("STOPPED");// Print String ("STOPPED") to LCD Screen
                    _delay_ms(500);// 500ms Delay
                    record = 0;// Set record to 0 (Stop Recording Tune)
                    TCCR5B = 0;// Set Prescaler No Clock Source (TURN TIMER/COUNTER 5 OFF)
                    print_flag = 1;// Set Print Flag to 1
                  }
                  button = 0;// Set Button to 0
                  break;

                case 8:// Play Tune/Stop Tune (Button B on Keypad)
                  button = 0;// Set button to 0
                  print_flag = 1;// Set print_flag to 1
                  if (record == 0)
                  {
                    for (int i = 0; i < temp_note_count; i++)
                    {
                      buzzer(temp_custom_buzzer[i], temp_custom_dur[i] + DRUM_DELAY);// Play Tune (buzzer(TUNE NOTE, NOTE DURATION)
                      if (button == 8 | button == 16)// BUTTON B OR D OF KEYPAD
                      {
                        button = 0;// Set button to 0
                        break;
                      }
                    }
                  }
                  else
                  {
                    lcd_clear();// Clear LCD Display
                    lcd_setCursor(0, 0);// Set Cursor to Home Position
                    lcd_print("RECORDING");// Print String ("RECORDING") to LCD Display
                    lcd_setCursor(0, 1);// Set Cursor to Second Line and Increment 0 Positions to the Right
                    lcd_print("IN PROGRESS");// Print String ("IN PROGRESS") to LCD Display
                    _delay_ms(500);//500ms Delay
                  }
                  break;

                case 12:// Clear Tune (Button C on Keypad)
                  count = 0;// Set Count to 0
                  temp_note_count = 0;// Set tem_note_count to 0
                  button = 0;// Set button to 0
                  lcd_clear();// Clear LCD Display
                  lcd_setCursor(6, 0);// Set Cursor to the First Line and Increment 6 Positions to the Right
                  lcd_print("TUNE");// Print String ("TUNE") to LCD Display
                  lcd_setCursor(4, 1);// Set Cursor to the Second Line and Increment 4 Positions to the Right
                  lcd_print("CLEARED!");// Print String ("CLEARED!") to LCD Display
                  _delay_ms(500);// 500ms Delay
                  print_flag = 1;// Set print_flag to 1
                  break;

                case 15:// Save Tune to EEPROM (Button # on Keypad)
                  if (record == 0)// Enters loop if a Tune Isn't Recording
                  {
                    EEPROM_write(0, temp_note_count);// Stores temp_note_count in First Address of EEPROM
                    lcd_clear();
                    lcd_setCursor(0, 0);
                    lcd_print("SAVING...");
                    _delay_ms(250);
                    for (int i = 0; i < temp_note_count; i++)
                    {
                      hiByte = ((temp_custom_buzzer[i]) >> 8) & 0xFF;//
                      loByte = (temp_custom_buzzer[i]) & 0xFF;
                      EEPROM_write((i * 2) + 1, hiByte);
                      EEPROM_write((i * 2) + 2, loByte);
                      hiByte = ((temp_custom_dur[i]) >> 8) & 0xFF;
                      loByte = (temp_custom_dur[i]) & 0xFF;
                      EEPROM_write((i * 2) + 1 + (temp_note_count * 2), hiByte);
                      EEPROM_write((i * 2) + 2 + (temp_note_count * 2), loByte);
                    }
                    lcd_clear();
                    lcd_setCursor(0, 0);
                    lcd_print("TUNE SAVED");
                    _delay_ms(500);
                    EEPROM_flag = 1;
                  }
                  print_flag = 1;
                  button = 0;
                  break;

                case 16:// Return/Exit (Button D on Keypad)
                  record = 0;
                  menu_level--;
                  button = 0;
                  print_flag = 1;
                  buzzer_manual = 0;
                  octave = 0;
                  TCCR5B = 0;//Turn Timer/Counter 5 OFF
                  break;
              }
            }
          }
        }
      }
      print_flag = 1;
    }
  }
}

void lcd_setup(void) {
  _delay_ms(100); // 100ms Delay

  //FUNCTION SET
  lcd_inst();// Call Instruction Routine
  LCD_DATA_PORT = FUNCTION_SET;
  enable_latch();// Call enable Latch Routine
  _delay_us(37);

  //ENTRY MODE SET
  LCD_DATA_PORT = ENTRY_MODE_SET;
  enable_latch();// Call Enable Latch Routine
  _delay_us(37);

  //DISPLAY ON/OFF
  LCD_DATA_PORT = DISPLAY_ONOFF;
  enable_latch();// Call Enable Latch Routine
  _delay_us(37);

  lcd_clear();//clear the display

  lcd_setCursor(0, 0); //Set cursor home

}

void enable_latch(void) {
  LCD_CONTROL_PORT |= (1 << ENABLE); // Set ENABLE Pin HIGH
  _delay_us(0.6);
  LCD_CONTROL_PORT &= ~(1 << ENABLE); // Set ENABLE Pin LOW
  _delay_us(0.6);
}

void lcd_inst(void) {
  LCD_CONTROL_PORT &= ~(1 << RS) & ~(1 << RW);//SET RS and R/W Pins LOW
}

void lcd_data(void) {
  LCD_CONTROL_PORT |= (1 << RS); //Set RS Pin HIGH
  LCD_CONTROL_PORT &= ~(1 << RW);//Set R/W Pin LOW
}

void lcd_setCursor(int a, int b) {
  lcd_flag();// Check LCD Busy Flag
  lcd_inst();// Call Instruction Routine
  LCD_DATA_PORT = 0;// Set LCD DATA PORT to 0
  LCD_DATA_PORT |= (1 << D1);// Set D1 LOW
  enable_latch();// Call Enable Latch Routine

  if (b == 0)// IF B==0,FIRST LINE IS SELECTED
  { 
    for (int i = 0; i < a; i++) 
    {
      lcd_flag();// Check LCD Busy Flag
      lcd_inst();// Call Instruction Routine
      LCD_DATA_PORT = 0;// Set LCD DATA PORT to 0
      LCD_DATA_PORT |= (1 << D2) | (1 << D4);// Set D2 and D4 HIGH
      enable_latch();// Call Enable Latch Routine
    }
  }
  if (b == 1)// IF B==1, SECOND LINE IS SELECTED 
  { 
    for (int i = 0; i < a + 40; i++)//CURSOR NEEDS TO MOVE 40 INCREMENTS TO MOVE TO SECOND LINE 
    { 
      lcd_flag();// Check LCD Busy Flag
      lcd_inst();// Call Instruction Routine
      LCD_DATA_PORT = 0;// Set LCD DATA PORT to 0
      LCD_DATA_PORT |= (1 << D2) | (1 << D4);// Set D2 and D4 HIGH
      enable_latch();// Call Enable Latch Routine
    }
  }

}

void lcd_clear(void) 
{
  lcd_flag();// Checks LCD Busy Flag
  lcd_inst();// Call Instruction Routine
  LCD_DATA_PORT = 0;// Set LCD DATA PORT to 0
  LCD_DATA_PORT |= (1 << D0);// Set D0 HIGH
  enable_latch();// Call Enable Latch Routine
}

void lcd_print(char const a[50]) {
  for (int i = 0; i < 50; i++) {
    if (a[i] == 0) 
    {
      return;// Exit Out of Function
    }
    else 
    {
      lcd_flag();// Check Busy Flag
      lcd_data();// Call DATA Routine
      LCD_DATA_PORT = a[i];// Set DATA PORT to 8BIT ASCII Character
      enable_latch();// Call Enable Latch Routine
    }
  }
}

void custom_char() {
  lcd_flag();// Check LCD Busy Flag
  lcd_inst();// Call Instruction Routine
  LCD_DATA_PORT = 0b01000000;//Set LCD DATA PORT to CGRAM
  enable_latch();// SENDS INSTRUCTION TO LCD SCREEN

  for (int i = 0; i < NUMBER_OF_CUSTOM_CHARACTERS; i++) 
  {
    for (int j = 0; j < 8; j++) 
    {
      lcd_flag();// Check LCD Busy Flag
      lcd_data();// Call Data Routine
      LCD_DATA_PORT = custom_character[i][j];
      enable_latch();// Call Enable Latch Routine
      _delay_ms(1);// 1ms Delay
    }
  }
  lcd_flag();// Check LCD Busy Flag
  lcd_inst();// Call Instruction Routine
  LCD_DATA_PORT  = 0b10000000;// Set LCD DATA PORT to DDRAM
  enable_latch();// Call Enable Latch Routine
}

void lcd_print_custom(int character) 
{ 
  switch (character) 
  {
    case 1:
      lcd_flag();// Check LCD Busy Flag
      lcd_data();// Call Data Routine
      LCD_DATA_PORT = 0x00;// Set LCD DATA PORT with Custom Character 1 Address
      enable_latch();// Call Enable Latch Routine
      break;
    case 2:
      lcd_flag();// Check LCD Busy Flag
      lcd_data();// Call Data Routine
      LCD_DATA_PORT = 0x01;// Set LCD DATA PORT with Custom Character 2 Address
      enable_latch();// Call Enable Latch Routine
      break;
  }
}

void lcd_flag(void) {
  LCD_DATA_PORT &= ~(1 << D7);// Set D7 LOW (If D7 is HIGH, Internal Pullup Resistor will Enable when Set to an Input)
  LCD_DATA_DIRECTION &= ~(1 << D7);//Set D7 to an Input Pin

  LCD_CONTROL_PORT &= ~(1 << RS);//Set RS LOW
  LCD_CONTROL_PORT |= (1 << RW);// Set R/W HIGH,

  //FROM THE DATA SHEET, WHEN IN READ MODE DATA IS READ FROM THE LCD ON THE FALLING EGDE OF THE ENABLE SIGNAL
  LCD_CONTROL_PORT |= (1 << ENABLE); // Enable HIGH

  LCD_CONTROL_PORT &= ~(1 << ENABLE); // Enable LOW
  _delay_us(0.6);
  LCD_CONTROL_PORT |= (1 << ENABLE); // Enable HIGH
  _delay_us(0.6);

  while ( LCD_DATA_PIN & B10000000)// Wait for Completion of Previous Write
  { 
    LCD_CONTROL_PORT &= ~(1 << ENABLE); // Enable LOW
    _delay_us(0.6);
    LCD_CONTROL_PORT |= (1 << ENABLE); // Enable HIGH
    _delay_us(0.6);
  }
  LCD_DATA_PORT &= ~(1 << D7); // Set D7 LOW
  LCD_DATA_DIRECTION |= (1 << D7); // Set D7 to an Output PinS
}

ISR(TIMER3_COMPA_vect) {
  TCNT3H = 0xFF;
  TCNT3L = 0xB2;
  if (seq == 1)
  {
    KEYPAD_COL_PORT = 0b00000111;// Set Bit 3 LOW
    seq = 2;// Set seq to 2
  }
  else if (seq == 2)
  {
    KEYPAD_COL_PORT = 0b00001011;// Set Bit 2 LOW
    seq = 3;// Set seq to 3
  }
  else if (seq == 3)
  {
    KEYPAD_COL_PORT = 0b00001101;// Set Bit 1 LOW
    seq = 4;// Set seq to 4
  }
  else if (seq == 4)
  {
    KEYPAD_COL_PORT = 0b00001110;// Set Bit 0 LOW
    seq = 1;// Set seq to 1
  }
}

//INTERRUPT HANDLER FOR INT0
ISR (INT0_vect)
{
  sei();// Enable Global Interrupts
  TCCR3B = 0;// Turn Off Pin Cycle Timer/Counter Interrupt
  if (bit_is_clear(KEYPAD_ROW_PIN, ROW1 ))//First Check
  {
    _delay_ms(25); //25ms Delay for Debounce
    if (bit_is_clear(KEYPAD_ROW_PIN, ROW1))//Second Check
    {
      if (record == 1)// Enters Loop if Recording of Tune is Activated
      {
        temp_custom_buzzer[temp_note_count] = 0;// Store 0 into temp_custom_buzzer
        temp_custom_dur[temp_note_count] = count;// Store Count (Duration of Break) into temp_custom_dur
        temp_note_count++;// Increment temp_note_count by 1
        count = 0;// Set Count to 0
      }
      if (seq == 1)// BUTTON * OF KEYPAD
      {
          
          if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
        {
          buzzer(FS[octave], 0);// Play Note with Selected Octave
          note = FS[octave];// Set note to Value of Frequency Played
        }
        else
      {
        button = 13;// Set Button to 13
      }
      }

      else if (seq == 2)// BUTTON D OF KEYPAD
      {
        button = 16;// Set Button to 16
      }
      else if (seq == 3)// BUTTON # OF KEYPAD
      {
        button = 15;// Set Button to 15
      }

      else if (seq == 4)// BUTTON 0 OF KEYPAD
      {
        if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
        {
          buzzer(G[octave], 0);// Play Note with Selected Octave
          note = G[octave];// Set note to Value of Frequency Played
        }
        else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
        {
          led_display(0, 0, 0, 0, 0, 0, 0, 0, 0, 1);// Set LED 10 HIGH
        }
        else
        {
          button = 14;//Set Button to 14
          
        }
      }
    }
  }
  while (bit_is_clear(KEYPAD_ROW_PIN, ROW1)); //Waits Until Button is Released (To Account for Multiple Button Presses)
  ICR4 = 0; OCR4A = 0; TCNT4 = 0;// Set ICR4, OCR4A and TCNT4 to 0 (Buzzer OFF)
  if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
  {
    led_display(0, 0, 0, 0, 0, 0, 0, 0, 0, 0);// Sets All LEDs of 10-Segment Display LOW
  }
  if (record == 1)// Enters Loop if Recording of Tune is Activated
  {
    temp_custom_buzzer[temp_note_count] = note;// Store Note Played into temp_custom_buzzer
    temp_custom_dur[temp_note_count] = count;// Store Count (Duration of Note Played) into temp_custom_dur
    temp_note_count++;// Increment temp_note_count by 1
    count = 0;// Set Count to 0
  }
  TCCR3B = (1 << CS32) | (1 << CS10);// Set Prescaler for Timer/Counter 3 Channel B to 1024 (Turn Pin Cycle Interrupt ON)
}
  //INTERRUPT HANDLER FOR INT1
  ISR (INT1_vect)
  {
    sei();// Enable Global Interrupts
    TCCR3B = 0;// Turn Off Pin Cycle Timer/Counter Interrupt
    if (bit_is_clear(KEYPAD_ROW_PIN, ROW2 )) //First Check
    {
      _delay_ms(25); //25ms Delay for Debounce
      if (bit_is_clear(KEYPAD_ROW_PIN, ROW2))// Second Check
      {
        if (record == 1)// Enters Loop if Recording of Tune is Activated
        {
          temp_custom_buzzer[temp_note_count] = 0;// Store 0 into temp_custom_buzzer
          temp_custom_dur[temp_note_count] = count;// Store Count (Duration of Break) into temp_custom_dur
          temp_note_count++;// Increment temp_note_count by 1
          count = 0;// Set count to 0
        }
        if (seq == 1)//BUTTON 7 OF KEYPAD
        {
          if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(DS[octave], 0);// Play Note with Selected Octave
            note = DS[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(0, 0, 0, 0, 0, 0, 1, 0, 0, 0);// Set LED 7 HIGH
          }
          else
          {
            button = 9;// Set Button to 9

          }
        }
        else if (seq == 2)// BUTTON C OF KEYPAD
        {
          // TURN 10-SEGMENT DISPLAY ON AND OFF WHILE TUNE PLAYING
          ICR4 = 0; OCR4A = 0; TCNT4 = 0;// Set ICR4, OCR4A and TCNT4 to 0 (Buzzer OFF)
          if (main_menu == 0 & menu_level == 3)// Enters Loop if a Tune is Playing 
          {
            lcd_clear();// Clear LCD Display
            lcd_setCursor(1, 0);// Set Cursor to the First Line and Increment 1 Position to the Right
            lcd_print("10-SEG DISPLAY");// Print String ("10-SEG DISPLAY") to LCD Display
            if (module[2] == 1)// Enters Loop if 10-SEGMENT DISPLAY==1 (ACTIVATED)
            {
              module[2] = 0;// Set 10-SEGMENT DISPLAY to 0 (DEACTIVATED)
              lcd_setCursor(1, 1);
              lcd_print("-DEACTIVATED-");
              _delay_ms(400);
            }
            else if (module[2] == 0)// Enters Loop if 10-SEGMENT DISPLAY==0 (DEACTIVATED)
            {
              module[2] = 1;// Set 10-SEGMENT DISPLAY to 1 (ACTIVATED)
              lcd_setCursor(2, 1);// Set Cursor to the Second Line and Increment 2 Positions to the Right
              lcd_print("-ACTIVATED-");// Print String ("-ACTIVATED-") TO LCD Display
              _delay_ms(400);// 400ms Delay
            }
            lcd_clear();// Clear LCD Display
            lcd_print("NOW PLAYING...");// Print String ("NOW PLAYING...") to LCD Display
          }
          else
          {
            button = 12;// Set Button to 12
          }
        }
        else if (seq == 3)// BUTTON 9 OF KEYPAD
        {
          if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(F[octave], 0);// Play Note with Selected Octave
            note = F[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(0, 0, 0, 0, 0, 0, 0, 0, 1, 0);// Set LED 9 HIGH
          }
          else
          {
            button = 11;// Set Button to 11

          }
        }
        else if (seq == 4)// BUTTON 8 OF KEYPAD
        {
          if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(E[octave], 0);// Play Note with Selected Octave
            note = E[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(0, 0, 0, 0, 0, 0, 0, 1, 0, 0);// Set LED 8 HIGH
          }
          else
          {
            button = 10;// Set Button to 10

          }
        }
      }
    }
    while (bit_is_clear(KEYPAD_ROW_PIN, ROW2)); //Waits Until Button is Released (To Account for Multiple Button Presses)
    ICR4 = 0; OCR4A = 0; TCNT4 = 0;// Set ICR4, OCR4A and TCNT4 to 0 (Buzzer OFF)
    if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
    {
      led_display(0, 0, 0, 0, 0, 0, 0, 0, 0, 0);// Sets All LEDs of 10-Segment Display LOW
    }
    if (record == 1)// Enters Loop if Recording of Tune is Activated
    {
      temp_custom_buzzer[temp_note_count] = note;// Store Note Played into temp_custom_buzzer
      temp_custom_dur[temp_note_count] = count;// Store Count (Duration of Note Played) into temp_custom_dur
      temp_note_count++;// Increment temp_note_count by 1
      count = 0;// Set Count to 0
    }
    TCCR3B = (1 << CS32) | (1 << CS10);// Set Prescaler for Timer/Counter 3 Channel B to 1024 (Turn Pin Cycle Interrupt ON)
  }

  //INTERUPT HANDLER FOR INT2
  ISR (INT2_vect)
  {
    sei();// Enable Global Interrupts
    TCCR3B = 0;// Turn Off Pin Cycle Timer/Counter Interrupt
    if (bit_is_clear(KEYPAD_ROW_PIN, ROW3 )) //First Check
    {
      _delay_ms(25); //25ms Delay for Debounce
      if (bit_is_clear(KEYPAD_ROW_PIN, ROW3))// Second Check
      {
        if (record == 1)// Enters Loop if Recording of Tune is Activated
        {
          temp_custom_buzzer[temp_note_count] = 0;// Store 0 into temp_custom_buzzer
          temp_custom_dur[temp_note_count] = count;// Store Count (Duration of Break) into temp_custom_dur
          temp_note_count++;// Increment temp_note_count by 1
          count = 0;// Set count to 0
        }
        if (seq == 1)// BUTTON 4 OF KEYPAD
        {
          if (drum_manual == 1)// Enters Loop if Drum is Activated in Manual Mode
          {
            OCR1A = SERVO1_HIT;// Set SERVO 2 to Hit Drum
            _delay_ms(DRUM_DELAY);//Delay of DRUM_DELAY
            while (bit_is_clear(KEYPAD_ROW_PIN, ROW3));//Waits Until Button is Released (To Account for Multiple Button Presses)
            OCR1A = SERVO1_HOME;// Set SERVO 1 to Home Position
            _delay_ms(DRUM_DELAY);//Delay of DRUM_DELAY
          }
          else if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(C[octave], 0);// Play Note with Selected Octave
            note = C[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(0, 0, 0, 1, 0, 0, 0, 0, 0, 0);// Set LED 4 HIGH
          }
          else
          {
            button = 5;// Set Button to 5

          }
        }
        else if (seq == 2)// BUTTON B OF KEYPAD
        {
          // TURN BUZZER ON AND OFF WHILE TUNE PLAYING
          ICR4 = 0; OCR4A = 0; TCNT4 = 0;// Set ICR4, OCR4A and TCNT4 to 0 (Buzzer OFF)
          if (main_menu == 0 & menu_level == 3)// Enters Loop if a Tune is Playing
          {
            lcd_clear();// Clear LCD Display
            lcd_setCursor(5, 0);// Set Cursor to the First Line and Increment 5 Positions to the Right
            lcd_print("BUZZER");// Print String ("BUZZER") to LCD Display
            if (module[1] == 1)// Enters Loop if BUZZER==1 (ACTIVATED) 
            {
              module[1] = 0;// Set BUZZER to 0 (DEACTIVATED)
              lcd_setCursor(1, 1);// Set Cursor to the Second Line and Increment 1 Position to the Right
              lcd_print("-DEACTIVATED-");// Print String ("-DEACTIVATED-") to LCD Display
              _delay_ms(400);// 400ms Delay
            }
            else if (module[1] == 0)// Enters Loop if BUZZER==1 (DEACTIVATED)
            {
              module[1] = 1;// Set BUZZER to 1 (ACTIVATED)
              lcd_setCursor(2, 1);// Set Cursor to the Second Line and Increment 2 Positions to the Right
              lcd_print("-ACTIVATED-");// Print String ("-ACTIVATED-") to LCD Display
              _delay_ms(400);// 400ms Delay
            }
            lcd_clear();// Clear LCD Display
            lcd_print("NOW PLAYING...");// Print String ("NOW PLAYING...") to LCD Display
          }
          else
          {
            button = 8;// Set Button to 8
          }
        }
        else if (seq == 3)// BUTTON 6 OF KEYPAD
        {
          if (drum_manual == 1)// Enters Loop if Drum is Activated in Manual Mode
          {
            OCR1B = SERVO2_HIT; // Set SERVO 2 to Hit Drum
            _delay_ms(DRUM_DELAY); // Delay of DRUM_DELAY
            while (bit_is_clear(KEYPAD_ROW_PIN, ROW3)); //Waits Until Button is Released (To Account for Multiple Button Presses)
            OCR1B = SERVO2_HOME; // Set SERVO 2 to Home Position
            _delay_ms(DRUM_DELAY); // Delay of DRUM_DELAY
          }
          else if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(D[octave], 0);// Play Note with Selected Octave
            note = D[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(0, 0, 0, 0, 0, 1, 0, 0, 0, 0);// Set LED 6 HIGH
          }
          else
          {
            button = 7;// Set Button to 7

          }
        }
        else if (seq == 4)// BUTTON 5 OF KEYPAD
        {
          if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(CS[octave], 0);// Play Note with Selected Octave
            note = CS[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(0, 0, 0, 0, 1, 0, 0, 0, 0, 0);// Set LED 5 HIGH
          }
          else
          {
            button = 6;// Set Button to 6

          }
        }
      }
    }
    while (bit_is_clear(KEYPAD_ROW_PIN, ROW3)); //Waits Until Button is Released (To Account for Multiple Button Presses)
    ICR4 = 0; OCR4A = 0; TCNT4 = 0;// Set ICR4, OCR4A and TCNT4 to 0 (Buzzer OFF)
    if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
    {
      led_display(0, 0, 0, 0, 0, 0, 0, 0, 0, 0);// Sets All LEDs of 10-Segment Display LOW
    }
    if (record == 1)// Enters Loop if Recording of Tune is Activated
    {
      temp_custom_buzzer[temp_note_count] = note;// Store Note Played into temp_custom_buzzer
      temp_custom_dur[temp_note_count] = count;// Store Count (Duration of Note Played) into temp_custom_dur
      temp_note_count++;// Increment temp_note_count by 1
      count = 0;// Set Count to 0
    }
    TCCR3B = (1 << CS32) | (1 << CS10);// Set Prescaler for Timer/Counter 3 Channel B to 1024 (Turn Pin Cycle Interrupt ON)
  }

  //INTERRUPT HANDLER FOR INT3
  ISR (INT3_vect)
  {
    sei();// Enable Global Interrupts
    TCCR3B = 0;// Turn Off Pin Cycle Timer/Counter Interrupt
    if (bit_is_clear(KEYPAD_ROW_PIN, ROW4 )) //First Check
    {
      _delay_ms(25); //25ms Delay for Debounce
      if (bit_is_clear(KEYPAD_ROW_PIN, ROW4))// Second Check
      {
        if (record == 1)// Enters Loop if Recording of Tune is Activated
        {
          temp_custom_buzzer[temp_note_count] = 0;// Store 0 into temp_custom_buzzer
          temp_custom_dur[temp_note_count] = count;// Store Count (Duration of Break) into temp_custom_dur
          temp_note_count++;// Increment temp_note_count by 1
          count = 0;// Set count to 0
        }

        if (seq == 1)// BUTTON 1 OF KEYPAD
        {
          if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(A[octave], 0);// Play Note with Selected Octave
            note = A[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(1, 0, 0, 0, 0, 0, 0, 0, 0, 0);// Set LED 1 HIGH
          }
          else
          {
            button = 1;// Set Button to 1

          }
        }
        else if (seq == 2)// BUTTON A OF KEYPAD
        {
          // TURN DRUM ON AND OFF WHILE TUNE PLAYING
          ICR4 = 0; OCR4A = 0; TCNT4 = 0;// Set ICR4, OCR4A and TCNT4 to 0 (Buzzer OFF)
          if (main_menu == 0 & menu_level == 3)// Enters Loop if a Tune is Playing
          {
            lcd_clear();// Clear LCD Display
            lcd_setCursor(6, 0);// Set Cursor to the First Line and Increment 6 Positions to the Right
            lcd_print("DRUM");// Print String ("DRUM") to LCD Display
            if (module[0] == 1)// Enters Loop if DRUM==1 (ACTIVATED)
            {
              module[0] = 0;// Set DRUM to 0 (DEACTIVATED)
              lcd_setCursor(1, 1);// Set Cursor to the Second Line and Increment 1 Position to the Right
              lcd_print("-DEACTIVATED-");// Print String ("-DEACTIVATED-") to LCD Display
              _delay_ms(400);//Delay 400ms
            }
            else if (module[0] == 0) // Enters Loop if DRUM==0 (DEACTIVATED)
            {
              module[0] = 1;// Set DRUM to 1 (ACTIVATED)
              lcd_setCursor(2, 1);// Set Cursor to the Second Line and Increment 2 Postions to the Right
              lcd_print("-ACTIVATED-");// Print String ("-ACTIVATED-") to LCD Display
              _delay_ms(400);// Delay 400ms
            }
            lcd_clear();// Clear LCD Display
            lcd_print("NOW PLAYING...");// Print String ("NOW PLAYING...") to LCD Display
          }
          else
          {
            button = 4;// Set Button to 4
          }
        }
        else if (seq == 3)// BUTTON 3 OF KEYPAD
        {
          if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(B[octave], 0);// Play Note with Selected Octave
            note = B[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(0, 0, 1, 0, 0, 0, 0, 0, 0, 0);// Set LED 3 HIGH
          }
          else
          {
            button = 3;// Set Button to 3

          }
        }
        else if (seq == 4) // BUTTON 2 OF KEYPAD
        {
          if (buzzer_manual == 1)// Enters Loop if Buzzer is Activated in Manual Mode
          {
            buzzer(AS[octave], 0);// Play Note with Selected Octave
            note = AS[octave];// Set note to Value of Frequency Played
          }
          else if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
          {
            led_display(0, 1, 0, 0, 0, 0, 0, 0, 0, 0);// Set LED 2 HIGH
          }
          else
          {
            button = 2;// Set button to 2

          }
        }
      }
    }

    while (bit_is_clear(KEYPAD_ROW_PIN, ROW4)); //Waits Until Button is Released (To Account for Multiple Button Presses)
    ICR4 = 0; OCR4A = 0; TCNT4 = 0;// Set ICR4, OCR4A and TCNT4 to 0 (Buzzer OFF)
    if (LED_manual == 1)// Enters Loop if 10-Segment Display is Activated in Manual Mode
    {
      led_display(0, 0, 0, 0, 0, 0, 0, 0, 0, 0);// Sets All LEDs of 10-Segment Display LOW
    }
    if (record == 1)// Enters Loop if Recording of Tune is Activated
    {
      temp_custom_buzzer[temp_note_count] = note;// Store Note Played into temp_custom_buzzer
      temp_custom_dur[temp_note_count] = count;// Store Count (Duration of Note Played) into temp_custom_dur
      temp_note_count++;// Increment temp_note_count by 1
      count = 0;// Set Count to 0
    }
    TCCR3B = (1 << CS32) | (1 << CS10);// Set Prescaler for Timer/Counter 3 Channel B to 1024 (Turn Pin Cycle Interrupt ON)
  }

  void buzzer(float note, int duration)
  {
    float pwm_period;// Variable to Store the Calculated PWM Period Value
    if (module[1] == 1) // Enters Loop if Buzzer is Activated
    {
      pwm_period = (1 / note) / (TIMER4_PRESCALER / CLOCK_FREQUENCY);// Converts Frequency into PWM period
      ICR4 = pwm_period;// Set TOP to Calculated PWM Period
      OCR4A = pwm_period / 2;// Set COMP to half the Calculated PWM Period (50% Duty Cycle)
      TCNT4 = 0;// Set BOTTOM to 0
    }
    if (duration >= DRUM_DELAY)// Enters loop if Duration is Greater than or Equal to DRUM_DELAY
    {
      for (int j = 0; j < (duration - DRUM_DELAY); j++)
      {
        _delay_ms(1);// 1ms Delay
      }
      ICR4 = 0; OCR4A = 0; TCNT4 = 0;// Set ICR4, OCR4A and TCNT4 to 0 (Buzzer OFF)
    }
  }

  //FUNCTION TO CONTROL THE STATE OF EACH LED ON THE 10-SEGMENT DISPLAY
  void led_display(int led_1, int led_2, int led_3, int led_4, int led_5, int led_6, int led_7, int led_8, int led_9, int led_10)
  {
    if (module[2] == 1)// Enters Loop if 10-Segment Display is Activated
    {
      if (led_1 == 1)
      {
        LED_0to7_PORT |= (1 << LED_0); // Set LED 1 HIGH
      }
      else
      {
        LED_0to7_PORT &= ~(1 << LED_0);// Set LED 1 LOW
      }
      if (led_2 == 1)
      {
        LED_0to7_PORT |= (1 << LED_1); // Set LED 2 HIGH
      }
      else
      {
        LED_0to7_PORT &= ~(1 << LED_1); // Set LED 2 LOW
      }
      if (led_3 == 1)
      {
        LED_0to7_PORT |= (1 << LED_2); // Set LED 3 HIGH
      }
      else
      {
        LED_0to7_PORT &= ~(1 << LED_2); // Set LED 3 LOW
      }
      if (led_4 == 1)
      {
        LED_8to9_PORT |= (1 << LED_3); // Set LED 4 HIGH
      }
      else
      {
        LED_8to9_PORT &= ~(1 << LED_3); // Set LED 4 LOW
      }
      if (led_5 == 1)
      {
        LED_0to7_PORT |= (1 << LED_4); // Set LED 5 HIGH
      }
      else
      {
        LED_0to7_PORT &= ~(1 << LED_4); // Set LED 5 LOW
      }
      if (led_6 == 1)
      {
        LED_0to7_PORT |= (1 << LED_5); // Set LED 6 HIGH
      }
      else
      {
        LED_0to7_PORT &= ~(1 << LED_5);// Set LED 6 LOW
      }
      if (led_7 == 1)
      {
        LED_0to7_PORT |= (1 << LED_6); // Set LED 7 HIGH
      }
      else
      {
        LED_0to7_PORT &= ~(1 << LED_6); // Set LED 7 LOW
      }
      if (led_8 == 1)
      {
        LED_0to7_PORT |= (1 << LED_7); // Set LED 8 HIGH
      }
      else
      {
        LED_0to7_PORT &= ~(1 << LED_7); // Set LED 8 LOW
      }
      if (led_9 == 1)
      {
        LED_8to9_PORT |= (1 << LED_8); // Set LED 9 HIGH
      }
      else
      {
        LED_8to9_PORT &= ~(1 << LED_8); // Set LED 9 LOW
      }
      if (led_10 == 1)
      {
        LED_8to9_PORT |= (1 << LED_9); // Set LED 10 HIGH
      }
      else
      {
        LED_8to9_PORT &= ~(1 << LED_9); // Set LED 10 LOW
      }
    }
    // IF THE LED 10-SEG IS NOT ACTIVATED ALL THE LED'S ARE OFF
    else
    {
      LED_0to7_PORT = 0; // Set LED 1 to 8 LOW
      LED_8to9_PORT &= ~(1 << LED_9) & ~(1 << LED_8); // SET LED 9-10 LOW
    }
  }

  void drum_stick(int stick_1, int stick_2)
  {
    if (module[0] == 1)// Enters Loop if Drum is Activated
    {
      if (stick_1 == 1)// Enters Loop if SERVO 2 Was the Previous Servo Used
      {
        OCR1A = SERVO1_HIT;// Set SERVO 1 to Hit Drum
      }
      if (stick_2 == 1)// Enters Loop if SERVO 1 Was The Previous Servo Used
      {
        OCR1B = SERVO2_HIT;// Set SERVO 2 to Hit Drum
      }
    }
    _delay_ms(DRUM_DELAY);// Delay of DRUM_DELAY
    OCR1A = SERVO1_HOME;// Set SERVO 1 to Home Position
    OCR1B = SERVO2_HOME;// Set SERVO 2 to Home Position
  }

  void EEPROM_write(unsigned int uiAdress, unsigned char ucData)
  {
    while (EECR & (1 << EEPE));// Wait for Completion of Previous Write
    EEAR = uiAdress;// Set Up Address Register
    EEDR = ucData;// Set Up Data Register
    EECR |= (1 << EEMPE);//Write Logical One to EEMPE
    EECR |= (1 << EEPE);// Start EEPROM Write by Seting EEPE
  }

  unsigned char EEPROM_read(unsigned int uiAdress)
  {
    while (EECR & (1 << EEPE));// Wait for Completion of Previous Write
    EEAR = uiAdress;// Set Up Address Register
    EECR |= (1 << EERE);// Start EEPROM Read by Writing EERE
    return EEDR;// Return Data from Data Register
  }

  ISR(TIMER5_COMPA_vect)
  {
    TCNT5H = 0xFF;
    TCNT5L = 0x14;
    count++;// Increment Count by 1
  }

  void octave_selection(void)
  {
    if (print_flag == 1)// Enters Loop if Hasn't Entered Loop Previously
    {
      lcd_clear();// Clear LCD Display
      lcd_setCursor(1, 0);// Set Cursor to First Line and Increment 1 Position to the Right
      lcd_print("PLEASE SELECT");// Print string ("PLEASE SELECT") to LCD Display
      lcd_setCursor(3, 1);// Set Cursor to Second Line and Increment 3 Positions to the Right
      lcd_print("AN OCTAVE");// Print String ("AN OCTAVE") to LCD Display
      print_flag = 0;// Set print_flag to 0
    }
    switch (button)
    {
      case 5:// OCTAVE 4 (Button 4 of Keypad)
        octave = 4;// Set octave to 4
        menu_level++;// Increment menu_level by 1
        print_flag = 1;// Set print_flag to 1
        break;

      case 6:// OCTAVE 5 (Button 5 of Keypad)
        octave = 5;// Set octave to 5
        menu_level++;// Increment menu_level by 1
        print_flag = 1;// Set print_flag to 1
        break;

      case 7:// OCTAVE 6 (Button 6 of Keypad)
        octave = 6;// Set octave to 6
        menu_level++;// Increment menu_level by 1
        print_flag = 1;// Set print_flag to 1
        break;

      case 9:// OCTAVE 7 (Button 7 of Keypad)
        octave = 7;// Set octave to 7
        menu_level++;// Increment menu_level by 1
        print_flag = 1;// Set print_flag to 1
        break;

      case 16:
        menu_level--;// Decrement menu_level by 1
        print_flag = 1;// Set print_flag to 1
        break;
    }
    button = 0;// Set Button to 0
  }


