# 🔵 Blind Navigation Hybrid AI System
### Real-time AI Guidance System for Visually Impaired Users

This project implements a **real-time blind navigation system** that detects walkable paths, obstacles, potholes, stairs, vehicles, and environmental hazards using a hybrid Computer Vision pipeline. It continuously guides visually impaired users via audio commands.

The system runs locally using a webcam and is optimized to work on mid-range hardware (e.g., **Core i5 6th Gen + 16GB RAM**).

**Example Audio Commands:**
> - “Move slightly left”
> - “Pothole ahead, stop!”
> - “Stairs detected”
> - “Walk forward safely”

---

## 🚀 Features

* **Hybrid Vision Pipeline:** Combines pretrained YOLOv8 with custom-trained classes for domain-specific objects (road, footpath, pothole, wet floor, stairs, bricks, obstacles, construction objects, signboards).
* **Depth Estimation:** Uses MiDaS / ZoeDepth for monocular distance estimation to warn users of proximity to obstacles.
* **Walkable-area Segmentation:** Highlights road/walkable areas to calculate the safest path.
* **GPS Navigation (Optional):** Accepts a destination and provides turn-by-turn guidance merged with camera-based obstacle avoidance.
* **Voice Interaction:**
    * **Input:** Speech-to-Text (Vosk/Whisper) for user commands.
    * **Output:** Text-to-Speech (pyttsx3/Coqui) for real-time guidance.
* **Logic Engine:** Merges object detections, depth data, and route info to produce timely, prioritized audio instructions.

---

## 📂 Project Structure

```text
blindnav_hybrid/
├── README.md
├── requirements.txt
├── .gitignore
├── setup.bat / setup.sh
├── LICENSE
├── data/
│   ├── raw/
│   ├── images/
│   │   ├── train/
│   │   └── val/
│   ├── labels/
│   │   ├── train/
│   │   └── val/
│   └── annotations/
├── models/
│   ├── pretrained/
│   └── custom/
├── src/
│   ├── __init__.py
│   ├── main.py
│   ├── config.py
│   ├── camera_stream.py
│   ├── object_detection.py
│   ├── custom_train.py
│   ├── depth_estimation.py
│   ├── segmentation.py
│   ├── gps_navigation.py
│   ├── speech_to_text.py
│   ├── text_to_speech.py
│   ├── logic_engine.py
│   ├── utils.py
│   └── viz.py
├── scripts/
│   ├── collect_images.py
│   ├── annotate_helper.py
│   └── convert_annotations.py
└── notebooks/





---

## 🧪 Installation & Setup (Windows)

1. Clone the repo:
```bash
git clone https://github.com/YOUR_USERNAME/Blind-Human-Navigation-Hybrid-AI-System.git
cd Blind-Human-Navigation-Hybrid-AI-System

## Setup Instructions

### 1. Create & Activate Virtual Environment

```bash
python -m venv .venv
# On Windows
.venv\Scripts\activate
# On Linux/Mac
source .venv/bin/activate

### 2. Upgrade pip & Install Dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt

### 3.(Optional) If on Linux/Mac, run setup script
bash setup.sh


### 4. Place Pretrained Weights
Make sure your pretrained weights are in the following folder structure:
models/pretrained/
  └── yolov8n.pt   (or other yolov8 weights)

## Train Custom Classes
### 1.Prepare YOLO-format dataset:
data/images/train/
data/images/val/
data/labels/train/
data/labels/val/

Each image must have a .txt label file (YOLO format):
<class_id> <x_center> <y_center> <width> <height> (normalized)

### 2.Create data.yaml with paths and class names. Example:
