# Arduino to Unity Input Module

An all-in-one script for Unity that captures input from Arduino 
and registers it as a device in the Unity Input System. 
This script is specifically designed to capture 2D values (x, y) 
and a digital input for the down-click or click-in of an Arduino 
connected joystick (z). This script also includes code to use for 
Arduino IDE in the comments.

## Arduino Configuration
*Elegoo Uno R3 with Analog Joystick Input connected and powered via USB

- GND  -> GND
- 5V   -> 5V
- VRx  -> A0
- VRy  -> A1
- SW   -> D2 

### Arduino IDE code that corresponds to the input capture of the Unity C# module:
```
int xAxisInput = A0;
int yAxisInput = A1;
int zClickInput = 2;

int xAxisValue;
int yAxisValue;
int zClickValue;

void setup() {
  Serial.begin(9600);
  pinMode(xAxisInput, INPUT);
  pinMode(yAxisInput, INPUT);
  pinMode(zClickInput, INPUT);

  // WAKE THE DIGITAL INPUT UP
  digitalWrite(zClickInput, HIGH);
}

void loop() {
  // READ X AND Y VALUES
  xAxisValue = analogRead(xAxisInput);
  yAxisValue = analogRead(yAxisInput);

  // READ DIGITAL INPUT Z-CLICK
  zClickValue = digitalRead(zClickInput);

  // FLIP CLICK VALUES AROUND SINCE WE HAD TO WAKE IT UP
  switch(zClickValue)
  {
    case 1:
      zClickValue = 0;
      break;
    case 0:
      zClickValue = 1;
      break;
  }

  //DEBUG - Used by Unity to get input
  Serial.println("x" + String(xAxisValue));
  Serial.println("y" + String(yAxisValue));
  Serial.println("z" + String(zClickValue));
  
  delay(50);
}
```

Good luck and have fun.
