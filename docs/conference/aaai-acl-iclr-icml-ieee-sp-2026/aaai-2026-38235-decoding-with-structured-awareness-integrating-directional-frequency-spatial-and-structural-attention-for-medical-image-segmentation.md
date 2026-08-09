---
title: "Decoding with Structured Awareness: Integrating Directional, Frequency-Spatial, and Structural Attention for Medical Image Segmentation"
title_zh: 结构化感知解码：集成方向、频率空间和结构注意力的医学图像分割
authors: "Fan Zhang, Zhiwei Gu, Hua Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38235/42197"
tags: ["query:immuno-topo"]
score: 4.0
evidence: "一种具有多域注意力的医学图像分割解码器，可应用于H&E切片中的细胞分割。"
tldr: "针对Transformer解码器在边缘细节、纹理识别和空间连续性方面的不足，本文提出一种新型医学图像分割解码器，融合方向性注意、频域-空域特征融合和结构注意。该方法在多个医学图像分割任务上表现优越，其注意力机制有望迁移至H&E切片细胞分割，提升精细分割性能。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38235/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1613, \"height\": 1067, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38235/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1772, \"height\": 672, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38235/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 722, \"height\": 549, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38235/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 831, \"height\": 522, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38235/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1628, \"height\": 640, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38235/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 451, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38235/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 487, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38235/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 771, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38235/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 921, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38235/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 901, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38235/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1801, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38235/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 874, \"height\": 229, \"label\": \"Table\"}]"
motivation: 现有Transformer解码器难以捕捉边缘细节、局部纹理和空间连续性。
method: 提出集成方向、频率-空间和结构注意力的解码器框架。
result: 在医学图像分割任务上取得了优越性能。
conclusion: 该解码器设计为医学分割提供了有效改进，具有迁移潜力。
---

## Abstract
To address the limitations of Transformer decoders in capturing edge details, recognizing local textures and modeling spatial continuity, this paper proposes a novel decoder framework specifically designed for medical image segmentation, comprising three core modules. First, the Adaptive Cross-Fusion Attention (ACFA) module integrates channel feature enhancement with spatial attention mechanisms and introduces learnable guidance in three directions (planar, horizontal, and vertical) to enhance responsiveness to key regions and structural orientations. Second, the Triple Feature Fusion Attention (TFFA) module fuses features from Spatial, Fourier and Wavelet domains, achieving joint frequency-spatial representation that strengthens global dependency and structural modeling while preserving local information such as edges and textures, making it particularly effective in complex and blurred boundary scenarios. Finally, the Structural-aware Multi-scale Masking Module (SMMM) optimizes the skip connections between encoder and decoder by leveraging multi-scale context and structural saliency filtering, effectively reducing feature redundancy and improving semantic interaction quality. Working synergistically, these modules not only address the shortcomings of traditional decoders but also significantly enhance performance in high-precision tasks such as tumor segmentation and organ boundary extraction, improving both segmentation accuracy and model generalization. Experimental results demonstrate that this framework provides an efficient and practical solution for medical image segmentation.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与整体含义

- **研究动机**：当前基于 Transformer 的医学图像分割解码器在捕捉边缘细节、识别局部纹理和建模空间连续性方面存在明显不足。传统跳层连接采用简单相加，易引入特征冗余和空间信息丢失。
- **整体目标**：提出一种“结构化感知解码器”框架，通过方向性注意力、频率‑空间融合和结构显著性筛选，显著提升病灶分割、器官边界提取等任务中的精度和泛化能力。

## 2. 方法论

### 2.1 总体框架

- 模型采用编码器‑解码器结构，编码器使用预训练的 PVTv2‑b2，解码器由三个核心模块协同构成：**ACFA**、**TFFA** 和 **SMMM**。

### 2.2 自适应交叉融合注意力（ACFA）

- **核心思想**：引入通道与空间双重门控，并学习三个方向（平面、水平、垂直）的可学习引导参数，强化模型对关键区域和结构方向的响应。
- **技术细节**：
  - 先对输入特征图分别施加通道门控和空间门控（通过平均/最大池化与 Sigmoid 激活），生成增强特征。
  - 沿通道维度将特征分为四个子集，三个分别与特定方向的 Tensor（初始化自均匀分布，并经可学习一维/二维深度可分离卷积调制）融合，第四分支使用普通卷积捕捉通用上下文。
  - 最终将四个分支的输出拼接，经 LayerNorm 和卷积融合得到方向感知增强特征。

### 2.3 三重特征融合注意力（TFFA）

- **核心思想**：结合空间域、傅里叶域和小波域的特征，实现全局依赖性建模与局部边缘/纹理保留的平衡。
- **分支设计**：
  - **小波分支**：采用 DoG（差分高斯）和 Mexican Hat 小波函数进行局部时频分析，通过可学习的尺度与平移参数实现多小波动态融合。
  - **傅里叶分支**：将图像变换到频域，经可学习权重矩阵调制高低频成分，增强全局结构表示。
  - **空间分支**：使用逐点卷积提取空间特征。
- **融合机制**：对三支输出施加注意力门控，分配动态权重进行自适应融合，避免简单叠加的语义平滑问题。最后经批归一化和激活函数输出。

### 2.4 结构感知多尺度掩蔽模块（SMMM）

- **核心思想**：优化编码器‑解码器间的跳层连接，通过多尺度上下文提取和结构显著性筛选来抑制冗余、增强语义交互。
- **技术流程**：
  1. 对编码器和解码器的同级特征分别进行逐点卷积激活空间线索。
  2. 利用深度可分离卷积（核尺寸 3×3 和 5×5）结合通道拆分与 ReLU 激活，构建多尺度感知模块，扩大感受野。
  3. 经多尺度融合后，输入掩蔽模块：使用三个不同的通道门控滤波器识别空间显著区域，并通过 Softmax 加权突出高响应部位。
  4. 将滤波结果相加后，用扩张卷积（膨胀率为 2）进一步融合上下文，最后经归一化和逐点卷积输出。

## 3. 实验设计

### 3.1 数据集

- **皮肤病变分割**：ISIC 2017（约 2000 张）和 ISIC 2018（2594 张），用于边界分割和多类别评估。
- **多器官分割**：Synapse 数据集（30 例腹部 CT，8 个器官像素级标注），用于跨器官识别的标准基准。
- **心脏分割**：ACDC 数据集（100 例心脏 MRI，含健康与病变病例，标注左/右心室和心肌）。

### 3.2 对比方法（Baseline）

- 涵盖经典与先进模型：TransUNet、Swin‑UNet、LeViT‑UNet、MISSFormer、ScaleFormer、HiFormer‑B、DAEFormer、PVT‑CASCADE、LKA、EMCAD、AD‑LA Former、CSWin‑UNet、DMSA‑Unet、EGE‑Unet、UltraLightVM‑UNet、VM‑UNetV2、Cascaded MERIT、TBConvL‑Net 等。
- 评价指标：Dice 相似系数（DSC）、Hausdorff 距离（HD95）、灵敏度（SE）、特异性（SP）、准确率（ACC）。

## 4. 资源与算力

- **硬件**：单张 NVIDIA A100 GPU（40 GB 显存）。
- **软件**：PyTorch 1.11.0。
- **训练配置**：
  - 批次大小：12。
  - 优化器：AdamW（学习率 1e‑4，权重衰减 1e‑4）。
  - 迭代次数：ISIC 2017/2018 训练 200 epoch；Synapse 300 epoch；ACDC 400 epoch。
- **未明确说明**：单次训练的实际耗时尚无直接报告。

## 5. 实验数量与充分性

- **对比实验**：
  - 在 Synapse 上完成 1 组多方法对比（13 种方法对比 8 个器官 DSC/HD95）。
  - ISIC 2017 和 2018 各 1 组对比（约 10 种方法，含 DSC/SE/SP/ACC）。
  - ACDC 上 1 组对比（7 种方法对比 RV/Myo/LV DSC）。
- **消融实验**：
  - Synapse 和 ISIC 2017 上分别进行模块累加消融（Baseline → +ACFA → +TFFA → +SMMM），含参数与计算量统计。
  - TFFA 内部消融（不同小波组合：无、仅 Mexican Hat、Mexican Hat + DoG）在 ISIC 2018 上进行。
- **定性分析**：Synapse 和 ISIC 2017 可视化分割结果对比，ISIC 2018 注意力热图。
- **评价**：实验覆盖多任务、多模态，消融设计逐步验证各模块贡献，对比方法丰富且包含近年 SOTA，整体充分且客观。

## 6. 主要结论与发现

- 本文提出的结构化感知解码器在多个医学分割任务上取得领先性能：
  - Synapse：DSC 83.92%，超越 EMCAD（83.63%），且对脾、肾等器官边界提取优势明显。
  - ISIC 2017：DSC 91.40%，ACC 97.26%，灵敏度和特异性均衡。
  - ACDC：DSC 92.75%，右心室分割显著提升。
- 消融实验证实三个模块协同增效：ACFA 增强方向感知，TFFA 融合频域信息提升边界精细度，SMMM 优化跳层连接减少冗余。
- 注意力热图表明模型能准确聚焦病灶区域，边缘光滑且内部结构捕捉完整。

## 7. 优点

- **多域融合视角**：同时利用空间、傅里叶和小波域的互补特性，对模糊边界和复杂纹理具显著增益。
- **结构感知能力**：通过方向引导和显著性掩蔽，增强对器官形态和病灶边界的建模，提高分割一致性。
- **模块化的即插即用设计**：各模块可独立或组合使用，易于集成到现有编码器‑解码器架构。
- **实验充分性**：在多种器官、皮肤病变、心脏等多任务上与大量 SOTA 模型公平对比，且具备内部组件消融。

## 8. 不足与局限

- **计算开销增加**：完整模型参数量 42.52M，计算量 18.29 GMac，相比基线有明显增长，可能限制在资源受限场景的部署。
- **编码器依赖**：实验仅基于 PVTv2‑b2 编码器，未验证该解码器搭配其他编码器（如纯 CNN 或不同 ViT 变体）的泛化性。
- **训练耗时未量化**：尽管给出了 epoch 数，但未报告每 epoch 训练时间，不便评估实际计算成本。
- **数据模态覆盖**：主要在 CT、MRI、皮肤镜图像上验证，未涉及超声、X 光或病理切片等常见医学图像，其泛化潜力尚待进一步测试。
- **潜在偏差风险**：所有数据集均为公开、去标识化，但样本量相对较小（如 Synapse 仅 30 例），可能影响临床场景下的可靠性。

（完）
