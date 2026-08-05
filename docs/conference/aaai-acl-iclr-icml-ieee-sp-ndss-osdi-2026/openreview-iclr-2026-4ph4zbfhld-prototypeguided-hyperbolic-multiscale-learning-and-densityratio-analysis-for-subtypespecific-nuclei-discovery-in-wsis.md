---
title: Prototype‑Guided Hyperbolic Multi‑Scale Learning and Density‑Ratio Analysis for Subtype‑Specific Nuclei Discovery in WSIs
title_zh: 基于原型引导的双曲多尺度学习与密度比分析的WSI亚型特异性细胞核发现
authors: "Kazumasa Ohara, Kei Taguchi, Ryoichi Koga, Tatsuya Yokota, Hiroaki Miyoshi, Noriaki Hashimoto, Ichiro Takeuchi, Hidekata Hontani"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=4Ph4ZbfhLd"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 利用多尺度双曲嵌入和密度比分析在WSI中发现诊断相关的细胞核亚型。
tldr: 针对淋巴瘤亚型驱动因素隐藏在细胞核形态变化中的问题，提出自监督框架，将细胞核与组织块联合嵌入双曲空间并利用密度比分析发现亚型特异性细胞核，为诊断提供可解释的细胞级证据。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 淋巴瘤进展表现为多尺度协同形态变化，但现有方法尺度分离且仅用组织级监督。
method: 使用包含感知自监督将细胞核块和组织块联合嵌入庞加莱球，并通过密度比分析发现亚型特异性核。
result: 在淋巴瘤WSI上发现了具有亚型区分能力的细胞核群体。
conclusion: 为病理亚型分析提供了单细胞水平的可解释发现方法。
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
- **研究背景**  
  淋巴瘤的进展表现为从单个细胞核到组织结构的跨尺度协调形态变化。然而，现有分析流程通常用独立模型处理不同尺度，且仅依赖组织级别的监督信号，掩盖了驱动亚型差异的细胞级关键因素。
- **核心问题**  
  如何在无需细胞级标注的情况下，直接从未标注的全切片图像（WSI）中发现具有亚型特异性的细胞核群体，从而为病理亚型判别提供细胞分辨率的可解释证据。
- **整体含义**  
  将细胞核与组织块嵌入同一双曲空间，利用层次包容关系进行自监督学习，使模型能够捕获从细粒度到全局的多尺度形态特征，进而通过密度比分析发现与亚型相关的细胞核表型，弥补了尺度分离与监督信号粗糙的不足。

## 2. 论文提出的方法论
- **核心思想**  
  采用“包容感知的自监督学习”（inclusion‑aware self‑supervision）：将局部细胞核块与包含它的全局组织块联合嵌入一个庞加莱球（Poincaré ball）中。双曲几何天然支持层次结构编码，通过跨尺度对齐损失让细胞核的表示向父级组织区域靠拢，使单一编码器无监督地学到跨尺度特征。
- **关键技术细节**
  - **双曲多尺度嵌入**：使用庞加莱球作为共享嵌入空间，组织切片级特征自然形成反映病灶状态和亚型的簇，而单细胞核独立表达弱，亚型差异主要源于不同核表型的组成比例。
  - **密度比分析**：在嵌入空间中，利用密度比估计发现哪些细胞核表型在某种亚型中富集或稀疏，从而定位亚型特异性的细胞核群体。
  - **自监督目标**：通过最大化局部块与包含它的全局块之间的相似性（可能采用对比或度量学习目标），提供无需人工细胞标签的学习信号。
- **流程概要**  
  采样细胞核块与组织块 → 编码器联合嵌入双曲空间 → 跨尺度对齐训练 → 密度比分析 → 输出单核级别的亚型特异性样本及空间分布模式。

## 3. 实验设计
- **数据集与场景**  
  在淋巴瘤WSI上进行了验证，具体数据集名称、样本数量、亚型种类等信息在提供的摘要及元数据中均未列出。
- **评价基准与对比方法**  
  摘要未提及对比的基准方法。仅说明所提框架能发现具有亚型区分能力的细胞核群体，但缺少与现有细胞级或组织级分析方法的定量比较。
- **评估指标**  
  未提供如亚型分类准确率、发现的特异性细胞核与临床标准的一致性等定量指标，仅定性描述“发现的核群体与组织级亚型结构一致，同时保留细胞分辨率可解释性”。

## 4. 资源与算力
- 摘要及元数据中未明确说明所用的GPU型号、数量、训练时长等算力信息。自监督训练的规模与计算开销无法评估。

## 5. 实验数量与充分性
- **实验组数**  
  基于现有文本，仅描述了一项在淋巴瘤WSI上的实验，未给出消融实验、跨数据集泛化实验、与多种现有方法的对比实验等。
- **充分性评价**  
  实验覆盖面极窄，缺乏定量的对比与消融分析，无法客观判断所提方法的有效性是否优于已有方案，实验充分性不足。

## 6. 论文的主要结论与发现
- 在淋巴瘤WSI上，所提自监督框架成功发现了具有亚型区分能力的细胞核群体。
- 单核单独携带的信息较弱，组织层级的亚型差异主要源自不同普通核表型的组成比例。
- 所提取的核级样本和空间分布模式与组织级亚型结构一致，可为病理诊断提供细胞水平的可解释依据。

## 7. 优点
- **多尺度统一建模**：首次将细胞核与组织块嵌入同一双曲空间，利用包容关系进行自监督，避免尺度分离。
- **层次感知几何**：双曲空间天然适配层次结构，提升了跨尺度特征对齐的自然度。
- **细胞级可解释性**：结合密度比分析，能够指出对亚型区分起关键作用的细胞核亚群，为病理AI提供细粒度证据。
- **无细胞标签要求**：完全自监督，减少了标注负担。

## 8. 不足与局限
- **实验验证有限**：仅在一个病种（淋巴瘤）WSI上定性展示，缺少多中心、多病种的定量评测。
- **缺乏横向对比**：未与现有组织级或细胞级分析方法进行对比，难以判断优势程度。
- **技术细节缺失**：摘要未给出具体的损失函数形式、密度比分析实现方式、编码器结构等，可复现性存疑。
- **应用限制**：该方法依赖组织块与细胞核块的包容关系，对采样策略和WSI预处理可能较敏感，通用性待验证。
- **算力信息不明**：无法评估实际部署的资源需求。

（完）
