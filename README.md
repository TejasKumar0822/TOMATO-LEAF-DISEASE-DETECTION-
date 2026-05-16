# TOMATO-LEAF-DISEASE-DETECTION-
# 🍅 Infield Disease Detection and Farming Treatment Recommendation System for Tomato Plants

> A deep learning-based real-time tomato leaf disease detection system built for Indian agricultural field conditions, using YOLO object detection models with a web-based farmer interface.

**B.Tech Capstone Project** | Department of AI & Data Science  
GITAM School of CSE, GITAM (Deemed to be University), Bengaluru — 2026

**Team:**
| Name | Registration No. |
|------|-----------------|
| D. Harshitha Chowdary | BU22CSEN0300406 |
| G. Tejas Kumar | BU22CSEN0300243 |
| M. Jahnavi | BU22CSEN0300202 |
| G. Mani Varshith | BU22CSEN0300360 |

**Guide:** Dr. N. Shobha Rani, Associate Professor

---

## 📌 Project Overview

Tomato crops in India are highly vulnerable to fungal, bacterial, and viral leaf diseases. Traditional manual inspection by farmers is time-consuming, inaccurate, and impractical at scale. This project develops an automated, real-time disease detection system using state-of-the-art YOLO object detection models trained on **real in-field tomato images** captured directly on Indian farms.

The system detects diseased regions in a leaf image, draws bounding boxes with disease class labels and confidence scores, and recommends actionable treatment — all through a simple web interface accessible to farmers.

---

## 🦠 Detectable Disease Classes

- Early Blight
- Late Blight
- Leaf Curl
- Leaf Miner
- Leaf Miner Egg
- Septoria Leaf Spot
- Spider Mite
- Pest Damage
- Healthy

---

## 🧠 Models Compared

| Model | Role |
|-------|------|
| YOLOv5 | Baseline object detector |
| YOLOv8s | Enhanced architecture (best performing) |
| YOLOv8n | Lightweight variant |
| YOLOv10 | Latest architectural improvements |
| EfficientNetB0 | CNN-based classification baseline |
| EfficientNetB4 | Deeper CNN classifier |

All models were trained and evaluated on the **same real-field dataset** under identical conditions for a fair comparison.

---

## 📊 Results Summary

| Metric | Value |
|--------|-------|
| Final Precision | 85.61% |
| Final Recall | 84.21% |
| mAP@0.5 | 85.96% |
| mAP@0.50–0.95 | ~80.47% |
| Confusion Matrix Accuracy | 86.01% |
| Inference Speed | ~9.8 ms/image (Tesla T4 GPU) |

**Best Model:** YOLOv8s — highest mAP with balanced precision-recall and consistent real-time inference.

---

## 🏗️ System Architecture

```
Input Image (Upload via Web / Smartphone)
        │
        ▼
  Data Acquisition Layer
  (Real field photos → Roboflow annotation → YOLO format dataset)
        │
        ▼
  Model Training Layer
  (Google Colab GPU | YOLOv5 / YOLOv8s / YOLOv8n / YOLOv10 / EfficientNet)
        │
        ▼
  Inference & Backend Layer
  (Flask/FastAPI REST API → Load best .pt weights → Run YOLO inference → NMS)
        │
        ▼
  Web Interface Layer
  (Upload image → Display bounding boxes + class label + confidence + treatment)
```

---

## 🗂️ Dataset

- Images were **captured directly on tomato farms** in India using smartphone cameras
- Contains real-world challenges: complex backgrounds, overlapping leaves, varied lighting, multiple disease instances per frame
- Annotated using **Roboflow** with bounding boxes and multi-class disease labels
- Exported in YOLO format (image files + normalized bounding box label files)
- Split into training, validation, and test sets

---

## ⚙️ Technology Stack

| Layer | Tools / Frameworks |
|-------|--------------------|
| Model Training | Python, PyTorch, YOLOv5, YOLOv8, YOLOv10, EfficientNet |
| Training Environment | Google Colab (GPU: Tesla T4) |
| Dataset Annotation | Roboflow |
| Backend | Flask / FastAPI |
| Frontend | HTML, CSS, JavaScript |
| Analysis & Visualization | Python, Matplotlib |
| Version Control | GitHub |

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/tomato-disease-detection.git
cd tomato-disease-detection
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Download Model Weights

> ⚠️ **Model weight files (.pt) are too large to include in this repository.**  
> Download the trained YOLOv8s weights and place them in the `models/` directory.

```
📁 models/
   └── best.pt   ← place downloaded weights here
```

> 🔗 **[Download trained model weights](#)**  *(replace `#` with your Google Drive / HuggingFace link)*

To retrain from scratch instead:

```bash
# YOLOv8 (Ultralytics)
yolo task=detect mode=train model=yolov8s.pt data=dataset.yaml epochs=100 imgsz=640

# YOLOv5
python train.py --img 640 --batch 16 --epochs 100 --data dataset.yaml --weights yolov5s.pt
```

### 4. Run the Web Application

```bash
python app.py
```

Open `http://localhost:5000` in your browser, upload a tomato leaf image, and get instant disease predictions with treatment recommendations.

---

## 📦 Requirements

```
torch
torchvision
ultralytics
opencv-python
flask
numpy
matplotlib
Pillow
requests
```

---

## 📁 Project Structure

```
├── app.py                  # Flask web application
├── models/
│   └── best.pt             # Trained YOLOv8s weights (download separately)
├── templates/
│   └── index.html          # Frontend UI
├── static/
│   ├── style.css
│   └── script.js
├── dataset/
│   ├── images/
│   ├── labels/
│   └── dataset.yaml
├── train/
│   └── train.py            # Training scripts
├── requirements.txt
└── README.md
```

---

## 💻 Hardware Requirements

| Mode | Minimum | Recommended |
|------|---------|-------------|
| Training | 8 GB RAM + GPU (6 GB VRAM) | Google Colab Pro / Tesla T4 |
| Inference (CPU) | 8 GB RAM | 16 GB RAM |
| Inference (GPU) | 4 GB VRAM | 6+ GB VRAM |

> Training was performed on **Google Colab** with a **Tesla T4 GPU (14,913 MiB)**.

---

## 🌱 Sustainable Development Goals

This project contributes to:

| SDG | Goal |
|-----|------|
| SDG 2 | Zero Hunger — supports food security through early crop disease detection |
| SDG 9 | Industry, Innovation and Infrastructure — applies AI to agriculture |
| SDG 12 | Responsible Consumption — reduces unnecessary pesticide usage |
| SDG 15 | Life on Land — promotes sustainable farming and biodiversity |

---

## 🔭 Future Work

- Expand dataset to cover more disease types, growth stages, and diverse Indian climate zones
- Integrate a **treatment recommendation module** with region-specific agronomic advice
- Optimize models via pruning and quantization for **mobile / edge deployment**
- Build a **mobile app** for offline use in rural areas with limited connectivity
- Explore automated hyperparameter tuning and neural architecture search

---

# 🍅 Infield Disease Detection and Farming Treatment Recommendation System for Tomato Plants

> A deep learning-based real-time tomato leaf disease detection system built for Indian agricultural field conditions, using YOLO object detection models with a web-based farmer interface.

**B.Tech Capstone Project** | Department of AI & Data Science  
GITAM School of CSE, GITAM (Deemed to be University), Bengaluru — 2026

**Team:**
| Name | Registration No. |
|------|-----------------|
| D. Harshitha Chowdary | BU22CSEN0300406 |
| G. Tejas Kumar | BU22CSEN0300243 |
| M. Jahnavi | BU22CSEN0300202 |
| G. Mani Varshith | BU22CSEN0300360 |

**Guide:** Dr. N. Shobha Rani, Associate Professor

---

## 📌 Project Overview

Tomato crops in India are highly vulnerable to fungal, bacterial, and viral leaf diseases. Traditional manual inspection by farmers is time-consuming, inaccurate, and impractical at scale. This project develops an automated, real-time disease detection system using state-of-the-art YOLO object detection models trained on **real in-field tomato images** captured directly on Indian farms.

The system detects diseased regions in a leaf image, draws bounding boxes with disease class labels and confidence scores, and recommends actionable treatment — all through a simple web interface accessible to farmers.

---

## 🦠 Detectable Disease Classes

- Early Blight
- Late Blight
- Leaf Curl
- Leaf Miner
- Leaf Miner Egg
- Septoria Leaf Spot
- Spider Mite
- Pest Damage
- Healthy

---

## 🧠 Models Compared

| Model | Role |
|-------|------|
| YOLOv5 | Baseline object detector |
| YOLOv8s | Enhanced architecture (best performing) |
| YOLOv8n | Lightweight variant |
| YOLOv10 | Latest architectural improvements |
| EfficientNetB0 | CNN-based classification baseline |
| EfficientNetB4 | Deeper CNN classifier |

All models were trained and evaluated on the **same real-field dataset** under identical conditions for a fair comparison.

---

## 📊 Results Summary

| Metric | Value |
|--------|-------|
| Final Precision | 85.61% |
| Final Recall | 84.21% |
| mAP@0.5 | 85.96% |
| mAP@0.50–0.95 | ~80.47% |
| Confusion Matrix Accuracy | 86.01% |
| Inference Speed | ~9.8 ms/image (Tesla T4 GPU) |

**Best Model:** YOLOv8s — highest mAP with balanced precision-recall and consistent real-time inference.

---

## 🏗️ System Architecture

```
Input Image (Upload via Web / Smartphone)
        │
        ▼
  Data Acquisition Layer
  (Real field photos → Roboflow annotation → YOLO format dataset)
        │
        ▼
  Model Training Layer
  (Google Colab GPU | YOLOv5 / YOLOv8s / YOLOv8n / YOLOv10 / EfficientNet)
        │
        ▼
  Inference & Backend Layer
  (Flask/FastAPI REST API → Load best .pt weights → Run YOLO inference → NMS)
        │
        ▼
  Web Interface Layer
  (Upload image → Display bounding boxes + class label + confidence + treatment)
```

---

## 🗂️ Dataset

- Images were **captured directly on tomato farms** in India using smartphone cameras
- Contains real-world challenges: complex backgrounds, overlapping leaves, varied lighting, multiple disease instances per frame
- Annotated using **Roboflow** with bounding boxes and multi-class disease labels
- Exported in YOLO format (image files + normalized bounding box label files)
- Split into training, validation, and test sets

---

## ⚙️ Technology Stack

| Layer | Tools / Frameworks |
|-------|--------------------|
| Model Training | Python, PyTorch, YOLOv5, YOLOv8, YOLOv10, EfficientNet |
| Training Environment | Google Colab (GPU: Tesla T4) |
| Dataset Annotation | Roboflow |
| Backend | Flask / FastAPI |
| Frontend | HTML, CSS, JavaScript |
| Analysis & Visualization | Python, Matplotlib |
| Version Control | GitHub |

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/tomato-disease-detection.git
cd tomato-disease-detection
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Download Model Weights

> ⚠️ **Model weight files (.pt) are too large to include in this repository.**  
> Download the trained YOLOv8s weights and place them in the `models/` directory.

```
📁 models/
   └── best.pt   ← place downloaded weights here
```

> 🔗 **[Download trained model weights](#)**  *(replace `#` with your Google Drive / HuggingFace link)*

To retrain from scratch instead:

```bash
# YOLOv8 (Ultralytics)
yolo task=detect mode=train model=yolov8s.pt data=dataset.yaml epochs=100 imgsz=640

# YOLOv5
python train.py --img 640 --batch 16 --epochs 100 --data dataset.yaml --weights yolov5s.pt
```

### 4. Run the Web Application

```bash
python app.py
```

Open `http://localhost:5000` in your browser, upload a tomato leaf image, and get instant disease predictions with treatment recommendations.

---

## 📦 Requirements

```
torch
torchvision
ultralytics
opencv-python
flask
numpy
matplotlib
Pillow
requests
```

---

## 📁 Project Structure

```
├── app.py                  # Flask web application
├── models/
│   └── best.pt             # Trained YOLOv8s weights (download separately)
├── templates/
│   └── index.html          # Frontend UI
├── static/
│   ├── style.css
│   └── script.js
├── dataset/
│   ├── images/
│   ├── labels/
│   └── dataset.yaml
├── train/
│   └── train.py            # Training scripts
├── requirements.txt
└── README.md
```

---

## 💻 Hardware Requirements

| Mode | Minimum | Recommended |
|------|---------|-------------|
| Training | 8 GB RAM + GPU (6 GB VRAM) | Google Colab Pro / Tesla T4 |
| Inference (CPU) | 8 GB RAM | 16 GB RAM |
| Inference (GPU) | 4 GB VRAM | 6+ GB VRAM |

> Training was performed on **Google Colab** with a **Tesla T4 GPU (14,913 MiB)**.

---

## 🌱 Sustainable Development Goals

This project contributes to:

| SDG | Goal |
|-----|------|
| SDG 2 | Zero Hunger — supports food security through early crop disease detection |
| SDG 9 | Industry, Innovation and Infrastructure — applies AI to agriculture |
| SDG 12 | Responsible Consumption — reduces unnecessary pesticide usage |
| SDG 15 | Life on Land — promotes sustainable farming and biodiversity |

---

## 🔭 Future Work

- Expand dataset to cover more disease types, growth stages, and diverse Indian climate zones
- Integrate a **treatment recommendation module** with region-specific agronomic advice
- Optimize models via pruning and quantization for **mobile / edge deployment**
- Build a **mobile app** for offline use in rural areas with limited connectivity
- Explore automated hyperparameter tuning and neural architecture search

---

## 📄 License

This project is developed for academic and research purposes as a B.Tech Capstone Project at GITAM University, Bengaluru (2026).
