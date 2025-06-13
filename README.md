# Causal-MSFF: Edge-Deployable Causal Multi-Scale Emergency Lane Control
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Framework](https://img.shields.io/badge/Framework-Causal%20AI%20%7C%20MultiScale%20Signal%20%7C%20Edge%20Computing-blue)

**Official implementation of:**  
*Causal-MSFF: An Edge-Deployable Framework for Causal Multi-Scale Emergency Lane Control in Highway Congestion*  
(Xuerui Fang, Gulimila Kezierbieke et al., 2025)

---

## 🚀 Key Innovations
首创融合因果推理与多尺度信号处理的边缘部署框架，实现非事故性拥堵的实时应急车道控制：
1. **因果时间同步**  
   - 采用PCMCI算法量化节点间交通流滞后依赖（$\tau_{ij}$）
   - 通过`Causal-TSS`模块将时延特征显式嵌入模型
2. **双路径特征融合**  
   - **局部特征**：Bior3.1小波基的DWT去噪 + 瞬态细节提取
   - **全局特征**：FFT频域模式分析
   - 创新性引入视频动态时间规整(**VDTW**)对齐异构视频流
3. **边缘轻量化部署**  
   - YOLOv12交通目标检测 + BiLSTM时序预测
   - 在线学习管线支持实时参数更新
   - 推理延迟<50ms (Jetson Xavier实测)

## 📊 性能优势
在南京G25高速数据集上显著超越基线方法：
| Metric       | Baseline | Causal-MSFF | Improvement |
|--------------|----------|-------------|-------------|
| Avg. MSE     | 0.8358   | **0.6352**  | ↓ 24%       |
| Mean $R^2$   | 0.0970   | **0.3100**  | ↑ 219.6%    |
| Traffic Speed| -        | **+10%**    | (应急车道激活)|

模块消融贡献：  
`Causal-TSS` → +53.9% $R^2$ | `D2FE` → +32.2% $R^2$

---

## 📁 数据集 (Available Now)
**Nanjing G25 Expressway Surveillance Dataset**  
*时空异构交通流多摄像机监控数据*
```bash
├── Node_107
│   ├── video_20240511_114103.mp4  # 33FPS, 1656s
│   └── traffic_counts.csv          # 车辆计数时间序列
├── Node_105
│   ├── video_20240511_115227.mp4  # 25FPS, 1296s 
│   └── traffic_counts.csv
└── Metadata
    ├── node_positions.gpkg        # 北斗定位地理信息
    └── calibration_report.pdf     # 传感器标定报告
