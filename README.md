# Causal-MSFF: Edge-Deployable Framework for Causal Multi-Scale Emergency Lane Control
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Framework](https://img.shields.io/badge/Framework-Causal_AI|MultiScale_Signal|Edge_Computing-blue)

**Official implementation of:**  
*Causal-MSFF: An Edge-Deployable Framework for Causal Multi-Scale Emergency Lane Control in Highway Congestion*  
(Xuerui Fang, Gulimila Kezierbieke et al., 2025)

---

## 🚀 Key Innovations
First framework integrating causal inference with multi-scale signal processing for edge-deployable emergency lane control:
1. **Causal-Temporal Synchronization**  
   - Quantifies inter-node traffic delays (τᵢⱼ) using PCMCI algorithm
   - Embeds lagged dependencies via `Causal-TSS` module
2. **Dual-Path Feature Fusion**  
   - **Local features**: DWT denoising with Bior3.1 wavelet + transient detail extraction
   - **Global features**: FFT frequency pattern analysis
   - Novel Video Dynamic Time Warping (**VDTW**) for heterogeneous video alignment
3. **Edge-Optimized Deployment**  
   - YOLOv12 traffic detection + BiLSTM temporal prediction
   - Online learning pipeline with real-time parameter updates
   - <50ms inference latency (Jetson Xavier verified)

## 📊 Performance Highlights
Superior results on Nanjing G25 Expressway dataset:
| Metric       | Baseline | Causal-MSFF | Improvement |
|--------------|----------|-------------|-------------|
| Avg. MSE     | 0.8358   | **0.6352**  | ↓ 24%       |
| Mean R²      | 0.0970   | **0.3100**  | ↑ 219.6%    |

Ablation contributions:  
`Causal-TSS` → +53.9% R² | `D2FE` → +32.2% R²

---

## 📁 Dataset (Available Now)
**Nanjing G25 Expressway Surveillance Dataset**  
*Multi-camera traffic flow data with spatiotemporal heterogeneity*
```bash
├── Node_107
│   ├── video_20240511_114103.mp4  # 33FPS, 1656s
│   └── traffic_counts.csv          # Vehicle count time-series
├── Node_105
│   ├── video_20240511_115227.mp4  # 25FPS, 1296s 
│   └── traffic_counts.csv
└── Metadata
    ├── node_positions.gpkg        # Beidou positioning data
    └── calibration_report.pdf     # Sensor calibration
