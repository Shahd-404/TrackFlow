# 🚗 SMART TMC – Smart Vehicle Detection & Excel Reporting System

**SMART TMC** is a Python-based system that detects, tracks, and counts vehicles in traffic surveillance videos. It captures snapshots of vehicles as they cross virtual counting lines, classifies them using YOLOv8, and generates structured Excel reports with timestamps, images, and vehicle types.

Optimized for Google Colab, TrackFlow balances speed and accuracy — processing 1 hour of video in approximately 17 minutes.

---

##  Features

-  Detect vehicles in video using background subtraction
-  Track each object across frames with position and speed awareness
-  Count vehicles when they cross predefined lines
-  Automatically capture and crop vehicle images
-  Log timestamps of each vehicle pass
-  Classify vehicle types using **YOLOv8** (on final snapshots only)
-  Export organized Excel reports per 15-minute intervals and direction
-  OCR-based time and site code detection (with manual fallback)

---

##  How It Works

###  Step 1: Load and Analyze Video
- Video is downloaded from **Google Drive** using its file ID
- First frame is analyzed with OCR to extract:
  - Start time (e.g. 06:00:00)
  - Site code (e.g. ATC,52)

###  Step 2: Define Counting Lines
User provides:
- Y position of the line
- X endpoint for left lane
- X start point for right lane

###  Step 3: Process Video (No YOLO yet)
- Each frame is processed using **background subtraction**
- Moving objects (vehicles) are tracked and monitored
- If a vehicle crosses the line:
  - It is counted
  - Its image is cropped and saved
  - Timestamp is recorded

 This keeps performance fast without running YOLO on every frame

###  Step 4: Classify Vehicles (YOLOv8)
- Once all vehicles are detected and saved:
- Each image is classified using YOLOv8 (`yolov8m.pt` or `yolov8x.pt`)
- Detected class (Car, Bus, Truck, etc.) is saved to the Excel report

---

##  Output Structure


---

###  Example Excel Report

#### 📋 Sheet: `Left Detections`

| Timestamp | Detected Car Image                                 | Vehicle Type |
|-----------|----------------------------------------------------|--------------|
| 06:00:12  | ![Car 1](image%20%282%29.png)                       | Car          |
| 06:01:05  | ![Car 2](image%20%283%29.png)                       | Truck        |



#### Sheet: `Summary`

| Vehicle Type | Count |
|--------------|-------|
| Car          | 15    |
| Bus          | 3     |
| Truck        | 5     |

---

##  Performance

- ⏱ Processes 1 hour of video in ~17 minutes on Google Colab (GPU)
- Designed for high-efficiency by skipping frames and delaying YOLO calls

---

##  Tech Stack

- **Python**
- **YOLOv8** (`ultralytics`)
- **OpenCV** – image processing and video handling
- **Pytesseract** – OCR from video frame
- **OpenPyXL** – writing to Excel with embedded images
- **Matplotlib / NumPy** – visualizations and calculations

---

##  Installation

```bash
pip install opencv-python pytesseract ultralytics gdown openpyxl matplotlib numpy

## ▶️ Run on Google Colab

You can run this project directly on **Google Colab** without installing anything locally.

Click the badge below to open the notebook:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/16SrBK8AKWLXT1M55E2kWUkyuqdBwnV9z?usp=sharing)

> Make sure to provide the Google Drive video ID when prompted, and follow the instructions in the notebook to start processing.






