---
title: "Supervise Less, See More: Training-free Nuclear Instance Segmentation with Prototype-Guided Prompting"
title_zh: 监督更少、看到更多：基于原型引导提示的免训练细胞核实例分割
authors: "Wen Zhang, Qin Ren, Wenjing Liu, Haibin Ling, Chenyu You"
date: 2026-04-30
pdf: "https://openreview.net/pdf/c33c4256b9284bf8994f7fdbc763181fbaf0c4b5.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 用于组织病理学的免训练细胞核实例分割框架
tldr: SPROUT针对细胞核实例分割中依赖密集监督和微调的问题，提出完全免训练免标注的提示框架，利用组织学先验构建切片特异的参考原型，在无需训练的情况下实现精确分割，为下游细胞分析提供基础。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有细胞核实例分割依赖密集监督和昂贵微调，训练免标注方法尚未充分探索。
method: 提出SPROUT，利用组织学先验构建切片特异参考原型，以提示方式实现免训练分割。
result: 在无需训练和标注的情况下实现准确的细胞核实例分割。
conclusion: 为计算病理学中的细胞核分割提供了轻量、有效的免训练方案。
---

## Abstract
Accurate nuclear instance segmentation is a pivotal task in computational pathology, supporting data-driven clinical insights and facilitating downstream translational applications. While large vision foundation models have shown promise for zero-shot biomedical segmentation, most existing approaches still depend on dense supervision and computationally expensive fine-tuning. Consequently, training-free methods present a compelling research direction, yet remain largely unexplored. 
In this work, we introduce SPROUT, a fully training- and annotation-free prompting framework for nuclear instance segmentation. SPROUT leverages histology-informed priors to construct slide-specific reference prototypes that mitigate domain gaps. These prototypes progressively guide feature alignment through a partial optimal transport scheme. The resulting foreground and background features are transformed into positive and negative point prompts, enabling the Segment Anything Model (SAM) to produce precise nuclear delineations without any parameter updates.
Extensive experiments across multiple histopathology benchmarks demonstrate that SPROUT achieves competitive performance without supervision or retraining, establishing a novel paradigm for scalable, training-free nuclear instance segmentation in pathology. Code is available at https://github.com/Y-Research-SBU/SPROUT.

---

## 论文详细总结（自动生成）

# SPROUT 论文总结

> **说明**：提供的 PDF 提取文本为 OpenReview 验证页面，未包含论文正文。以下总结仅基于论文标题、摘要及元数据。因此，涉及具体数据集、算力、实验数量、公式等细节无法从现有材料中获取，将在相应部分明确标注。

## 1. 论文的核心问题与整体含义

- **研究背景**：细胞核实例分割是计算病理学中的关键任务，能够为数据驱动的临床判断和下游转化应用提供基础。
- **现有问题**：当前主流方法大多依赖密集标注监督，并且需要昂贵的模型微调；虽然大型视觉基础模型在零样本生物医学分割上展现出潜力，但完全免训练、免标注的方法仍未被充分探索。
- **研究动机**：减少对人工标注和训练算力的依赖，实现可扩展、轻量的细胞核实例分割，是病理图像分析中一个具有现实意义的方向。
- **整体含义**：SPROUT 试图证明，在不进行任何参数更新、不使用任何标注的情况下，通过引入组织学先验和提示机制，也能在细胞核实例分割任务上取得有竞争力的性能。

## 2. 论文提出的方法论

- **核心思想**：SPROUT 是一个完全免训练、免标注的提示框架，利用组织学先验构建切片特异的参考原型，以缩小域差距，并将学习到的前景/背景特征转化为正/负点提示，驱动 SAM 进行分割。
- **关键技术细节**：
  - **组织学先验**：利用病理组织学中关于细胞核形态、分布等的先验知识，为每个切片构建具有特异性的参考原型。
  - **切片特异参考原型**：这些原型用于缓解不同切片、不同数据分布之间的域差距。
  - **部分最优传输**：通过 partial optimal transport 方案，原型渐进地引导特征对齐，使前景和背景特征得到更好的区分。
  - **正/负点提示生成**：将对齐后的前景特征与背景特征分别转换为正点提示和负点提示。
  - **SAM 免训练分割**：将上述点提示输入 Segment Anything Model（SAM），在**不更新任何参数**的情况下输出细胞核实例的精确轮廓。
- **算法流程（文字描述）**：
  1. 输入组织病理图像；
  2. 利用组织学先验构建切片特异性参考原型；
  3. 通过部分最优传输逐步对齐特征；
  4. 从对齐后的特征中提取前景/背景信息，生成正/负点提示；
  5. 将点提示送入 SAM；
  6. SAM 直接输出细胞核实例分割结果，全程无训练、无微调。

## 3. 实验设计

- **数据集 / 场景**：摘要中仅提到“multiple histopathology benchmarks”（多个组织病理学基准），但**未列出具体数据集名称**。因此无法确定是否包含如 MoNuSeg、PanNuke、CoNSeP 等常用数据集，也无法判断覆盖的染色类型或器官类型。
- **Benchmark 类型**：为细胞核实例分割任务，通常涉及分割精度、实例级匹配等指标，但现有材料未给出具体指标名称（如 Dice、AJI、PQ 等）。
- **对比方法**：摘要称 SPROUT “achieves competitive performance without supervision or retraining”，但**未列出具体对比方法**。因此无法得知其与哪些监督方法、零样本方法或 SAM 基线进行了比较。

## 4. 资源与算力

- 现有材料中**未提及任何算力信息**，包括 GPU 型号、数量、训练时长、显存占用等。
- 由于 SPROUT 方法本身是免训练、免微调的，理论上对训练算力需求极低；但推理阶段使用 SAM 仍可能需要一定 GPU 资源，具体资源消耗在现有材料中无法确认。

## 5. 实验数量与充分性

- **无法从现有材料判断实验数量**。摘要仅提到“extensive experiments across multiple histopathology benchmarks”，但没有给出具体实验组数、数据集数量、消融实验细节或统计显著性检验。
- 因此，无法客观评价其实验是否充分、是否公平。要判断这一点，需要论文全文中的实验表格、消融研究、对比基线设置以及误差分析等内容。
- 从摘要的表述看，作者声称进行了广泛实验，但读者需要查阅全文才能验证其充分性和公平性。

## 6. 论文的主要结论与发现

- SPROUT 在**无需监督信号、无需重新训练或微调**的情况下，能够在多个组织病理学基准上取得具有竞争力的细胞核实例分割性能。
- 该方法为计算病理学中的细胞核分割提供了一种**可扩展、轻量、免训练**的新范式。
- 证明了利用组织学先验和提示机制可以有效桥接基础分割模型与病理图像之间的域差距。

## 7. 优点

- **免训练、免标注**：极大降低了数据准备和计算成本，适合资源受限场景。
- **即插即用**：直接利用 SAM 的预训练能力，不需要修改 SAM 参数，部署灵活。
- **利用组织学先验**：引入领域知识构建切片特异原型，体现对病理图像特点的深入理解。
- **部分最优传输机制**：在无需训练的情况下实现特征对齐，具有理论动机。
- **点提示生成方式**：将前景/背景特征转化为正/负提示，使 SAM 能够产生实例级分割，而不仅是语义分割。
- **代码开源**：提供代码链接，有利于复现和后续研究。

## 8. 不足与局限

- **材料不完整**：由于提供的 PDF 提取文本仅为验证页面，无法获取论文全文，因此无法评估具体实验细节、公式正确性、方法实现细节等。
- **依赖 SAM 的预训练能力**：如果 SAM 对病理图像的基础表征不足，方法效果可能受限；但现有材料未报告这一风险。
- **组织学先验的适用范围未知**：切片特异参考原型可能对特定染色、放大倍数或组织类型更敏感，泛化能力需要更多数据验证。
- **竞争性能的具体水平未知**：摘要称“competitive”，但未给出量化结果，无法判断其与强监督方法或最新基线的差距。
- **实例分割精度可能受点提示质量影响**：正/负点提示的生成依赖特征对齐效果，若对齐不佳，可能误导 SAM 产生错误分割；现有材料未提供失败案例分析。

（完）
