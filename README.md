# Raspberry Pi 4 & YOLOv8 Real-time Object Detection (HW6)

This project implements a real-time object detection system using **YOLOv8** and **Picamera2** on a Raspberry Pi 4. 
The system captures high-resolution video streams and performs AI inference to identify objects with live FPS monitoring.

https://github.com/user-attachments/assets/6474cd3a-9eea-4423-959a-dc47e071d999

🛠️ Development Environment

* **Hardware:** Raspberry Pi 4 (8GB RAM recommended)
* **OS:** Raspberry Pi OS (Bookworm, 64-bit)
* **Camera:** Raspberry Pi Camera Module (v2 / v3)
* **Library:** Ultralytics YOLOv8, Picamera2, OpenCV

🎬 Demo Preview

* **Model:** yolov8n.pt (Nano version for edge computing)
* **Output:** Real-time annotated video with bounding boxes and FPS counter.

🔌 Hardware Setup (Camera)

The camera was connected via the CSI (Camera Serial Interface) port.
* **Interface:** Picamera2 (libcamera-based)
* **Resolution:** 1280x1280 (Configurable for performance)
* **Capture Format:** RGB888

⚙️ Key Implementation (Code Snippet)

The following core logic handles frame capture and YOLOv8 inference.
```python
# Initialize Picamera2
picam2 = Picamera2()
picam2.configure("preview")
picam2.start()

# Load YOLOv8 Model
model = YOLO("yolov8n.pt")

# Main Loop
while True:
    frame = picam2.capture_array()
    results = model(frame)
    annotated_frame = results[0].plot()
    
    # Calculate & Display FPS
    fps = 1000 / results[0].speed['inference']
    cv2.putText(annotated_frame, f'FPS: {fps:.1f}', (10, 30), ...)



