---
title: "SPROUT: Training-free Nuclear Instance Segmentation with Automatic Prompting"
title_zh: "SPROUT: 无训练的自动提示核实例分割"
authors: "Wen Zhang, Qin Ren, Wenjing Liu, Haibin Ling, Chenyu You"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=pqLlFR5ken"
tags: ["query:cellseg"]
score: 9.0
evidence: 利用基础模型和染色先验进行自动提示的无训练核实例分割，用于数字病理
tldr: 核实例分割对数字病理至关重要，但现有方法依赖昂贵标注和微调，计算开销大。SPROUT提出无训练框架，创新性地利用组织学染色先验构建切片特异性参考，自动生成提示用于基础模型分割。实验证明该方法在零样本设定下达到与微调方法可比的性能，且显著降低了计算开销。为病理学细胞分割提供了轻量高效的解决方案，有助于快速部署。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有核实例分割方法依赖大量标注和微调，计算和标注成本高。
method: 利用染色先验构建参考，自动提示基础模型进行无训练分割。
result: 零样本分割性能与微调方法可比，且计算开销显著降低。
conclusion: 为数字病理核分割提供了无需训练的高效框架。
---

## Abstract
Nuclear instance segmentation is a cornerstone task in digital pathology, with broad potential to drive clinical decision-making and accelerate therapeutic discovery. Recent advances in large vision foundation models have shown promise for zero-shot segmentation in biomedical domains. However, most efforts in pathology still rely on pre-trained vision models through fine-tuning or adapter modules. These approaches demand costly annotations and heavy computation, leaving efficient training-free methods largely unexplored.
To this end, we propose SPROUT, a simple yet effective framework for annotation-free prompting. Specifically, we leverage histology-informed stain priors to construct slide-specific references for mitigating domain gaps and instantiate a prototype-guided partial optimal transport scheme to progressively refine nuclear representations. In addition, we embed high-quality positive and negative prompts into the Segment Anything Model (SAM) without any fine-tuning.
Extensive experiments across multiple histopathology benchmark datasets demonstrate that SPROUT achieves competitive performance while requiring neither annotations nor retraining. These results establish SPROUT as a scalable, training-free solution for nuclear instance segmentation in computational pathology. Our codes are available at here.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：数字病理学中的核实例分割是重要的基础任务，对于临床决策和药物发现具有支撑作用。现有方法大多依赖大规模标注数据和模型微调（fine-tuning）或适配器模块，标注成本高昂，且重训计算开销大，因此急需一种无需训练、无需标注的高效分割方案。
- **整体含义**：探索在零样本设定下，利用视觉基础模型（如SAM）进行自动提示的核实例分割，通过引入组织学染色先验和最优传输技术，实现与微调方法竞争的性能，同时避免昂贵的标注和计算开销，为计算病理学提供可扩展的轻量化解决方案。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出SPROUT框架，实现无训练（training-free）、无标注（annotation-free）的自动化提示核实例分割。利用组织学染色先验构建切片特异性的参考信息，并通过原型引导的部分最优传输逐步细化核表示，最终将生成的高质量正负提示嵌入SAM，直接完成分割，无需任何微调。
- **关键技术细节**：
  - **染色先验构建参考（Histology-informed stain priors）**：利用不同染色剂（如H&E）的光学特性与组织着色规律，构造与当前切片高度相关的参考图像/特征，缩小域差异，作为后续提示生成的先验基础。
  - **原型引导的部分最优传输（Prototype-guided Partial Optimal Transport）**：通过构建类别原型，并应用部分最优传输匹配机制，逐步精炼核的视觉表征，自动筛选出可靠的阳性（前景）和阴性（背景）提示区域。
  - **自动提示嵌入SAM**：将上述精炼后的正负像素提示直接输入预训练的Segment Anything Model，在无需微调的条件下输出实例级核分割结果。

### 3. 实验设计：使用了哪些数据集/场景，benchmark是什么，对比了哪些方法

- **数据集**：多个组织病理学基准数据集（文中未逐一列出名称，但提到“across multiple histopathology benchmark datasets”），推测可能包含常见核分割数据集如MoNuSeg、Kumar、CoNSeP或TCGA相关数据集。
- **场景**：零样本核实例分割，即不针对目标数据集进行任何训练或标注调优。
- **benchmark与对比方法**：与依赖微调的分割方法进行对比（具体方法名未给出），以验证无训练方案的可比性能。基线包括需要标注和重训的现有主流核分割模型。

### 4. 资源与算力

- **算力需求**：由于SPROUT为训练无关方法，无需进行模型微调，因此不消耗大规模GPU训练资源。文中摘要强调“无训练”和低计算开销，但未给出具体的推理硬件配置、GPU型号或推理时间数据。从方法论推断，计算成本主要集中在自动提示生成和单次SAM前向推理，所需算力远低于训练范式。

### 5. 实验数量与充分性

- **实验数量**：虽然原文未详细列出表格，但摘要提到“extensive experiments across multiple histopathology benchmark datasets”，可以推断作者在多个数据集上进行了综合评估。可能包括：与全监督/微调方法的性能对比、消融实验验证各组件（染色先验、部分最优传输等）的贡献、不同提示策略的影响等。
- **充分性与客观性**：若实验确实涵盖了多个公开基准并与现有方法公平对比，且消融实验设计完善，则实验较为充分。由于是零样本设定，对比公平性关键在于确保无训练方法不接触目标数据集任何标注信息，文中明确强调“requiring neither annotations nor retraining”，符合公平对比原则。但需要更多细节来验证数据分割、指标一致性和统计显著性。

### 6. 论文的主要结论与发现

- SPROUT在零样本、无训练、无标注的条件下，在多个组织病理学基准数据集上取得了与当前微调方法可竞争的分割性能。
- 组织学染色先验和原型引导部分最优传输是自动生成高质量提示的关键，有效缓解了基础模型在病理图像上的域偏移问题。
- 该框架显著降低了核实例分割任务的门槛，无需昂贵标注和重计算，易于快速部署到不同染色和扫描条件下，具有高可扩展性。

### 7. 优点：方法或实验设计上的亮点

- **训练无关**：完全避免了数据集特定的微调步骤，大幅降低计算开销和对标注的依赖。
- **领域适配创新**：巧妙利用染色先验构建切片特异性参考，是无训练适配病理图像的自然思路。
- **智能提示生成**：通过原型和最优传输机制自动挖掘可靠的正负提示，无需人工交互或手动设计提示。
- **即插即用**：直接驱动现有基础模型（SAM），无需修改模型结构，保证了通用性和易用性。
- **实验对标强**：直接与需要全标注和微调的方法在同基准上对比，验证了无训练方案的实用性。

### 8. 不足与局限

- **染色依赖性**：方法强依赖于标准组织学染色（如H&E）的光谱特性，对于非常规染色或染色质量不佳的切片，构建的参考可能失准，影响提示质量。
- **边界复杂情况**：核密集堆叠、高度重叠或边界模糊区域的实例分割效果文中未专门讨论，可能仍是挑战。
- **实验细节缺失**：摘要未披露具体的数据集规模、评价指标细节以及推理效率数据，无法全面评估普适性和实时性。
- **对比范围可能有限**：未提及与最新的其他无训练分割或聚类方法进行直接比较，可能遗漏同类基线。
- **基础模型限制**：性能上限受限于所选用的基础模型（SAM）的能力，若SAM本身对病理核形态敏感度不足，提示精炼可能无法完全弥补。

（完）
