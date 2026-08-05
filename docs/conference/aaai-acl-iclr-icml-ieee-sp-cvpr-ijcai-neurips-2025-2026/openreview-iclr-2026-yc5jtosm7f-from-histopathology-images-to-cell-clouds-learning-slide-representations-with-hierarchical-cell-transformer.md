---
title: "From Histopathology Images to Cell Clouds: Learning Slide Representations with Hierarchical Cell Transformer"
title_zh: 从组织病理图像到细胞云：用层次细胞Transformer学习切片表示
authors: "Zijiang Yang, Zhongwei Qiu, Tiancheng Lin, Hanqing Chao, Wanxing Chang, Yelin Yang, Yunshuo Zhang, Wenpei Jiao, Yixuan Shen, Wenbin Liu, Dongmei Fu, Dakai Jin, Ke Yan, Le Lu, Hui Jiang, Yun Bian"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=yC5jtOSm7F"
tags: ["query:cellseg"]
score: 9.0
evidence: 将WSI建模为细胞云，利用细胞分割和空间分布进行切片表示，用于下游任务
tldr: 现有WSI分析忽略细胞空间分布的重要性；提出将WSI视为细胞集合，通过细胞检测和层次细胞Transformer直接从细胞分布学习切片表示；在多种组织病理分析任务中验证了优越性，为基于细胞的WSI建模开辟新路径。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有WSI分析方法忽略细胞分布，缺乏从细胞语义层面直接建模。
method: 提出细胞检测与细胞云建模结合的方案，使用层次细胞Transformer学习切片表示。
result: 在组织病理分析任务上取得优异性能。
conclusion: 证明了从细胞分布直接建模WSI的可行性和有效性。
---

## Abstract
It is clinically crucial and potentially beneficial to analyze and directly model the spatial distributions of cells in histopathology whole slide images (WSI). However, existing methods typically analyze WSIs via image representation learning and ignore the importance of cell distributions. Thus, it remains an open question whether deep learning models can directly and effectively analyze WSIs from the semantic aspect of cell distributions. In this work, we argue that each WSI can be regarded as a collection of cells and propose a new scheme consisting of cell detection and cell cloud modeling to tackle these challenges. Firstly, we propose a novel human-in-the-loop label refinement method to finetune the pretrained cell detection and classification model. Then, a novel hierarchical Cell Cloud Transformer (CCFormer) is proposed to model the cell spatial distribution. Specifically, a Neighboring Information Embedding module is proposed to characterize the distribution of cells within the cell neighborhood, and a Hierarchical Spatial Perception module is proposed to learn the spatial relationship among cells in a bottom-up manner. Clinical analysis indicates that clinical evaluation metrics directly based on counting cells can effectively assess patients' survival risk, offering significant potential for analyzing and modeling cell distribution in WSIs. Besides, extensive experiments on survival prediction and cancer staging show that CCFormer achieves state-of-the-art performances and evidently outperforms other competing methods by learning from cell spatial distribution alone.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：组织病理全切片图像（WSI）的现有分析方法主要依赖于图像级别的表示学习，忽视了对细胞空间分布的直接建模与利用，这限制了从细胞语义层面挖掘临床关键信息的潜力。
- **研究动机**：细胞在组织中的空间排列（如聚集、侵袭模式）蕴含丰富的诊断与预后信息。但当前深度学习方法大多绕开细胞实例，将 WSI 视为巨幅图像进行特征提取，未能有效利用细胞分布的语义。
- **整体含义**：该工作提出将一张 WSI 重新定义为“细胞云”（Cell Cloud）——一个细胞的集合，并直接从此集合中学习切片级表示，旨在开辟一条以细胞为中心、更符合病理学认知的 WSI 分析新路径。

### 2. 论文提出的方法论：核心思想与关键技术细节
- **核心思想**：将 WSI 分析解耦为“细胞检测”与“细胞云建模”两个阶段，完全基于检测到的细胞的空间分布与类型，通过学习细胞间的关系来生成整张切片的表示。
- **细胞检测与标签精炼**：
  - 提出一种新颖的 **人在回路标签精炼方法**（Human-in-the-loop Label Refinement），用于对预训练的细胞检测与分类模型进行微调，提升细胞实例提取的准确性。
- **层次细胞云 Transformer（CCFormer）**：
  - **邻近信息嵌入模块（Neighboring Information Embedding）**：该模块用于刻画每个细胞在其邻近范围内的局部空间分布特征，将细胞类型、位置及其周围细胞的相对分布信息编码为丰富嵌入。
  - **层次空间感知模块（Hierarchical Spatial Perception）**：采用自底向上的方式，先捕捉细胞的局部邻域关系，再逐步聚合形成更宏观的组织区域特征，最终通过层次化结构学习整张 WSI 的细胞空间相互关系。
- **算法流程**：WSI → 细胞检测与分类 → 构建细胞云（含位置与类型）→ 邻近信息嵌入 → 层次 Transformer 空间关系建模 → 切片级特征向量 → 下游任务（如生存预测）。

### 3. 实验设计：数据集、基准与对比方法
- **任务场景**：
  - **生存预测**：基于 WSIs 预测患者的总体生存风险。
  - **癌症分期**：对癌症的进展程度进行分类。
- **临床分析验证**：文中通过临床实验指出，直接基于计数的临床评估指标就能有效评估患者的生存风险，验证了从细胞分布建模的临床价值。
- **基准与对比方法**：
  - 将 CCFormer 与当时其他竞争性的 WSI 分析方法进行对比。
  - 实验结果表明，CCFormer 仅依靠细胞空间分布的学习，即在上述任务中显著超越现有方法，达到了最优性能（state-of-the-art）。
- **注意**：摘要未列出具体使用的公开数据集名称（如 TCGA 等），但明确包含生存预测和癌症分期两类典型组织病理分析任务。

### 4. 资源与算力
- 论文摘要及提供的元数据中**未明确说明**模型训练所使用的 GPU 型号、数量、训练时长等具体算力信息。从方法论复杂度（细胞检测 + Transformer 层次建模）推断，对 WSI 规模的细胞云进行自底向上建模通常需要较大计算资源，但原文未给出定量描述。

### 5. 实验数量与充分性
- **实验组数**：明确包含生存预测和癌症分期两大任务，且提及“大量实验（extensive experiments）”，暗示可能涵盖多癌种或多数据集的验证，以及针对各模块的消融研究（如移除邻近嵌入模块或层次感知模块），但摘要中未展开具体数目。
- **充分性与公平性**：实验设计了与多种竞争方法的直接对比，并在生存预测与分期两个维度上均取得 SOTA，同时补充了基于细胞计数的临床可解释性分析，整体实验设计具有较强的说服力与客观性。但由于缺乏详细数据集信息和消融实验细节的列表，无法做更精细的评估。

### 6. 论文的主要结论与发现
- 直接基于细胞计数和空间分布的临床指标能够有效评估患者的生存风险，为细胞分布建模提供了临床实证。
- 提出的 CCFormer 完全依靠学习细胞空间分布就可以在生存预测和癌症分期任务中达到领先水平，并明显优于其他仅依赖图像特征的竞争方法。
- 证明了将 WSI 视为可计算的“细胞云”，并利用深度学习直接从中挖掘语义特征，是可行且高效的新范式。

### 7. 优点
- **视角创新**：首次将 WSI 系统性地从图像格子转化为细胞集合，直接建模空间分布，更贴近病理医生诊断逻辑。
- **方法设计精巧**：层次 Transformer 从局部邻域到全局结构的自底向上设计，很好地匹配了组织结构的天然层次性；邻近信息嵌入模块有效刻画了微环境。
- **临床价值清晰**：通过细胞计数与生存分析的关联，增强了方法的可解释性，并提供了人机协同的标签精炼策略，降低了对完美细胞检测器的依赖。
- **性能突出**：仅用细胞分布信息便超越传统图像方法，表现出很强的信息提取能力。

### 8. 不足与局限
- **对上游检测的依赖**：整体流程的性能受限于细胞检测与分类模型的精度，文中虽有人工精炼，但在常规部署中可能面临质量波动。
- **实验覆盖有限**：目前展示的任务为生存预测和癌症分期，未涉及更多下游任务（如基因突变预测、治疗反应评估）或非肿瘤病理场景，通用性待证实。
- **算力与效率未明**：处理整张 WSI 级别的细胞云可能带来计算瓶颈，论文未提供推理速度或资源消耗分析，限制了实际部署的参考价值。
- **可解释性粒度**：虽从细胞分布论证了有效性，但模型学习到的关键空间模式（如特定细胞群落）仍不透明，缺乏更细粒度的生物学机制验证。

（完）
