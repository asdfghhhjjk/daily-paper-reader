---
title: "MAPLE: Multi-scale Attribute-enhanced Prompt Learning for Few-shot Whole Slide Image Classification"
title_zh: MAPLE：面向少样本全切片图像分类的多尺度属性增强提示学习
authors: "Junjie Zhou, WEI SHAO, Yagao Yue, Wei Mu, Peng Wan, Qi Zhu, Daoqiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yHi8Ao6GAe"
tags: ["query:immuno-topo"]
score: 8.0
evidence: 提出用于数字病理少样本全切片图像分类的深度学习方法
tldr: 现有少样本WSI分类方法多依赖切片级提示，忽略组织学实体的亚型特异性表型差异。本文提出多尺度属性增强提示学习框架MAPLE，联合整合局部与全局视觉语义，在多个层级进行预测，有效捕捉细胞核、腺体等关键结构的形态变化，提升癌症诊断的准确性与泛化性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有方法使用切片级提示，无法捕捉亚型特异的组织学实体表型变化，限制癌症诊断性能。
method: 提出层次化框架MAPLE，通过多尺度属性增强提示学习，对齐视觉与文本特征，捕获组织实体的局部与全局语义。
result: 在少样本WSI分类任务上，MAPLE有效提升泛化能力，准确识别亚型特异的组织学差异。
conclusion: 多尺度属性增强提示学习能更好地利用组织学实体信息，为计算病理中的少样本诊断提供新范式。
---

## Abstract
Prompt learning has emerged as a promising paradigm for adapting pre-trained vision-language models (VLMs) to few-shot whole slide image (WSI) classification by aligning visual features with textual representations, thereby reducing annotation cost and enhancing model generalization. Nevertheless, existing methods typically rely on slide-level prompts and fail to capture the subtype-specific phenotypic variations of histological entities (e.g., nuclei, glands) that are critical for cancer diagnosis. To address this gap, we propose Multi-scale Attribute-enhanced Prompt Learning (MAPLE), a hierarchical framework for few-shot WSI classification that jointly integrates multi-scale visual semantics and performs prediction at both the entity and slide levels. Specifically, we first leverage large language models (LLMs) to generate entity-level prompts that can help identify multi-scale histological entities and their phenotypic attributes, as well as slide-level prompts to capture global visual descriptions. Then, an entity-guided cross-attention module is proposed to generate entity-level features, followed by aligning with their corresponding subtype-specific attributes for fine-grained entity-level prediction. To enrich entity representations, we further develop a cross-scale entity graph learning module that can update these representations by capturing their semantic correlations within and across scales.  The refined representations are then aggregated into a slide-level representation and aligned with the corresponding prompts for slide-level prediction. Finally, we combine both entity-level and slide-level outputs to produce the final prediction results. Results on three cancer cohorts confirm the effectiveness of our approach in addressing few-shot pathology diagnosis tasks.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：全切片图像（WSI）在癌症诊断中至关重要，但其像素规模极大、标注昂贵，使得少样本场景下的分类极具挑战。近期，基于预训练视觉-语言模型（VLM）的提示学习（prompt learning）方法通过将视觉特征与文本表示对齐，在少样本 WSI 分类中展现出减少标注成本、提升泛化能力的潜力。
- **核心问题**：现有提示学习方法通常只使用切片级（slide-level）提示，无法捕捉组织学实体（如细胞核、腺体等）在亚型（subtype）层面特异性的表型变异，而这些实体层面的细微差异对癌症精准诊断不可或缺。因此，模型对组织学细节的感知能力受限，诊断性能不足。
- **整体含义**：该工作旨在提出一种多尺度、属性增强的提示学习框架，将局部实体语义与全局切片语义联合建模，从而在少样本条件下更准确地识别癌症亚型特异的组织学变化，为计算病理学提供新范式。

## 2. 方法论

- **核心思想**：构建层次化框架 **MAPLE (Multi-scale Attribute-enhanced Prompt Learning)**，同时利用实体级提示（entity-level prompts）和切片级提示，对齐多尺度视觉与文本特征，实现实体级和切片级联合预测。
- **关键技术细节**：
    - **多尺度提示生成**：首先借助大语言模型（LLM）自动生成两类文本提示：①实体级提示，用于描述多尺度组织学实体及其表型属性（如核异型性、腺体结构等）；②切片级提示，用于捕获全局视觉描述。
    - **实体特征提取与对齐**：设计了一个**实体引导的交叉注意力模块（entity-guided cross-attention module）**，从 WSI 图像特征中提取对应不同实体类型的特征表示，然后将这些实体级视觉特征与各自的亚型特异性属性文本提示进行对齐，实现细粒度的实体级预测。
    - **跨尺度实体图学习**：提出**跨尺度实体图学习模块（cross-scale entity graph learning）**，通过构建实体之间的语义关联图（同一尺度内以及跨尺度），对实体表示进行信息传递与更新，从而丰富实体表征。
    - **聚合与切片级预测**：经过图网络增强后的实体表示被聚合成一个切片级整体表示，并与切片级提示对齐，完成切片级预测。
    - **最终决策**：将实体级输出与切片级输出进行融合，得到最终的分类结果。

- **公式/算法流程（文字描述）**：
    1. 利用 LLM 生成实体级提示集合和切片级提示；
    2. 输入 WSI 图像，经过视觉编码器得到多尺度特征图；
    3. 通过实体引导交叉注意力，为各类型实体提取特征；
    4. 将实体视觉特征与属性提示进行对比学习对齐，计算实体级分类损失；
    5. 构建跨尺度图，使用图神经网络更新实体特征；
    6. 聚合更新后的实体特征为切片表示，与切片级提示对齐，计算切片级分类损失；
    7. 联合实体级和切片级损失训练，推理时综合两者输出得到最终预测。

## 3. 实验设计

- **数据集/场景**：论文在**三个癌症队列**上评估方法，具体癌症类型未在摘要中详述（可能包含不同来源的病理数据）。
- **Benchmark 与对比方法**：任务设定为少样本 WSI 分类。对比对象是**现有依赖切片级提示的方法**，但摘要未列出具体对比方法名称，仅说明“existing methods typically rely on slide-level prompts”。
- **实验指标**：未明确说明，通常应包括准确率、AUC 等分类指标。
- **公平性**：由于缺乏详细对比方法和实验细节，无法判断对比是否绝对公平，但同为少样本 VLM 微调范式下的方法对比，应具有一定可比性。

## 4. 资源与算力

- 摘要及提供的元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力信息，无法从现有材料中获取相关细节。

## 5. 实验数量与充分性

- **实验组数**：至少包括 3 个数据集（3 个癌症队列）上的主实验，加上消融研究（如各模块的有效性验证），以及可能的多尺度、属性增强等组件分析。根据摘要“Results on three cancer cohorts confirm the effectiveness”，可推断实验涉及多个数据源。
- **充分性与客观性**：使用多个独立队列能在一定程度上验证泛化性；但摘要未提供标准差、显著性检验、对比方法的详细结果，因此难以全面评判充分性。从框架设计看，进行了多层次预测和图学习模块的搭配，推测作者进行了相应的消融实验，但信息不完备。

## 6. 主要结论与发现

- MAPLE 通过引入多尺度属性增强提示，能够充分捕捉组织学实体的亚型特异性表型差异，显著提升少样本 WSI 分类性能。
- 在三个癌症队列上的实验结果证实了该方法在少样本病理诊断任务中的有效性与泛化能力。
- 多尺度实体级与切片级联合建模、跨尺度图信息融合，是提升诊断准确率的关键。

## 7. 优点

- **方法创新性**：首次将多尺度实体属性提示引入少样本 WSI 分类，弥补了现有方法仅关注切片全局语义的局限。
- **层次化设计**：从实体级到切片级的联合预测与融合，逻辑清晰，既可捕获细节又兼顾全局上下文。
- **语义利用充分**：利用 LLM 生成丰富、可解释的文本提示，并显式建模实体间的跨尺度语义关联，使视觉-语言对齐更具病理学意义。

## 8. 不足与局限

- **信息缺失**：摘要未提供数据集具体信息、对比方法列表、性能数值等，难以评估其绝对提升幅度及与当前最优方法（SOTA）的比较情况。
- **偏差风险**：不同癌症队列的数据分布、染色差异可能影响结论稳定性，论文如何消除域偏差未提及。
- **应用限制**：
    - 依赖大语言模型生成高质量实体描述提示，在实际部署中可能受限于 LLM 的医学知识覆盖度和可靠性。
    - 多尺度实体检测与属性对齐的计算复杂度可能较高，对大规模 WSI 的推理效率需进一步评估。
    - 未讨论模型在不同染色、扫描仪条件下的鲁棒性，以及扩展到更多癌种的可迁移性。

（完）
