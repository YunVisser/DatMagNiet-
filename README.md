# DatMagNiet-

//Code 1 meet minimale gewicht


#include <Servo.h> //library servo

const int out = 12;
const int in = A0;      //pressure plate
const int ServPin = 9; //servo
const int triggerpoint = 130; //als de druk meer dan 130 is gaat de servo bewegen

Servo myservo;  //create servo object to control a servo

void setup() {
  //here my setup code, to run once:
  Serial.begin(9600);
  pinMode(out, OUTPUT);
  pinMode(in, INPUT);
  myservo.attach(ServPin);  //attaches the servo on pin 9 to the servo object
}

void loop() {
  //here the main code, to run repeatedly:

  digitalWrite(out, LOW);
  delayMicroseconds(2);

  digitalWrite(out, HIGH);
  delayMicroseconds(10);
  digitalWrite(out, LOW);

  Serial.println(analogRead(A0)); //tekst van A0 uitprinten in de seriële monitor

  delay(100); //100 mili sec. wachten

  if (analogRead(A0) > triggerpoint) { //A0 groter is dan triggerpoint
    sweep(200); //0,2sec voordat die verder sweept
  }
}

//beweging van de servo
void sweep(int x) {
  myservo.write(10);
  delay(x);
  myservo.write(170);
  delay(x);
}
 
 
 //Code 2 meet gemiddelde gewicht 
 

#include <Servo.h> //library servo

const int in = A0; //pressure plate
const int ServPin = 9; //servo
int triggerpoint = 130; //als de druk meer dan 130 is gaat de servo bewegen

int minRead; //minimum read
int maxRead; //maximum read

Servo myservo;  //create servo object to control a servo

void setup() {
  //here my setup code, to run once:
  Serial.begin(9600);
  pinMode(in, INPUT);
  myservo.attach(ServPin);  //attaches the servo on pin 9 to the servo object

  minRead = analogRead(A0);
  maxRead = analogRead(A0);
}

void loop() {
  //here the main code, to run repeatedly:
  //tekst wat tussen de"" staan uitprinten in de seriële monitor
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

  delay(100); //100 mili sec.wachten

  if (analogRead(A0) > triggerpoint) { 
    sweep(200); //0,2sec voordat die verder sweept
  }
}

//beweging van de servo
void sweep(int x) {
  myservo.write(10);
  delay(x);
  myservo.write(170);
  delay(x);
}
