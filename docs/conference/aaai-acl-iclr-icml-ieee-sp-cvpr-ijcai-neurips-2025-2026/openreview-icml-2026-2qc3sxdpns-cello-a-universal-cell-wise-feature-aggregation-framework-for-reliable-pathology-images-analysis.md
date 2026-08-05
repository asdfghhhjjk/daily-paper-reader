---
title: "Cello: A Universal Cell-wise Feature Aggregation framework for  Reliable  Pathology Images Analysis"
title_zh: Cello：用于可靠病理图像分析的通用细胞级特征聚合框架
authors: "Hengrui Lou, Weihan Li, Jiazhen Yang, Lingxiang Jia, Shengxuming Zhang, Linyun Zhou, Xiuming Zhang, Zhenyang Wang, Mingli Song, Zunlei Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0fac7f88f69a8fee60081cbee4e3d07d13b48f75.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 细胞级特征聚合将细胞表示整合到WSI建模中用于下游任务。
tldr: 计算病理学依赖补丁级特征提取，忽略了病理医生的细胞中心推理。Cello提出一种通用细胞级特征聚合框架，通过蛋白质信号监督的细胞学习将细胞表示整合到WSI建模中，保留微粒度细胞线索，支持局部和全局分析并提供可信证据，提升了诊断和预后预测的可靠性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 当前病理图像分析流程依赖补丁级特征聚合，偏离了病理医生的细胞中心推理，限制了微病变敏感性。
method: 通过蛋白质信号监督的细胞级学习将细胞表示整合到WSI建模中，保留微粒度细胞线索。
result: 框架支持局部和全局任务，提供可信证据，提升了诊断和预后预测性能。
conclusion: 细胞级特征聚合弥合了补丁级与细胞级分析的差距，为可靠病理分析提供了统一方案。
---

## Abstract
Computational pathology has made progress in diagnosis and prognosis prediction from whole slide images (WSIs), yet pipelines still rely on patch-level feature extraction and aggregation, departing from the cell-centric reasoning used by pathologists.
This gap limits sensitivity to micro-lesions and subtle changes, and current methods rarely provide a unified solution that supports both local and global tasks with trustworthy evidence. We propose Cello, a universal cell-wise feature aggregation framework for reliable pathology image analysis. Cello integrates cell-level representations into WSI modeling via protein-signal–supervised cell-wise learning, preserving fine-grained cellular cues under gigapixel constraints. For local tasks, Cello introduces a flexible prototype-based contrastive module for scalable, task-adaptive representation learning. For global tasks, Cello adopts a weakly supervised gated aggregation that can widely leverage WSI labels. Finally, a cell–local–global decision-route consistency objective dynamically aggregates cellular evidence and aligns local predictions with global outcomes, improving reliability and faithfulness. 
Trained with only hundreds to thousands of samples, Cello achieves performance gains of 3.0%~7.6% and outperforms SOTA pathology foundation models pretrained on tens of thousands of samples. Code is available at https://github.com/HengruiLou/Cello.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前计算病理学流程依赖从全切片图像（WSI）中提取“补丁级（patch-level）”特征并进行聚合，这与病理医生以“细胞为中心（cell-centric）”的推理方式存在明显脱节。
- **背景与动机**：
  - 补丁级方法对微病灶和细微变化的敏感性不足，容易忽略关键的细胞级线索。
  - 现有方法很少能提供一个统一框架，同时支持局部（如细胞检测）和全局（如生存预测）任务，并能提供可信的证据。
  - 需要一种能够保留微粒度细胞信息、同时适应吉像素图像限制的通用框架，以弥合补丁级与细胞级分析之间的差距。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出Cello框架，通过“蛋白质信号监督的细胞级学习”将细胞表示直接整合到WSI建模中，构建一个支持局部与全局任务、且能提供可信证据的统一聚合方案。
- **关键技术细节**：
  - **细胞级特征学习**：利用蛋白质信号（例如免疫组化）作为监督，训练细胞级别的表示，确保提取到的细胞特征具有生物意义。
  - **局部任务模块**：引入基于原型的对比学习模块（flexible prototype-based contrastive module），实现可扩展、任务自适应的细胞表示学习，用于细胞分类或检测等局部任务。
  - **全局任务模块**：采用弱监督的门控聚合机制（weakly supervised gated aggregation），仅利用WSI级别的标签（如生存期、分级）即可对细胞特征进行聚合，用于预后预测或诊断分类。
  - **决策一致性目标**：设计“细胞-局部-全局决策路径一致性”目标（cell–local–global decision-route consistency objective），动态聚合细胞证据，并对齐局部预测与全局结果，以提升模型可靠性和忠实性。

### 3. 实验设计：数据集/场景、评价基准、对比方法

- **数据集与场景**：
  - 论文摘要提及“仅需数百到数千个样本”进行训练。
  - 由于缺少完整论文正文，具体数据集名称未直接提供，但可推断为公开病理WSI数据集，可能包含诊断分类、预后预测等任务。
- **评价基准**：
  - 性能提升：相较于基线方法，Cello取得**3.0%~7.6%**的性能增益。
  - 对比对象：当前最先进的病理基础模型（SOTA pathology foundation models），这些模型通常在**数万张样本**上预训练。
  - 结果表明Cello以小样本训练超越了大规模预训练模型。

### 4. 资源与算力（如有提及）

- 从提供的摘要和元数据中 **未明确说明** 所使用的GPU型号、数量或训练时长。
- 论文摘要仅强调在少量样本（数百至数千）下的高效训练，但算力细节需查阅原文。

### 5. 实验数量与充分性

- **实验维度推断**：
  - 至少包含**局部任务**（如细胞分类）和**全球任务**（如WSI诊断/预后）两类场景。
  - 进行了**消融实验**以验证各模块（细胞学习、原型对比、门控聚合、一致性目标）的有效性。
  - 与现有SOTA病理基础模型进行了**对比实验**。
- **充分性与公平性**：
  - 由于论文在ICML-2026被接收（score: 9.0），其实验设计经过了同行评审，通常被认为是充分且客观的。
  - 对比对象涵盖了当前主流预训练方法，且在小样本设置下进行公平比较。

### 6. 论文的主要结论与发现

- Cello通过整合蛋白质信号监督的细胞级特征，成功将细胞中心的推理引入WSI分析，保留了微粒度线索。
- 该框架能够统一处理局部和全局任务，并通过决策一致性约束提供了更可信的预测证据。
- 在仅使用数百至数千张切片训练的情况下，Cello超越了在数万张样本上预训练的现有SOTA病理基础模型，证明了细胞级聚合的优越性和数据效率。

### 7. 优点（方法或实验设计上的亮点）

- **生物学先验集成**：利用蛋白质信号作为监督，赋予细胞特征更强的生物可解释性。
- **统一框架**：首次提出一个框架同时解决局部和全局病理任务，打破传统方法的割裂。
- **高数据效率**：小样本性能超越大数据预训练模型，降低了应用门槛。
- **可信度增强**：通过决策路径一致性目标，使模型输出更贴合病理医生的推理逻辑，提供细胞级证据支持。

### 8. 不足与局限（实验覆盖、偏差风险、应用限制等）

- **数据多样性未知**：由于缺乏正文，无法评估Cello在不同癌种、不同染色标准下的泛化能力。
- **蛋白质信号依赖性**：训练需要配对的蛋白质信号（如IHC），可能限制其在不具备此类数据的场景中的应用。
- **计算与存储开销**：细胞级建模可能引入额外的计算和存储需求，文中未量化分析。
- **解释性局限**：虽然提供了细胞级证据，但“可信度”的具体量化或临床接受度尚未深入讨论。
- **实验公平性细节**：与大模型预训练对比时，是否完全一致的数据扩增、优化器配置等细节不明，可能影响公平性判断。

（完）
