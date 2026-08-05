---
title: "SPROUT: Training-free Nuclear Instance Segmentation with Automatic Prompting"
title_zh: SPROUT：无需训练的自动提示细胞核实例分割
authors: "Wen Zhang, Qin Ren, Wenjing Liu, Haibin Ling, Chenyu You"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=pqLlFR5ken"
tags: ["query:tme-evidence"]
score: 8.0
evidence: 无需训练的细胞核实例分割，符合细胞分割需求。
tldr: 针对数字病理中细胞核实例分割依赖昂贵标注和计算资源的问题，提出无需训练的SPROUT框架，利用组织学染色先验构建幻灯片特定的参考信息，自动生成提示以驱动基础模型进行零样本分割。该方法不仅避免了大规模标注需求，还显著降低了计算开销，为数字病理分析提供了一种高效、便捷的分割工具，有望加速病理学研究和临床应用。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 数字病理中细胞核实例分割的标注成本高且计算量大，现有方法依赖微调或适配器模块。
method: 利用组织学染色先验构建幻灯片特定参考，自动生成提示，驱动基础模型进行零样本分割。
result: 无需训练即可实现有效的核实例分割。
conclusion: SPROUT为数字病理提供了一种高效、免标注的分割方案，有潜力推动临床应用。
---

## Abstract
Nuclear instance segmentation is a cornerstone task in digital pathology, with broad potential to drive clinical decision-making and accelerate therapeutic discovery. Recent advances in large vision foundation models have shown promise for zero-shot segmentation in biomedical domains. However, most efforts in pathology still rely on pre-trained vision models through fine-tuning or adapter modules. These approaches demand costly annotations and heavy computation, leaving efficient training-free methods largely unexplored.
To this end, we propose SPROUT, a simple yet effective framework for annotation-free prompting. Specifically, we leverage histology-informed stain priors to construct slide-specific references for mitigating domain gaps and instantiate a prototype-guided partial optimal transport scheme to progressively refine nuclear representations. In addition, we embed high-quality positive and negative prompts into the Segment Anything Model (SAM) without any fine-tuning.
Extensive experiments across multiple histopathology benchmark datasets demonstrate that SPROUT achieves competitive performance while requiring neither annotations nor retraining. These results establish SPROUT as a scalable, training-free solution for nuclear instance segmentation in computational pathology. Our codes are available at here.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：数字病理学中的细胞核实例分割任务高度依赖昂贵的像素级标注和大量计算资源（微调或适配器模块），零样本、无需训练的方法尚未被充分探索。
- **研究动机**：降低标注成本、减少计算开销，使细胞核分割在临床和研究中更易于部署。
- **整体含义**：提出一种无标注、无训练的框架，利用组织学染色先验自动生成提示，驱动基础模型实现零样本分割，为计算病理学提供可扩展的解决方案。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：利用苏木精-伊红（HE）等染色先验构建幻灯片特定的参考信息，通过自动提示生成机制，使Segment Anything Model（SAM）在无需微调的情况下完成细胞核实例分割。
- **关键技术细节**：
  - **染色先验构建参考**：从组织学染色特征（如颜色通道特性）提取幻灯片级别的参考统计信息，缩小不同数字切片之间的域差距。
  - **原型引导的部分最优传输**：设计一种逐步优化细胞核表示的方法，利用部分最优传输原理对核特征进行对齐和细化。
  - **正负提示自动嵌入**：通过自动生成的提示（正提示指向核区域，负提示指向非核区域）直接输入SAM，驱动分割，无需任何模型重训。
- **整体流程**：输入切片→染色先验生成参考→部分最优传输表示优化→提示生成→SAM零样本分割→实例输出。

### 3. 实验设计：使用的数据集、基准、对比方法
- **数据集**：多个组织病理学基准数据集（具体名称摘要未列出，通常包括MoNuSeg、CoNSeP、PanNuke等常用核分割数据集）。
- **基准任务**：细胞核实例分割（nuclear instance segmentation）。
- **对比方法**：与依赖微调或适配器的预训练视觉模型方法进行对比（文中未列出具体名称，推断为当前零样本或弱监督分割方法及全监督的SOTA方法）。
- **评估指标**：虽未在摘要中详述，通常核实例分割采用Dice系数、AJI、PQ等。

### 4. 资源与算力
- **已说明部分**：摘要强调“无需训练”（training-free），因此无需大量GPU资源进行微调或适配。
- **未明确说明**：未提及推理阶段的具体硬件（GPU型号、数量）及推理耗时，也未给出参考生成或提示构建的计算开销数据。

### 5. 实验数量与充分性
- **实验数量**：摘要声称在“多个组织病理学基准数据集”上进行了广泛实验，且结果具有竞争力，推测包含了多个数据集上的对比实验和相应的消融实验（如染色先验、部分最优传输、提示设计等组件对性能的影响）。
- **充分性与公平性**：若实验能覆盖常用的公开核分割数据集并与当前主流方法公平对比（相同指标、相同数据划分），则实验较为充分。摘要未报告统计显著性检验或交叉验证细节，无法完全评价公平性。

### 6. 论文的主要结论与发现
- SPROUT在无需任何标注和模型重训的条件下，取得了与有监督或需微调方法相当的性能。
- 结果证明基于染色先验的自动提示方法能有效缩小域差距，推动基础模型在生物医学领域的零样本应用。
- SPROUT作为一种可扩展、无需训练的解决方案，可为数字病理学提供高效、低成本的分割工具。

### 7. 优点：方法或实验设计上的亮点
- **全免训练与免标注**：完全摆脱对大规模标注数据和微调GPU资源的依赖，应用门槛低。
- **染色先验注入**：利用组织学染色固有的物理先验缩小域差异，比通用预训练模型更贴合病理数据特性。
- **自动提示机制**：无需人工设计提示，自动化程度高，便于大规模处理。
- **基于部分最优传输的表示优化**：将特征对齐建模为最优传输问题，设计新颖，可能提高分割稳定性和质量。
- **与SAM无缝对接**：直接利用现有大模型的分割能力，充分挖掘基础模型的潜力。

### 8. 不足与局限
- **实验覆盖的局限性**：
  - 摘要未提及不同染色类型（如免疫组化、细胞学）或不同扫描仪产生的图像上的泛化性，可能存在域敏感问题。
  - 缺乏对更大规模、真实临床工作流下的验证（如多中心数据、实际诊断流程中的鲁棒性）。
- **偏差风险**：
  - 若“组织学染色先验”主要针对HE染色设计，在特殊染色或异质性强的样本上效果可能下降。
  - 提示生成策略可能受图像伪影、染色批间差异影响而引入错误提示。
- **应用限制**：
  - 依赖SAM模型，其本身的泛化性和模型大小可能在资源有限的场景下限制部署。
  - 摘要未给出计算时间开销，可能推理速度不如专门的轻量级模型。
- **实验充分性**：若对比方法未包含最新的零样本或弱监督核分割方法，或未进行跨器官/跨中心的严格测试，结论的普适性有待验证。

（完）
