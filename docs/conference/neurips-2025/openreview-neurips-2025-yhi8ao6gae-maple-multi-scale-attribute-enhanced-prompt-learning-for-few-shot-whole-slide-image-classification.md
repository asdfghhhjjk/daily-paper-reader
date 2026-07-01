---
title: "MAPLE: Multi-scale Attribute-enhanced Prompt Learning for Few-shot Whole Slide Image Classification"
title_zh: MAPLE：用于少样本全切片图像分类的多尺度属性增强提示学习
authors: "Junjie Zhou, WEI SHAO, Yagao Yue, Wei Mu, Peng Wan, Qi Zhu, Daoqiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yHi8Ao6GAe"
tags: ["query:profile"]
score: 7.0
evidence: 利用组织学实体的多尺度视觉语义进行少样本全切片图像分类
tldr: 现有少样本全切片图像分类方法忽视组织学实体（如细胞核、腺体）的亚型特异性表型变异，本文提出多尺度属性增强提示学习框架（MAPLE），通过层次化整合多尺度视觉语义，同时从图像块和切片层面进行预测，有效捕捉形态学细节，提升少样本场景下的分类精度，减少了对大量标注的依赖，为数字病理诊断提供高效工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有少样本WSI分类方法依赖切片级提示，忽略关键组织学实体的亚型特异性表型差异，影响诊断准确性。
method: 提出MAPLE框架，层次化整合多尺度视觉语义，同时进行图像块和切片级预测，增强对组织学实体形态特征的建模。
result: 在少样本WSI分类任务上，MAPLE有效捕捉细胞核和腺体等实体的形态变异，显著提升分类性能。
conclusion: MAPLE通过多尺度属性增强提示学习，为少样本病理图像分类提供了高效且可泛化的解决方案。
---

## Abstract
Prompt learning has emerged as a promising paradigm for adapting pre-trained vision-language models (VLMs) to few-shot whole slide image (WSI) classification by aligning visual features with textual representations, thereby reducing annotation cost and enhancing model generalization. Nevertheless, existing methods typically rely on slide-level prompts and fail to capture the subtype-specific phenotypic variations of histological entities (e.g., nuclei, glands) that are critical for cancer diagnosis. To address this gap, we propose Multi-scale Attribute-enhanced Prompt Learning (MAPLE), a hierarchical framework for few-shot WSI classification that jointly integrates multi-scale visual semantics and performs prediction at both the entity and slide levels. Specifically, we first leverage large language models (LLMs) to generate entity-level prompts that can help identify multi-scale histological entities and their phenotypic attributes, as well as slide-level prompts to capture global visual descriptions. Then, an entity-guided cross-attention module is proposed to generate entity-level features, followed by aligning with their corresponding subtype-specific attributes for fine-grained entity-level prediction. To enrich entity representations, we further develop a cross-scale entity graph learning module that can update these representations by capturing their semantic correlations within and across scales.  The refined representations are then aggregated into a slide-level representation and aligned with the corresponding prompts for slide-level prediction. Finally, we combine both entity-level and slide-level outputs to produce the final prediction results. Results on three cancer cohorts confirm the effectiveness of our approach in addressing few-shot pathology diagnosis tasks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：在少样本全切片图像（WSI）分类任务中，现有基于提示学习的方法大多只利用切片级提示，忽视了组织学实体（如细胞核、腺体等）所呈现的亚型特异性表型变异。这种表型差异对癌症精准诊断至关重要，但现有方法无法有效捕捉。
- **整体含义**：为了弥补这一不足，论文提出将多尺度视觉语义信息（实体级与切片级）显式引入提示学习框架，通过属性增强的方式提升模型对关键形态细节的感知能力，从而在降低大量标注依赖的同时，提高少样本病理诊断的准确性与鲁棒性。

### 2. 论文提出的方法论
- **核心思想**：提出**多尺度属性增强提示学习框架 MAPLE**，层次化地整合组织学实体的多尺度视觉语义，并联合进行实体级和切片级预测，以强化对亚型特异性形态特征的建模。
- **关键技术细节与流程**：
  - **提示生成**：
    - 利用大语言模型（LLM）生成**实体级提示**，这些提示对应于不同尺度的组织学实体及其表型属性（如细胞核大小、腺体形状等）。
    - 同时生成**切片级提示**，用于捕捉全局视觉描述（如组织整体结构、肿瘤区域分布等）。
  - **实体级特征提取与对齐**：
    - 设计**实体引导的交叉注意力模块**，从图像块特征中生成实体级特征表示。
    - 将这些实体级特征与对应的亚型特异性属性（文本端）进行对齐，实现 **细粒度的实体级预测**。
  - **特征增强与融合**：
    - 提出**跨尺度实体图学习模块**，构建实体间的图关系，捕捉实体在不同尺度下以及跨尺度间的语义相关性，并据此更新实体表示，从而丰富特征表达。
  - **切片级预测与最终输出**：
    - 将精炼后的跨尺度实体表示聚合为切片级表示，并与切片级提示对齐，进行切片级预测。
    - 最终将实体级输出与切片级输出结合，得到综合的分类结果。

### 3. 实验设计
- **数据集与场景**：
  - 在 **三个癌症队列数据集** 上进行验证（具体癌种未在摘要中详细说明，但应涉及不同癌症类型的WSI）。
  - 实验场景设定为 **少样本WSI分类**，即每类仅有极少量标注样本用于训练。
- **Benchmark 与对比方法**：
  - 基准任务为少样本全切片图像分类性能。
  - 对比方法应为当前主流的基于视觉-语言模型的提示学习方法，以及可能包含其他少样本分类策略，但摘要及元数据中未列出具体方法名称。
- **评价指标**：通常包括分类准确率、AUC、F1-score等，但论文此处未具体说明。

### 4. 资源与算力
- 文本（含摘要与元数据）**未明确提及具体的资源与算力信息**，如使用的GPU型号、数量、训练时长或显存消耗等。

### 5. 实验数量与充分性
- **实验数量**：至少包含在三个不同数据集上的主实验结果，以及可能涉及消融实验、模块有效性验证等，但摘要未提供确切组数。
- **充分性与公平性**：
  - 从结论看，实验从不同癌症队列验证了方法的有效性，基本覆盖了少样本病理诊断的典型场景。
  - 但因缺乏详细的对比方法列表和消融设计描述，**暂时无法从现有信息判断实验是否全面覆盖各类基线、是否完全公平（例如各方法是否采用相同的预训练模型和数据处理）**。

### 6. 论文的主要结论与发现
- MAPLE 通过多尺度属性增强提示学习，能够有效捕捉细胞核、腺体等组织学实体的亚型特异性形态变异。
- 该框架在多个癌症队列的少样本WSI分类任务上取得了显著的性能提升，证明了整合多尺度视觉语义和双重预测的有效性。
- 该方法减少了对大量标注数据的依赖，为开发高效、可泛化的数字病理诊断工具提供了可行方案。

### 7. 优点
- **创新性融合**：首次将组织学实体的多尺度属性信息以提示学习的形式注入视觉-语言模型，弥补了现有方法忽略细微表型差异的不足。
- **双重预测机制**：结合实体级细粒度预测和切片级全局预测，使模型既能关注局部关键形态，又能把握整体组织结构。
- **知识增强设计**：利用LLM生成医学知识驱动的实体属性提示，使文本语义更贴近病理诊断需求；跨尺度图学习模块进一步增强了实体表示的辨别力。
- **临床价值导向**：针对真实病理诊断中的少样本难题，提供了切实可行的解决路径，有望降低对大量像素级标注的依赖。

### 8. 不足与局限
- **细节缺失**：当前提供的信息仅为摘要和元数据，**缺少对对比方法、消融实验设置、超参数、计算开销等细节的具体说明**，难以全面评估方法复杂度和实用性。
- **泛化性证明有限**：实验仅在三个癌症数据集上进行，是否适用于更多种类的肿瘤或非肿瘤性病变、不同制片条件、不同扫描仪等场景尚未验证。
- **潜在误差风险**：LLM生成的医学属性提示可能存在不准确或过度泛化的问题，对病理亚型的覆盖完备性未讨论；实体检测与图构建过程可能引入噪声，但文中未分析此类误差的影响。
- **计算效率未知**：多尺度实体提取和图学习可能增加推理耗时，是否适用于临床实时诊断环境有待检验。

（完）
