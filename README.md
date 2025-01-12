# 1-Temperature Sensor and LED Indicator Project (Digital)

## Description

This project is a simple Arduino Uno temperature monitoring system. It uses the TMP36 temperature sensor to measure the ambient temperature and displays the result using three LED indicators (Green, Yellow, and Red) based on the temperature range.

- **Green LED**: Indicates moderate temperature (< 25°C).
- **Yellow LED**: Indicates high temperature (25°C to 35°C).
- **Red LED**: Indicates very high temperature (> 35°C).

The temperature readings are also displayed in the Serial Monitor for monitoring and debugging purposes.

### How It Works
1. The TMP36 temperature sensor sends an analog signal to pin A0.
2. The analog input is converted to Celsius using the `map()` function.
3. Based on the measured temperature:
   - If the temperature is below 25°C, the Green LED is turned ON.
   - If the temperature is between 25°C and 35°C, the Yellow LED is turned ON.
   - If the temperature is above 35°C, the Red LED is turned ON.
4. The temperature value is printed in the Serial Monitor.

### Components Required
1. **Arduino Uno**: Acts as the microcontroller.
2. **TMP36 Temperature Sensor**: Measures the ambient temperature (Analog Input).
3. **3 LEDs (Green, Yellow, Red)**: Visual indicators for different temperature ranges.
4. **Breadboard**: For connecting components.
5. **Resistors**: Current-limiting resistors for the LEDs.
6. **Jumper Wires**: For wiring connections.
7. **USB Cable**: To power the Arduino and upload the code.

### Signal Types
- **TMP36 Sensor**: Sends an analog signal to pin A0.
- **LEDs**: Controlled via digital pins 2, 3, and 4.

### Circuit Diagram
```
https://www.tinkercad.com/things/4g1i7yWBksM/editel
```

![Copy of TMP36 Temperature Sensor With Arduino (1)](https://github.com/user-attachments/assets/6b2d358b-abc0-439c-b6e6-115e5497c075)

![image](https://github.com/user-attachments/assets/774117dc-4ef8-4ead-ade5-10357c3e272d)

![image](https://github.com/user-attachments/assets/1e5d3c88-3292-48a0-bf28-07a4951e3bf8)


![image](https://github.com/user-attachments/assets/822fb09b-654b-4da5-901b-df3adbba936f)



### Setup Instructions
1. Connect the components as shown in the circuit diagram.
2. Open the Arduino IDE and paste the provided code below.
3. Select the correct board (Arduino Uno) and the COM port.
4. Upload the code to the Arduino.
5. Open the Serial Monitor (Ctrl+Shift+M) to view the temperature readings.
6. Observe the LEDs turning ON/OFF based on the temperature range.

### Code
```cpp
int celsius = 0;

void setup()
{
  pinMode(A0, INPUT);       // Temperature sensor input
  Serial.begin(9600);       // Initialize serial communication
  pinMode(2, OUTPUT);       // Green LED
  pinMode(3, OUTPUT);       // Yellow LED
  pinMode(4, OUTPUT);       // Red LED
}

void loop()
{
  // Read temperature from the sensor and convert to Celsius
  celsius = map(((analogRead(A0) - 20) * 3.04), 0, 1023, -40, 125);

  // Print temperature to the Serial Monitor
  Serial.print("Temperature: ");
  Serial.print(celsius);
  Serial.println(" °C");

  // Control LEDs based on temperature
  if (celsius < 25) { // Moderate temperature
    digitalWrite(2, HIGH); // Green LED ON
    digitalWrite(3, LOW);  // Yellow LED OFF
    digitalWrite(4, LOW);  // Red LED OFF
  } 
  else if (celsius >= 25 && celsius <= 35) { // Hot temperature
    digitalWrite(2, LOW);  // Green LED OFF
    digitalWrite(3, HIGH); // Yellow LED ON
    digitalWrite(4, LOW);  // Red LED OFF
  } 
  else if (celsius > 35) { // Very hot temperature
    digitalWrite(2, LOW);  // Green LED OFF
    digitalWrite(3, LOW);  // Yellow LED OFF
    digitalWrite(4, HIGH); // Red LED ON
  }

  delay(1000); // Wait for 1 second before the next reading
}
```

### Applications
- **Educational purposes**: Great for beginners to learn about temperature sensors and LED control with Arduino.
- **Temperature Monitoring**: Can be used as a simple temperature monitoring system.
- **Alarm Systems**: Can be further developed into a temperature-based warning or alarm system.

---

# 2-PIR Motion Sensor and LED Project (Analog)

## Description

This project uses an Arduino Uno with a PIR (Passive Infrared) Motion Sensor to detect motion. When the PIR sensor detects motion, the built-in LED on the Arduino board is turned ON, and a message is displayed in the Serial Monitor indicating motion detection.

### How It Works
1. The PIR sensor is connected to the Arduino via digital pin 2.
2. The Arduino reads the digital signal from the PIR sensor (either HIGH or LOW):
   - **HIGH**: Motion is detected.
   - **LOW**: No motion is detected.
3. When motion is detected:
   - The built-in LED is turned ON.
   - The message “Sensor activated!” is sent to the Serial Monitor.
4. If no motion is detected:
   - The built-in LED remains OFF.

### Components Required
1. **Arduino Uno**: Microcontroller for processing sensor data.
2. **PIR Motion Sensor**: Detects motion based on infrared heat signatures.
3. **Breadboard**: For connecting the components.
4. **Jumper Wires**: For wiring connections.
5. **USB Cable**: To power the Arduino and upload the code.

### Circuit Diagram
```
https://www.tinkercad.com/things/74cU53Y4xcj-pir-motion-sensor-digital-input/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard%2Fdesigns%2Fcircuits
```

![PIR Motion Sensor (Digital Input)](https://github.com/user-attachments/assets/20e1a224-0159-40fc-b600-7f6b83b7df1c)

![image](https://github.com/user-attachments/assets/4cfc1342-4847-4f2b-84ba-7bd5ad1a601d)

![image](https://github.com/user-attachments/assets/c407ec2c-fe4d-4fc9-b61e-78ae8c76fd20)

### Signal Types
- **PIR Sensor**: Sends a digital signal (HIGH/LOW) to digital pin 2.
- **Built-in LED**: Controlled via the digital output pin.

### Setup Instructions
1. Connect the components as shown in the circuit diagram.
2. Open the Arduino IDE and copy the code provided below.
3. Select the correct board (Arduino Uno) and COM port.
4. Upload the code to the Arduino board.
5. Open the Serial Monitor to observe motion detection messages.

### Code
```cpp
int sensorState = 0;

void setup()
{
  pinMode(2, INPUT);             // Set PIR sensor pin as input
  pinMode(LED_BUILTIN, OUTPUT);  // Set built-in LED pin as output
  Serial.begin(9600);            // Initialize Serial Monitor
}

void loop()
{
  // Read the state of the PIR sensor (digital input)
  sensorState = digitalRead(2);
  
  // Check if the sensor pin is HIGH (motion detected)
  if (sensorState == HIGH) {
    digitalWrite(LED_BUILTIN, HIGH); // Turn ON the built-in LED
    Serial.println("Sensor activated!"); // Print message to Serial Monitor
  } else {
    digitalWrite(LED_BUILTIN, LOW);  // Turn OFF the built-in LED
  }
  
  delay(10); // Short delay to improve performance
}
```

### Applications
- **Home Security Systems**: Detect motion for alarms or surveillance.
- **Automation**: Trigger lights or devices when motion is detected.
- **Energy Saving**: Turn devices ON/OFF based on room occupancy.

### Notes
- The PIR sensor has a slight delay after detecting motion; this is normal.
- Ensure the sensor is stable and not obstructed for accurate detection.

