# [Mini-MedicBot](https://minimedicbot002.netlify.app/)

![Untitled](https://github.com/user-attachments/assets/0e0a632a-67f5-443b-9633-eb24b81a8aaa)
**An open-source robotic assistant for medical applications**


## 🚀 About the Project
MedicBot is an open-source medical assistant robot designed to help with basic healthcare tasks. This project includes:

- **3D Printable Parts**: STL files for printing the robot's body.
- **Electronics & Assembly Guide**: Components list and assembly instructions.
- **Software & Code**: Python scripts to control the robot.

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

| Component          | Amazon US Price | Amazon EU Price |
|--------------------|----------------|----------------|
| Raspberry Pi 5    | $X.XX           | €X.XX          |
| 20KG Servo Motor  | $X.XX           | €X.XX          |
| Battery Pack      | $X.XX           | €X.XX          |
| PLA Filament      | $X.XX           | €X.XX          |
| Screws & Bolts    | $X.XX           | €X.XX          |

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

🔗 [GitHub Repository](https://github.com/moondream2/moondream)

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

## 📜 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🏥 Acknowledgments
Thanks to the open-source community for supporting robotics and medical innovation!

---
🔗 **Stay Connected**  
📧 Contact: your-email@example.com  
🌐 Website: [MedicBot Project](https://your-website.com)



