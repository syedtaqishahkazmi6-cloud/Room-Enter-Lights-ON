# Room-Enter-Lights-ON
This project implements a touchless light control system using an Ultrasonic sensor, an OLED display, and a Relay module. The system toggles a light (represented by the relay) ON or OFF whenever an object is detected within a specific range.
This project implements a touchless light control system using an Ultrasonic sensor, an OLED display, and a Relay module. The system toggles a light (represented by the relay) ON or OFF whenever an object is detected within a specific range.

## 🔗 Wokwi Simulation
You can view and run the simulation here:
[https://wokwi.com/projects/461731925906866177](https://wokwi.com/projects/461731925906866177)

## 🛠 Features
- **Touchless Control:** Uses ultrasonic waves to detect proximity.
- **Toggle Logic:** Prevents flickering; one detection turns it ON, the next detection turns it OFF.
- **Visual Feedback:** Real-time status updates on a 128x64 I2C OLED display.
- **Industrial Interface:** Relay output to control high-voltage appliances (simulated).

## 📟 Component Pinout

| Component | Pin Name | Arduino/MCU Pin |
| :--- | :--- | :--- |
| **Ultrasonic Sensor** | Trig | Pin 9 |
| **Ultrasonic Sensor** | Echo | Pin 10 |
| **Relay Module** | Signal | Pin 12 |
| **OLED Display** | SDA | A4 (or SDA) |
| **OLED Display** | SCL | A5 (or SCL) |
| **Power** | VCC | 5V |
| **Ground** | GND | GND |

## 📚 Required Libraries
To compile this project, ensure the following libraries are installed in your environment (Wokwi or Arduino IDE):
1. **Adafruit SSD1306** (Display Driver)
2. **Adafruit GFX Library** (Graphics Support)
3. **Adafruit BusIO** (I2C Communication)

## 🧠 Logic Explanation

### 1. Distance Calculation
The HC-SR04 sensor sends a pulse and measures the time it takes to return. This duration is converted into centimeters using the speed of sound formula:
`Distance = (Duration * 0.034) / 2`

### 2. State-Change Detection (Edge Triggering)
Instead of checking if an object **is** present, the code checks for the **moment** an object appears.
- If `objectPresent` is TRUE and `lastObjectPresent` was FALSE, the system knows a new object has just entered the detection zone.
- This prevents the relay from rapidly switching back and forth while an object remains in front of the sensor.

### 3. Toggle Mechanism
A boolean variable `relayState` is flipped (`!relayState`) every time a valid detection occurs.
- **ON:** Sets the Relay pin to HIGH and updates OLED to "Lights: ON".
- **OFF:** Sets the Relay pin to LOW and updates OLED to "Lights: OFF".

### 4. Software Debouncing
A `delay(500)` is implemented after each toggle to ignore minor sensor noise or rapid movements, ensuring a clean switch operation.

## 🚀 Setup Instructions
1. Open the [Wokwi project link](https://wokwi.com/projects/461731925906866177).
2. Ensure the `libraries.txt` file contains the three libraries mentioned above.
3. Click the **Start Simulation** button.
4. Click on the **Ultrasonic Sensor** in the simulation to adjust the distance slider. Move it below 20cm to trigger the relay.
"""

with open("README.md", "w") as f:
    f.write(readme_content)
