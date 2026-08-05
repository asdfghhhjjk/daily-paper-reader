---
title: "Cello: A Universal Cell-wise Feature Aggregation framework for  Reliable  Pathology Images Analysis"
title_zh: Cello：面向可靠病理图像分析的通用细胞级特征聚合框架
authors: "Hengrui Lou, Weihan Li, Jiazhen Yang, Lingxiang Jia, Shengxuming Zhang, Linyun Zhou, Xiuming Zhang, Zhenyang Wang, Mingli Song, Zunlei Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0fac7f88f69a8fee60081cbee4e3d07d13b48f75.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 提出一种细胞级特征聚合框架，将细胞表征融入全切片图像建模，实现可靠的病理图像分析。
tldr: 现有计算病理学流水线多依赖斑块级特征提取，偏离病理学家以细胞为核心的推理方式，限制了对微小病变的敏感性。本文提出 Cello，一种通用细胞级特征聚合框架，通过蛋白质信号监督的细胞级学习将细胞表征整合到全切片图像建模中，在吉像素约束下保留细粒度细胞线索，支持局部与全局任务并提供可信证据。实验表明，Cello 在多种病理分析任务中性能优越，为可靠病理图像分析提供了一种统一方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有 WSI 分析忽视细胞级推理，无法捕捉细微病变变化。
method: 提出 Cello，通过蛋白质信号监督的细胞级学习，将细胞表征融入 WSI 建模，支持局部和全局任务。
result: 在多种病理任务上，Cello 展示了细粒度细胞线索对提升分析可靠性的有效性。
conclusion: 细胞级特征聚合是弥补斑块级方法不足、实现可靠病理分析的关键途径。
---

## Abstract
Computational pathology has made progress in diagnosis and prognosis prediction from whole slide images (WSIs), yet pipelines still rely on patch-level feature extraction and aggregation, departing from the cell-centric reasoning used by pathologists.
This gap limits sensitivity to micro-lesions and subtle changes, and current methods rarely provide a unified solution that supports both local and global tasks with trustworthy evidence. We propose Cello, a universal cell-wise feature aggregation framework for reliable pathology image analysis. Cello integrates cell-level representations into WSI modeling via protein-signal–supervised cell-wise learning, preserving fine-grained cellular cues under gigapixel constraints. For local tasks, Cello introduces a flexible prototype-based contrastive module for scalable, task-adaptive representation learning. For global tasks, Cello adopts a weakly supervised gated aggregation that can widely leverage WSI labels. Finally, a cell–local–global decision-route consistency objective dynamically aggregates cellular evidence and aligns local predictions with global outcomes, improving reliability and faithfulness. 
Trained with only hundreds to thousands of samples, Cello achieves performance gains of 3.0%~7.6% and outperforms SOTA pathology foundation models pretrained on tens of thousands of samples. Code is available at https://github.com/HengruiLou/Cello.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前计算病理学中，全切片图像（WSI）分析的主流流程依赖“斑块级（patch-level）特征提取 + 聚合”，这与病理学家以细胞为中心（cell-centric）的推理方式严重背离。
- **冲突与局限**：
  - 斑块级方法难以捕捉细微病灶和微小变化（micro-lesions），导致对早期病变或局部异常不敏感。
  - 现有方法很难同时支持局部任务（如细胞检测、分割）和全局任务（如诊断、预后预测），且缺乏可信任的证据支撑。
- **整体含义**：需要一种能够保留细粒度细胞线索、同时适配多尺度病理任务的统一框架，提升分析的可靠性和临床可解释性。

### 2. 论文提出的方法论

- **核心思想**：提出 **Cello**，一个通用细胞级特征聚合框架，将细胞级别的表征整合入全切片图像建模，以蛋白质信号监督进行细胞级学习（protein-signal–supervised cell-wise learning），从而在吉像素约束下保留细胞细节。
- **关键技术细节**：
  - **细胞级学习**：利用蛋白质表达信号作为监督，学习细胞级别的特征表示，使模型能够感知单细胞形态与分子特征。
  - **局部任务模块**：引入基于原型的灵活对比学习模块（prototype-based contrastive module），实现可扩展、任务自适应的表示学习，适用于细胞分类、分割等局部密集预测。
  - **全局任务模块**：采用弱监督门控聚合（weakly supervised gated aggregation），可以广泛利用全切片级别的弱标签（如诊断类别），进行全局特征聚合。
  - **决策路径一致性目标**：设计 **cell–local–global decision-route consistency** 目标，动态聚合细胞证据，强制局部预测与全局输出对齐，增强模型可靠性和忠实性（faithfulness）。
- **公式/算法流程（文字说明）**：
  1. 以蛋白质信号监督预训练细胞级特征提取器。
  2. 对WSI中的细胞进行特征提取，得到细胞级嵌入。
  3. 局部任务：用原型对比学习对细胞嵌入进行自适应聚合与分类。
  4. 全局任务：通过可学习的门控机制将所有细胞嵌入聚合成整张WSI的特征，并用弱监督（仅WSI标签）训练。
  5. 联合优化时，加入一致性损失，使细胞证据、局部预测和全局决策路径一致。

### 3. 实验设计

- **数据集/场景**：
  - 摘要未列出具体数据集名称，但从上下文可推断涉及多个公开病理学基准数据集，用于诊断分类、预后预测、病灶分割等任务。
  - 训练仅需“数百到数千个样本”，相较于需要数万样本预训练的基础模型，样本效率极高。
- **Benchmark 与对比方法**：
  - 对比对象为当前先进的病理基础模型（SOTA pathology foundation models），这些模型在数万张病理图像上预训练。
  - 对比任务包括局部任务和全局任务，覆盖多种病理分析场景。
- **主要指标**：性能提升幅度为 **3.0% ∼ 7.6%**，表明Cello在全切片分析任务上的一致性优势。

### 4. 资源与算力

- 提供的论文摘要和元数据中 **未明确说明** 使用的GPU型号、数量、训练时长或具体的算力消耗。
- 从方法设计看，模型利用细胞级特征，相比斑块级大型Transformer可能会降低计算量，但缺乏确切数据。

### 5. 实验数量与充分性

- **实验数量推断**：摘要没有给出具体的实验表格数量，但提到与多个SOTA病理基础模型对比，以及同时支持局部和全局任务，暗示至少覆盖若干数据集、多种任务组合。
- **充分性与客观性**：
  - 方法声称在多种任务上均取得显著提升，并强调仅需少量样本训练，实验结果具有跨任务的泛化性。
  - 对比的是数万样本预训练的基础模型，避免了不公平的预训练数据量优势，对比相对公平。
  - 消融实验未在摘要中体现，但核心模块（细胞学习、原型对比、门控聚合、一致性损失）应各有消融验证（需查看原文）。

### 6. 论文的主要结论与发现

- 将细胞级特征整合进WSI建模可以有效弥补现有斑块级方法的局限性。
- 通过蛋白质信号监督的细胞级学习，可以在吉像素尺度下保留细粒度信息。
- **Cello** 在只用几百到几千样本训练的情况下，性能超越在数万样本上预训练的病理基础模型，证明了细胞中心表示的高效性与强泛化能力。
- 提出的 cell–local–global 一致性机制提升了模型的可信性与证据追溯能力。

### 7. 优点

- **创新性强**：回归病理学家“细胞中心”范式，为计算病理学提供全新的特征聚合视角。
- **统一性**：同时支持局部和全局病理任务，改变了以往需要两套独立流水线的做法。
- **高效样本利用**：仅需少量标签数据即可达到极强性能，大幅降低标注成本。
- **可解释性提升**：一致性目标和细胞证据聚合让模型的决策路径更透明，符合可靠AI的需求。
- **对比公平**：与大量样本预训练的基础模型比较，且性能占优，说服力强。

### 8. 不足与局限

- **细节缺失**：摘要未提供具体数据集、消融实验、算力成本和训练耗时，难以判断实际落地可行性。
- **蛋白质依赖**：细胞级学习需要蛋白质信号监督，可能限制在没有此类多组学数据的场景中的推广。
- **泛化风险**：仅提及性能提升百分比，未讨论不同癌症类型、不同扫描仪、不同染色条件下的鲁棒性。
- **应用限制**：虽然统一了局部和全局任务，但实际临床部署中需要处理更大规模的WSI，计算效率与吞吐量未知。
- **评估偏差**：与预训练基础模型的比较可能存在领域差异，预训练数据规模巨大，但可能未针对特定任务微调，对比的公平性需进一步审视。

（完）
