# Hard-Arduino
## LCD
### Description
The goal of this project was to get a LCD to display text and then use a button and LCD to count the number of times the button has been pressed. 
### Code
```C++
// LCD code Engineering 2

int buttonpin = 12; //set pin for button to 12
int buttonstate = 0;
int previousbuttonstate = 0;
int counter = 0; 
#include <Wire.h>
#include <LiquidCrystal_I2C.h> 
LiquidCrystal_I2C lcd(0x3F,16,2);  // set the LCD address to 0x27 for a 16 chars and 2 line display.  
// If 0x27 doesn't work, try 0x3F.

void setup() {
  pinMode(buttonpin, INPUT); //set button as input
  lcd.init();
  lcd.backlight();
}

void loop() {
  lcd.setCursor(0, 0); //set the lcd cursor to first column and first row 
  lcd.print("My Name is Zachary"); //lcd displays "My Name is Zachary" on first line
  buttonstate = digitalRead(buttonpin); //read state of button
  lcd.setCursor(0, 1); //set cursor to column 1, row 2
  lcd.print("Button number : "); //lcd displays the button number
  if (buttonstate == HIGH && previousbuttonstate == LOW) { //if you press the button
    counter +=1; //counter goes up by 1
    lcd.print(counter); //lcd displays the counter value
  } 
  buttonstate = previousbuttonstate; //set the button to off after it is released
  delay(100); //delay so it doesn't count more than one value per press
}
```
### Wiring Diagram
<img src="lcdwiring.png" alt="lcdwiring" style="width:500px;">

### Reflection
I really enjoyed this project. It was the first time I had ever used a LCD display before and it was very cool. I did learn a few new thing about LCD's while doing this project. I need to remember to use set cursor otherwise none of the stuff you are trying to say will appear. I also need to remember to carefully examine were each wire goes, because with the back pack two wires go to anolog pin 4 and 5. I mixed this up a couple of times and the LCD did not work. Overall I liked this project. It was fun to write stuff on the display and the counter was pretty cool. 
## Photointerupter
### Description
Create a code that will turn on a light when an object is placed in between a photointerupter. Also count the number of times the photointerupter has triggered and print that number in the serial monitor. 
### Code
```C++
int Led = 8;
int photo = 2;
int val;
int photostate = 0;
volatile byte state = LOW;
int counter = 0; //variables

void setup() {
  pinMode(Led, OUTPUT); //set led as output
  pinMode(photo, INPUT_PULLUP);    //output/input pins
  Serial.begin(9600);           //links serial monitor
  attachInterrupt(digitalPinToInterrupt(photo), Read, CHANGE);   //interrupts photo pin, makes state unequal which turns LED on
}

void loop() {
  digitalWrite(Led, state);

  Serial.print(state);//Prints state and counter value
  Serial.print("   ");
  Serial.println(counter/2);
}

void Read() {
  state = !state; //Makes state unequal
  counter++;}
```
### Wiring Diagram
<img src="photointerupter.png" alt="photointerupter" style="width:500px;">

### Reflection
I really like the Photointerupter project. Using attach interupt to make sure that the photointerupter would always trigger exactly when something was placed in it was really cool.  
