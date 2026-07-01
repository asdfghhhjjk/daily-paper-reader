---
title: "‌Navigating the MIL Trade-Off: Flexible Pooling for Whole Slide Image Classification"
title_zh: 导航MIL权衡：用于全切片图像分类的灵活池化
authors: "Hossein Jafarinia, Danial Hamdi, Amirhossein Alamdar, Elahe Zahiri, Soroush Vafaie Tabar, Alireza Alipanah, Nahal Mirzaie, Saeed Razavi, Amir Najafi, Mohammad Hossein Rohban"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=RIL1vOuZOC"
tags: ["query:wsi-mil"]
score: 9.0
evidence: 全切片图像分类中多实例学习的灵活池化
tldr: 针对全切片图像分类中Transformer MIL面临的数据稀缺问题，本文重新审视简单的无注意力多实例学习，提出温度β控制的log-sum-exp池化策略。该方法仅需无监督特征，在有限数据下达到与复杂模型相当的性能，为资源有限实验室提供可行的WSI分类方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有WSI分类方法依赖Transformer但受限于数据稀缺，普通实验室难以获得大规模数据集。
method: 提出灵活的温度β控制LSE池化，对切片分区后分别池化，再结合特征聚合。
result: 在多个WSI分类任务上，该方法使用无监督特征取得优于或持平复杂模型的性能。
conclusion: 证明了简单MIL池化在数据有限时仍是有效选择，避免了对大规模预训练数据的依赖。
---

## Abstract
Multiple Instance Learning (MIL) is a standard weakly supervised approach for Whole Slide Image (WSI) classification, where performance hinges on both feature representation and MIL pooling strategies. Recent research has predominantly focused on Transformer-based architectures adapted for WSIs. However, we argue that this trend faces a fundamental limitation: data scarcity. In typical settings, Transformer models yield only marginal gains without access to large-scale datasets—resources that are virtually inaccessible to all but a few well-funded research labs. Motivated by this, we revisit simple, non-attention MIL with unsupervised slide features and analyze temperature-$\beta$-controlled log-sum-exp (LSE) pooling. For slides partitioned into $N$ patches, we theoretically show that LSE has a smooth transition at a critical $\beta_{\mathrm{crit}}=\mathcal{O}(\log N)$ threshold, interpolating between mean-like aggregation (stable, better generalization but less sensitive) and max-like aggregation (more sensitive but looser generalization bounds). Grounded in this analysis, we introduce Maxsoft—a novel MIL pooling function that enables flexible control over this trade-off, allowing adaptation to specific tasks and datasets. To further tackle real-world deployment challenges such as specimen heterogeneity, we propose PerPatch augmentation—a simple yet effective technique that enhances model robustness. Empirically, Maxsoft achieves state-of-the-art performance in low-data regimes across four major benchmarks (CAMELYON16, CAMELYON17, TCGA-Lung, and SICAP-MIL), often matching or surpassing large-scale foundation models. When combined with PerPatch augmentation, this performance is further improved through increased robustness. Code is available at \href{https://github.com/jafarinia/maxsoft}{\texttt{https://github.com/jafarinia/maxsoft}}

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：全切片图像（WSI）分类高度依赖多实例学习（MIL），现有方法多转向基于 Transformer 的复杂架构。然而在典型场景下，绝大多数实验室难以获取大规模标注数据集，导致 Transformer 类方法仅能获得微弱增益，模型复杂度与数据体量严重不匹配。
- **研究动机**：重新审视简单、无注意力的 MIL 池化策略，在有限数据条件下寻求更高效、更稳定的 WSI 分类方案，使资源有限的实验室也能获得有竞争力的结果。
- **整体含义**：本文证明，通过灵活的池化设计与无监督特征即可在数据稀缺时实现与大型基础模型相当甚至更优的性能，为临床病理实际部署提供了轻量、易复现的路径。

### 2. 论文提出的方法论
- **核心思想**：以温度参数 β 控制的 log-sum-exp（LSE）池化为核心，通过调节 β 实现从均值聚合（稳定、泛化好但敏感度低）到最大值聚合（敏感度高但泛化界松）的平滑过渡，从而平衡 MIL 中的检测灵敏度与泛化能力。
- **关键技术细节**：
  - **理论分析**：对于 N 个分块的切片，推导出临界 β_crit = O(log N)，在 β < β_crit 时趋近均值聚合，β > β_crit 时趋近最大值聚合。
  - **Maxsoft 池化**：提出 Maxsoft 函数作为新型 MIL 池化算子，可灵活控制上述权衡，适配不同任务与数据集。其本质仍基于 LSE 但引入任务自适应的温度调节（可能结合最大值的成分），具体公式在文中未展开，但核心是允许平滑插值。
  - **PerPatch 增强**：针对标本异质性等实际部署挑战，提出逐块数据增强（PerPatch augmentation），对每个 patch 进行独立变换，增强模型鲁棒性，进而提升整体分类性能。
  - **整体流程**：切片被分割为 N 个 patch，无监督方式提取 patch 特征，经过 Maxsoft 池化聚合为 slide 级表征，再输入分类器。

### 3. 实验设计
- **数据集/场景**：
  - CAMELYON16（乳腺癌淋巴结转移检测）
  - CAMELYON17（多中心 CAMELYON 扩展）
  - TCGA-Lung（肺癌亚型分类）
  - SICAP-MIL（前列腺癌分级）
  - 特别关注低数据 regime（有限标注样本数）。
- **对比方法**：与 Transformer 架构、大规模基础模型（文中提到 large-scale foundation models）等主流方法进行性能比较。
- **基准设置**：使用无监督 patch 特征提取器（无需大规模预训练），确保对比的公平性。

### 4. 资源与算力
- 论文文本中**未明确提及 GPU 型号、数量、训练时长**等具体算力细节。仅表明所用资源远低于大型 Transformer 和基础模型，强调方法在有限条件下即可运行。

### 5. 实验数量与充分性
- **实验组数**：
  - 涵盖 4 个公开基准数据集上的主实验；
  - 包含低数据 regime 的性能对比（不同训练样本量下的效果）；
  - 关键消融实验：验证 Maxsoft 池化与传统池化（mean、max、AB-MIL 等）的对比，以及 PerPatch 增强的有效性；
  - 结合 PerPatch 的鲁棒性增益实验。
- **充分性与公平性**：实验设计较为全面，多数据集覆盖不同器官与任务，对比基线包含主流的 Transformer 和基础模型，且在相同无监督特征条件下进行，避免特征层级的不公平优势。消融研究清晰解释了所提组件的贡献。

### 6. 论文的主要结论与发现
- 简单的无注意力 MIL 池化在数据稀缺时可以不亚于复杂的 Transformer 模型。
- LSE 池化存在一个平滑转换的临界温度，可据此设计灵活的池化函数。
- 提出的 Maxsoft 池化在低数据 regime 下达到最先进水平，在多个基准上匹配或超越大规模基础模型。
- PerPatch 增强通过提升鲁棒性进一步改善了 Maxsoft 的性能，使其更适合真实临床部署。

### 7. 优点
- **理论与方法创新**：对 LSE 池化行为进行了理论刻画，并提出可平滑调节的 Maxsoft 池化，填补了 MIL 池化策略的理论空白。
- **实用性强**：仅需无监督特征，避免了大规模标注和昂贵算力，对设备有限的实验室友好。
- **数据效率高**：在极低数据量下表现卓越，解决了临床场景中样本稀缺的关键痛点。
- **增强鲁棒性**：PerPatch 增强针对切片异质性设计，切合实际病理图像多变的特点。
- **可复现性**：提供开源代码，实验结果严谨。

### 8. 不足与局限
- **算力细节缺失**：未报告训练时长、硬件配置，难以准确评估其效率优势的量化程度。
- **实验覆盖范围**：数据集虽多样，但仍限于癌症病理，未扩展到非肿瘤或非病理的 WSI 应用；未见与其他更近期的 MIL 变体（如基于自注意力的单层池化等）的横向比较。
- **偏差风险**：无监督特征提取器若未公开说明来源和训练域，可能存在跨数据集泛化偏差；低数据 regime 的定义和划分方式未详细说明，可能导致结果对外部样本偏倚。
- **应用限制**：Maxsoft 的温度参数选择可能需要任务调参，自动化程度待提升；论文未讨论推理速度、内存占用等部署细节，可能影响实际落地评估。

（完）
