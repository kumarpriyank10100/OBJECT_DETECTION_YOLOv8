# 👁️ Real-Time Vision (YOLOv8 Evolution)

This project demonstrates the implementation of real-time object detection using **YOLOv8**. It is structured in two distinct phases: moving from a standard local implementation to a sophisticated **Cloud-Native AR Overlay** system.

---

## 🛠️ Phase 1: The Local Foundation

The initial implementation focuses on a standard Python-to-Hardware connection. Using OpenCV's `VideoCapture`, the script accesses a local camera and runs inference frame-by-frame.

* **Logic:** Synchronous Frame Capture  YOLO Inference  Bounding Box Plotting.
* **Environment:** Best suited for local PCs, Edge devices (Raspberry Pi), or Jetson Nano.

---

## 🚀 Phase 2: The Cloud Upgrade (Live AR Overlay)

The "Pro" version of this project addresses the critical limitation of cloud environments like **Google Colab**, which lack direct access to user hardware.

### The Engineering Solution: The JS-Python Bridge

Instead of a standard Python loop, I engineered an **Augmented Reality (AR) Overlay** system:

1. **Native Browser Stream:** Uses JavaScript to access the webcam via the browser's `navigator.mediaDevices` API for 0-latency viewing.
2. **Transparent Canvas:** A hidden HTML5 canvas captures frames and sends them to the Python backend as Base64 strings.
3. **Inference:** YOLOv8 processes the frame on the remote server.
4. **Asynchronous Overlay:** The Python script returns **only** the bounding box data, which is then drawn onto a transparent overlay on the user's screen.

### Why this is an Upgrade:

* **Latency Separation:** The video stays smooth because the raw stream never leaves your browser. Only small detection packets are sent across the web.
* **Cloud Compatibility:** Solves the `VideoCapture(0)` error in remote environments.
* **UX Design:** Uses a non-blocking UI that allows for real-time interaction without the "choppy" lag associated with traditional cloud video processing.

---

## 📊 Feature Comparison

| Feature | Phase 1: Local | Phase 2: Cloud (Upgrade) |
| --- | --- | --- |
| **Video Latency** | Low | **Near-Zero (Native)** |
| **Platform** | Local Machine Only | **Google Colab / Browser** |
| **Architecture** | Direct Hardware Link | **JavaScript-Python Bridge** |
| **Visualization** | `cv2.imshow` | **Transparent HTML5 Overlay** |

---

## 💻 How to Run

### Local Version

```bash
pip install ultralytics opencv-python
python local_detection.py

```

### Cloud Upgrade

1. Open the notebook in Google Colab.
2. Ensure you have granted Camera Permissions in your browser.
3. Run the cell; the JavaScript bridge will initialize the handshake and start the overlay.

---

## 💡 Key Takeaways

* **Bridging Environments:** Developed a solution to bypass hardware limitations in virtualized environments.
* **Asynchronous Processing:** Learned to handle data transfer between the client (Browser) and the server (Colab).
* **Model Optimization:** Used the YOLOv8 Nano model to ensure high-speed processing on CPU-based cloud instances.

---

