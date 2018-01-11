# musical

//define pines
const int trigPin = 9;
const int echoPin = 10;
const int buzzer = 2;
const int treshold = 13;
int redPin = 7;
int greenPin = 6;
int bluePin = 5;

#include "pitches.h"
long duration;
int redAmount;
int blueAmount;
int distance;
int note;
int notes[] = {
  //hungarian minor scale 
  NOTE_G2, NOTE_G3,  NOTE_A3,  NOTE_AS3, NOTE_D4,  NOTE_DS4, NOTE_FS4, NOTE_G4,  NOTE_A4,  NOTE_AS4, NOTE_D5,  NOTE_DS5, NOTE_FS5, NOTE_G5   
  
};
void setup() {
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
pinMode(buzzer, OUTPUT);
pinMode(redPin, OUTPUT);
pinMode(greenPin, OUTPUT);
pinMode(bluePin, OUTPUT);
Serial.begin(9600);


}
void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);
// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);
// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);
// Calculating the distance duration*0.034/2 (divide/2)
distance= duration*0.034/4;
redAmount= 130+distance*9;
blueAmount= 255-distance*19;
note= notes[distance];



   if(distance <=13){

    tone(buzzer, notes[distance]);
    delay(100);
    setColor(redAmount, 0, blueAmount);
    Serial.println(note);
  }
  else {
    noTone(buzzer);
    setColor(0, 0, 0);
  }
}

void setColor(int red, int green, int blue){
  #ifdef COMMON_ANODE
    red = 255 - red;
    green = 255 - green;
    blue = 255 - blue;

  #endif
  analogWrite(redPin, red);
  analogWrite(greenPin, green);
  analogWrite(bluePin, blue);
}
  
