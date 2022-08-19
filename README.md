# lab_4
## Microcomputers group_12

    SRI LANKA INSTITUE OF INFORMATION TECHNOLOGY
    B.Sc. Eng. Department of Electronic & Computer Engineering
    EC 2131 – Micro Computers
    Laboratory 04 - group 12
    Lecturer/ Instructor -Mr.Lasantha Seneviratne
        
    Date of Performance -20/07/2022 
    Due date -19/08/2022 
    Date submitted -19/08/2022

    Details of the student/ID Number Name (As per the institute records )
- Wijeruwan K.N.N-EN21483592
- Siriwardhana A.N.K-EN21477584
- Bandusena R.P.N.M -EN21484032


## Content
- Objective
- Apparatus
- Introduction
- Task
- Operation Table
- Breadboard Implementation
- The PCB Design
- An Image of the Real Implementation
- Code
- Results
- Discussion
- References

## Objective
The main objective of this lab is for you to develop a small water level controlling system of a water tank using the knowledge of interrupts and other programming techniques of PIC16f877a from all the labs we did throughout the course. 

## Apparatus
- 12v-5v convertor (7805)
- 22pf capacitor 
- 20MHz crystal
- 10k, 330ohm resistor 
- Diode
- L293d motercontroller 
- Pic16f877a
- 100uf capacitor 
- 12v input jack
- Ultrasonic sensor
- Motors

## Introduction
The objective of the project is to build a water level detector which can regulate the water level using a suitable sensor with the aid of the PIC16F877A Microcontroller. In this system, Ultrasonic Sensor was used as the sensor to detect the water level.
  
An ultrasonic sensor is an instrument that measures the distance to an object using ultrasonic sound waves. An ultrasonic sensor uses a transducer to send and receive ultrasonic pulses that relay back information about an object’s proximity. High-frequency sound waves reflect from boundaries to produce distinct echo patterns. 

Ultrasonic sensors work by sending out a sound wave(ultrasonic) at a frequency above the range of human hearing.  The transducer of the sensor acts as a microphone to receive and send the ultrasonic sound. The sensor determines the distance to a target by measuring time lapses between the sending and receiving of the ultrasonic pulse. 

By calculating the travel time and the speed of sound, the distance can be calculated. The formula for this calculation is D = ½ T x C (where D is the distance, T is the time, and C is the speed of sound ~ 343 meters/second). This will give out the signals for the relevant distances to the Microcontroller. 
(For the implementation the IR sensor was not selected as it wouldn’t work perfectly with the water level conditions.)

The signals from the sensor will be transferred to the Microcontroller as the input signals. The PIC microcontroller PIC16F877A is one of the most renowned microcontrollers in the industry. This microcontroller is very convenient to use, the coding or programming of this controller is also easier. It has a total number of 40 pins and there are 33 pins for input and output. PIC16F877A is used in many pic microcontroller projects. PIC16F877A also have much application in digital electronics circuits. From this Microcontroller it gives the particular outputs to Switch ON or Switch OFF the DC motors.

According to the given outputs from the Microcontroller the DC motors will work to regulate the water level of the tank.


## Task
Below is a water tank that has two DC motors where the motor one is used to pump the water into the tank the motor two is used to suck the water out from the water tank and there are three sensors that are used to measure the water level of the tank. The operations of the two DC motors according to the switch state is given in a table right after the diagram.

### Operation Table
![Screenshot 2022-08-19 143343](https://user-images.githubusercontent.com/111522052/185584824-6dd93e77-e4cc-489c-8773-6fd93fced128.png)

## The PCB Design
![rsz_11whatsapp_image_2022-08-17_at_91210_pm](https://user-images.githubusercontent.com/111522052/185592679-b27002d9-9524-4bc6-b30a-8fde0faa6e94.jpg)![rsz_whatsapp_image_2022-08-17_at_91313_pm](https://user-images.githubusercontent.com/111522052/185592899-5dc541b0-0cfc-4ebb-966c-e235f837db4c.jpg)
![rsz_3rsz_4my_project](https://user-images.githubusercontent.com/111522052/185596594-40b26239-626d-43c7-825c-9dd97b976bc9.jpg)![rsz_whatsapp_image_2022-08-16_at_123601_pm](https://user-images.githubusercontent.com/111522052/185597619-2a118e5a-ae02-4544-bf4a-f926c7bf7f3e.jpg)
![WhatsApp Image 2022-08-19 at 6 18 40 PM](https://user-images.githubusercontent.com/111522052/185622212-4b724a1b-1c49-45bf-a462-be3c006119dc.jpeg)
![rsz_whatsapp_image_2022-08-16_at_123600_pm_1](https://user-images.githubusercontent.com/111522052/185598110-16b8d5f4-856a-4c76-b778-b8fd22fbf87d.jpg)


## Images of the realtime implementation
![rsz_2whatsapp_image_2022-08-19_at_10500_pm](https://user-images.githubusercontent.com/111522052/185614882-009b7c14-7e89-4bd1-af2d-6f8a46a4eaf9.jpg)
![rsz_1whatsapp_image_2022-08-19_at_125628_pm](https://user-images.githubusercontent.com/111522052/185615715-ad9180ca-4384-4066-9175-73f90f97ed55.jpg)

## Results
According to the above displayed code the distance between the water level will be calculated. MOTOR1  and MOTOR2 will work to the given outputs of the PIC16F877A Microcontroller. From the distance 35cm to 25cm the MOTOR1 will be turned ON. And from the distance 25cm to 15cm the MOTOR1 will again be turned ON. After 15cm the timer1 interrupt flag will be logic high. So when the calculated distance is less than 15cm MOTOR1 will turned OFF and the MOTOR2 will be turned ON for 500 milliseconds and it will turned OFF. So, the PCB circuit will work according to the updated truth table values.


## Code Used for The Full Implementation
    // CONFIG
    #pragma config FOSC = HS      // Oscillator Selection bits (HS oscillator)
    #pragma config WDTE = OFF     // Watchdog Timer Enable bit (WDT disabled)
    #pragma config PWRTE = ON     // Power-up Timer Enable bit (PWRT disabled)
    #pragma config BOREN = ON     // Brown-out Reset Enable bit (BOR disabled)
    #pragma config LVP = OFF      // Low-Voltage (Single-Supply) In-Circuit Serial Programming Enable bit (RB3 is digital I/O, HV on MCLR must be used for programming)
    #pragma config CPD = OFF      // Data EEPROM Memory Code Protection bit (Data EEPROM code protection off)
    #pragma config WRT = OFF      // Flash Program Memory Write Enable bits (Write protection off; all program memory may be written to by EECON control)
    #pragma config CP = OFF       // Flash Program Memory Code Protection bit (Code protection off)

    // #pragma config statements should precede project file includes.
    // Use project enums instead of #define for ON and OFF.

    #include <xc.h>
    #define _XTAL_FREQ 20000000
    #define trigger RB1
    #define echo RB0


    void __interrupt() timer_isr (void){
    
    if(TMR1IF==1){
       
        RC5=1;
        RC4=0;
        __delay_ms(500);
        RC5=0;
        
        TMR1IF=0;        
        }
                
    }

    void main (void){
    TRISB0=1;  // INTERRUPT PIN, ECHO SENSER
    TRISB1=0;  //TRIGER PIN
    TRISC4=0;  //MOTER 2
    TRISC5=0;   //INTERRUPT LED MOTER 1
    T1CON=0X20;   // 1:4- PRES-SCALAR AND SET INTERNAL CLOCK
    RC4=0;
    RC5=0;
    
    TMR1IE=1; //Enable timer interrupt bit in PIE1 register
    GIE=1;   //GLOBAL INTERRUPT ENABLE BIT=1(ACCESS TO INTERRUPT)
    PEIE=1;  //PERIPERAL INTERRUPT ENABLE BIT=1(CONTROLL THE EXTERNAL DEVICES USING INTERRUPT)
    TMR1IF=0;   
    // T1SYNC=0;
   
    int time_taken;
    int distance;
    
    while(1){
  
        TMR1H = 0;   //CLEAR THE TIMER1 2 REGISTERS VALUES 
        TMR1L = 0;
               
        trigger = 1;
        __delay_ms(10);
        trigger = 0;
        
        
        while(echo==0);
             
        TMR1ON = 1;
        
        while(echo==1);
        
        TMR1ON = 0;
       //Echo pin will stay low till the wave return back
        
        time_taken = (TMR1L | (TMR1H<<8));  //resulting value will be saved in the registers TMR1H and TMR1L
        distance = (0.0272*time_taken)/2;
        
        
        time_taken = time_taken*0.8;  //in micro seconds
        
        
       if(distance<35 && 25<distance ){
           RC4=1;
           
       } 
       else{
           RC4=0;
       }
        
        
       if(distance<25 && 15<=distance){
           RC4=1;
           
       } 
       else{   
           RC4=0;

       }

       
       if(distance<=15){
           TMR1IF=1;     
       }              
    } 
           
    return;
    }

