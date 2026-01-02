# Railway Track Tampering Detection – Sensor ML Module

This repository contains the **sensor-based machine learning module** developed as part of the **Hack4Delhi Hackathon** for detecting intentional railway track tampering.

---

## Problem Context

Railway track tampering (cutting, hammering, loosening bolts) introduces **abnormal vibration patterns** that differ from normal operational vibrations caused by train movement or environmental factors.

However, **real-world labeled tampering vibration data is not publicly available**, making supervised learning impractical.

---

## Solution Overview

We implement an **unsupervised anomaly detection approach** that learns *normal vibration behavior* and flags abnormal vibration windows that may indicate tampering.

Each data row represents a **fixed-length vibration window**, captured using track-mounted vibration sensors.

---

## Machine Learning Approach

### Data Representation
- Each row = one vibration window
- Columns: `vibration_0` → `vibration_485` (time-series samples)
- Metadata columns (e.g., `condition`, `label`) are excluded from training

### Feature Engineering
From each vibration window, the following statistical features are extracted:
- Mean
- Standard Deviation
- Peak-to-Peak Amplitude
- Root Mean Square (RMS)
- Kurtosis
- Skewness

These features capture both **energy** and **distribution shape** of vibrations.

---

## Model Used

- **Isolation Forest** (Unsupervised Anomaly Detection)
- Trained only on normal vibration data
- Outputs an anomaly score per vibration window
- Higher score ⇒ more anomalous behavior

Isolation Forest is chosen because:
- No labeled tampering data exists
- It scales well to high-dimensional data
- It is widely used in industrial anomaly detection

---

## Validation Strategy

Since real tampering data is unavailable:
- Synthetic vibration spikes are injected to simulate tampering-like disturbances
- The model shows significantly higher anomaly scores for these simulated events

This validates the model’s ability to detect abnormal mechanical behavior.

---

## Output

- Continuous anomaly score per vibration window
- Percentile-based thresholding converts scores into **high-risk alerts**
- These alerts are later fused with camera-based detections in the full system

---

## Role in Full Hackathon Solution

This sensor ML module provides:
- **Early detection** of mechanical disturbances
- Detection independent of lighting, weather, or visibility
- Physics-based evidence of tampering

It is fused with a **camera-based tampering detection model** to produce high-confidence alerts for railway authorities.

---

## Dataset Note
Link: https://www.kaggle.com/datasets/ziya07/high-speed-train-bogie-vibration-and-fault-diagnosis 

The datasets used for training and testing are **not included** in this repository due to GitHub file size limitations (>25 MB).

The notebook clearly documents:
- Expected dataset structure
- Feature extraction logic
- Model training process

This ensures reproducibility in principle.
---

## Technologies Used

- Python
- Pandas, NumPy
- SciPy
- Scikit-learn
- Matplotlib

---

## File Description

- `sensor_anomaly_detection.ipynb`  
  → Complete ML pipeline: data preprocessing, feature engineering, model training, anomaly scoring, and validation.

---

## Conclusion

This repository demonstrates a **production-style, explainable, and realistic ML approach** to detecting railway track tampering using vibration sensor data.

The focus is on correctness, robustness, and real-world deployment feasibility.
