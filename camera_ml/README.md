# Camera-Based Visual Tampering Detection (RTAM)

This folder contains the **camera-based ML module** of RTAM.

## 👤 Contributor
- Developed by: **[Divyam Mehra](https://github.com/mayvid4210)**

## 📌 Role in RTAM
This model provides **visual confirmation of track defects or tampering**, complementing the sensor-based anomaly detection.

## 🧠 ML Approach
- Model: ResNet50 (Transfer Learning)
- Framework: PyTorch
- Task: Normal vs Defective classification
- Explainability: Grad-CAM heatmaps

## 📊 Why This Matters
- Human-interpretable evidence
- Visual localization of defects
- Improves confidence of alerts

## 📎 Notebook
- `camera_tampering_detection.ipynb`

The prediction from this model is sent to the **fusion layer** for final decision-making.
