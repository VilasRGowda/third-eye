# third-eye#include <SoftwareSerial.h>

SoftwareSerial mySerial(9, 10);// 9 Rx ,10 Tx which is GSM , GPS

 int distance, duration;

 int trigPin=6; // Connect the Trig Pin of the HC SR-04 at pin 8 of Arduino

 int echoPin=7; // Connect the Echo Pin of the HC SR-04 at pin 9 of Arduino

 int Buzzer=9; // Connect a Buzzer at pin 6 of Arduino

void setup() {

 Serial.begin(9600); // Baud rate for Serial Monitor

 mySerial.begin(9600);

 pinMode(trigPin, OUTPUT); // Trigger Pin should be assigned as an Output of the Arduino

 pinMode(echoPin, INPUT); // Echo Pin should be assigned as an Input to the Arduino

 pinMode(Buzzer, OUTPUT); // Buzzer to be used as an output of the Arduino

 Serial.println(" WELCOME TO THIRD EYE FOR BLINDS");

 digitalWrite(Buzzer, LOW);

}

void loop() {

 digitalWrite(trigPin, HIGH); // Transmitting Ultrasonic sound

 delayMicroseconds(10); // for 10 Microseconds

 digitalWrite(trigPin, LOW); // Stop transmitting

 digitalWrite(echoPin, HIGH); // Wait for the reflected Ultrasonic sound (Thus Echo)

 duration=pulseIn(echoPin, HIGH); // Calculating the total time taken by the sound wave to return

 distance=(duration/2)/29.1;// Distance = Total Time taken (To and Fro) * Speed of sound

 digitalWrite(Buzzer, LOW);

 /* Here the value of the speed of sound is taken as (1/29.1) = 0.03436 cm/s.
 
 * The Total time is consideredd to be the time taken from transmission of sound to the reception of 

sound.

 * Thus the time is divided by 2 as it travels the same distance twice (to and fro).

 */

 

 Serial.print(distance); // To show the distance of the obstacle on the serial monitor.

 Serial.println(" CM");

 delay(500);

 

/*Stick not i Hand*/

 /*Controlling the Buzzer*/

 if(distance < 10) // If the obstacle is at distance less than 10cms

{

 Serial.println("Abstacles is Their");

 digitalWrite(Buzzer, HIGH);

 delay(500);

 delay(500);

 } // The buzzer will beep at an interval of 500ms

}
