# 👁️ Real-Time Vision: YOLOv8 Object Detection Pipeline

A high-performance, real-time computer vision pipeline utilizing the **YOLOv8 (You Only Look Once v8)** architecture. This project demonstrates the integration of a state-of-the-art CNN with live hardware streams to perform multi-class object localization and classification at 30+ FPS.

---

## 🏗️ Architectural Depth

Unlike its predecessors, YOLOv8 introduces several key innovations that significantly boost both speed and mean Average Precision (mAP):

### 1. The Backbone (Feature Extraction)

The model uses a **modified CSPDarknet53** backbone. It replaces the traditional C3 modules with **C2f (Cross-stage Partial Bottleneck with two convolutions)** modules. This allows for better gradient flow and more diverse feature representation without a heavy computational penalty.

### 2. Anchor-Free Head

YOLOv8 moves away from anchor boxes to an **Anchor-Free Detection** strategy.

* **The Benefit:** By predicting the center of an object directly rather than the offset from a predefined box, it reduces the complexity of the post-processing stage and makes the model more robust to irregular object shapes.

### 3. Decoupled Head

The detection head is now **decoupled**, meaning it processes classification (what the object is) and regression (where the box is) in separate branches. This separation leads to faster convergence and higher accuracy.

---

## 📊 Performance Benchmarks (COCO Dataset)

This project defaults to the **Nano (YOLOv8n)** variant to ensure real-time responsiveness on consumer-grade CPUs.

| Model Variant | Size (px) | mAP (val 50-95) | Speed (CPU ms) | Parameters |
| --- | --- | --- | --- | --- |
| **YOLOv8n (Used)** | **640** | **37.3** | **~80.4** | **3.2M** |
| YOLOv8s | 640 | 44.9 | ~128.4 | 11.2M |
| YOLOv8m | 640 | 50.2 | ~234.7 | 25.9M |

---

## 🛠️ Implementation Strategy

### **The Pipeline**

1. **Frame Capture:** OpenCV pulls raw BGR frames from the camera buffer.
2. **Preprocessing:** Frames are automatically resized and normalized to  by the Ultralytics engine.
3. **Inference:** The forward pass generates confidence scores and bounding box coordinates.
4. **NMS (Non-Maximum Suppression):** Overlapping detections are pruned based on an Intersection over Union (IoU) threshold.
5. **Real-time Visualization:** Resulting tensors are mapped back to pixel coordinates and rendered on the display window.

---

## 💻 Setup & Usage

### 1. Installation

Ensure you have a Python environment ready. Install the core dependencies:

```bash
pip install ultralytics opencv-python

```

### 2. Execution

Run the detection script. On the first run, the pre-trained COCO weights (`yolov8n.pt`) will automatically download.

```bash
python main.py

```

### 3. Controls

* **Quit:** Press `q` to safely release the camera resources and close the OpenCV window.
* **Confidence Tuning:** You can adjust the `conf=0.5` parameter in the script to filter out low-probability detections.

---
