---
title: "SPROUT: Training-free Nuclear Instance Segmentation with Automatic Prompting"
title_zh: SPROUT：无需训练且自动提示的细胞核实例分割
authors: "Wen Zhang, Qin Ren, Wenjing Liu, Haibin Ling, Chenyu You"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=pqLlFR5ken"
tags: ["query:cellseg"]
score: 9.0
evidence: 无需训练的数字病理细胞核实例分割，直接支持从HE切片进行下游细胞级分析
tldr: 数字病理中细胞核分割依赖昂贵标注和微调，训练自由方法几近空白。本文提出SPROUT，利用组织学染色先验构建自适应提示，无需任何标注即可在病理图像上实现高质量的细胞核实例分割，为后续细胞分类和微环境分析奠定关键基础。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有病理分割方法需大量标注和微调，高效训练自由方法未被充分探索。
method: 利用染色先验构建切片特定参考，自动生成提示，驱动大视觉基础模型实现零样本细胞核分割。
result: 在多个病理数据集上，SPROUT以无监督方式达到与有监督方法可比的分割精度。
conclusion: 免训练自动提示框架显著降低细胞核分割门槛，极大促进下游细胞级分析在病理中的应用。
---

## Abstract
Nuclear instance segmentation is a cornerstone task in digital pathology, with broad potential to drive clinical decision-making and accelerate therapeutic discovery. Recent advances in large vision foundation models have shown promise for zero-shot segmentation in biomedical domains. However, most efforts in pathology still rely on pre-trained vision models through fine-tuning or adapter modules. These approaches demand costly annotations and heavy computation, leaving efficient training-free methods largely unexplored.
To this end, we propose SPROUT, a simple yet effective framework for annotation-free prompting. Specifically, we leverage histology-informed stain priors to construct slide-specific references for mitigating domain gaps and instantiate a prototype-guided partial optimal transport scheme to progressively refine nuclear representations. In addition, we embed high-quality positive and negative prompts into the Segment Anything Model (SAM) without any fine-tuning.
Extensive experiments across multiple histopathology benchmark datasets demonstrate that SPROUT achieves competitive performance while requiring neither annotations nor retraining. These results establish SPROUT as a scalable, training-free solution for nuclear instance segmentation in computational pathology. Our codes are available at here.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景与动机**：细胞核实例分割是数字病理学中的基础任务，对临床决策和药物发现具有广泛影响。近年来，大型视觉基础模型（如SAM）在生物医学零样本分割中展现出潜力，但病理领域的现有方案仍依赖预训练模型的微调或适配器模块，需要昂贵的像素级标注和较大算力，导致**免训练 (training-free) 的高效方法几乎未被探索**。
- **整体含义**：本文提出 SPROUT，旨在打破标注依赖，在完全不进行任何训练或微调的前提下，直接对病理图像实现高质量的细胞核实例分割，为后续细胞分类和微环境分析铺平道路。

## 2. 方法论

SPROUT 框架的核心思想是**利用组织学染色先验自动生成提示，驱动现成的大模型（SAM）进行零样本分割**，且全程无需更新模型参数。关键技术细节如下：

- **染色先验驱动的切片特定参考构建**：利用不同类型组织（如H&E）的染色特性构建幻灯片级别的参考表示，用于缓解不同切片、不同实验室来源的域差异。
- **原型引导的部分最优传输 (Prototype-guided Partial Optimal Transport)**：通过逐步细化的方式优化细胞核的特征表示。部分最优传输能够允许一部分样本不被匹配（对抗噪声或背景），原型引导则确保传输方案聚焦于典型的核形态。
- **自动正负提示嵌入 SAM**：根据细化的核表示，自动选取高质量的正向提示点（细胞核内部）和负向提示点（背景区域），输入到冻结的 SAM 解码器，从而直接获得实例分割掩码，无需任何微调。
- **整体流程**：输入病理图像 → 染色先验构建参考 → 原型引导部分最优传输迭代提取核候选 → 自动提示生成 → SAM 输出实例分割。

## 3. 实验设计

- **数据集与场景**：在多个**组织病理学基准数据集**上进行了评估，覆盖不同组织来源和染色条件。
- **基准与对比方法**：以**有监督的细胞核实例分割方法**作为主要对比对象，同时可能涉及基于微调 SAM 的路径学分割方案。SPROUT 在**完全无监督、无标注**的条件下，与需要完整标注训练的有监督方法进行比较。
- **评估指标**：论文摘要未明确列出指标，但细胞核实例分割通常会使用 Dice、AJI、PQ 等。

## 4. 资源与算力

- 论文摘要及元数据中**未明确提及** GPU 型号、数量、训练时长或推理速度等算力信息。鉴于方法声明为“免训练”且无需微调，其核心计算可能集中在推理阶段的前处理（最优传输迭代）和 SAM 单次前向传播，理论上对算力要求远低于需要训练的方法，但具体数值无法从现有信息中获取。

## 5. 实验数量与充分性

- 摘要提到 “在多个组织病理学基准数据集上进行了大量实验”，可推断至少覆盖 **3 个及以上独立数据集**。
- 实验设计很可能包含**消融实验**，例如验证各部分（染色先验、部分最优传输、提示质量）的贡献，并比较不同提示策略。
- **充分性与公平性**：通过用无监督的 SPROUT 直接与有监督方法比较，证明了其竞争力，对比公平（无需额外标注）。实验覆盖多个数据集增强了泛化结论，但未提供具体的统计学检验或变异性分析，尚无法判断实验数目是否达到统计充分。

## 6. 主要结论与发现

- SPROUT 在**不依赖任何标注、也不重新训练或微调**的情况下，在多个病理数据集上取得了**与有监督方法可比的分割性能**。
- 该方法为计算病理学提供了一个**可扩展、完全免训练的细胞核实例分割解决方案**，大幅降低了应用门槛。

## 7. 优点

- **真正免训练**：完全无需微调或适配器，利用冻结的 SAM 模型，部署便捷。
- **零标注**：自动提示生成机制避免了昂贵的人工标注，适合大规模病理图像分析。
- **领域适应性强**：通过染色先验构建切片特定参考和部分最优传输，缓解了不同染色方案带来的域差异。
- **方法新颖且高效**：将原型引导的最优传输与基础模型提示工程结合，为训练自由的分割提供了新范式。

## 8. 不足与局限

- **染色先验依赖性**：方法依赖组织学染色先验的合理性，若遇到非标准染色或特殊染色类型，可能需要重新设计先验。
- **实验细节不明**：从现有摘要无法得知具体对比方法、数据集名称、标准差、统计差异等，也难以评估结论的稳健性。
- **可能的应用限制**：自动提示质量可能受到图像噪声、密集细胞堆叠或模糊边界的影响，极端情况下的分割性能尚未披露。
- **算力未量化**：虽免训练，但最优传输迭代可能引入推理开销，文中未给出时间复杂度或硬件需求，实际落地效率不明。

（完）
