# 目标跟踪
## 1 传统目标跟踪方法
这类方法主要依赖于手工设计的特征提取和滤波器。

### 1.1基于生成模型的方法
- 均值漂移（Mean-Shift）：通过目标的颜色直方图特征进行相似性计算，迭代找到目标区域的最佳匹配。

- CamShift（Continuously Adaptive Mean Shift）：在Mean-Shift的基础上，自适应调整窗口大小。

- Kalman滤波（Kalman Filter, KF）：基于线性状态空间模型，通过预测和更新步骤来估计目标状态。

### 1.2 基于判别模型的方法
- 粒子滤波（Particle Filter, PF）：利用蒙特卡洛方法对目标状态进行采样，并根据观察模型计算权重，适用于非线性和非高斯分布的问题。

- 光流法（Optical Flow）：基于目标的运动信息估计其在连续帧中的位移，例如Lucas-Kanade光流。

- 相关滤波（Correlation Filter, CF）：利用傅里叶变换加速目标匹配计算，包括MOSSE、KCF、DSST等。


## 2 深度学习目标跟踪方法
深度学习方法利用卷积神经网络（CNN）、循环神经网络（RNN）或Transformer等进行特征提取和目标预测，性能大幅超越传统方法。

### 2.1 基于检测的跟踪（Tracking by Detection）
- 采用目标检测器（如YOLO、Faster R-CNN）在每帧图像中进行目标检测，并利用数据关联（如匈牙利算法、Kalman滤波）进行目标匹配和跟踪。

- 代表性方法：DeepSORT（Simple Online and Realtime Tracker）。

### 2.2 基于孪生网络（Siamese Network）的跟踪
通过一个孪生网络（Siamese Network）对目标和搜索区域进行特征匹配，实现目标定位。

- 代表性方法：

    - SiamFC（Siamese Fully Convolutional Network）

    - SiamRPN（Siamese Region Proposal Network）

    - SiamCAR（Siamese Center-Aware Tracker）

### 2.3 基于Transformer的目标跟踪
Transformer结构被引入目标跟踪领域，增强了全局注意力机制，使得模型能够捕捉长期依赖关系。

- 代表性方法：
  - TrTr（Transformer Tracking）
  - OSTrack（Object Seeker Tracker）
  - TransT（Transformer Tracking with Dense Feature Flow）

### 2.4 基于端到端学习的方法
- 端到端学习方式训练一个统一的网络进行目标跟踪，而无需单独的目标检测或特征匹配模块。

- 代表性方法：
    - DETR-based Tracker（DEtection TRansformer）

## 3 多目标跟踪（Multi-Object Tracking, MOT）
多目标跟踪涉及多个目标的检测、身份保持和轨迹预测，常见方法包括：

- SORT（Simple Online and Realtime Tracker）：基于目标检测器、Kalman滤波和匈牙利算法进行数据关联。
- DeepSORT：在SORT基础上加入深度学习特征（如ReID）提升目标区分能力。
- FairMOT：采用单一网络同时进行目标检测和ReID，提升跟踪性能。
- ByteTrack：优化数据关联策略，提高低置信度目标的跟踪能力。

## 4 目标跟踪与红外小目标
在红外目标跟踪中，目标通常较小且背景复杂，常用的方法包括：

- 基于小目标检测的跟踪（IRSTD + Tracking）

- 自适应滤波（如红外相干跟踪滤波）

- 基于Transformer的红外目标跟踪（如TransT扩展到红外领域）


**[返回主页](/README.md)**