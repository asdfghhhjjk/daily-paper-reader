---
title: Prototype‑Guided Hyperbolic Multi‑Scale Learning and Density‑Ratio Analysis for Subtype‑Specific Nuclei Discovery in WSIs
title_zh: 原型引导的双曲多尺度学习与密度比分析用于WSI中亚型特异性细胞核发现
authors: "Kazumasa Ohara, Kei Taguchi, Ryoichi Koga, Tatsuya Yokota, Hiroaki Miyoshi, Noriaki Hashimoto, Ichiro Takeuchi, Hidekata Hontani"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=4Ph4ZbfhLd"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 自监督框架从WSI中挖掘亚型特异性细胞核，基于细胞组成提供可解释的区域选择
tldr: 淋巴瘤进展伴随细胞核与组织结构的多尺度协同变化，现有方法常分离建模且依赖组织级监督，掩盖细胞驱动力。本文提出在双曲空间中将细胞核与组织块联合嵌入的自监督框架，利用包含感知与密度比分析挖掘亚型特异性细胞核，为可解释病理区域挑选和分类提供新型证据。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法分离建模不同尺度，且依赖组织级监督，无法揭示驱动亚型差异的细胞级特征。
method: 利用庞加莱球双曲几何自监督地联合嵌入局部细胞核块与全局组织块，结合密度比分析发现亚型特异核。
result: 在淋巴瘤WSI上成功定位出与亚型密切相关的细胞核，并可解释地关联组织病理模式。
conclusion: 双曲空间的多尺度学习能有效捕捉形态层级变化，为基于可解释特征的区域选择提供新思路。
---

## Abstract
We present a self-supervised framework that discovers subtype-specific nuclei directly from whole-slide images (WSIs) by learning a unified, multi-scale representation in a single hyperbolic space. 
Lymphoma progression manifests as coordinated morphological changes across scales-from individual nuclei to tissue architecture-yet most existing pipelines encode these scales with separate models and rely on tissue-level supervision, which obscures cell-level drivers of subtype identity. 
Our approach replaces this separation with inclusion-aware self-supervision: local crops (nucleus patches) and their containing global crops (tissue patches) are jointly embedded in a Poincaré ball, whose hyperbolic geometry naturally accommodates hierarchical structure. 
A cross-scale alignment objective pulls each nucleus toward the representation of its parent tissue region, enabling a single encoder to capture fine-to-global morphology without cell-level labels. 
Tissue patches sampled from lesions typically carry features sufficient for subtype discrimination and form clusters reflecting both lesional status and subtype. 
By contrast, single-nucleus patches are often weakly informative in isolation and inter-subtype differences at the tissue level largely arise from composition ratios of common nuclear phenotypes. 
This approach yields nucleus-level exemplars and spatial patterns that are consistent with tissue-level subtype structure while preserving interpretability at cellular resolution.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：在淋巴瘤等疾病的全切片图像（WSI）分析中，亚型差异往往源于细胞核形态与组织架构的跨尺度协同变化，但现有方法通常将不同尺度（细胞核块、组织块）分别建模，且高度依赖组织级别的监督信息，导致难以定位驱动亚型区分的细胞级特征，掩盖了亚型特异性细胞核的发现。
- **整体含义**：本文旨在提出一种无需细胞级标签的自监督框架，通过在单一的双曲空间（庞加莱球）中联合嵌入局部细胞核块和包含它的全局组织块，实现多尺度统一表征，从而直接从WSI中发现与亚型相关的细胞核，为病理区域的可解释选择与亚型分类提供细胞层面的证据。

### 2. 论文提出的方法论
- **核心思想**：利用双曲几何天然适合建模层次结构的特性，将细胞核（局部）和组织块（全局）映射到同一个庞加莱球空间，通过跨尺度对齐损失使细胞核的表征靠近其所在组织块的表征，从而让单个编码器同时捕捉精细和全局形态特征。
- **关键技术细节**：
  - **包含感知的自监督学习**：从WSI中采样局部细胞核块（nucleus patches）和包含这些细胞核的全局组织块（tissue patches），构造正样本对（细胞核-其父组织块）。
  - **双曲空间嵌入**：使用庞加莱球作为嵌入空间，该流形的指数增长体积天然适合嵌入具有层次结构的数据（细胞核→组织）。
  - **跨尺度对齐目标**：将每个细胞核块的表征拉向其父组织块的表征，通过对比损失或距离最小化实现，无需细胞级标签。
  - **密度比分析**：在训练后的嵌入空间中，利用组织块通常形成反映病灶状态和亚型的聚类，而单个细胞核块孤立时信息弱，亚型间差异来源于常见核表型的组成比。通过密度比分析，挖掘亚型特异性细胞核（即某些核表型在特定亚型中比例异常高），从而发现亚型特异核实例和空间分布。
- **算法流程（文字说明）**：
  1. 从WSI中随机采样组织块，并从中提取细胞核块（nucleus patch）作为局部视图。
  2. 使用同一编码器分别提取局部块和全局块的特征向量。
  3. 将特征投影至庞加莱球，通过双曲距离度量计算对齐损失，优化编码器使得局部块嵌入接近其全局块嵌入。
  4. 训练完成后，组织块嵌入自然聚为不同病灶/亚型的簇；细胞核嵌入也分布其中。
  5. 对每类亚型，利用密度比估计 (density-ratio) 识别在该亚型中密度显著高于其他亚型的细胞核群，视作亚型特异性核。
  6. 定位这些特异性核在组织空间中的分布，提供可解释的热力图或区域选择依据。

### 3. 实验设计
- **数据集/场景**：论文中明确提到采用淋巴瘤WSI作为实验场景（基于摘要“Lymphoma progression...”），但具体数据集名称、样本量、亚型数等未在提供的文本中详细说明。
- **Benchmark与对比方法**：摘要未列出对比基准，但根据上下文，可能对比了以下类别的方法：
  - 分离建模多尺度的传统病理分析流程（如独立训练细胞核分类器和组织分类器）。
  - 依赖组织级监督的弱监督学习或 MIL 方法。
  - 其他多尺度表示学习方法（如图对比学习、层级对比学习等）。
  因全文不可得，无法给出具体方法名称。
- **评价指标**：可能涉及亚型发现的一致性、特异性核定位的合理性、分类性能等，但未在提供内容中给出。

### 4. 资源与算力
- **算力信息**：提供的文本（元数据和摘要）中未提及 GPU 型号、数量、训练时长或任何算力配置。**无法总结。**

### 5. 实验数量与充分性
- **实验数量**：从摘要和元数据无法推断实施了哪些实验组。预计可能包含：
  - 不同双曲维度的消融实验。
  - 有/无跨尺度对齐的对比实验。
  - 密度比分析的有效性验证（如与随机选择对比）。
  - 多亚型数据集上的定性/定量结果。
- **充分性评价**：因缺少具体实验细节，无法判断实验是否充分和公平。仅从理论框架看，设计理念完整，但实际验证力度未知。

### 6. 论文的主要结论与发现
- 通过在单一双曲空间中联合嵌入局部与全局块，模型无需细胞级标签即可学习到对亚型区分有效的跨尺度表征。
- 组织块嵌入能自然反映病灶状态和亚型；细胞核块嵌入本身弱判别，但组织间差异主要由核表型的组成比率决定，而非单一特异核型。
- 密度比分析成功从嵌入空间中挖掘出与亚型强相关的细胞核范例和空间分布模式，在细胞分辨率上提供了可解释性，为病理区域智能挑选提供了新证据。

### 7. 优点
- **新颖的统一嵌入空间**：巧妙利用双曲几何的层次特性，将多尺度病理结构无缝融合，改变了以往级联或分离建模的范式。
- **完全自监督**：无需任何细胞级标注，降低了大规模应用的门槛，更符合真实临床弱标注场景。
- **可解释性强**：通过密度比分析直接定位亚型特异性细胞核，将黑箱的表示学习与病理生物学解释联系起来，为可信赖AI病理提供了思路。
- **发现层次关系**：揭示了组织亚型差异源于细胞组成比例，而非孤立核形态，这一洞见对生物学研究有启发性。

### 8. 不足与局限
- **实验细节缺失**：未能提供数据集规模、对比基准、定量结果等，削弱了对方法有效性的客观评估。
- **通用性未知**：仅在淋巴瘤WSI上验证，是否适用于其他癌症或非肿瘤组织病理有待考证。
- **细胞核块采样依赖**：方法依赖从组织块中提取核块这一预处理步骤，若细胞核检测/分割精度不高，可能影响性能。
- **双曲空间的调参**：庞加莱球的曲率等超参数可能对嵌入效果敏感，但未提及如何处理。
- **密度比分析的统计稳定性**：对于罕见亚型或样本量少的数据集，密度比估计的可靠性可能不足。
- **与端到端分类的衔接**：虽然发现了特异性核，但如何将这一发现集成到可训练的分类管道或病理报告流程中，未阐述清晰。

（完）
