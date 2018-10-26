#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 2, en = 3, d4 = 4, d5 = 5, d6 = 6, d7 = 7;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

#define alcohol A0
#define vib 8

void setup() {
  // put your setup code here, to run once:
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.setCursor(0,0);
  lcd.print(" ANTI-THEFT FOR");
  lcd.setCursor(0,1);
  lcd.print("    VEHICELS");
  delay(5000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Initializing...");
  delay(3000);
  Serial.begin(9600);
}

void loop() {
  // put your main code here, to run repeatedly:
  int vibval = digitalRead(8);
  int alcval = analogRead(A0);
  Serial.print("Alcohol Value: ");
  Serial.println(alcval);
  Serial.print("Vibration Value: ");
  Serial.println(vibval);
  if(alcval>=500)
  {
  lcd.clear();
  lcd.print("Driver is drunk!");
  Serial.println("Driver is drunk!");
  }
  else if(vibval == 0)
  {
  lcd.clear();
  lcd.print("    Accident");
  lcd.setCursor(0,1);
  lcd.print("    Detected!");
  Serial.println("Accident Detected!");
  }
  else
  {
  lcd.clear();
  lcd.print("Driver is sobar!");
  }
  delay(500);
    
}
