# potentiometer-input-lcd-display
**Q: LCD info?**  
LCD 1602 using I2C, or I2C LCD. Wire connections:

<center>
<table>
<tr>
  <th>Arduino</th>
  <th>I2C LCD</th>
</tr>
<tr>
  <td>5V</td>
  <td>VCC</td>
</tr>
<tr>
  <td>GND</td>
  <td>GND</td>
</tr>
<tr>
  <td>A4</td>
  <td>SDA</td>
</tr>
<tr>
  <td>A5</td>
  <td>SCL</td>
</tr>
</table>
</center>

<center><small>
Table: Arduino - I2C LCD connection.
</small></center>

Install library within Arduino IDE: “Tools” -> “Manage Libraries”, search “LiquidCrystal I2C”, select “LiquidCystal I2C by Frank de Brabander”. Code to display a 4-digit number:
```
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

**Q: Potentiometer input?** 
Wire connection
<center>
<table>
<tr>
  <th>Arduino</th>
  <th>Potentiometer</th>
</tr>
<tr>
  <td>5V</td>
  <td>left pin</td>
</tr>
<tr>
  <td>A0</td>
  <td>middle pin</td>
</tr>
<tr>
  <td>GND</td>
  <td>right pin</td>
</tr>
</table>
</center>

<center><small>
Table: Arduino - potentiometer connection. The left, middle, right pins of the potentiometer are when the spin button is facing.
</small></center>

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