
# FAN-SPEED-CONTROLLER-SYSTEM-USING-TEMPERATURE-SENSOR
# EXP 1(A) FAN SPEED CONTROLLER SYSTEM USING TEMPERATURE SENSOR

# Aim:
	To measure the Temperature using DHT11/DHT22/TMP36  sensor with Arduino UNO Board/ESP-32 using Tinker CAD.

# Hardware / Software Tools required:
	PC/ Laptop with Internet connection
    Tinker CAD tool (Online)
	Arduino UNO Board/ESP-32
	Temperature Sensor (DHT11/DHT22/TMP36)

# Circuit Diagram:



# Procedure // Modify the procedure based on your circuit

Step 1: Set Up the Tinkercad Environment
1.	Log in to Tinkercad: Open Tinkercad in your web browser and log in to your account.
2.	Create a New Circuit: In the Tinkercad dashboard, click on "Circuits" and then select "Create New Circuit."
Step 2: Add Components to the Circuit
1.	Arduino Uno: Drag an Arduino Uno board from the components panel onto the workspace.
2.	TMP36 Sensor: Search for the TMP36 sensor in the components panel and drag it into the workspace.
3.	Breadboard: Drag a small breadboard to the workspace to help with wiring connections.
4.	Resistor (Optional): A resistor may not be necessary for this simple setup, but you can include it for more accurate readings.
5.	Wires: Use wires to connect the components.

Step 3: Connect the TMP36 Sensor to the Arduino
1.	TMP36 Pins:
o	Vout (Middle Pin): Connect this to an analog input pin on the Arduino (e.g., A0).
o	GND (Right Pin): Connect this pin to the ground (GND) on the Arduino.
o	Vs (Left Pin): Connect this to the 5V pin on the Arduino.
2.	Breadboard Wiring:
o	TMP36 Vout (Middle Pin) to Arduino A0: Use a wire to connect the middle pin (Vout) of the TMP36 sensor to the A0 analog input pin on the Arduino.
o	TMP36 GND (Right Pin) to Breadboard GND Rail: Connect the GND pin of the TMP36 sensor to the ground rail of the breadboard.
o	TMP36 Vs (Left Pin) to Breadboard 5V Rail: Connect the Vs pin of the TMP36 sensor to the 5V rail of the breadboard.
o	Arduino GND to Breadboard GND Rail: Connect a wire from the Arduino GND pin to the ground rail on the breadboard.
o	Arduino 5V to Breadboard 5V Rail: Connect a wire from the Arduino 5V pin to the power rail on the breadboard.
Step 4: Write the Arduino Code
1.	Code Editor: Click on the "Code" button at the top of the Tinkercad workspace to open the code editor.
2.	Set the Coding Mode: Ensure the editor is in "Text" mode to write your code in C/C++.
3.	Enter the Code: Write the following code to read the temperature from the TMP36 sensor
Step 5: Simulate the Circuit
1.	Start Simulation: Click the "Start Simulation" button at the top of the workspace to run the circuit and code.
2.	Monitor Output: Open the serial monitor by clicking the "Serial Monitor" button to view the temperature readings in both Celsius and Fahrenheit.
Step 6: Troubleshoot and Refine
1.	Check Connections: Ensure that all connections are made correctly on the breadboard and the Arduino.
2.	Adjust Code: If needed, tweak the code to improve accuracy or change the format of the output.
Step 7: Save Your Work
1.	Stop Simulation: Click "Stop Simulation" to end the simulation.
2.	Save the Circuit: Click "Save" to keep your circuit design and code for future use.


# Program
```
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

float temp;
int tempPin = A1;
int relayPin = 8;

#define fan 9

void setup(){
    pinMode(fan, OUTPUT);
    pinMode(relayPin, OUTPUT);
  
    lcd.begin(16, 3);
  
    lcd.setCursor(1, 1);
    lcd.print("Group 8");
    delay(3000);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Aidil,Lia,Najiaa");
    delay(3000);
    lcd.clear();
    lcd.print("Lets Get Started");
    delay(2000);
    lcd.clear();
    lcd.print("TEMPERATURE FAN");
    delay(2000);
    lcd.clear();
  
}

void loop()
{
    lcd.setCursor(3,0);
  	lcd.print("Recording");
  lcd.setCursor(2, 1);
  lcd.print("Temperature..");
  delay(3000);
  lcd.clear();
  lcd.setCursor(0,2);
  temp = analogRead(tempPin);
  //temp = temp*0.48828125;
  float voltage = temp * 5.0;
 	voltage /= 1024.0; 
 
 	// print out the voltage
 	lcd.print(voltage); lcd.println(" volts");
 
 	// now print out the temperature
 	float temperatureC = (voltage - 0.5) * 100 ;  //converting from 10 mv per degree wit 500 mV offset
 	                                              //to degrees ((voltage - 500mV) times 100)
 	
  lcd.setCursor(0, 0);
  lcd.print("Temperature = ");
  lcd.setCursor(2,1);
  //lcd.print(temp);
  lcd.print(temperatureC); lcd.println(" degrees C");
  delay(3000);
  lcd.clear();
  
  if(temperatureC >= 20)
  {
  	poweronRelay();
    if(temperatureC >= 20 && temperatureC <= 25)
    {
      analogWrite(fan,51);
      digitalWrite(6, LOW);
      lcd.print("Fan Speed: 20% ");
      delay(2000);
      lcd.clear();
    }
    else if(temperatureC <= 35)
    {
      analogWrite(fan,102);
      digitalWrite(6, LOW);
      lcd.print("Fan Speed: 40% ");
      delay(2000);
      lcd.clear();
    }
    else if(temperatureC <= 40)
    {
      analogWrite(fan,153);
      digitalWrite(6, HIGH);
      lcd.print("Fan Speed: 60% ");
      delay(2000);
      lcd.clear();
    }
    else if(temperatureC <= 44)
    {
      analogWrite(fan,200);
      digitalWrite(6, HIGH);
      lcd.print("Fan Speed: 80% ");
      delay(2000);
      lcd.clear();
    }
    else if(temperatureC >= 45)
    {
      analogWrite(fan,255);
      digitalWrite(6, HIGH);
      lcd.print("Fan Speed: 100% ");
      delay(2000);
      lcd.clear();
    }
  }
  else if(temperatureC < 20)
  {
  	poweroffRelay();
  }
}

void poweronRelay()
  {
  	digitalWrite(relayPin, HIGH);
    digitalWrite(6, HIGH);
    lcd.print("Fan ON");
    delay(2000);
    lcd.clear();
  }

void poweroffRelay()
  {
  	digitalWrite(relayPin, LOW);
    digitalWrite(6, LOW);
  	analogWrite(fan,0);
    lcd.print("Fan OFF");
    delay(2000);
    lcd.clear();
  }
```


# output:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ab6433fe-1fa5-43a9-8cc1-355fdac1c964" />


# Result
Thus,the Temperature using DHT11/DHT22/TMP36 sensor with Arduino UNO Board/ESP-32 using Tinker CAD are verified.

