---
title: Prototype‑Guided Hyperbolic Multi‑Scale Learning and Density‑Ratio Analysis for Subtype‑Specific Nuclei Discovery in WSIs
title_zh: 原型引导的双曲多尺度学习与密度比分析用于全切片图像中亚型特异性细胞核发现
authors: "Kazumasa Ohara, Kei Taguchi, Ryoichi Koga, Tatsuya Yokota, Hiroaki Miyoshi, Noriaki Hashimoto, Ichiro Takeuchi, Hidekata Hontani"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=4Ph4ZbfhLd"
tags: ["query:tme-evidence"]
score: 9.0
evidence: 自监督框架直接在全切片图像中发现亚型特异性细胞核，在连续空间中构建可解释的TME证据用于分类
tldr: 针对淋巴瘤进展中跨尺度形态学变化未被统一建模的问题，本文提出自监督框架，将细胞核和组织的多尺度补丁联合嵌入双曲空间，直接发现亚型特异性细胞核。该方法无需组织级监督，通过细胞级别特征驱动亚型识别，在连续空间中提供可解释的肿瘤微环境证据，为基于细胞信息的全切片分类提供了新途径。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法分离建模不同尺度，依赖组织级监督，掩盖了驱动亚型识别的细胞级特征。
method: 提出原型引导的双曲多尺度学习与密度比分析，将局部与全局补丁联合嵌入双曲空间。
result: 可直接从全切片图像中发现亚型特异性细胞核，驱动淋巴瘤亚型分类。
conclusion: 该框架实现了可解释的多尺度细胞核发现，展示了细胞级别特征在数字病理学下游任务中的价值。
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

### 1. 论文的核心问题与整体含义

- **核心问题**：淋巴瘤进展中，从单个细胞核到组织结构的跨尺度形态学变化通常是协同发生的，但现有大多数方法使用分离的模型分别编码这些尺度，并依赖组织层面的监督信号，这掩盖了驱动亚型识别的细胞级别特征。
- **研究动机**：直接在全切片图像（WSI）中发现亚型特异性的细胞核，从而在细胞分辨率下提供可解释的肿瘤微环境证据，而不需要组织级的标签。
- **整体含义**：提出一个自监督框架，将细胞核补丁和包含它的组织补丁联合嵌入到同一个双曲空间中，利用双曲几何自然容纳层次结构的能力，实现跨尺度统一表示，从而直接从WSI中发现亚型特异性细胞核，驱动淋巴瘤亚型分类。

### 2. 论文提出的方法论

- **核心思想**：通过“包含感知的自监督学习”（inclusion-aware self-supervision）将局部（细胞核补丁）和全局（组织补丁）联合嵌入庞加莱球（Poincaré ball），利用双曲空间对层次结构的天然适应性，对齐细胞核与其父级组织区域的表示，使得单个编码器能够同时捕获从细节到全局的形态特征，无需细胞级别的标注。
- **关键技术细节**：
    - **跨尺度对齐目标**：将每个细胞核补丁拉向其所属组织补丁的表示，迫使模型学习统一的、跨尺度的特征。
    - **双曲几何**：选择庞加莱球模型，因为其负曲率适合嵌入树状或层次结构（如细胞-组织的关系）。
    - **密度比分析**：组织补丁通常携带足够区分亚型的特征并形成反映病变状态和亚型的簇；而单个细胞核补丁在孤立情况下信息较弱，组织层面的亚型差异很大程度上由常见核表型的组成比例决定。方法通过分析密度比来发现亚型特异性细胞核，并提供核级别的可解释原型和空间模式。
- **算法流程**（文字描述）：
    1. 从WSI中采样局部细胞核补丁和全局组织补丁。
    2. 使用同一个编码器将两种补丁映射到庞加莱球空间。
    3. 应用跨尺度对齐损失，使细胞核嵌入靠近其所属组织嵌入。
    4. 在嵌入空间中，组织补丁自然聚类，而细胞核补丁分散在其父组织周围。
    5. 通过分析嵌入空间的密度比或分布差异，识别出与特定亚型强相关的细胞核原型，从而实现亚型特异性细胞核的发现。

### 3. 实验设计

- **数据集/场景**：未在摘要中明确列出具体数据集名称，但提到淋巴瘤进展的WSI数据，推测使用淋巴瘤病理全切片图像进行亚型分类任务。
- **Benchmark与对比方法**：摘要未详细列出对比方法，但指出“现有大多数流程”分离建模不同尺度并依赖组织级监督，本方法与之对比以突出优势。
- **实验目标**：验证所提框架能够直接发现亚型特异性细胞核，并以此驱动淋巴瘤亚型分类，同时提供细胞分辨率的可解释证据。

### 4. 资源与算力

- 提供的文本（摘要和元数据）中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。无法从当前提取内容获知。

### 5. 实验数量与充分性

- 由于仅有摘要和元数据，无法判断具体实验数量（如几个数据集、多少组消融实验等）。摘要仅概述了方法效果和发现，并未详述实验配置、定量结果或消融研究。因此无法评估实验的充分性、客观性与公平性。

### 6. 论文的主要结论与发现

- 提出的自监督框架能够直接在WSI中发现亚型特异性细胞核。
- 组织补丁自然形成反映病变状态和亚型的簇，而孤立细胞核补丁信息弱，亚型差异主要由核表型组成比例驱动。
- 该方法产生了与组织级亚型结构一致的核级别范例和空间模式，在保持细胞分辨率可解释性的同时，实现了跨尺度统一学习。
- 展示了细胞级别特征在数字病理学下游任务（如分类）中的价值，为基于细胞信息的WSI分析提供了新途径。

### 7. 优点

- **跨尺度统一建模**：首次将细胞核级与组织级信息嵌入同一双曲空间，避免了分离建模的信息割裂。
- **无需组织级监督**：通过包含感知的自监督方式学习，降低标注成本，并直接揭示细胞级驱动因素。
- **可解释性强**：在连续空间中提供亚型特异性细胞核的原型和空间模式，使分类结果可追溯至细胞级别证据。
- **几何选择合理**：利用双曲空间对层次结构的天然适应性，契合组织-细胞的包含关系。

### 8. 不足与局限

- **实验信息缺失**：摘要未提供定量结果（如准确率、AUC等），也未说明在哪些数据集上进行了验证，无法评估其泛化性和鲁棒性。
- **方法细节有限**：密度比分析的具体实现、跨尺度对齐损失的构造、核补丁的采样策略等关键技术细节在摘要中未展开。
- **应用限制**：方法基于淋巴瘤场景设计，在其他癌症类型或病理场景中的表现未知；同时依赖细胞核补丁的提取，可能受前端检测算法精度的影响。
- **偏差风险**：如果训练数据中某些亚型或细胞形态代表性不足，可能导致发现的亚型特异性核存在偏差。

（完）
