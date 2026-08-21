---
title: "MUSE: Multi-Scale Dense Self-Distillation for Nucleus Detection and Classification"
title_zh: MUSE：用于细胞核检测与分类的多尺度密集自蒸馏
authors: "Zijiang Yang, Hanqing Chao, Bokai Zhao, Yelin Yang, Yunshuo Zhang, Dongmei Fu, Junping Zhang, Le Lu, Ke Yan, Dakai Jin, Minfeng Xu, Yun Bian, Hui Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38170/42132"
tags: ["query:cell-path"]
score: 9.0
evidence: 组织病理图像中的细胞核检测与分类自监督方法
tldr: 现有细胞核检测与分类方法依赖大量人工标注，难以充分利用未标注数据。本文提出MUSE，一种多尺度密集自蒸馏方法，核心是NuLo机制：基于预测细胞核位置的坐标引导局部自蒸馏，无需严格空间对齐。该方法在组织病理图像上学习更具判别力的细胞核表示，有望降低标注成本并提升下游病理分析性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 518}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 666}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 579}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1780, \"height\": 519}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 341}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1846, \"height\": 1133}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1846, \"height\": 1135}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 212}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 252}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1820, \"height\": 459}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 625, \"height\": 212}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 626, \"height\": 219}]"
motivation: 现有NDC方法依赖大量昂贵的人工标注，且未能充分利用大规模未标注数据学习判别性表示。
method: 提出MUSE多尺度密集自蒸馏方法，核心NuLo机制基于预测核位置进行坐标引导的灵活局部自蒸馏，无需严格空间对齐。
result: 该方法在组织病理图像上学习到更具判别力的细胞核表示，减少了对人工标注的依赖。
conclusion: MUSE为细胞核检测与分类提供了有效的自监督学习方案，可支撑后续病理分析任务。
---

## Abstract
Nucleus detection and classification (NDC) in histopathology analysis is a fundamental task that underpins a wide range of high-level pathology applications. However, existing methods heavily rely on labor-intensive nucleus-level annotations and struggle to fully exploit large-scale unlabeled data for learning discriminative nucleus representations. In this work, we propose MUSE (MUlti-scale denSE self-distillation), a novel self-supervised learning method tailored for NDC. At its core is NuLo (Nucleus-based Local self-distillation), a coordinate-guided mechanism that enables flexible local self-distillation based on predicted nucleus positions. By removing the need for strict spatial alignment between augmented views, NuLo allows critical cross-scale alignment, thus unlocking the capacity of models for fine-grained nucleus-level representation. To support MUSE, we design a simple yet effective encoder-decoder architecture and a large field-of-view semi-supervised fine-tuning strategy that together maximize the value of unlabeled pathology images. Extensive experiments on three widely used benchmarks demonstrate that MUSE effectively addresses the core challenges of histopathological NDC. The resulting models not only surpass state-of-the-art supervised baselines but also outperform generic pathology foundation models.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：组织病理图像中的细胞核检测与分类（Nucleus Detection and Classification, NDC）是疾病诊断、生物标志物评估和预后预测等高层病理分析的基础任务。
- **核心痛点**：
  - 现有 NDC 方法高度依赖人工标注的细胞核级标签，标注成本极高且耗时。
  - 病理图像通常只标注小视野（约 128 μm）的高倍率切片，样本多样性和组织上下文信息受限。
  - 大规模未标注病理图像未能被充分用于学习判别性的细胞核表示。
- **问题根源**：
  - 通用自监督学习方法（如 DINO、DINOv2）主要面向自然图像或图像级表示，缺乏对细胞核级密集预测任务的自适应。
  - 现有病理基础模型虽然参数量大、预训练数据多，但往往在小视野（如 256×256 像素）上训练，缺乏跨尺度局部对齐能力，细胞核级特征不够判别。
- **整体含义**：论文提出 **MUSE（Multi-scale dense self-distillation）**，一种专门为 NDC 设计的自监督学习方法，旨在从大规模未标注病理图像中学习高质量、多尺度、细胞核级判别表示，从而降低标注依赖并提升下游任务性能。

## 2. 论文提出的方法论

### 2.1 总体框架
- 采用 **DINO 教师-学生自蒸馏**范式：教师网络通过指数滑动平均（EMA）更新，学生网络通过梯度下降优化。
- 在图像级自蒸馏的基础上，引入 **细胞核级局部自蒸馏（NuLo）**，形成多尺度密集自蒸馏。
- 设计轻量灵活的 **编码器-解码器架构**，支持可变输入尺寸（96~1024 像素）和多级特征融合。

### 2.2 架构细节
- **编码器**：基于 ViT，提取多级编码特征 \(F_e\)（共 \(N_e=4\) 层，等间隔选取）。
- **重装配层（Reassembly Layers）**：将编码 token 序列转换为二维特征图，调整通道数和空间尺寸，供解码器使用。
- **解码器**：由残差块组成，逐级融合编码器特征图，输出多个解码特征图 \(F_d\)。
- **最终表示**：
  - 图像级表示：编码器的 CLS token \(f_{cls}\)。
  - 密集表示：解码器输出拼接后的统一特征图 \(f_{map}\)。

### 2.3 数据预处理与多尺度裁剪
- **ROI 裁剪**：从全切片图像（WSI）中先裁剪感兴趣区域（ROI），再在 ROI 上进行多尺度视图裁剪。
- **MPP-Based Cropping**：基于微米每像素（MPP）的物理尺度裁剪，通过随机采样输出 MPP，生成具有指定物理分辨率的视图。公式化定义为：
  \[
  \{I_o, C_o\} = O_{crop}(I_e, C_e; MPP_e, MPP_o, R_o)
  \]
  其中 \(MPP_o\) 随机生成，\(R_o\) 为输出像素分辨率。裁剪后通过坐标无关的索引方案（\(O_{in}\)）唯一标识每个细胞核，实现跨视图核匹配。

### 2.4 NuLo：细胞核级局部自蒸馏
- 对于每个视图，使用编码器-解码器提取 \(f_{map}\)，然后根据细胞核坐标通过 **双线性插值** 获得每个核的特征 \(f_c\)。
- 对于同一 ROI 生成的两个视图，通过核索引交集 \(K_{cap}\) 匹配对应核。
- 损失函数：
  \[
  \mathcal{L}_{nu} = \sum_{K_{cap}} -P_t^{(nu)}(F_c^{(1)}[K_{cap}]) \log P_s^{(nu)}(F_c^{(2)}[K_{cap}])
  \]
  其中 \(P_t^{(nu)}\) 和 \(P_s^{(nu)}\) 分别计算教师和学生输出的概率。
- 该机制**无需严格空间对齐**，允许翻转、尺度变化等增强，支持跨尺度核表示学习。

### 2.5 优化目标
- 总损失：
  \[
  \mathcal{L}_{MUSE} = \lambda_{image}\mathcal{L}_{image} + \lambda_{nu}\mathcal{L}_{nu}
  \]
  实验中 \(\lambda_{image} = \lambda_{nu} = 1\)。
- **LFoV 预训练**：将全局视图和局部视图的分辨率从 224/96 扩展到 512/208 像素，以捕获更大组织上下文。

### 2.6 下游微调
- **LFoV 样本扩展**：将小视野标注区域扩展到大视野样本（如 1024×1024 像素），标注区域可随机出现在样本中。
- **半监督微调**：
  - 对标注区域：使用 MSE 损失回归坐标，交叉熵损失分类类型。
  - 对未标注区域：先用模型生成伪标签，筛选高置信度提议点，施加一致性正则化损失 \(\mathcal{L}_{cons}\)。
- 总微调损失：
  \[
  \mathcal{L}_{ft} = \lambda_{reg}\mathcal{L}_{reg} + \lambda_{type}\mathcal{L}_{type} + \lambda_{cons}\mathcal{L}_{cons}
  \]

## 3. 实验设计

### 3.1 数据集
- **预训练数据**：自建 **TCGA nu**，包含 483,627 个 ROI 补丁，来自 TCGA 项目，细胞核坐标自动检测。
- **下游评估数据集**（3 个广泛使用的基准）：
  - **BRCAM2C**：乳腺癌多类细胞检测，20x 和 40x 放大倍数。
  - **OCELOT**：重叠细胞与组织数据集，20x 和 40x。
  - **PUMA**：黑色素瘤核与组织分割数据集，20x 和 40x。
- **评估任务**：
  - **细胞核分类**：仅需根据给定核坐标预测核类型，使用 KNN、线性探测（LIN）、端到端微调（FT），指标为 ACC（%）。
  - **细胞核检测与分类（NDC）**：预测核位置和类型，使用 F1 分数（分为淋巴细胞、肿瘤核、其他核及平均）。

### 3.2 对比方法
- **通用预训练基线**（基于 ImageNet 等）：
  - DINO（ResNet-50, ViT-S/16, ViT-B/16）
  - MAE（ViT-B/16）
  - iBOT（ViT-S/16, ViT-B/16）
  - DINOv2（ViT-S/14, ViT-B/14）
- **病理预训练模型**：
  - MoCoV2（ResNet-50, TCGA）
  - DINO（ViT-S/16, TCGA）
  - DINOv2（ViT-S/16, ViT-B/16, TCGA nu）
  - CHIEF（Swin-T, custom）
  - CTransPath（Swin-T, custom）
  - CONCH（ViT-B/16, custom，视觉-语言）
  - UNI（ViT-L/16, Mass-100k）
  - Prov-GigaPath（ViT-G/14, custom）
- **监督 NDC 方法**：
  - MCSpatNet、PointNu-Net、SMILE、SENC、CGT、CellViT、DPA-P2PNet

### 3.3 实现细节
- 默认使用 ViT-B/16 编码器，除非另有说明。
- MUSE 支持不同编码器（ResNet-50, ViT-S/16, ViT-B/16），展示灵活性。
- 部分对比方法在 TCGA nu 上重新预训练以进行更公平比较（如 DINOv2）。

## 4. 资源与算力

- 论文正文**未明确提及**所使用的 GPU 型号、数量、训练时长等具体算力信息。
- 仅在“Implementation”部分提到“请参阅 arXiv 扩展版获取详细超参数”，但提供的提取文本中未包含算力细节。
- **因此，无法从当前文本中获知实际训练资源消耗**，需要查阅扩展版或代码仓库。

## 5. 实验数量与充分性

### 5.1 实验组数
- **主要结果表**：
  - 表 1：细胞核分类 FT 结果，对比 8 类预训练方法 × 多架构，在 3 个数据集 × 2 个放大倍数上的表现，共约 30+ 行。
  - 表 2：细胞核分类 KNN 和 LIN 结果，同样大规模对比。
  - 表 3：NDC 的 F1 分数对比，MUSE 与 7 个监督 SOTA 方法在 3 个数据集上比较。
- **消融实验**：
  - 表 4：解码器与多级上下文的影响（3 组）。
  - 表 5：多尺度裁剪的物理分辨率组合（3 组）。
  - 表 6：预训练损失（图像级 vs 核级 vs 组合，3 组）。
  - 表 7：微调组件（LFoV、一致性正则化，3 组）。
- **合计**：主要结果 + 消融约 **10 张表格**，覆盖不同架构、数据集、评估协议和模块。

### 5.2 充分性与客观性
- **充分性**：实验覆盖了 3 个不同组织/癌症类型的数据集，2 种放大倍数，3 种评估协议（KNN、LIN、FT），以及多种模型架构。消融实验系统验证了关键设计（解码器、多级融合、多尺度裁剪、核级损失、微调策略）。
- **客观性**：与最新通用预训练模型和病理基础模型进行了广泛对比；部分模型在相同自建数据集（TCGA nu）上重新预训练以消除数据差异；评估指标统一（ACC、F1），符合领域惯例。
- **公平性**：在与监督 NDC 方法对比时，MUSE 采用相对简单的点基下游流水线，未使用复杂的空间统计或图构建，但性能仍占优，增强了说服力。

## 6. 论文的主要结论与发现

- **MUSE 显著提升细胞核表示学习**：在细胞核分类任务上，MUSE 预训练模型（如 ViT-B/16）在 FT、LIN、KNN 指标上均优于通用自监督模型和多数病理基础模型。
- **数据效率高**：仅使用约 0.5M 未标注补丁，MUSE 即可超越使用数百万甚至数十亿样本的病理基础模型（如 CONCH、UNI、Prov-GigaPath）。
- **LFoV 预训练有效**：扩展预训练视野（512/208 像素）进一步提升性能，LFoV-MUSE 在多个指标上取得最佳结果。
- **NDC 性能优越**
