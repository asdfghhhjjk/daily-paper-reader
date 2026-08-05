---
title: "SPROUT: Training-free Nuclear Instance Segmentation with Automatic Prompting"
title_zh: SPROUT：基于自动提示的训练无关细胞核实例分割
authors: "Wen Zhang, Qin Ren, Wenjing Liu, Haibin Ling, Chenyu You"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=pqLlFR5ken"
tags: ["query:cellseg"]
score: 8.0
evidence: "无需训练的细胞核实例分割从H&E中提取细胞级信息用于下游任务"
tldr: "针对数字病理中细胞核实例分割依赖成本高昂标注的问题，SPROUT提出一种无需训练的自动提示框架，利用组织学染色先验构建切片特异性参考，结合大视觉基础模型实现零样本分割。在多个数据集上证明了有效性和高效性，为从H&E切片中无监督地提取细胞级信息提供了轻量方案。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有病理细胞核分割方法依赖大量标注和微调，成本高昂。
method: 利用染色先验自动构建提示，结合基础模型实现零样本核分割。
result: 在多数据集上取得有竞争力的分割性能且无需训练。
conclusion: SPROUT为数字病理核分割提供了一种高效、无需训练的新范式。
---

## Abstract
Nuclear instance segmentation is a cornerstone task in digital pathology, with broad potential to drive clinical decision-making and accelerate therapeutic discovery. Recent advances in large vision foundation models have shown promise for zero-shot segmentation in biomedical domains. However, most efforts in pathology still rely on pre-trained vision models through fine-tuning or adapter modules. These approaches demand costly annotations and heavy computation, leaving efficient training-free methods largely unexplored.
To this end, we propose SPROUT, a simple yet effective framework for annotation-free prompting. Specifically, we leverage histology-informed stain priors to construct slide-specific references for mitigating domain gaps and instantiate a prototype-guided partial optimal transport scheme to progressively refine nuclear representations. In addition, we embed high-quality positive and negative prompts into the Segment Anything Model (SAM) without any fine-tuning.
Extensive experiments across multiple histopathology benchmark datasets demonstrate that SPROUT achieves competitive performance while requiring neither annotations nor retraining. These results establish SPROUT as a scalable, training-free solution for nuclear instance segmentation in computational pathology. Our codes are available at here.

---

## 论文详细总结（自动生成）

# 论文详细总结：SPROUT

## 1. 核心问题与研究动机
- **任务背景**：细胞核实例分割是数字病理学的基石任务，对临床决策和药物发现具有重要价值。
- **现状痛点**：
  - 现有方法大多依赖大规模标注数据进行微调（fine-tuning）或插入适配器模块（adapter），标注成本高昂，计算负担重。
  - 尽管大型视觉基础模型（如SAM）在生物医学零样本分割中展现了潜力，但在病理学领域，真正无需训练的零样本方法仍未被充分探索。
- **整体含义**：亟需一种高效、无需标注、无需训练的细胞核分割方案，降低病理图像分析的门槛和成本。

## 2. 方法论
### 2.1 核心思想
SPROUT 提出一种“自动提示框架”，利用组织学染色先验知识构建切片特异性的参考信息，引导分割基础模型（SAM）在没有任何训练或微调的情况下完成细胞核实例分割。

### 2.2 关键技术细节
- **染色先验驱动的自动提示**：
  - 利用H&E染色中细胞核与背景在颜色、形态上的固有差异，自动构建正、负提示（prompts）。
  - 为每一张病理切片生成切片特异性的参考，以避免领域漂移。
- **原型引导的部分最优传输机制**：
  - 采用部分最优传输（Partial Optimal Transport）理论，逐步优化细胞核的表征。
  - 通过原型（prototype）引导，迭代提升核实例的表示质量。
- **与SAM的无缝集成**：
  - 将自动生成的高质量正、负提示直接嵌入SAM，无需进行任何微调或适配，实现真正的零样本分割。

### 2.3 算法流程（文字描述）
1. 输入H&E染色病理切片。
2. 利用染色先验自动提取切片特异性参考，生成初始提示。
3. 通过原型引导的部分最优传输迭代优化提示和核表征。
4. 将最终提示输入到冻存的SAM解码器中，输出细胞核实例分割结果。
5. 整个过程无需训练，不需要任何像素级标注。

## 3. 实验设计
### 3.1 数据集与基准
- 实验覆盖 **多个组织病理学基准数据集**（具体名称摘要未列出），通常应包括不同器官、不同扫描仪、不同染色条件的数据。
- 基准任务为细胞核实例分割。

### 3.2 对比方法
- 摘要未列出具体对比方法，仅提及“competitive performance”表明性能与需要微调的现有方法具有可比性。
- 可能包括基于基础模型微调的方法、基于适配器的方法、以及经典分割方法。

## 4. 资源与算力
- **论文未明确说明** GPU 型号、数量或运行时长。
- 从方法性质推断：由于完全无需训练，SPROUT 在推理阶段的计算消耗相对较低，不需要大规模训练集群，具有轻量高效的特性。

## 5. 实验数量与充分性
- **实验数量**：未给出精确组数，但“多数据集”、“广泛实验”暗示包含：
  - 多个跨中心数据集的横向对比；
  - 消融实验（如验证染色先验、部分最优传输、提示设计等组件的有效性）；
  - 可能包含与训练依赖方法的性能对比。
- **充分性与客观性**：
  - 使用公开的组织病理学基准数据集，保证公平性。
  - 零样本/无需训练的性质避免了不公平的优势（如额外标注或训练）。
  - 但缺少数据集名称和对比方法列表，使得外部可复现性判断受限。
- **潜在偏差**：方法高度依赖染色先验，可能对染色质量不一的真实世界数据敏感。

## 6. 主要结论与发现
- SPROUT 在 **无需任何标注和再训练** 的条件下，取得了与其他需要微调的方法相当的分割性能。
- 证明组织学染色先验结合基础模型强大的零样本能力，可以成为数字病理细胞核分割的可行范式。
- 框架具有 **可扩展性** 和 **易部署性**，为无监督提取细胞级信息提供了轻量化解决方案。

## 7. 优点
- **零标注、零训练**：完全免除昂贵的人工标注和模型微调负担。
- **染色先验的巧妙利用**：将领域知识转化为自动提示信号，填补了“训练无关”方法在病理细分领域的空白。
- **即插即用**：与现有强大基础模型（SAM）自然结合，无需任何架构修改。
- **减轻计算负担**：避免了大规模训练，推理效率高，适合临床快速部署。

## 8. 不足与局限
- **数据集细节缺失**：摘要未列出具体数据集和对比方法，影响对泛化性的精确评估。
- **染色依赖性**：对H&E染色标准化要求较高，若染色不规范（如过染、欠染、伪影），染色先验可能失效。
- **复杂场景的鲁棒性**：未提及对重叠、聚集细胞核、不同细胞类型等复杂情况的表现。
- **性能上限**：虽然“竞争性”，但零样本方法在精度上可能仍低于经过充分微调的专用模型，尤其在高难度样本上。
- **实验覆盖度**：未展示在不同器官、不同病理类型上的系统评估，泛化能力有待更多验证。

（完）
