---
title: Prototype‑Guided Hyperbolic Multi‑Scale Learning and Density‑Ratio Analysis for Subtype‑Specific Nuclei Discovery in WSIs
title_zh: 基于原型引导的双曲多尺度学习和密度比分析的WSI亚型特异性细胞核发现
authors: "Kazumasa Ohara, Kei Taguchi, Ryoichi Koga, Tatsuya Yokota, Hiroaki Miyoshi, Noriaki Hashimoto, Ichiro Takeuchi, Hidekata Hontani"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=4Ph4ZbfhLd"
tags: ["query:profile"]
score: 9.0
evidence: 多尺度双曲空间学习在WSI中发现亚型特异性核，融合细胞和图像块表示用于计算病理。
tldr: 淋巴瘤亚型依赖细胞和组织的协调形态变化，但现有方法分离多尺度建模。本文提出自监督框架，将细胞核局部图像块和其所在的组织全局图像块联合嵌入双曲空间，利用双曲几何捕获层次结构，通过包含感知对比学习统一多尺度表示。在WSI上实验发现亚型特异性核，并利用密度比分析定位关键细胞群体。该方法为从全切片图像中可解释地发现驱动亚型的细胞特征提供了新途径。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 淋巴瘤亚型由跨尺度形态变化驱动，现有方法分离建模，掩盖了细胞级驱动因素。
method: 将细胞核和包含它的组织图像块联合嵌入双曲空间，通过自监督包含感知学习统一多尺度表示。
result: 在WSI中发现亚型特异性核，并通过密度比分析验证其与亚型的关联。
conclusion: 方法提供了从WSI中可解释地发现细胞级亚型形态标志物的新框架。
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

## 1. 论文的核心问题与整体含义

- **研究背景**：淋巴瘤等疾病的亚型分类依赖从单个细胞核到整体组织结构的跨尺度形态变化，但这些尺度的信息在现有计算病理方法中常被分离建模。
- **核心问题**：组织级的亚型判别通常掩盖了细胞级的关键驱动因素；传统监督方法需要昂贵的细胞级标注，难以直接从全切片图像（WSI）中发现具有亚型特异性的细胞核。
- **整体含义**：该工作试图通过一个统一的自监督框架，在不依赖细胞标签的情况下，自动挖掘出驱动亚型差异的细胞核实例，从而为可解释的形态学标志物发现提供新路径。

## 2. 论文提出的方法论

- **核心思想**：将局部核图像块（nucleus patch）和包含它的全局组织图像块（tissue patch）联合嵌入到同一个双曲空间（Poincaré 球）中，利用双曲几何天然表达层次结构的能力，实现包含感知的自监督多尺度学习。
- **关键技术细节**：
  - **包含感知自监督**：训练时，以组织块作为“父区域”，其内部的核块作为“子实例”，设计跨尺度对齐目标，将核表示拉向其所属组织块的表示。
  - **双曲嵌入**：所有表征集映射到 Poincaré 球模型，使得层次化的尺度关系（核 ⊂ 组织）在几何上得到保留。
  - **单编码器统一多尺度**：同一个编码器同时处理不同尺度的图像块，捕获从细胞精细纹理到区域组织构型的特征，无需细胞级标注。
  - **原型引导**（据标题推测，摘要未详细展开）：可能通过原型对比学习或原型分配机制，对核与组织块的聚类结构进行约束，以增强判别性和可解释性。
  - **密度比分析**：在发现核级表征后，利用密度比估计定位具有亚型特异性的关键核群体，量化其与组织亚型的关联。
- **流程简述**：从 WSI 中采样成对的组织块与内部核块 → 输入共享编码器获得双曲嵌入 → 拉近包含关系对的表示 → 在双曲空间形成反映亚型与病灶状态的核/组织聚类 → 通过密度比筛选亚型特异性核。

## 3. 实验设计

- 由于所提供文本仅包含摘要与元数据，**无法获知具体数据集、benchmark 及对比方法**。
- 根据疾病背景可推测使用了淋巴瘤 WSI 数据集，但文中未明确说明其来源、样本量、亚型类别、染色方式等。
- 未提及对比的 baseline 方法（基于摘要判断，可能比较了分离建模的多尺度方法，但无细节）。

## 4. 资源与算力

- 提供的论文摘要与元数据中**没有任何关于算力资源的信息**（GPU 型号、数量、训练时长均未提及）。

## 5. 实验数量与充分性

- 由于仅有摘要，**无法得知具体实验组数**（如不同数据集验证、跨尺度对齐的消融实验、有无双曲空间的对比等）。
- 无法评估实验是否充分、客观与公平；摘要仅给出了定性结论（组织块聚类反映亚型，单核块信息弱，亚型差异来自核表型组成比例等），缺乏定量指标支撑。

## 6. 论文的主要结论与发现

- 组织块（组织级）特征通常已包含足够区分亚型的信息，其嵌入可形成反映病灶状态与亚型的聚类。
- 单个核图像块独立来看携带的亚型信息较弱；组织层面的亚型差异主要源于不同共有核表型的**组成比例变化**，而非存在绝对独有的特殊核类型。
- 所提方法能够产出与组织级亚型结构一致的核级示例和空间分布模式，在保持细胞分辨率的同时提供可解释的亚型特异性核发现。
- 密度比分析有效定位了对亚型判别贡献突出的关键细胞群体。

## 7. 优点

- **统一的跨尺度表示**：用单一模型和同一空间同时处理核与组织尺度，避免分离建模的信息割裂。
- **几何先验的巧妙利用**：双曲空间天然适配层次包含关系，使核与组织的嵌入分布更具结构化。
- **全自监督，无需细胞标签**：大幅降低标注成本，利于在临床 WSI 上快速部署。
- **发现驱动而非预定义**：不是简单分类已知核类型，而是从数据中自动挖掘亚型相关的细胞群，增加了发现新标志物的潜力。
- **强调可解释性**：最终产出空间定位和核级解释，契合计算病理对透明性的需求。

## 8. 不足与局限

- **实验信息严重缺失**：摘要与元数据未提供任何数据量、定量结果、对比方法和统计检验，无法评估实际性能与泛化性。
- **可能的偏差风险**：仅涉及淋巴瘤场景，未提及其他癌症或不同染色条件，方法的普适性存疑；包含关系可能受组织块大小和采样策略影响。
- **技术细节不明**：“原型引导”的具体机制、双曲嵌入的维度与优化策略、密度比分析的具体实现均未在现有材料中展开。
- **应用限制**：依赖准确的核检测前序步骤，若核分割不准可能影响学习；自监督对齐的假设（同块内核应与组织表示相似）可能在肿瘤异质性极大时面临挑战。

（完）
