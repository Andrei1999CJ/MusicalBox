# MusicalBox

This repository contains the Musical Box project written in 2 programming languages. One is written in Assembly and the other one is written in C (written at register level).

Musical Box is an embedded project made by me on the 3rd year in the University.
Below are the requirements for the project:
- system should be able to sing a song with at least 5 musical notes
- system should be able to detect the distance to an object
- system should start the song when the it detetcts an object very close to him
- system should be able to indicate in which is state it is(object detected & song is started / no object detected)


Hardware components
- PIC18F4550 uC
- an ultrasonic sensor(hc-sr04) used for distance detection
- a buzzer to convert the electrical signal to sound
- a transistor used to amplify the signal for the buzzer a bit
- a diode used for protection for the transistor
- a RGB led (common catode) used to indicate the states of the system
- a resistor used to control the current that enters the transistor
- 2 resistors that controls the current that enters the RGB led (one for the red color the other one for the green color)

Hardware Diagram

![image](https://github.com/Andrei1999CJ/MusicalBox/assets/86969370/962737fb-d013-4912-abb4-256decf8f0bb)


Software Requirements

In order to sing a song using the buzzer we need to generate this kind of signal but with different frequencies

![image](https://github.com/Andrei1999CJ/MusicalBox/assets/86969370/877865bc-a26b-43d4-98b7-2f2043ee15f5)

This can be achieved by generating a pwm signal with 50% duty cycle using the uC. The pwm signals for the musical notes will not be generated using the CCP module of the uC.

The musical notes of the song are(rounded):

C4 - frequency - 261 [Hz]

F4 - frequency - 349 [Hz]

E4 - frequency - 329 [Hz]

D4 - frequency - 293 [Hz]

B4 - frequency - 493 [Hz]

A4 - frequency - 440 [Hz]

G4 - frequency - 392 [Hz] 

The song is : C F E C D E F C C B A F G G F

The RGB led will be controlled using the CCP module of the controller(module that generates pwm signals). For led controlling we are using 2 complementary pins of the CCP module(when a pin is 1L the other one is 0L).

When an object is detected => start song => RC2 - pwm 0% duty cycle(0L) => RD5 pin - pwm 100% duty cycle(1L) - led is red.

When an object is not detected => song is not started => RC2 - pwm 100% duty cycle(1L) => RD5 pin - pwm 0% duty cycle(0L) - led is green.


In order to detect an object I used HC-SR04 Ultrasonic sensor

![image](https://github.com/Andrei1999CJ/MusicalBox/assets/86969370/13dafa1a-a480-4f03-9026-03e453481544)


When TRIG PIN is 1L for at least 10 us => the sensor transmits a 40 [Khz] frequency signal

The sensor receives the reflected signal after the collision with an object.

ECHO pin will stay in 1L for how long it tooked the signal to return to the sensor.

In order to calculate the distance to an object we use this formula: distance = (speed * time) / 2

speed = speed of sound in air = 340m/s = 0.0034 cm/us

If we detect an object below 5 cm => song starts













