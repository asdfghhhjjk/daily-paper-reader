---
title: "Screener: Self-supervised Pathology Segmentation Model for 3D Medical Images"
title_zh: "Screener: 用于3D医学图像的自监督病理分割模型"
authors: "Mikhail Goncharov, Eugenia Soboleva, Mariia Donskova, Ivan Oseledets, Marina Munkhoeva, Maxim Panov"
date: 2025-01-23
pdf: "https://openreview.net/pdf?id=fNyfV5otuV"
tags: ["query:cellseg"]
score: 8.0
evidence: 用于3D医学图像的自监督病理分割模型
tldr: Screener将病理分割视为无监督视觉异常分割问题，通过密集自监督学习提取特征，替代了有监督预训练和手工编码。在超过3万未标记的3D医学图像上训练，实现了对所有病理发现的准确分割，无需任何标注，在病理图像分析中具有重要应用价值。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-fnyfv5otuv/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1753, \"height\": 752, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fnyfv5otuv/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1512, \"height\": 1685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fnyfv5otuv/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1777, \"height\": 618, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fnyfv5otuv/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1777, \"height\": 949, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-fnyfv5otuv/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fnyfv5otuv/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1774, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fnyfv5otuv/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1768, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fnyfv5otuv/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1762, \"height\": 259, \"label\": \"Table\"}]"
motivation: 有监督模型只能检测有限类别病理，难以覆盖所有异常模式。
method: 将病理分割视为无监督异常分割，采用密集自监督特征和掩码不变条件变量。
result: 在大量未标记数据上训练，实现了准确的病理分割。
conclusion: Screener为无监督病理分割提供了有效框架，可推广至全切片图像分析。
---

## Abstract
Accurate segmentation of all pathological findings in 3D medical images remains a significant challenge, as supervised models are limited to detecting only the few pathology classes annotated in existing datasets. To address this, we frame pathology segmentation as an unsupervised visual anomaly segmentation (UVAS) problem, leveraging the inherent rarity of pathological patterns compared to healthy ones. We enhance the existing density-based UVAS framework with two key innovations: (1) dense self-supervised learning (SSL) for feature extraction, eliminating the need for supervised pre-training, and (2) learned, masking-invariant dense features as conditioning variables, replacing hand-crafted positional encodings. Trained on over 30,000 unlabeled 3D CT volumes, our model, Screener, outperforms existing UVAS methods on four large-scale test datasets comprising 1,820 scans with diverse pathologies. Code and pre-trained models will be made publicly available.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

现有3D医学图像中的病理分割严重依赖有监督学习，但标注数据集仅覆盖少数病理类别（如肺癌、肾肿瘤、肝肿瘤），导致模型无法检测其他常见病理（如气胸）。与此相对，未标注的CT图像（如NLST、AMOS、AbdomenAtlas）数量庞大却未被有效利用。因此，论文旨在开发一种**完全无监督**的病理分割模型，其核心假设是病理模式在CT图像中比健康模式更罕见，从而将问题转化为**无监督视觉异常分割（UVAS）**。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
采用**密度估计框架**，假设健康图像模式分布密集，病理模式位于低密度区域。通过两个模块实现：

- **描述符模型（Descriptor Model）**：使用密集自监督学习（SSL）提取每个体素的特征向量，替代依赖ImageNet预训练或医学任务特定有监督编码器的方法。
- **条件模型（Condition Model）**：学习一种**掩码不变的特征**作为条件变量，替代手工设计的位置编码（如sin-cos编码），使得条件模型能够忽略病理信息（因为病理无法从上下文掩码中可靠推断），从而简化密度模型的估计。

### 关键技术细节
#### 描述符模型
- 架构：U-Net-like，输出高分辨率特征图（分辨率与输入相等）。
- 训练：对随机3D裁剪图进行数据增强（如颜色抖动），提取正样本对（同一位置在不同裁剪中的特征），使用InfoNCE或VICReg目标优化。
- 对比VICReg效果略优于InfoNCE。

#### 条件模型
- 与描述符模型共享相同架构，但训练时额外加入**随机掩码**（masking），并强制条件特征对掩码保持不变（即掩码不变性）。
- 该设计使条件特征仅包含可从上下文推断的信息（如解剖位置、患者年龄），而不包含病理存在与否的信息。

#### 密度模型
- 两种参数化：
  - **高斯模型**：条件高斯，通过MLP预测均值和方差（可用1×1×1卷积实现密集预测）。
  - **归一化流（Normalizing Flow）**：使用Glow层构建可逆映射，支持条件版本（在affine coupling层中注入条件）。
- 训练时最小化负条件对数似然；推理时将全图分割为重叠patch，聚合得到全局异常图。

### 算法流程（文字说明）
1. 预训练描述符模型：在未标注CT上（30,000+ volumes）通过密集SSL训练（VICReg或InfoNCE）。
2. 预训练条件模型：同一数据上，但数据增强包含随机块掩码，训练特征对掩码不变。
3. 训练密度模型：将预训练的描述符和条件模型冻结，在每个位置p取描述符y[p]和条件c[p]，学习条件密度q(y|c)，优化负对数似然。
4. 推理：对新CT图像，分patch提取描述符和条件，计算每个patch的负对数条件密度图，上采样并聚合得到全图异常得分。

## 3. 实验设计

### 数据集
- **训练集**：NLST（25,652 volumes）、AMOS（2,123 volumes）、AbdomenAtlas（4,607 volumes），均为未标注数据（包含各类病理）。
- **测试集**：四个公开数据集，共1,820 scans：
  - LIDC（肺癌，1,017 scans）
  - MIDRC（肺炎，115 scans）
  - KiTS（肾肿瘤，298 scans）
  - LiTS（肝肿瘤，117 scans）

### 基准方法
- 重建类：Autoencoder, f-AnoGAN（3D版本）
- 合成异常类：DRAEM（3D）、MOOD-Top1
- 密度类：MSFlow（基于ImageNet预训练特征+归一化流）

### 评估指标
- 像素级AUROC（整个曲线面积）
- AUROC up to FPR 0.3（低假阳性率下的敏感度）
- AUPRO up to FPR 0.3（proportion-based指标）
- 不采用Dice等指标，因为测试集标注不完整（如MIDRC中气胸未标注），Dice会惩罚检测到未标注的病理。

## 4. 资源与算力

论文明确提及：
- **硬件**：一张NVIDIA RTX H100-80GB GPU。
- **训练时长**：
  - 描述符模型和条件模型各训练300k batches，约3天（共6天）。
  - 密度模型训练500k batches，约3天。
- **总时长**：约6天（两阶段串行，实际可并行）。
- **优化器**：AdamW，学习率warm-up至0.0003，余弦衰减，weight decay 1e-6，梯度裁剪1.0。

## 5. 实验数量与充分性

### 实验组数
- **主实验**：对比6种基线方法×4个数据集，共24组指标（表2）。
- **条件模型消融**：4种条件（无、sin-cos pos、APE、masking-equiv）×2种密度模型（高斯、归一化流）×4个数据集，共32组（表3）。
- **描述符模型消融**：5种描述符（ImageNet+MSFlow、STU-Net、SimCLR、VICReg32、VICReg128）×1种密度模型（归一化流，无条件）×4个数据集，共20组（表4）。
- **定性结果**：图3展示了多组CT切片与异常图。
- **附加分析**：附录E讨论了重建类方法失败原因。

### 充分性评估
- **优点**：消融实验系统，覆盖了方法论中的关键设计（条件源、描述符类型、密度模型复杂度），且在不同病理（肺、肝、肾、肺炎）上验证，具有较好泛化性。
- **局限性**：
  - 未在自然图像异常基准（如MVTec AD）上测试。
  - 仅测试四种病理类型，未覆盖所有常见CT异常（如骨病变、血管疾病）。
  - 训练数据以胸部CT为主（NLST），可能偏向特定解剖区域。
  - 未进行跨数据集泛化测试（如直接用胸部模型测试头部CT）。
- **公平性**：基线方法均实现3D版本，参数调整合理，对比条件明确（MSFlow与Screener均使用归一化流，但特征不同）。消融实验公平比较了相同密度模型下的条件源。

## 6. 主要结论与发现

1. **完全自监督框架有效**：Screener在四个测试集上以较大幅度超越所有基线（如LIDC上AUROC达0.96 vs 次优0.82），证明病理分割可被重新定义为无监督异常检测。
2. **领域特异性自监督特征优于监督特征**：对比ImageNet预训练（MSFlow）和医学任务预训练（STU-Net），自监督VICReg描述符表现最好。
3. **掩码不变条件模型显著提升简单密度模型**：当使用高斯密度时，条件模型带来的提升最为明显（AUROC从0.81提升至0.96）；而使用复杂度高的归一化流时，条件效果减弱，说明简单密度+强大条件可达到类似表现。
4. **大规模未标注数据有效利用**：30,000+ volumes训练出的模型能检测多种类型病理，且能识别标注遗漏的异常（如气胸）。

## 7. 优点

- **方法创新**：
  - 首次将密集自监督学习用于密度UVAS框架，消除对ImageNet预依存的依赖，适应医学图像域差异。
  - 提出**可学习掩码不变条件变量**，将实验设计从手工编码推广到自监督学习，且理论直觉清晰（条件变量应忽略病理信息）。
- **实验设计**：大规模训练（30k+ volumes）、多病理测试（4个数据集）、消融全面（条件、描述符、密度模型），评估指标考虑了真实标注不完整的问题。
- **实践意义**：无需任何标注即可分割多种病理，有潜力作为临床辅助筛查工具。代码和模型已承诺开源，可复现。

## 8. 不足与局限

- **临床相关性偏差**：异常视觉模式未必对应病理（如噪声、金属伪影），可能导致假阳性；反之罕见良性变异可能被遗漏，导致假阴性。
- **数据偏差**：训练集以胸部CT为主（NLST），同样测试的腹部CT（KiTS, LiTS）表现略低于胸部（如AUROC 0.90 vs 0.96），说明对不熟悉解剖区域的泛化受限。
- **计算成本**：两阶段自监督训练总时长约6天（单GPU H100），且需大量内存（80GB），对资源有限的机构不友好。
- **未充分探索多尺度**：论文仅使用单分辨率特征，并未使用特征金字塔或多尺度聚合（仅在附录提及为未来工作）。
- **评估范围局限**：仅针对四种病理类型，未在更广泛异常类型（如骨折、梗死）上验证，且未与有监督模型比较（因不属于无监督设置）。
- **概念验证性质**：作者明确称其为“proof-of-concept”，尚需在更大规模、更多标准化基准上验证。未评估临床实用性指标（如假阳性率/患者）。

（完）
