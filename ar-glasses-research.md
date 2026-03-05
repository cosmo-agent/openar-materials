# 开源AR眼镜调研报告

## 一、主要开源硬件项目

### 1. OpenAR (芬兰东芬兰大学)

- **官网**: https://sites.uef.fi/openar/
- **特点**: 完全开源，专为爱好者设计，成本极低(30-150€)
- **版本演进**:
  - OpenAR 1.0: 首个版本
  - OpenAR 2.0: 改进模块化
  - OpenAR 2.1: 集成热成像相机
  - OpenAR 2.2: 增加蓝牙模块
  - OpenAR-M: 最新紧凑型版本
- **下载**: 提供完整的机械、电路、固件文件

### 2. Open Source Smart Glasses (Mentra Community)

- **GitHub**: https://github.com/Mentra-Community/OpenSourceSmartGlasses
- **功能**: 显示屏、麦克风、无线手机连接、处方镜片支持、LED指示灯
- **配套系统**: Wearable Intelligence System
- **应用**: 实时语言翻译、情境搜索引擎、智能助手、网页搜索

### 3. Team Open Smart Glasses (TOSG)

- **官网**: https://teamopensmartglasses.com/
- **目标**: 构建开源智能眼镜技术以升级人类思维
- **社区**: 包含开源工程师团队和领先硬件公司

### 4. Zero (DIY Pi Zero AR眼镜)

- **作者**: Reddit用户 mi_kotalik
- **硬件**: Raspberry Pi Zero + SPI显示屏
- **功能**: 视频播放、蓝牙音频、提词器、图片查看器
- **光学**: 最初尝试PETG打印镜片，后改用树脂浇铸镜片
- **帧率**: 优化至60 FPS
- **V2计划**: 使用Compute Module 4，支持3D渲染、GPS、空间追踪

### 5. Low-Cost AR (Augmentation Lab)

- **官网**: https://augmentationlab.org/projects/low-cost-ar-glasses
- **方案**: 拆解手机，使用其电子元件制作镜框
- **目标**: 经济实惠、易于构建、实用性强

---

## 二、硬件技术方案

### 显示技术

| 方案         | 描述                        | 优缺点                               |
| ------------ | --------------------------- | ------------------------------------ |
| SPI显示屏    | 小尺寸OLED/LCD，通过SPI连接 | 成本低，易于控制，但分辨率和尺寸受限 |
| 波导光学     | 专业AR眼镜使用的光波导      | 图像质量好，但成本极高，难以DIY      |
| 树脂浇铸镜片 | 自制透镜方案                | 极低成本，但光学质量差               |
| 分光棱镜     | 半透半反镜方案              | 中等成本，可实现叠加显示             |

### 计算平台

- **Raspberry Pi Zero**: 低成本，足够运行基础AR功能
- **Raspberry Pi Compute Module 4**: 更强性能，支持3D渲染
- **手机拆解方案**: 利用现有手机的完整生态系统
- **ESP32**: 超低成本，适合简单HUD功能

### 光学设计挑战

根据社区讨论，AR光学是关键难点：

- 专业波导光学需要数百万美元研发投入
- 自制镜片质量难以保证
- 焦距、视场角(FOV)、眼盒(eyebox)设计复杂
- 建议选择现成光学模组或接受较低图像质量

---

## 三、开源算法与软件

### 1. 手势识别与追踪

- **MediaPipe Hands**: Google开源，实时手部关键点检测
- **OpenCV + 传统CV**: 肤色检测、轮廓分析
- **GRLib**: 开源手势检测识别Python库 (arXiv:2310.14919)
- **深度学习方案**: CNN-based手势识别

### 2. 眼动追踪

- **FaceSight (ACM论文)**: 在AR眼镜上实现的手到面部手势感应
- **红外相机方案**: 在眼镜桥接处安装红外相机追踪手部行为

### 3. SLAM与空间定位

- **ORB-SLAM3**: 开源视觉SLAM
- **OpenVSLAM**: 基于特征的开源SLAM框架
- **RTAB-Map**: 实时外观建图

### 4. AI视觉识别

- **YOLO系列**: 实时目标检测
- **TensorFlow Lite**: 移动端优化推理
- **OpenCV DNN模块**: 支持多种预训练模型

### 5. 语音与NLP

- **Whisper (OpenAI)**: 开源语音识别
- **Vosk**: 离线语音识别
- **Ollama/Local LLM**: 本地大语言模型运行

---

## 四、外观与结构设计

### 镜框设计

- **3D打印**: PLA/PETG/树脂材料
- **设计工具**: Tinkercad(入门)、Fusion 360(专业)
- **轻量化**: 关键考虑，眼镜需长时间佩戴

### 近视模式实现方案

1. **处方镜片适配**: 预留标准镜片安装槽位
2. **屈光度调节**: 物理调节透镜位置实现变焦
3. **隐形眼镜配合**: 用户佩戴隐形眼镜使用AR眼镜
4. **磁吸镜片**: 可更换的近视镜片组件

### 人体工程学

- 重量分布: 电池后置平衡
- 散热设计: 被动散热优先
- 鼻托: 可调节设计

---

## 五、推荐学习资源

### 关键GitHub项目

1. `Mentra-Community/OpenSourceSmartGlasses`
2. `WearableIntelligenceSystem`
3. OpenAR各版本下载页面

### 论文与文档

- FaceSight: ACM CHI 2021论文
- GRLib: arXiv 2310.14919
- Vision-based Hand Detection综述 (ScienceDirect)

### 社区

- Reddit r/AR_MR_XR
- Smart Glasses Community
- Hackaday AR项目

---

## 六、你们项目的建议

基于调研，对你们计划的四个功能建议如下：

### 1. 近视模式

**推荐方案**: 磁吸式处方镜片 + 物理屈光度微调
**参考**: OpenAR的标准镜片槽位设计

### 2. AI视觉识别 + 手指/眼球追踪

**推荐方案**:

- 手势: MediaPipe Hands + 定制手势库
- 眼动: 红外LED + 小型摄像头方案
- 处理器: RK3588或高通AR专用芯片

### 3. AI对话 (查询/翻译)

**推荐方案**:

- 本地Whisper语音识别
- 云端/边缘端LLM API
- 本地TTS语音合成

### 4. 导航等AR功能

**推荐方案**:

- 9轴IMU (加速度计+陀螺仪+磁力计)
- GNSS模块 (GPS/北斗)
- 可选: 视觉SLAM增强定位

---

_报告生成时间: 2026-03-03_
_数据来源: GitHub、学术论文、开源硬件社区_
