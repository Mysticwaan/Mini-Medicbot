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
```
MedicBot/
├── stl_files/            # 3D model files for printing
├── software/             # Python scripts for controlling the robot
├── docs/                 # Additional documentation
├── hardware/             # Circuit diagrams and wiring
└── README.md             # This file
```

## 🛠️ Materials & Cost
Below is a cost estimation for the required materials from **Amazon US** and **Amazon EU**:

| Component               | Amazon US Price | Amazon EU Price |
|-------------------------|-----------------|-----------------|
| Raspberry Pi 5          | [$120.00](https://www.raspberrypi.com/products/raspberry-pi-5/) | [€120.00](https://www.raspberrypi.com/products/raspberry-pi-5/) |
| 20KG Servo Motor        | [$13.59](https://www.amazon.com/dp/B0DQGZDJW7) | [€15.00](https://www.amazon.de/dp/B0DQGZDJW7) |
| Battery Pack            | [$87.99](https://www.amazon.com/dp/B0BMLT6T9B) | [€80.00](https://www.amazon.de/dp/B0BMLT6T9B) |
| PLA Filament (1kg spool)| [$20.00](https://www.amazon.com/dp/B07MZBYN6F) | [€22.00](https://www.amazon.de/dp/B07MZBYN6F) |
| Screws & Bolts Set      | [$25.00](https://www.amazon.com/dp/B07F742WJ7) | [€27.00](https://www.amazon.de/dp/B07F742WJ7) |

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

## 🔌 Hardware Setup
1. Connect the Raspberry Pi 5 to the servos and sensors.
2. Wire according to the provided schematics in the `hardware/` folder.
3. Ensure all connections are secure before powering on.

## 💻 Running the Software
### Prerequisites
Ensure you have the following installed:
```sh
sudo apt update && sudo apt install python3 python3-pip
pip install gpiozero opencv-python numpy
```

### Running MedicBot
To start the robot, execute the following command:
```sh
python3 software/main.py
```

### Features
- Voice control (optional: add microphone support)
- Object detection using OpenCV
- Remote control via a web interface

## 🛠 Models Used

### 🎙️ Whisper (OpenAI) – Speech-to-Text

🔗 [GitHub Repository](https://github.com/openai/whisper)

**Why Whisper?**
- Best-in-class accuracy for real-time speech recognition
- Handles multiple languages and noisy environments

### 👁️ Moondream2 – Advanced Vision AI

🔗 [GitHub Repository](https://github.com/vikhyat/moondream)

**Why Moondream2?**
- Real-time object detection, segmentation, and VQA (Visual Question Answering)
- Capable of understanding complex visual scenes, answering queries about them
- Highly optimized for embedded AI applications like Raspberry Pi 5, ensuring superior speed and performance
- Uses transformer-based architecture to enhance contextual understanding in vision-based tasks

## 🎨 Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature-name`).
3. Commit your changes (`git commit -m 'Add feature'`).
4. Push to your branch (`git push origin feature-name`).
5. Open a Pull Request.

---



