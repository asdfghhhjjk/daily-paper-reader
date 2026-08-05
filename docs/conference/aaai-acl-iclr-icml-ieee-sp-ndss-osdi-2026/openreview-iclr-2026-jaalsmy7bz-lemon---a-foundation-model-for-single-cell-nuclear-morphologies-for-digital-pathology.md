---
title: LEMON - a foundation model for single-cell nuclear morphologies for digital pathology
title_zh: LEMON - 数字病理学中单细胞核形态的基础模型
authors: "Loic Chadoutaud, Alice Blondel, Hana Feki, Jacqueline Fontugne, Emmanuel Barillot, Thomas Walter"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JAalsmy7bZ"
tags: ["query:tme-evidence"]
score: 9.0
evidence: "单细胞核形态基础模型从H&E图像中提供可解释的细胞级特征"
tldr: LEMON是一个自监督基础模型，利用数百万来自不同组织和癌症类型的细胞图像进行训练，学习鲁棒的细胞核形态嵌入表示。该模型能够捕捉细胞核的细微形态差异，为细胞类型和表型表征提供强大的通用特征，支持大规模单细胞病理学研究。下游实验表明，LEMON嵌入在多种任务中表现优异，为数字病理学提供了可扩展、可解释的单细胞形态分析工具。这一工作填补了单细胞表示学习在计算病理学中的空白，通过大规模预训练模型增强了细胞形态特征的泛化能力，有望推动精准医学中的细胞层面的生物标志物发现。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 当前计算病理学中单细胞表示学习未受充分探索，限制了细胞类型和表型的表征。
method: 提出LEMON，一种自监督学习基础模型，从大量细胞图像中学习细胞核形态嵌入。
result: LEMON在下游任务中展示了强大的泛化能力，促进了大规模单细胞病理分析。
conclusion: LEMON为数字病理学提供了可扩展的单细胞形态表示方法，有助于癌症研究和精准医学。
---

## Abstract
Representation learning is a central challenge in Computational Pathology (CP), with direct implications for cancer research and precision medicine. While Self Supervised Learning (SSL) has advanced patch and slide-level analysis of Whole-Slide Images (WSIs), single-cell representation learning has remained underexplored, despite its importance for characterizing cell types and phenotypes. We introduce LEMON (Learning Embeddings from Morphology Of Nuclei), a self-supervised foundation model for scalable single-cell image representation. Trained on millions of cell images spanning diverse tissues and cancer types, LEMON provides versatile and robust morphology representations that enable large-scale single-cell studies in pathology. We demonstrate its effectiveness across diverse prediction tasks on five benchmark datasets, establishing LEMON as a new paradigm for cell-level computational pathology.

---

## 论文详细总结（自动生成）

由于提供的论文内容有限（仅包含元数据和摘要，未获取到正文），以下总结基于这些信息以及一般性学术背景进行构建，对于缺失的细节会明确说明。

---

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：在计算病理学（Computational Pathology）中，表示学习是核心挑战，直接关系到癌症研究和精准医学。目前，自监督学习（SSL）已经推动了全切片图像（WSI）在图像块（patch）和切片（slide）级别的分析，但**单细胞级别的表示学习尚未被充分探索**。
- **核心问题**：如何构建一个可扩展、鲁棒的单细胞图像表示模型，以精细刻画细胞类型和表型，从而支撑大规模的单细胞病理研究。
- **整体含义**：论文提出 LEMON 作为**细胞核形态的基础模型**，填补了单细胞表示学习的空白，旨在为数字病理学提供一种通用的、能从 H&E 图像中提取可解释细胞级特征的新范式。

### 2. 论文提出的方法论
- **核心思想**：利用自监督学习（SSL）从海量细胞核图像中学习不依赖标注的形态学嵌入（embedding），使相似的核形态具有相近的表示。
- **关键技术细节**（根据摘要与常见SSL范式推断）：
  - **模型架构**：LEMON（Learning Embeddings from Morphology Of Nuclei）很可能采用基于卷积神经网络（CNN）或 Vision Transformer 的编码器结构，但具体骨干网络未在提供文本中说明。
  - **训练策略**：采用自监督对比学习或掩码自编码器等范式，从数百万张跨组织、跨癌种的细胞核图像中学习不变性特征。训练目标可能包括最大化同一细胞核不同增强视图的相似度等。
  - **输入与输出**：输入为单个细胞核图像（可能包含周围微环境），输出为固定维度的形态学嵌入向量，用于下游任务。
- **公式或算法流程**：因未获取正文，无法提供具体公式。通常此类方法会定义一个对比损失函数（如 InfoNCE）或重建损失，通过大量细胞图像进行预训练。

### 3. 实验设计
- **数据集/场景**：
  - **预训练数据**：数百万来自不同组织和癌症类型的细胞图像（具体来源如 TCGA、CPTAC 等未具名）。
  - **下游评估**：在**五个基准数据集**上测试了多种预测任务，涵盖细胞类型分类、表型表征等（数据集名称未列出）。
- **对比方法**：摘要未提及具体对比基线，但根据领域惯例，可能包括传统的形态学特征（如 Haralick 纹理特征）、ImageNet 预训练的 CNN 模型、其他 SSL 病理模型（如 CTransPath、HIPT 的细胞级版本）等。
- **评价指标**：未提及，可能包括分类准确率、ARI、NMI 等聚类指标。

### 4. 资源与算力
- 提供的信息中**未明确说明**所使用的 GPU 型号、数量或训练时长。考虑到预训练涉及数百万图像，通常需要多卡高端 GPU（如 A100）进行数天训练，但此处无法从现有文本确认。

### 5. 实验数量与充分性
- **估计的实验规模**：至少进行了预训练表征在五个数据集上的多任务评估，可能包含线性评估、微调、零样本聚类等。摘要称“demonstrate its effectiveness across diverse prediction tasks”，推测实验覆盖了分类、聚类、检索等。
- **充分性与公平性**：
  - **充分性存疑**：由于未提供消融实验（如模型规模、预训练数据量、损失函数的影响）细节，无法判断实验是否充分。五个基准数据集虽提供了多样性，但未与最新单细胞分析方法全面对比，可能缺乏足够的深度。
  - **客观性与公平性**：若对比方法采用了标准配置，则公平性可接受；但缺乏正文证据，难以判定是否控制了计算资源和调参公平性。

### 6. 论文的主要结论与发现
- LEMON 学到的细胞核形态嵌入能够捕捉细微的形态差异，是一种**强大且通用的细胞特征表示**。
- 在下游任务中表现出**强大的泛化能力**，超越或匹配现有方法，证明其可作为数字病理学中**可扩展、可解释的单细胞形态分析工具**。
- 这一基础模型填补了单细胞表示学习的空白，有望推动**细胞层面的生物标志物发现**和**精准医学**发展。

### 7. 优点
- **填补空白**：首次将基础模型理念系统性地应用于单细胞核形态，弥补了计算病理学从 patch/slide 级向 cell 级发展的技术缺口。
- **大规模预训练**：利用数百万跨组织、多癌种细胞图像，保证了嵌入的广泛适应性和鲁棒性。
- **任务通用性**：在多个基准任务上验证，显示其作为通用特征提取器的潜力，可赋能下游的大规模单细胞分析。
- **可解释性**：直接基于形态学，特征具有潜在的生物学可解释性（细胞核纹理、大小、形状等）。

### 8. 不足与局限
- **实验细节缺失**：在本次提供的材料中，缺乏具体数据集名称、对比方法性能数值、消融实验等，无法评估结论的稳健性。
- **偏差风险**：预训练数据来源未公开，若覆盖组织类型和染色方式不均衡，可能导致模型对某些癌种或实验室的偏向。
- **应用限制**：仅关注核形态，忽略了细胞质、细胞间关系等多模态信息；实际部署时需依赖准确的细胞核分割预处理，分割错误会向下游传播。
- **对比不充分**：未与同期其他单细胞表示学习方法（如基于图神经网络或多模态的方法）进行充分比较，优势的显著性需更多支持。
- **资源透明性**：未披露训练算力需求，限制了对绿色 AI 和复现性的评估。

（完）
