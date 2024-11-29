# IOT_lia

// Change made by both users
October 11th, 2024 

 

Brainstorming ideas: 

Light chase lane, light range depending on the strength of the outside light 

straight 

"A heater" depending on the temperature 

-------------------------------------------------

 

 

 

We chose to creat3 an LED circuit in which the intensity will be controlled by the strength of the outside ambient light. 

 
The LEDs will have a chase function (extra)


The LEDs will be lit at different intensities depending on that of the light. 
 

Materials: 


LEDs 
Esp32 
Power source 
Resistors 
3D circuit printed 
Raspberry Pi 


// Change by Samir
October 18th, 2024

We uploaded the schematic on another file of how the project is going to function.


// Change by Samir
Thursday, November 21st, 2024 

We have not managed to show 50% of our project implementation, not even close to doing so. 

We have a bit of our code, but the hardware is not yet ready and not done for demonstration.. 



// Change by Rayen
Saturday, November 23rd, 2024

//include libraries
#include <Arduino.h>
//define the pins 
#define LED_1  15
#define LED_2  16
#define LED_3  17
#define LED_4  18
#define LED_5  13
#define LED_6  27
#define LED_7  26
#define LED_8  25
const int photoR = 34; //i am not sure yet
int power = 200;
//Variables
int value;
int delay_on = 100;
int delay_off = 0;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  pinMode(LED_3, OUTPUT);
  pinMode(LED_4, OUTPUT);
  pinMode(LED_5, OUTPUT);
  pinMode(LED_6, OUTPUT);
  pinMode(LED_7, OUTPUT);
  pinMode(LED_8, OUTPUT);
  pinMode(photoR, INPUT);// setting photoresistor as an input for the voltage devider
}

void loop() {
  // put your main code here, to run repeatedly:
 mesureLight();
 chase();
 
}
/*I am going to use a 10k ohm resistor for the voltage drop, use it as a percentage of how strong the light should be
it will be something like (basically a map)
max_val = 255 //5v
min_val = 0// 0v
it will basically controll the strength of the leds so the more light the less resistance so more voltage.
less light would mean less voltage and the leds would be dim. 
and for fun I am throwing in the chase.




*/
void mesureLight(){

  value = analogRead(photoR);
  power = map(value, 0, 4095, 255, 0);// suposed to turn the value from the light sensor to how much power would be sent to the led
  Serial.println(value); //by testing the max value was 4095 and the lowest was 0
  Serial.println(power);
  
  delay(100);


}



void chase() {
  analogWrite(LED_1, power);
  delay(delay_on);
  analogWrite(LED_1, LOW);
  delay(delay_off);

  analogWrite(LED_2, power);
  delay(delay_on);
  analogWrite(LED_2, LOW);
  delay(delay_off);

  analogWrite(LED_3, power);
  delay(delay_on);
  analogWrite(LED_3, LOW);
  delay(delay_off);

  analogWrite(LED_4, power);
  delay(delay_on);
  analogWrite(LED_4, LOW);
  delay(delay_off);

  analogWrite(LED_5, power);
  delay(delay_on);
  analogWrite(LED_5, LOW);
  delay(delay_off);

  analogWrite(LED_6, power);
  delay(delay_on);
  analogWrite(LED_6, LOW);
  delay(delay_off);
  
  analogWrite(LED_7, power);
  delay(delay_on);
  analogWrite(LED_7, LOW);
  delay(delay_off);

  analogWrite(LED_8, power);
  delay(delay_on);
  analogWrite(LED_8, LOW);
  delay(delay_off);

}

**
The code was done on Arduino IDE and is functioning, but we have just to implement the MQTT and Historian Data (maybe). 
I might add a potentiamoter to controll the speed

**

------------------------------------------------------------------------------------------------------------------------------------
//change made 24-11-29 by Rayen

-------------------------------------------------------------------------------------------------------------------------------------

//include libraries
#include <Arduino.h>
//define the pins 
#define LED_1  15
#define LED_2  16
#define LED_3  17
#define LED_4  18
#define LED_5  13
#define LED_6  27
#define LED_7  26
#define LED_8  25
const int photoR = 34; // photoresistor
const int potR = 35; //potentiameter 
int power;
int speed;
//Variables
int value;
int value2;
int delay_off = 0;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  pinMode(LED_3, OUTPUT);
  pinMode(LED_4, OUTPUT);
  pinMode(LED_5, OUTPUT);
  pinMode(LED_6, OUTPUT);
  pinMode(LED_7, OUTPUT);
  pinMode(LED_8, OUTPUT);
  pinMode(photoR, INPUT);// setting photoresistor as an input for the voltage devider
  pinMode(potR, INPUT);// setting the potentiameter as an input for the voltage devider
  
}

void loop() {
  // put your main code here, to run repeatedly:
mesureSpeed();
mesureLight();
chase();
 
}
/*I am going to use a 10k ohm resistor for the voltage drop, use it as a percentage of how strong the light should be
it will be something like (basically a map)
max_val = 255 //5v
min_val = 0// 0v
it will basically controll the strength of the leds so the more light the less resistance so more voltage.
less light would mean less voltage and the leds would be dim. 
and for fun I am throwing in the chase.




*/
void mesureLight(){

  value = analogRead(photoR);
  power = map(value, 0, 4095, 255, 0);// suposed to turn the value from the light sensor to how much power would be sent to the led
  Serial.println(value); //by testing the max value was 4095 and the lowest was 0
  Serial.println(power);
  
  delay(100);


}
void mesureSpeed(){
  value2 = analogRead(potR);
  speed = map(value2, 0, 4095, 40, 1000);
  Serial.println(value2); //by testing the max value was 4095 and the lowest was 0
  Serial.println(speed);

  
}


void chase() {
  analogWrite(LED_1, power);
  delay(speed);
  analogWrite(LED_1, LOW);
  delay(delay_off);

  analogWrite(LED_2, power);
  delay(speed);
  analogWrite(LED_2, LOW);
  delay(delay_off);

  analogWrite(LED_3, power);
  delay(speed);
  analogWrite(LED_3, LOW);
  delay(delay_off);

  analogWrite(LED_4, power);
  delay(speed);
  analogWrite(LED_4, LOW);
  delay(delay_off);

  analogWrite(LED_5, power);
  delay(speed);
  analogWrite(LED_5, LOW);
  delay(delay_off);

  analogWrite(LED_6, power);
  delay(speed);
  analogWrite(LED_6, LOW);
  delay(delay_off);
  
  analogWrite(LED_7, power);
  delay(speed);
  analogWrite(LED_7, LOW);
  delay(delay_off);

  analogWrite(LED_8, power);
  delay(speed);
  analogWrite(LED_8, LOW);
  delay(delay_off);

}

**
I added a potentiometer to control the speed, which also affects the scan time. A benefit would be that it can be adjusted which leads to using less data.
Now, we are working on the python side of things. 

**
