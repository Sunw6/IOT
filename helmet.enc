
#include "config.h"
#include <TinyGPS++.h>
#include <SoftwareSerial.h>
#include <ESP8266WiFi.h>

TinyGPSPlus  gps;              // The TinyGPS++ object
SoftwareSerial  ss(4, 5) ;   // The serial connection to the GPS device.

float lattitude , longitude;
String date_str , time_str , lat_str , lng_str;

#define alcoholpin A0
#define vibrationpin 0

int current = 0;
int last = -1;
bool current2 = false;
bool last2 = false;

AdafruitIO_Feed *vibration = io.feed("vibration");
AdafruitIO_Feed *alcohol = io.feed("alcohol");

int count = 0;
AdafruitIO_Feed *locatelat = io.feed("locatelat");
AdafruitIO_Feed *locatelng = io.feed("locatelng");
void setup() {
  Serial.begin(115200);
  ss.begin(9600);
  pinMode(alcoholpin, INPUT);
  pinMode(vibrationpin, INPUT);
  while(! Serial);
  Serial.print("Connecting to Adafruit IO");
  io.connect();
  while(io.status() < AIO_CONNECTED) {
    Serial.print(".");
    delay(500);
  }
  Serial.println();
  Serial.println(io.statusText());

}

void loop() {
        io.run();
        current = analogRead(alcoholpin);
        if(current == last)
        return;
        Serial.print("sending -> ");
        Serial.println(current);
        alcohol->save(current);
        last = current;
        if(digitalRead(vibrationpin) == LOW)
        current2 = true;
        else
        current2 = false;
        if(current2 == last2)
        return;
        Serial.print("sending button -> ");
        Serial.println(current2);
        vibration->save(current2);
        last2 = current2;
    while (ss.available() > 0)
    if ( gps.encode( ss.read() ))
    {
        if (gps.location.isValid())
      {
        lattitude = gps.location.lat();
        lat_str = String(lattitude , 6);
        longitude = gps.location.lng();
        lng_str = String(longitude , 6);
        io.run();
        current = analogRead(alcoholpin);
        if(current == last)
        return;
        Serial.print("sending -> ");
        Serial.println(current);
        alcohol->save(current);
        last = current;
        if(digitalRead(vibrationpin) == LOW)
        current2 = true;
        else
        current2 = false;
        if(current2 == last2)
        return;
        Serial.print("sending button -> ");
        Serial.println(current2);
        vibration->save(current2);
        last2 = current2;
        Serial.print("sending -> ");
        Serial.println(lat_str);
        locatelat->save(lat_str);
        Serial.print("sending -> ");
        Serial.println(lng_str);
        locatelng->save(lng_str);
        delay(3000);

    }
   }
}
