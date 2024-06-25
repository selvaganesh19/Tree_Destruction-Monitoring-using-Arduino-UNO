# destruction-monitoring-using-Arduino-UNO
// Transmitter Program

#include <SPI.h>

#include<LoRa.h>

#include<Wire.h>

#include<LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,16,2); // set theLCD address to 0x27 for a 16 chars and 2 line display

int led = 3;

String inString = ""; // stringto hold input

int val = 0;

void setup() {

Serial.begin(9600);

pinMode(led,OUTPUT);

lcd.init(); // initialize the lcd

lcd.init();

lcd.backlight();

lcd.setCursor(0,0);

lcd.print(" Lora ");

lcd.setCursor(0,1);

lcd.print(" Receiver ");

while (!Serial);

Serial.println("LoRaReceiver");

if (!LoRa.begin(433E6)) { // or 915E6

Serial.println("Starting LoRa failed!");

while (1);

}

}

void loop() {
int packetSize = LoRa.parsePacket();

if (packetSize) {

while(LoRa.available())

{

int inChar = LoRa.read();

inString+= (char)inChar;

}

Serial.println(inString);

StringmyString = inString;

String val1=getValue(myString, ':', 0);

String val2=getValue(myString, ':', 1);

String val3=getValue(myString, ':', 2);

if(val1.toInt()==LOW)

{

lcd.setCursor(0,0);

lcd.print(" object ");

lcd.setCursor(0,1);

lcd.print(" detected ");

digitalWrite(led,HIGH);

delay(1000);

digitalWrite(led,LOW);

}

elseif(val2.toInt()==LOW)

{

lcd.setCursor(0,0);

lcd.print(" Metal ");

lcd.setCursor(0,1);

lcd.print(" detected ");

digitalWrite(led,HIGH);

delay(1000);

digitalWrite(led,LOW);

}
elseif(val3.toInt()==LOW)

{

lcd.setCursor(0,0);

lcd.print(" sound ");

lcd.setCursor(0,1);

lcd.print(" detected ");

digitalWrite(led,HIGH);

delay(1000);

digitalWrite(led,LOW);

}

else

{

lcd.setCursor(0,0);

lcd.print(" Lora ");

lcd.setCursor(0,1);

lcd.print(" reaciever ");

delay(1000);

}

inString = "";

LoRa.packetRssi();

}

}

StringgetValue(Stringdata, char separator, int index)

{

int found = 0;

int strIndex[] = { 0, -1 };
intmaxIndex= data.length() - 1;

for (int i= 0; i<= maxIndex && found <= index; i++) {

if (data.charAt(i)== separator || i==maxIndex) {

found++;

strIndex[0] = strIndex[1] + 1;

strIndex[1] =(i ==maxIndex) ? i+1 : i;

}

}

returnfound> index? data.substring(strIndex[0], strIndex[1]) :"";

}
