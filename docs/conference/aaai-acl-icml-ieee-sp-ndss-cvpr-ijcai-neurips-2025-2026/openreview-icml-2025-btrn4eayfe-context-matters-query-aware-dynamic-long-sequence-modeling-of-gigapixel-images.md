---
title: "Context Matters: Query-aware Dynamic Long Sequence Modeling of Gigapixel Images"
title_zh: 上下文重要：面向千兆像素图像的查询感知动态长序列建模
authors: "Zhengrui Guo, Qichen Sun, Jiabo MA, Lishuang Feng, Jinzhuo Wang, Hao Chen"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=BtRn4eayfE"
tags: ["query:cell-path"]
score: 5.0
evidence: 查询感知动态长序列建模用于千兆像素WSI分析
tldr: 针对千兆像素WSI分析中全自注意力的二次复杂度问题，提出Querent查询感知长上下文动态建模框架，在理论上以有界误差逼近全自注意力，同时实现实际效率。该方法在计算病理学应用中展现了潜力，可支持WSI的高效长序列建模。不过其重点在于序列建模效率，而非针对细胞级特征提取。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 850, \"height\": 477}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1724, \"height\": 979}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 774, \"height\": 682}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 834, \"height\": 417}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 854, \"height\": 483}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 857, \"height\": 353}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-btrn4eayfe/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1776, \"height\": 920}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-btrn4eayfe/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1775, \"height\": 856}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-btrn4eayfe/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 583}]"
motivation: 全自注意力在千兆像素WSI上计算复杂度过高，现有降复杂度方法牺牲建模能力。
method: 提出Querent，通过查询感知动态长序列建模实现全自注意力的有界逼近。
result: 在计算病理学任务上权衡效率与建模能力。
conclusion: 为WSI分析提供高效长序列建模方案，是计算病理学的基础性方法。
---

## Abstract
Whole slide image (WSI) analysis presents significant computational challenges due to the massive number of patches in gigapixel images. While transformer architectures excel at modeling long-range correlations through self-attention, their quadratic computational complexity makes them impractical for computational pathology applications. Existing solutions like local-global or linear self-attention reduce computational costs but compromise the strong modeling capabilities of full self-attention. In this work, we propose **Querent**, *i.e.*, the **quer**y-awar**e** long co**nt**extual dynamic modeling framework, which achieves a theoretically bounded approximation of full self-attention while delivering practical efficiency. Our method adaptively predicts which surrounding regions are most relevant for each patch, enabling focused yet unrestricted attention computation only with potentially important contexts. By using efficient region-wise metadata computation and importance estimation, our approach dramatically reduces computational overhead while preserving global perception to model fine-grained patch correlations. Through comprehensive experiments on biomarker prediction, gene mutation prediction, cancer subtyping, and survival analysis across over 10 WSI datasets, our method demonstrates superior performance compared to the state-of-the-art approaches. Codes are available at https://github.com/dddavid4real/Querent.

---

## 论文详细总结（自动生成）

# 论文总结：Context Matters: Query-aware Dynamic Long Sequence Modeling of Gigapixel Images

## 1. 论文核心问题与整体含义

- **研究背景**：全切片图像（WSI）属于千兆像素级图像，通常被切分为海量 patch，给计算病理学中的长序列建模带来巨大挑战。
- **核心问题**：Transformer 的自注意力机制虽然擅长建模长程依赖，但其计算复杂度为二次方，直接应用于 WSI 的 patch 序列时计算代价过高，难以实用。
- **现有方案局限**：局部-全局注意力、线性注意力等方法虽然降低了计算成本，但往往牺牲了全自注意力的强建模能力。
- **整体含义**：论文提出 **Querent**，即 **quer**y-awar**e** long co**nt**extual dynamic modeling framework，目标是在理论上以有界误差逼近全自注意力，同时在实际效率上可行，从而为 WSI 分析提供高效的长序列建模基础方法。

## 2. 方法论

- **核心思想**：让查询（query）动态感知上下文，即对每个 patch 自适应预测其周围最相关的区域，仅针对潜在重要上下文进行注意力计算，而不是对所有 patch 做全量注意力。
- **关键技术细节**：
  - **查询感知的区域重要性估计**：为每个 patch 判断哪些周围区域最值得关注，实现聚焦但不限制范围的注意力计算。
  - **区域级元数据计算**：通过高效的区域级元数据计算和重要性估计，减少冗余计算。
  - **有界逼近**：方法在理论上保证对全自注意力进行有界误差逼近，从而在降低计算开销的同时尽量保留全自注意力的建模能力。
  - **全局感知保留**：尽管注意力计算是选择性的，但仍保留全局感知，以建模细粒度 patch 间相关性。
- **公式或算法流程**：原文摘要未给出具体公式或逐步算法流程。可概括为：
  1. 将 WSI 切分为 patch 序列；
  2. 对每个 patch 作为 query，预测其潜在重要上下文区域；
  3. 仅对重要区域计算注意力；
  4. 利用区域级元数据降低计算成本；
  5. 输出长序列表示用于下游任务。

## 3. 实验设计

- **数据集 / 场景**：论文在 **超过 10 个 WSI 数据集** 上进行实验，覆盖 4 类计算病理学任务：
  - 生物标志物预测（biomarker prediction）
  - 基因突变预测（gene mutation prediction）
  - 癌症亚型分型（cancer subtyping）
  - 生存分析（survival analysis）
- **Benchmark**：以这 4 类任务上的性能作为评估基准，具体数据集名称和指标在摘要中未列出。
- **对比方法**：与 state-of-the-art 方法进行对比，但摘要未列出具体对比方法名称。

## 4. 资源与算力

- 提供的摘要和元数据中 **未明确说明** GPU 型号、GPU 数量、训练时长、显存占用或吞吐量等算力信息。
- 因此无法从当前内容中评估其实际计算资源需求或效率提升的具体数值。

## 5. 实验数量与充分性

- **实验规模**：从摘要看，覆盖 **超过 10 个 WSI 数据集** 和 4 类任务，实验范围较广。
- **元数据旁证**：论文包含 6 张图和 3 张表，可能对应主实验对比、消融实验等，但未提供具体图表内容，无法确认具体实验数量。
- **充分性**：从多数据集、多任务、对比 SOTA 的设计来看，实验框架较为充分；代码公开也增加了可复现性。
- **客观性与公平性**：摘要宣称“优于最先进方法”，但未提供具体指标、统计显著性检验或公平性细节，因此无法从现有信息完全判断客观性。对比方法的实现细节、超参数设置、数据划分方式均未提供。

## 6. 主要结论与发现

- Querent 能够在理论上以有界误差逼近全自注意力，并在实际效率上可行。
- 在生物标志物预测、基因突变预测、癌症亚型分型和生存分析等任务上，Querent 相比现有 SOTA 方法表现出更优性能。
- 该方法为千兆像素 WSI 的高效长序列建模提供了一种有前景的基础方案。

## 7. 优点

- **理论保证**：提供对全自注意力的有界误差逼近，而非单纯启发式降复杂度。
- **查询感知动态建模**：根据每个 patch 的查询需求自适应选择重要上下文，更灵活且保留全局感知。
- **效率与建模能力兼顾**：通过区域级元数据计算和重要性估计，在降低计算开销的同时尽量保留细粒度 patch 相关性。
- **实验覆盖广**：在超过 10 个 WSI 数据集、4 类计算病理学任务上验证。
- **开源可复现**：提供代码链接，有助于后续研究复现和扩展。

## 8. 不足与局限

- **信息缺失较多**：摘要未给出具体公式、算法伪代码、理论误差界形式、数据集名称、对比方法、算力开销等关键细节。
- **无法评估效率真实增益**：未提供 GPU 资源、训练时间、推理时间或内存占用等效率指标，难以判断实际部署价值。
- **实验公平性与稳健性未知**：未报告统计显著性检验、多次实验方差、数据划分策略等，结果稳健性存疑。
- **应用范围较聚焦**：全文围绕计算病理学 WSI 场景，是否适用于其他长序列任务尚未验证。
- **侧重点限制**：元数据指出该方法重点在序列建模效率，而非细胞级特征提取；因此对于需要细粒度细胞特征的病理任务，可能并非直接优化目标。
- **对比细节不足**：仅表述为“优于 SOTA”，但缺少具体对比方法名称和性能差距，难以判断提升幅度。

（完）
