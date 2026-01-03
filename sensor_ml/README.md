# Sensor-Based Anomaly Detection (RTAM)

This folder contains the **sensor-based ML module** of RTAM.

## Contributor
- Developed by: **[Devanshi Yadav](https://github.com/Devanshi-Y)**

## Role in RTAM
This model provides **continuous, physics-based early detection** of railway track tampering by analyzing vibration signals.

## ML Approach
- Model: Isolation Forest
- Learning Type: Unsupervised
- Input: Vibration sensor windows
- Output: Anomaly score (0–1)

## Why This Matters
- Works 24×7
- Does not require labeled data
- Detects tampering before visible damage

## Notebook
- `sensor_anomaly_detection.ipynb`

The anomaly score produced here is sent to the **fusion layer** in the backend.

