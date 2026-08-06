---
title: "Biology-Guided Prototype Booster: Enhancing Latent Representations of Foundation Models for Gene Expression Prediction"
title_zh: 生物学引导的原型增强器：增强基础模型潜在表征用于基因表达预测
authors: "Chaoyi Li, Quan Nguyen"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ygv7GTp1k8"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 基于组织学图像的深度学习预测基因表达
tldr: "针对现有基础模型嵌入在基因表达预测任务上适应性不足的问题，提出生物学引导的原型增强器(BP-Booster)，利用生物学先验优化H&E组织学图像的表征，提升从图像预测空间转录组基因标志物的性能，为精准病理学提供了更高效且易适应的计算工具。"
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: "空间转录组技术成本高且耗时，从H&E图像预测基因表达成为替代方案，但现有基础模型表征未针对该任务优化。"
method: "提出BP-Booster，利用生物学原型增强基础模型生成的H&E图像嵌入，提升对基因表达预测的任务适应性。"
result: 方法在基因表达预测上预期优于通用嵌入，但摘要未给出具体结果。
conclusion: BP-Booster能有效优化病理图像表征，促进数字病理中的分子预测。
---

## Abstract
Spatial transcriptomics (ST) is a cutting-edge technology that enables the measurement of gene expression while preserving spatial context and generating detailed tissue images. However, ST technology remains time-consuming and costly. The ability to predict ST gene markers of cancer from histology-grade H&E-stained tissue images is opening new horizons for precision and personalised pathology. Despite the success of foundation models in generating general-purpose embeddings of H&E-images, these representations are not optimized for gene expression prediction and lack task-specific adaptability. To address this limitation, we introduce Biology-Guided Prototype Booster (BP-Booster), leveraging biological prior knowledge to guide the construction and training of learnable prototypes for embedding reconstruction, thereby improving gene expression prediction. We demonstrate superior performance of BP-Booster across datasets, various cancer tissue types and different ST platforms. We also show that BP-Booster can flexibly integrate various foundation models to enhance their task-specific representations, enhancing explainability and applicability in clinically relevant tasks like predicting cancer biomarkers. Code will be released upon acceptance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：从常规苏木精-伊红（H&E）染色组织学图像预测空间转录组（ST）基因表达已成为精准病理学的前沿方向，但现有基础模型（Foundation Models）产生的通用图像嵌入并未针对基因表达预测任务进行优化，缺乏任务特异性的适应能力。
- **研究动机**：空间转录组技术能保留组织空间背景的同时测量基因表达，但过程昂贵、耗时。若能直接从低成本、标准化的H&E图像准确预测基因标志物，将大幅推动个体化病理学发展。因此，需要一种方法，将基础模型的通用表征提升为更适合基因表达预测的专用表征。
- **整体含义**：论文旨在通过融入生物学先验知识，增强病理图像表征，从而提升从图像预测基因表达的性能，使深度学习方法在数字病理中更高效、更具解释性和临床可用性。

### 2. 论文提出的方法论

- **方法名称**：生物学引导的原型增强器（Biology-Guided Prototype Booster, BP-Booster）
- **核心思想**：
  - 利用生物学先验知识（如已知的基因表达模式、分子通路或组织形态关联）指导可学习原型（Prototypes）的构建与训练。
  - 通过这些原型对基础模型生成的组织图像嵌入进行重构与增强，从而提高嵌入对基因表达预测任务的适应性。
- **技术细节（基于摘要推断）**：
  - **输入**：H&E染色组织学图像，通过预训练的基础模型（如病理学专用的大型视觉模型）获取初始潜在嵌入。
  - **生物学原型构建**：引入一组可学习的原型向量，这些原型的初始化或训练过程受到生物学知识的引导（例如，通过已知基因表达谱或组织注释约束原型应与生物学上有意义的模式对齐）。
  - **嵌入增强**：利用原型与初始嵌入之间的交互（如注意力机制或重构损失），对嵌入进行修正和丰富，生成增强后的任务特异性表征。
  - **预测头**：增强后的嵌入进入下游预测头，输出空间基因表达值。
  - **训练目标**：结合基因表达预测的回归/分类损失，以及可能促使原型具有生物学意义的辅助损失项（如原型与已知生物标记的对齐）。
- **灵活性**：BP-Booster 能够作为即插即用模块，集成到各种不同的基础模型之上，提升它们的任务专用性。

### 3. 实验设计

- **数据集与场景**：
  - 使用了多个数据集，涵盖不同类型的癌症组织（如多种癌种）。
  - 涉及不同空间转录组平台生成的数据（例如10x Visium等），体现跨平台泛化能力。
- **评估基准（Benchmark）**：
  - 任务是预测与癌症相关的基因标志物（gene markers）的表达。
  - 对比基准可能包括：直接使用基础模型嵌入进行预测、其他嵌入增强方法、或专门为基因表达预测设计的端到端模型。
- **对比方法**：
  - 摘要未明确列出具体对比方法名称，但暗示是与“通用嵌入”方法和其他未进行生物学适配的基础模型表征进行对比。

### 4. 资源与算力

- 摘要中**未提供**任何关于GPU型号、数量、训练时长或计算资源消耗的信息。无法从已有文本推断所需的算力规模。

### 5. 实验数量与充分性

- **实验数量估计**：
  - 据摘要声称，实验覆盖了“多个数据集”、“多种癌种类型”和“不同ST平台”。
  - 很可能包含与若干现有方法的全面比较、消融实验（验证生物学先验和原型机制的作用）、跨模型集成实验等。
- **充分性与客观性评估**：
  - 摘要强调方法取得了“优越性能”（superior performance），且具备灵活性，但未给出具体数字或统计显著性。
  - 由于缺乏定量结果，无法从摘要判断实验对比是否绝对公平、基线是否顶配。但声称的多数据集、多平台测试增加了结论的可靠范围。
  - 消融实验和跨基础模型的验证（如果文中确实有）将增强客观性。

### 6. 论文的主要结论与发现

- BP-Booster 能够显著提升基础模型从H&E图像预测空间基因标志物的性能。
- 该方法在不同数据集、癌种和ST技术平台上均表现出优越的泛化能力。
- 通过利用生物学先验知识增强表征，不仅提高了预测准确性，还增强了模型的可解释性（例如，原型可与生物医学概念相联系），使其更适合癌症生物标记物预测等临床应用。
- BP-Booster 可灵活与多种现有基础模型结合，作为一种通用的表征增强策略。

### 7. 优点（方法或实验设计亮点）

- **跨领域桥接**：巧妙地将领域知识（生物学先验）注入数据驱动的表征学习中，使模型更“理解”病理图像背后的分子信息。
- **模型无关性**：设计为即插即用的增强器，可配合任意病理基础模型，扩展性强，无需重新训练大型模型。
- **关注可解释性**：引入原型机制，使得增强过程可能具有可追溯性，原型可能对应有生物学意义的组织模式或分子特征，有利于临床信任。
- **评估全面性**：声称进行了多数据集、多癌种、多平台验证，减少了过拟合特定数据分布的风险。

### 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）

- **具体实验数据缺失**：摘要无任何量化结果，无法评估实际增益幅度、稳定性及与基线的差异是否显著。
- **生物学先验的定义与来源不明确**：“生物学先验知识”的具体形式、如何获取、对不同任务的通用性如何，均未在摘要中说明。这可能成为方法应用时的瓶颈。
- **原型数量的确定与泛化**：原型构建可能需要调参，对新组织类型或稀有基因标记的泛化能力有待细究。
- **计算开销未知**：未提及原型增强过程带来的额外计算开销，实时性或有算力限制场景下的实用性存疑。
- **潜在偏差**：训练数据若偏重特定癌种或固定实验室流程，可能遗漏染色变化、扫描仪差异等现实因素。
- **仅限于H&E到ST的预测**：方法的价值建立在从H&E预测基因表达的可行性上，虽然前沿，但该任务本身尚存争议，临床验证仍需大量工作。

（完）
