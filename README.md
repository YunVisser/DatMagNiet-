# DatMagNiet-


#include <Servo.h>

const int in = A0; //Pressure plate
const int ServPin = 9; //servo 
int triggerpoint = 130;

int minRead; //minimum read
int maxRead; //maximum read

Servo myservo;  // create servo object to control a servo
// twelve servo objects can be created on most boards

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  pinMode(in, INPUT);
  myservo.attach(ServPin);  // attaches the servo on pin 9 to the servo object

  minRead = analogRead(A0);
  maxRead = analogRead(A0);
}

void loop() {
  
  Serial.print(" minRead: ");
  Serial.print(minRead);
  Serial.print(" maxRead: ");
  Serial.print(maxRead);
  Serial.print(" triggerpoint= ");
  Serial.print(triggerpoint);
  Serial.print(" = ");
  Serial.println(analogRead(A0));

  if (analogRead(A0) < minRead) {
    minRead = analogRead(A0);
  }

  else if (analogRead(A0) > maxRead) {
    maxRead = analogRead(A0);
  }
  triggerpoint = ((maxRead - minRead) / 2) + minRead;

  delay(100); //100 mili sec.

  if (analogRead(A0) > triggerpoint) {
    sweep(200); //0,2sec voordat die verder sweept
  }
}

void sweep(int x) {
  myservo.write(10);
  delay(x);
  myservo.write(170);
  delay(x);
}
 
