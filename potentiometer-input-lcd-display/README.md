# potentiometer-input-lcd-display
**Project description**\
Read in potentiometer dial into a number (0 to 1023), and display the number into a LCD.

**Info on LCD**  \
LCD 1602 using I2C, or I2C LCD. \
Refer to the schematics for wire connections.

Install library within Arduino IDE: “Tools” -> “Manage Libraries”, search “LiquidCrystal I2C”, select “LiquidCystal I2C by Frank de Brabander”. \
Code to display a 4-digit number:
```c
include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

int controlValue = 1024;

void setup() 
{
  lcd.init();
  lcd.backlight();
}

void loop()
{
  lcd.setCursor(0,0);
  lcd.print("    ");
  lcd.setCursor(0,0);
  lcd.print(controlValue);
}
```
Note: The “controlValue” is a number from 0 to 1023. `lcd.print(“    ”)` clears previous writing. Note: `lcd.setCursor(COL_INDEX, ROW_INDEX)` with both `COL_INDEX` and `ROW_INDEX` starts from 0. 
Following Peter Dalmaris “Tech Exploration Arduino Step by Step” -> Section 15 “The Liquid Crystal Display” -> “119 Connect LCD using the I2C adaptor”, [Udemy link].

**Info on Potentiometer input** \
Code to read in potentiometer:
```c
int controlValue = 1024;

void setup() 
{
  Serial.begin(9600);
}

void loop()
{
  controlValue = analogRead(A0);
  Serial.println(controlValue);
}
```

**Schematics**
![Schematics](schematics.png?raw=true)