---
title: "HistoPrism: Unlocking Functional Pathway Analysis from Pan-Cancer Histology via Gene Expression Prediction"
title_zh: "HistoPrism: 通过基因表达预测从泛癌组织学解锁功能性通路分析"
authors: "Susu Hu, Qinghe Zeng, Nithya Bhasker, Jakob Nikolas Kather, Stefanie Speidel"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=6dTHxb9JuA"
tags: ["query:immuno-topo"]
score: 9.0
evidence: "从H&E组织学进行泛癌基因表达预测并用通路级评估"
tldr: "为了实现从H&E组织学图像进行泛癌基因表达预测，HistoPrism采用高效Transformer架构，并引入通路级基准以评估功能相关性。该模型在多个癌症类型中超越现有方法，证明了从组织学预测基因表达通路的可行性，为解析肿瘤生物学提供了新手段。"
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: "从H&E预测基因表达可替代测序，但现有模型泛化性差且缺乏功能评估。"
method: 提出Transformer架构进行泛癌预测，并设计通路级基准。
result: 在通路水平上超越最新方法，展示出跨癌症的泛化能力。
conclusion: HistoPrism为基于组织学的功能基因组学分析提供了可扩展且临床实用的框架。
---

## Abstract
Predicting spatial gene expression from H\&E histology offers a scalable and clinically accessible alternative to sequencing, but realizing clinical impact requires models that generalize across cancer types and capture biologically coherent signals. Prior work is often limited to per-cancer settings and variance-based evaluation, leaving functional relevance underexplored. We introduce HistoPrism, an efficient transformer-based architecture for pan-cancer prediction of gene expression from histology. To evaluate biological meaning, we introduce a pathway-level benchmark, shifting assessment from isolated gene-level variance to coherent functional pathways. HistoPrism not only surpasses prior state-of-the-art models on highly variable genes and, but more importantly, achieves substantial gains on pathway-level prediction, demonstrating its ability to recover biologically coherent transcriptomic patterns. With strong pan-cancer generalization and improved efficiency, HistoPrism establishes a new standard for clinically relevant transcriptomic modeling from routinely available histology.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）  
- **动机**：传统基因表达测序（如空间转录组学）成本高且不易推广，而从常规 H&E 染色组织切片预测基因表达可成为一种可扩展、临床易得的替代方案。然而，现有方法普遍存在两个关键局限：  
  - 模型多针对单一癌症类型训练，跨癌种泛化能力弱；  
  - 评估标准仅关注基因表达值的方差解释度，忽略了所预测信号的生物学功能相关性。  
- **整体含义**：该论文旨在突破上述瓶颈，提出一个能从泛癌 H&E 图像中预测基因表达的模型，并建立以功能通路为导向的评估体系，从而让基于组织学的转录组分析真正走向临床应用，为肿瘤生物学解释提供功能层面的洞察。

## 2. 论文提出的方法论  
- **核心思想**：设计一个高效的 Transformer 架构（HistoPrism），实现输入 H&E 组织学图像、直接输出全基因组基因表达水平的端到端预测，同时引入通路级基准来评估预测结果的生物学一致性。  
- **关键技术细节**（基于给定摘要的合理推导）：  
  - **HistoPrism 模型**：采用 Transformer 作为编码器，利用自注意力机制从整张组织切片中捕获与基因表达相关的形态学特征。模型可能通过图块化（patching）处理大尺寸图像，再聚合为基因表达向量。  
  - **通路级基准**：将基因表达按已知功能通路（如 KEGG、Reactome）聚合为通路活性分数，以通路为单位评估预测值与真实值的一致性，取代传统单基因层面的方差评估。  
  - **训练策略**：在泛癌数据集上联合训练，使模型学习跨癌种共有的转录调控模式，从而提升泛化能力。  
- **算法流程简述**：输入 H&E 图像 → 图像分块与线性投影 → Transformer 编码器提取全局特征 → 输出层映射至基因表达值 → 以基因表达回归损失和通路级损失联合优化。

## 3. 实验设计  
- **数据集与场景**：采用大规模泛癌 H&E 组织学图像及配对的 bulk 或空间转录组数据（原文未指明具体来源，常见的泛癌资源如 TCGA 可能被使用）。  
- **基准（Benchmark）**：论文自行设计了**通路级基准**，将评估重心从基因方差转移到功能通路的重建准确度。  
- **对比方法**：与先前的 state‑of‑the‑art 模型（文中未列出具体名称）在基因级高变基因和通路级两个层面进行比较。  

## 4. 资源与算力  
- 所提供文本（摘要与元数据）中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力细节，因此无法给出具体资源消耗信息。

## 5. 实验数量与充分性  
- **实验数量**：摘要仅概要提及在基因级（高变基因）和通路级进行性能对比，并展示了跨癌种泛化结果，但未给出具体实验组数（如消融实验、不同癌症类型的子实验、超参数研究等）。  
- **充分性评价**：就现有信息而言，实验覆盖了核心的创新点验证（通路级评估与泛化能力），但因缺乏消融研究、数据集规模、统计检验等细节，尚无法完全判断实验的充分性与否。对比是否公平也需查阅完整论文中是否对齐了相同训练条件和评估指标。

## 6. 论文的主要结论与发现  
- HistoPrism 在高变基因预测上超越了现有最优模型，**更关键的是**，在通路级预测上取得了实质性增益，证明其能恢复生物学上连贯的转录组模式。  
- 模型表现出良好的泛癌泛化能力，同时具有更高计算效率，确立了利用常规组织学进行临床相关转录组建模的新标准。  
- 结论：HistoPrism 为基于 H&E 的功能基因组学分析提供了一个可扩展、临床实用的框架。

## 7. 优点  
- **功能导向的创新评估**：首次将通路级基准引入组织学基因表达预测任务，使评估更贴近生物学意义，弥补了单纯方差评估的不足。  
- **架构高效且泛化**：基于 Transformer 的设计兼顾了预测性能和计算效率，并在泛癌场景下验证了跨癌种迁移能力。  
- **临床转化潜力**：直接从常规病理切片推断功能通路，为低资源环境下的肿瘤分子分型、靶向治疗提供了可能。

## 8. 不足与局限  
- **信息披露不完整**：摘要未提供数据集构成、对比方法名称、算力消耗、超参数等细节，影响可复现性与客观评判。  
- **通路基准的局限**：通路定义依赖现有数据库，可能忽略未知调控关系；且通路活性聚合方式可能丢失单基因的精细信息。  
- **应用偏差风险**：若训练数据存在癌种或人群分布不均，模型泛化可能带有偏差；H&E 制片染色差异也易引入 domain shift。  
- **生物学验证缺失**：预测的通路变化是否真实反映肿瘤功能状态，缺乏进一步的生物学实验（如空间转录组、免疫组化）交叉验证。

（完）
