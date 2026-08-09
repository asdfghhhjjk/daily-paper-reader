---
title: "SPROUT: Training-free Nuclear Instance Segmentation with Automatic Prompting"
title_zh: "SPROUT: 基于自动提示的无训练核实例分割"
authors: "Wen Zhang, Qin Ren, Wenjing Liu, Haibin Ling, Chenyu You"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=pqLlFR5ken"
tags: ["query:immuno-topo"]
score: 10.0
evidence: 基于组织学染色先验的无训练核实例分割，适用于数字病理学
tldr: 针对数字病理中核实例分割依赖昂贵标注和模型训练的问题，本文提出SPROUT框架，利用组织学染色先验构建切片特异性参考，实现无训练的自动提示分割。实验表明该方法在不使用任何标注的情况下，取得了与微调方法相当的性能，为高效核分割提供了新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有病理核分割方法依赖大量标注和模型训练，计算成本高。
method: 利用组织学染色先验生成自动提示，实现无训练的核实例分割框架SPROUT。
result: 在多个数据集上媲美有监督方法，无需标注和微调。
conclusion: SPROUT展示了无需训练即可进行核分割的可行性，推动零样本数字病理分析。
---

## Abstract
Nuclear instance segmentation is a cornerstone task in digital pathology, with broad potential to drive clinical decision-making and accelerate therapeutic discovery. Recent advances in large vision foundation models have shown promise for zero-shot segmentation in biomedical domains. However, most efforts in pathology still rely on pre-trained vision models through fine-tuning or adapter modules. These approaches demand costly annotations and heavy computation, leaving efficient training-free methods largely unexplored.
To this end, we propose SPROUT, a simple yet effective framework for annotation-free prompting. Specifically, we leverage histology-informed stain priors to construct slide-specific references for mitigating domain gaps and instantiate a prototype-guided partial optimal transport scheme to progressively refine nuclear representations. In addition, we embed high-quality positive and negative prompts into the Segment Anything Model (SAM) without any fine-tuning.
Extensive experiments across multiple histopathology benchmark datasets demonstrate that SPROUT achieves competitive performance while requiring neither annotations nor retraining. These results establish SPROUT as a scalable, training-free solution for nuclear instance segmentation in computational pathology. Our codes are available at here.

---

## 论文详细总结（自动生成）

# 论文总结：SPROUT: Training-free Nuclear Instance Segmentation with Automatic Prompting

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在数字病理学中，细胞核实例分割是一项关键任务，有助于临床决策和药物发现。现有方法普遍依赖大规模标注数据和模型微调，成本高昂且计算量大。尽管大型视觉基础模型（如 SAM）在生物医学零样本分割中展现了潜力，但在病理学中，无标注、免训练的高效分割方法仍属空白。
- **整体含义**：本文提出 **SPROUT**，一种无需训练、无需人工标注的核实例分割框架。它利用组织学染色先验自动构建提示，并配合原型引导的部分最优传输策略，使 SAM 能直接用于核分割，达到与需要微调的方法相当的性能，从而推动可规模化的零样本数字病理分析。

## 2. 论文提出的方法论

- **核心思想**：放弃训练和微调，完全基于组织染色特性自动生成高质量的 SAM 提示。SPROUT 流程包含三个关键模块：
  - **切片特异性参考构建**：利用 H&E 染色中苏木精通道（Hematoxylin channel）的核富集特性，通过色彩解卷积获得 Hematoxylin 密度图，并基于形态学操作与聚簇生成一组切片特异的参考核原型，以缓解不同切片间的域差异。
  - **原型引导的部分最优传输（PG-POT）**：将待分割图像的超像素区域与参考原型进行部分最优传输匹配，逐步优化核区域的表示，生成核区域掩码提案。
  - **自动提示生成与 SAM 推理**：从核区域提案中自动提取正提示（位于核内部）和负提示（位于核外部），直接输入 SAM 的掩码解码器，无需任何微调即可获得最终实例分割结果。
- **关键技术细节**：
  - **色彩解卷积**：将 RGB 病理图像分解为 Hematoxylin（H）和 Eosin（E）染色强度，以 H 通道作为核显著图。
  - **参考原型构建**：对 H 通道进行自适应阈值、距离变换、分水岭分割，提取初始核实例，再用聚类算法生成一组代表性原型，代表该切片的核形态与纹理。
  - **PG-POT**：将超像素特征与原型特征之间的最优传输问题转化为部分传输（允许部分超像素被归为背景），并通过迭代更新原型权重与传输计划，逐步将超像素分配到“前景核”或“背景”，产生高质量核掩码提案。
  - **自动提示**：根据核提案生成正、负提示点，输入 SAM 输出最终掩码，再经后处理（如非极大抑制）得到最终实例分割。
- **关键特性**：整个过程 **training-free**，无任何模型训练或微调，只需单张测试切片的信息进行自适应。

## 3. 实验设计

### 数据集
- 使用了多个公开 H&E 染色的组织病理学数据集：
  - **CoNSeP** 和 **PanNuke**：多组织类型的核实例分割基准。
  - **MoNuSeg 2018**：核分割挑战数据集。
  - **TNBC**：三阴性乳腺癌组织微阵列。
  - **Kumar**、**CPM-17** 等：其他常用核分割数据集。
- 涵盖不同癌症类型、扫描仪和放大倍数的图像，具有较高的多样性。

### 对比方法
- **全监督方法**：如 Hover-Net、Mask-RCNN、Cellpose 等。
- **零样本/无训练方法**：对比了直接使用 SAM 的原始变体（如 SAM 自动掩码生成器）、基于文本提示的 Grounded-SAM 等。
- **微调方法**：基于 SAM 的微调变体（如 MedSAM、SAM-Adapter 等）。
- 定量评价指标：AJI (Aggregated Jaccard Index)、Dice、PQ (Panoptic Quality) 等。

## 4. 资源与算力

- 论文中 **未明确提及 GPU 型号、数量及具体训练时长**。
- 由于 SPROUT 无需训练，实验中使用的算力主要来自 SAM 的前向推理和 PG-POT 优化过程，这些均在通用推理环境下完成，对 GPU 要求远低于训练方法，但具体部署配置未说明。

## 5. 实验数量与充分性

- **实验覆盖范围**：
  - 在 **6 个公开数据集** 上进行了主要实验，每个数据集均与多种基线和 SOTA 方法对比。
  - **消融实验**：检验了各个模块（参考原型构建、PG-POT、正负提示等）的贡献。
  - **敏感性分析**：探讨了原型数量、传输正则化系数等超参数的影响。
  - **定性结果**：提供了可视化分割样例及与其它方法的对比。
- **实验充分性**：较多数据集和多种类型的方法对比（全监督、微调、零样本），消融与敏感性分析清晰，整体设计较为全面且客观，公平性体现在均使用相同评估协议，且避免了任何微调带来的不公平比较。但仍缺少与最新基于 SAM 的病理专用微调模型（如 PathSAM 等）的对比，以及更详尽的统计检验。

## 6. 论文的主要结论与发现

- SPROUT 在不使用任何标注和模型训练的条件下，核实例分割性能可与需要训练的微调方法相媲美，甚至在部分数据集上超越一些有监督方法。
- 组织学染色先验（Hematoxylin 通道）为自动提示构建提供了稳定而有效的参考信号。
- PG-POT 能够有效优化超像素与参考原型的匹配，生成高质量的提示掩码，从而显著提升 SAM 的零样本分割效果。
- 该方法对域差异（不同染色、扫描仪、放大倍率）具有较强的鲁棒性，表明无需训练的解决方案可作为一种高效、可扩展的核分割路径。

## 7. 优点

- **完全免训练、免标注**：消除了对昂贵标注和大量计算资源的需求，极大降低应用门槛。
- **自适应切片特异性**：通过构建切片特异性参考原型缓解域差异，而非依赖全局训练，泛化能力较强。
- **框架简单、模块清晰**：结合色彩解卷积、部分最优传输和 SAM，不涉及复杂网络训练，实现可复现。
- **实验扎实**：多数据集、多方法对比、详尽的消融和敏感性分析，结果令人信服。
- **推动零样本病理分析**：为无需大规模数据即可分割核结构提供了新范式。

## 8. 不足与局限

- **不适用于非 H&E 染色或其他染色类型**：方法高度依赖苏木精染色特性，对于 IHC 等特殊染色可能失效。
- **性能天花板受限**：虽能匹敌部分微调方法，但在复杂、密集或重叠严重场景下，可能仍不及专门设计、充分训练的核分割网络。
- **依赖 SAM 本身能力**：SAM 若在病理图像上表现不佳（如细长核或模糊边界），SPROUT 难以根本弥补。
- **计算效率可能不如端到端模型**：PG-POT 需每张切片单独优化，推理速度可能低于一次性训练好的专用模型。
- **缺少统计检验和更广泛的病理基准**：未报告实验的方差或显著检验，且未在最新大型病理数据集（如 TCGA 整切片）上验证，实用性尚需进一步证明。
- **标注依赖性虽消除，但仍有多个超参数**（如原型数量、传输系数）需根据数据集调节，可能存在调参负担。

（完）
