<div align="center" style="text-align: center;">
   
  # [Mini-MedicBot!](https://minimedicbot002.netlify.app/)

<p> Super hackable, affordable, and end-to-end (sim2real, RL) 3D-printed open-source humanoid robot platform. Fully open-source, including hardware, SDK, and sim environments. </p>

![image](https://github.com/user-attachments/assets/7fab5267-df9c-4e16-ad23-c0da0a0384cc)


<p> This project is built by the open-source community and is currently work in progress. We welcome your feedback, issues, and pull requests in GitHub.  </p>

<h1>
   <span> · </span>
  <a href="https://minimedicbot002.netlify.app/">Website</a> 🌐 
  <span> · </span>
</h1>

**An open-source robotic assistant for medical applications**

![ezgif-232b073cbd34b8](https://github.com/user-attachments/assets/6ec9644c-9d96-4b5c-9522-d3b459a52956)

## 🚀 About the Project
MedicBot is an open-source medical assistant robot designed to help with basic healthcare tasks. This project includes:

- **3D Printable Parts**: STL files for printing the robot's body.
- **Electronics & Assembly Guide**: Components list and assembly instructions.
- **Software & Code**: Python scripts to control the robot.

![eb0b8d74-1961-49f5-9601-6d48183af9d5](https://github.com/user-attachments/assets/99015e0f-dce0-485c-9e24-71d833515dfd)

## 📁 Project Structure
MedicBot/
├── stl_files/ # 3D model files for printing
├── software/ # Python scripts for controlling the robot
├── docs/ # Additional documentation
├── hardware/ # Circuit diagrams and wiring
└── README.md # This file

## 🛠️ Materials & Cost
Below is a cost estimation for the required materials from **Amazon US** and **Amazon EU**:

| Component               | Amazon eu Price |
|-------------------------|-----------------|
| Raspberry Pi pico 2 W     | [£14.83](https://www.amazon.co.uk/Pre-soldered-Microcontroller-Raspberry-Dual-core-Dual-architecture/dp/B0DPNDVC54) |
| SG90 Servo Motors (x10) | [£12.29](https://www.amazon.co.uk/Helicopter-Airplane-Control-Compatible-Arduino/dp/B0FGJRQC5S) |
| Battery Supply            | [$20.99](https://www.amazon.co.uk/GeeekPi-Raspberry-Uninterruptible-Management-Expansion/dp/B09S5YKBXC) |
| 2PCS 1.28 inch LCD| [$8.99](https://www.amazon.co.uk/dp/B0DM569VDT?ref=ppx_yo2ov_dt_b_fed_asin_title) |
| PCA9685 microcontroller    | [$5.00](https://www.amazon.co.uk/DollaTek-PCA9685-Channel-12-bit-Driver/dp/B0BKZC1XWR) |

*(Prices are subject to change. Check your local store for updated values.)*

## 🖨️ 3D Printing Instructions
1. Download STL files from the `stl_files/` directory.
2. Use your preferred slicer software (e.g., Cura, PrusaSlicer).
3. Recommended settings:
   - Layer Height: **0.2mm**
   - Infill: **20-30%**
   - Supports: **As needed**
   - Material: **PLA/ABS**
4. Print and assemble according to the assembly guide.

---

## 🧩 Embedded Control System (Pico W + GC9A01A + PCA9685)

The **Mini-MedicBot embedded brain** runs on a **Raspberry Pi Pico W** that handles:
- **Servo control** via PCA9685 (I²C)
- **Facial display** on a GC9A01A TFT screen (SPI)
- **Wi-Fi interface** for web-based remote control

### ⚙️ Wiring Diagram

| **Device / Function** | **Pico Pin (GPIO)** | **Physical Pin #** | **Notes**                                   |
| --------------------- | ------------------- | ------------------ | ------------------------------------------- |
| **TFT VCC**           | **3V3 (OUT)**       | **Pin 36**         | **3.3V power only (⚠️ Do not use VBUS/5V)** |
| **TFT GND**           | **GND**             | **Pin 38**         | Common ground                               |
| **TFT SCL (Clock)**   | **GP18**            | **Pin 24**         | SPI0 Clock (SCK)                            |
| **TFT SDA (Data)**    | **GP19**            | **Pin 25**         | SPI0 MOSI                                   |
| **TFT DC**            | **GP12**            | **Pin 16**         | Data/Command select                         |
| **TFT CS**            | **GP13**            | **Pin 17**         | Chip Select                                 |
| **TFT RST**           | **GP14**            | **Pin 19**         | Reset pin                                   |
| **PCA9685 VCC**       | **3V3 (OUT)**       | **Pin 36**         | Logic power (shared with TFT)               |
| **PCA9685 V+**        | **External 5V**     | —                  | Servo power supply (⚡ separate 5V rail)     |
| **PCA9685 GND**       | **GND**             | **Pin 38**         | Shared ground with Pico + Servos            |
| **PCA9685 SDA**       | **GP0**             | **Pin 1**          | I²C SDA                                     |
| **PCA9685 SCL**       | **GP1**             | **Pin 2**          | I²C SCL                                     |
| **Servos (1–6)**      | **PCA9685 CH0–CH5** | —                  | Controlled via PCA9685 outputs              |

⚡ **Power Note:**
> Use a separate 5V 2A+ power source for servos.  
> All grounds (Pico, PCA9685, and servos) **must share common GND**.

---

### 💻 Combined Code Example

```cpp
#include <Adafruit_GFX.h>
#include <Adafruit_GC9A01A.h>
#include <Adafruit_PWMServoDriver.h>
#include <SPI.h>
#include <Wire.h>
#include <WiFi.h>
#include <math.h>

// ---------- TFT SPI ----------
#define TFT_CS   13
#define TFT_DC   12
#define TFT_RST  14
Adafruit_GC9A01A tft(&SPI, TFT_DC, TFT_CS, TFT_RST);

// ---------- PCA9685 I2C ----------
const int I2C_SDA = 0;
const int I2C_SCL = 1;
Adafruit_PWMServoDriver pwm(0x40);

// ---------- Wi-Fi ----------
const char* ssid = "YourSSID";
const char* password = "YourPassword";
WiFiServer server(80);

// Servo setup
const uint8_t SERVO_CH[6] = {0, 1, 2, 3, 4, 5};
const int PULSE_MIN = 900, PULSE_CENTER = 1500, PULSE_MAX = 2100;

// ---------- Helper Functions ----------
inline int angleToUs(int angle, int minUs = PULSE_MIN, int maxUs = PULSE_MAX) {
  angle = constrain(angle, 0, 180);
  return map(angle, 0, 180, minUs, maxUs);
}
inline void setAngle(uint8_t ch, int angle) {
  pwm.writeMicroseconds(ch, angleToUs(angle));
}

// Draw smile (arc)
void drawSmile(int cx, int cy, int rx, int ry, int startAngle, int endAngle) {
  for (int angle = startAngle; angle <= endAngle; angle++) {
    float rad = angle * 3.14159 / 180;
    int x = cx + cos(rad) * rx;
    int y = cy + sin(rad) * ry;
    tft.fillCircle(x, y, 2, GC9A01A_BLACK);
  }
}

// Draw various faces
void drawFace(int faceId) {
  tft.fillScreen(GC9A01A_YELLOW);
  tft.drawCircle(120, 120, 100, GC9A01A_BLACK);
  int eyeY = 90;
  int eyeXOffset = 35;
  switch (faceId) {
    case 0: tft.fillCircle(85, eyeY, 15, GC9A01A_BLACK); tft.fillCircle(155, eyeY, 15, GC9A01A_BLACK); drawSmile(120,140,60,40,200,340); break;
    case 1: tft.fillCircle(85, 90, 15, GC9A01A_BLACK); tft.fillCircle(155, 90, 15, GC9A01A_BLACK); drawSmile(120,200,60,40,20,160); break;
    case 2: tft.fillCircle(85, 90, 15, GC9A01A_BLACK); tft.fillCircle(155, 90, 15, GC9A01A_BLACK); tft.fillCircle(120, 160, 20, GC9A01A_BLACK); break;
  }
}

// ---------- Setup ----------
void setup() {
  Serial.begin(115200);
  tft.begin();
  Wire.setSDA(I2C_SDA);
  Wire.setSCL(I2C_SCL);
  Wire.begin();
  pwm.begin();
  pwm.setOscillatorFrequency(27000000);
  pwm.setPWMFreq(50);
  for (uint8_t i = 0; i < 6; i++) setAngle(SERVO_CH[i], 90);

  WiFi.begin(ssid, password);
  Serial.print("Connecting to WiFi");
  while (WiFi.status() != WL_CONNECTED) { delay(500); Serial.print("."); }
  Serial.println("\nConnected! IP: " + WiFi.localIP().toString());
  server.begin();
}

// ---------- Loop ----------
void loop() {
  static unsigned long lastFace = 0;
  static int faceId = 0;
  if (millis() - lastFace > 2000) {
    drawFace(faceId++);
    if (faceId >= 3) faceId = 0;
    lastFace = millis();
  }

  WiFiClient client = server.accept();
  if (!client) return;
  while (client.connected() && !client.available()) delay(1);
  String request = client.readStringUntil('\r'); client.flush();

  int chPos = request.indexOf("ch=");
  int anglePos = request.indexOf("angle=");
  if (chPos > 0 && anglePos > 0) {
    int ch = request.substring(chPos + 3, request.indexOf('&', chPos)).toInt();
    int angle = request.substring(anglePos + 6, request.indexOf(' ', anglePos)).toInt();
    if (ch >= 0 && ch < 6) setAngle(SERVO_CH[ch], angle);
    Serial.printf("Servo %d → %d°\n", ch, angle);
  }
}
```
💡 Result

✅ GC9A01A TFT displays animated facial expressions.
✅ PCA9685 + Wi-Fi enables 6-channel servo web control.
✅ Ideal for Mini-MedicBot head control module or interactive emotion display.

💻 Running the Software
Prerequisites
sudo apt update && sudo apt install python3 python3-pip
pip install gpiozero opencv-python numpy
To start the robot:
python3 software/main.py
