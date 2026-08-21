---
title: "SMILE: A Scale-aware Multiple Instance Learning Method for Multicenter STAS  Lung Cancer Histopathology Diagnosis"
title_zh: SMILE：面向多中心STAS肺癌组织病理诊断的尺度感知多实例学习方法
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/1093.pdf"
tags: ["query:cell-path"]
score: 6.0
evidence: "尺度感知多实例学习方法用于多中心肺癌H&E全切片诊断"
tldr: 多中心STAS肺癌组织病理诊断面临尺度差异和数据异质性挑战。本文提出SMILE，一种尺度感知的多实例学习方法，能适应全切片图像中的多尺度病理结构。实验表明该方法可提升多中心数据上的诊断准确性，为肺癌组织病理诊断提供了有效工具。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-1093/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1765, \"height\": 793}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-1093/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 822, \"height\": 411}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-1093/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1725, \"height\": 697}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-1093/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 889, \"height\": 710}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-1093/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1841, \"height\": 439}]"
motivation: 多中心STAS肺癌诊断存在尺度差异和数据异质性，影响模型泛化。
method: 提出尺度感知的多实例学习方法，适应全切片图像中不同尺度的病理特征。
result: 在多中心STAS肺癌数据集上验证了诊断性能的提升。
conclusion: 尺度感知MIL可有效提升多中心STAS肺癌诊断的准确性和鲁棒性。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

# SMILE 论文详细总结

## 1. 论文的核心问题与整体含义

- **研究背景与动机**  
  - STAS（Spread Through Air Spaces，经气腔播散）是肺癌中一种新发现的侵袭模式，与更高的肿瘤分级、KRAS 突变、较差的无复发生存期以及手术方式选择密切相关。
  - 目前 STAS 诊断主要依赖病理医生人工观察，过程耗时、主观性强、不同机构间一致性差，临床手动诊断准确率约 74%（AUC ≈ 0.67）。
  - 公开数据集中缺乏系统的 STAS 标注，且 STAS 病灶具有稀疏、异质、尺度多变等特点，传统人工检查和常规深度学习方法难以有效识别。

- **整体含义**  
  - 本文构建并公开了三个多中心 STAS 肺癌病理数据集，并提出一种尺度感知多实例学习方法 SMILE，用于全切片图像（WSI）级别的 STAS 自动诊断。
  - 研究旨在减少模型对局部高注意力区域的过度依赖，提高对稀疏、异质性 STAS 病灶的识别能力，为计算病理学在 STAS 辅助诊断中的应用奠定基础。

## 2. 方法论

- **总体框架：多实例学习（MIL）**  
  - 将每张 WSI 视为一个 bag，WSI 切分出的 patch 视为 instance。
  - 如果 bag 中至少一个 instance 被判定为 STAS，则该 bag 标签为 STAS；否则为非 STAS。
  - 流程分为三步：实例级特征提取、特征融合、bag 级预测。

- **实例级特征提取**  
  - **离线阶段**：使用预训练的 CTransPath 骨干网络（结合 CNN 与 Transformer，经语义对比学习预训练）提取每个 patch 的特征向量，冻结骨干权重。
  - **在线阶段**：通过 `BatchNorm1d → Linear → ReLU` 三层可训练网络对提取的特征进行微调，得到实例特征矩阵 \(H \in \mathbb{R}^{n \times d}\)。

- **尺度自适应注意力机制（核心创新）**  
  - 首先使用常规注意力模块生成每个实例的注意力分数：  
    \(A = W_a \left( \tanh(V_a H) \odot \sigma(U_a H) \right)\)，  
    其中 \(V_a, U_a, W_a\) 为可学习参数，\(\odot\) 为逐元素乘法。
  - 对 \(A\) 进行 Max-Min 归一化，并设定阈值 `Threshold`：超过阈值的注意力分数会被标记。
  - 引入缩放因子 `Factor`：对超过阈值的注意力分数乘以 `Factor`，未超过的部分保持不变。
  - 经 Softmax 后得到尺度缩放后的注意力权重 \(SA\)，再聚合实例特征：  
    \(z = \sum_{i=1}^{n} sa_i h_i\)。

- **Bag 级预测与损失函数**  
  - 使用线性层 + Sigmoid 激活输出 bag 级预测概率。
  - 优化目标为标准二元交叉熵损失。

## 3. 实验设计

- **数据集**  
  - **STAS-CSU**：来自中南大学湘雅二医院，含 356 例肺腺癌患者，共 1290 张冷冻切片（FS）和石蜡切片（PS）WSI，其中 247 张 FS（81 STAS / 158 非 STAS）、1043 张 PS（585 STAS / 436 非 STAS）。
  - **STAS-TCGA**：来自 TCGA 数据库，共纳入 424 张肺腺癌 WSI，其中 155 张 STAS
