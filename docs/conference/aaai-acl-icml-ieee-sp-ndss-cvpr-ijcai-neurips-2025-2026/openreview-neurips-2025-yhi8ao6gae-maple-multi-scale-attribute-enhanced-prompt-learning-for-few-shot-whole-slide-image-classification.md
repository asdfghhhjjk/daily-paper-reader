---
title: "MAPLE: Multi-scale Attribute-enhanced Prompt Learning for Few-shot Whole Slide Image Classification"
title_zh: MAPLE：面向少样本全切片图像分类的多尺度属性增强提示学习
authors: "Junjie Zhou, WEI SHAO, Yagao Yue, Wei Mu, Peng Wan, Qi Zhu, Daoqiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yHi8Ao6GAe"
tags: ["query:cell-path"]
score: 6.0
evidence: 纳入细胞级属性（细胞核、腺体）进行WSI分类，与基于细胞级特征的诊断相关
tldr: 该论文针对少样本全切片图像分类中缺乏细胞级、腺体级等组织学实体信息的问题，提出MAPLE，一种多尺度属性增强提示学习框架。该方法将多尺度视觉语义与提示学习相结合，同时利用细胞核、腺体等属性进行预测。实验表明其在癌症诊断任务上取得了更好的性能和泛化能力。这项工作将细胞级特征有效融入WSI分类，为计算病理学提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有方法依赖切片级提示，无法捕捉细胞核、腺体等组织学实体的亚型特异性表型变异。
method: 提出多尺度属性增强提示学习框架，联合整合多尺度视觉语义并同时进行预测。
result: 在少样本WSI分类中提升了性能，尤其在癌症诊断方面。
conclusion: 通过纳入细胞级属性增强了WSI分类的可解释性和泛化能力。
---

## Abstract
Prompt learning has emerged as a promising paradigm for adapting pre-trained vision-language models (VLMs) to few-shot whole slide image (WSI) classification by aligning visual features with textual representations, thereby reducing annotation cost and enhancing model generalization. Nevertheless, existing methods typically rely on slide-level prompts and fail to capture the subtype-specific phenotypic variations of histological entities (e.g., nuclei, glands) that are critical for cancer diagnosis. To address this gap, we propose Multi-scale Attribute-enhanced Prompt Learning (MAPLE), a hierarchical framework for few-shot WSI classification that jointly integrates multi-scale visual semantics and performs prediction at both the entity and slide levels. Specifically, we first leverage large language models (LLMs) to generate entity-level prompts that can help identify multi-scale histological entities and their phenotypic attributes, as well as slide-level prompts to capture global visual descriptions. Then, an entity-guided cross-attention module is proposed to generate entity-level features, followed by aligning with their corresponding subtype-specific attributes for fine-grained entity-level prediction. To enrich entity representations, we further develop a cross-scale entity graph learning module that can update these representations by capturing their semantic correlations within and across scales.  The refined representations are then aggregated into a slide-level representation and aligned with the corresponding prompts for slide-level prediction. Finally, we combine both entity-level and slide-level outputs to produce the final prediction results. Results on three cancer cohorts confirm the effectiveness of our approach in addressing few-shot pathology diagnosis tasks.

---

## 论文详细总结（自动生成）

## 一、论文的核心问题与整体含义

- **研究背景**：在少样本全切片图像（WSI）分类中，提示学习通过将视觉特征与文本表示对齐，降低了标注成本并提升了预训练视觉-语言模型（VLM）的泛化能力。
- **核心问题**：现有提示学习方法通常只依赖**切片级提示**，难以捕捉组织学实体（如细胞核、腺体等）在亚型层面的表型变异，而这些细胞级、腺体级信息对癌症诊断至关重要。
- **整体含义**：论文提出 **MAPLE（Multi-scale Attribute-enhanced Prompt Learning）**，即多尺度属性增强提示学习框架，旨在将多尺度视觉语义、实体级属性与切片级全局信息联合建模，从而提升少样本病理诊断的准确性与可解释性。

## 二、论文提出的方法论

MAPLE 采用分层式框架，同时进行实体级和切片级预测，主要包含以下关键设计：

- **多尺度提示生成**：
  - 利用大语言模型（LLM）生成**实体级提示**，用于识别多尺度组织学实体及其表型属性（如细胞核、腺体等）。
  - 同时生成**切片级提示**，用于捕获整张切片的全局视觉描述。
- **实体级特征生成与预测**：
  - 提出**实体引导的交叉注意力模块**，生成实体级特征。
  - 将实体级特征与对应亚型特异性属性进行对齐，完成细粒度的实体级预测。
- **跨尺度实体图学习**：
  - 设计**跨尺度实体图学习模块**，通过建模同一尺度内和不同尺度间的实体语义相关性，更新和增强实体表示。
- **切片级表示与预测**：
  - 将经过图学习优化后的实体表示聚合为切片级表示。
  - 与切片级提示对齐，进行切片级预测。
- **最终融合**：
  - 将实体级输出与切片级输出结合，得到最终分类结果。

> 注：论文摘要未给出具体公式或算法伪代码，上述流程基于摘要文字描述整理。

## 三、实验设计

- **数据集 / 场景**：
  - 论文在**三个癌症队列（cancer cohorts）**上进行了验证，用于少样本病理诊断任务。
  - 摘要未明确给出具体数据集名称、样本量、癌种类型或切片来源。
- **Benchmark**：
  - 任务设定为**少样本全切片图像分类**。
  - 核心评估指标未在摘要中明确列出。
- **对比方法**：
  - 摘要提到与现有基于提示学习的 VLM 方法进行对比，但未列出具体对比算法名称或版本。

## 四、资源与算力

- 论文摘要和元数据中**未明确说明所用 GPU 型号、数量、训练时长、显存消耗或推理成本**。
- 由于方法涉及大语言模型生成提示、交叉注意力、图学习以及多尺度预测，其计算复杂度可能高于简单切片级方法，但具体算力需求无法从现有材料中确认。

## 五、实验数量与充分性

- **实验规模**：
  - 摘要明确提到在**三个癌症队列**上验证效果，说明至少覆盖了多个独立数据集。
  - 但摘要未提供消融实验、敏感性分析、跨癌种泛化实验、统计显著性检验或误差棒等细节。
- **充分性与客观性评估**：
  - 从现有信息看，**多队列验证具有一定外部效度**，但缺少详细实验设置、对比方法列表和定量指标，难以全面判断实验是否充分、公平。
  - 如果论文原文包含更完整的消融和对比实验，需以全文为准；仅基于摘要无法确认实验数量是否足够支撑结论。

## 六、论文的主要结论与发现

- MAPLE 通过引入**细胞核、腺体等多尺度组织学实体属性**，弥补了传统切片级提示学习的不足。
- 在三个癌症队列上的结果表明，该方法在**少样本病理诊断任务**中取得了更好的性能和泛化能力。
- 方法将细胞级、实体级特征有效融入 WSI 分类，有望提升病理诊断的**可解释性**和临床相关性。

## 七、优点

- **多尺度属性增强**：显式建模细胞核、腺体等组织学实体，更贴合病理医生的诊断逻辑。
- **提示学习与视觉-语言对齐**：利用 LLM 自动生成实体级和切片级提示，减少人工设计成本。
- **层级预测结构**：同时进行实体级细粒度预测和切片级全局预测，信息利用更充分。
- **图学习建模跨尺度关系**：通过跨尺度实体图捕获实体间语义关联，增强实体表示。
- **潜在可解释性**：实体级属性对齐有助于解释分类依据，对临床辅助诊断具有价值。

## 八、不足与局限

- **实验细节不足**：摘要未提供具体数据集、样本量、对比方法、评估指标和统计检验，难以完整评估方法有效性。
- **算力与效率未知**：未报告计算资源，结合 LLM、图学习和多尺度推理，实际部署效率可能受限。
- **泛化范围有限**：仅在三个癌症队列上验证，尚未覆盖非癌疾病、不同染色协议或不同扫描仪来源的数据。
- **方法复杂度较高**：多尺度实体生成、跨尺度图学习和双层级预测可能增加训练与推理开销。
- **公平性存疑**：未明确对比方法的调参策略或预训练模型是否一致，因此对比公平性无法从现有信息判断。

（完）
