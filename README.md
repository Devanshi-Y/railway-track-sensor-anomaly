# RTAM – Machine Learning Module

This repository contains the **Machine Learning layer** of **RTAM (Railway Track Anomaly Monitor)**, developed for the **Hack4Delhi Hackathon**.

RTAM is a multi-modal AI system for detecting **intentional railway track tampering** by combining sensor-based and camera-based intelligence.

---

## Purpose of This Repository

This repository focuses exclusively on **ML intelligence**, which includes:

- Sensor-based vibration anomaly detection
- Camera-based visual tampering detection
- ML-level logic that feeds into the backend fusion layer

Frontend and backend services are **outside the scope** of this repository and are documented at a system level in `PROJECT_OVERVIEW.md`.

---

## ML Modules in This Repository

### 1. Sensor-Based ML (`sensor_ml/`)

**Role:**  
Provides **continuous, physics-based early detection** of abnormal track behavior using vibration sensor data.

**Key Characteristics:**
- Unsupervised learning (Isolation Forest)
- Works without labeled tampering data
- Detects anomalies before visible damage occurs

---

### 2. Camera-Based ML (`camera_ml/`)

**Role:**  
Provides **visual confirmation and explainability** by analyzing CCTV images of railway tracks.

**Key Characteristics:**
- Deep learning (ResNet50 – Transfer Learning)
- Supervised classification (Normal vs Defective)
- Grad-CAM heatmaps for explainability

---

## Why Both SensorML and CameraML Are Needed

| Aspect | Sensor ML | Camera ML |
|------|-----------|-----------|
Early detection | ✅ | ❌ |
Works at night / fog | ✅ | ❌ |
Visual evidence | ❌ | ✅ |
Explainability | ✅ (statistical) | ✅ (Grad-CAM) |
Requires labeled data | ❌ | ✅ |

Individually, each model has limitations.  
**Together, they form a reliable and deployable system.**

---
## Explainability Approach

RTAM uses **different explainability strategies** for each ML module, chosen according to the nature of the data and model.

### Sensor-Based ML Explainability
The sensor anomaly detection model is based on **unsupervised statistical learning**.  
Explainability is achieved through **feature-level interpretation**, including:
- Mean vibration level
- Signal variance
- RMS energy
- Kurtosis and skewness

Anomalies are justified by observing significant deviations in these statistical features from learned normal behavior.

This form of explainability is appropriate for **time-series sensor data**, where visual explanations are not applicable.

---

### Camera-Based ML Explainability
The camera-based model uses **deep learning (ResNet50)** and provides **visual explainability** using **Grad-CAM heatmaps**.

Grad-CAM highlights the specific regions of the track image that influenced the model’s prediction, making the decision interpretable for human operators.

---

### Why Different Explainability Methods Are Used
Different ML models require different explainability approaches:

| Model Type | Explainability Method |
|-----------|-----------------------|
Sensor ML (Isolation Forest) | Statistical / Feature-based |
Camera ML (CNN) | Visual (Grad-CAM) |

Using the **correct explainability method for each model** ensures transparency, trust, and suitability for real-world deployment.

---

## ML Outputs

- **Sensor ML Output:**  
  Continuous anomaly score (0–1)

- **Camera ML Output:**  
  Classification + confidence + heatmap

These outputs are consumed by the **backend fusion logic** to generate a final risk decision.

---

## System-Level Integration

The ML outputs from this repository are integrated into:
- Backend fusion logic
- Alerting services
- Frontend dashboards

For complete system architecture, workflow, and deployment strategy, refer to **`PROJECT_OVERVIEW.md`**.
