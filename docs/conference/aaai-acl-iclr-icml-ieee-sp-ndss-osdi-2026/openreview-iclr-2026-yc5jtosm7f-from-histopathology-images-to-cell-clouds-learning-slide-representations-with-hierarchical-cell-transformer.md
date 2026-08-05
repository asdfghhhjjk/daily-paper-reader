---
title: "From Histopathology Images to Cell Clouds: Learning Slide Representations with Hierarchical Cell Transformer"
title_zh: 从组织病理学图像到细胞云：使用层次化细胞变换器学习切片表示
authors: "Zijiang Yang, Zhongwei Qiu, Tiancheng Lin, Hanqing Chao, Wanxing Chang, Yelin Yang, Yunshuo Zhang, Wenpei Jiao, Yixuan Shen, Wenbin Liu, Dongmei Fu, Dakai Jin, Ke Yan, Le Lu, Hui Jiang, Yun Bian"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=yC5jtOSm7F"
tags: ["query:profile"]
score: 9.0
evidence: 使用层次化变换器从WSI中的细胞空间分布学习切片级表示
tldr: 该论文提出将WSI视为细胞云：先检测细胞，然后使用层次化细胞变换器将细胞级特征聚合为切片级表示，直接利用细胞空间分布进行组织病理学分析，实验验证其在分类任务中的有效性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有WSI分析方法多基于图像表示，忽略了细胞空间分布的关键语义。
method: 提出细胞检测和细胞云建模方案，使用层次化细胞变换器从细胞分布学习切片表示。
result: 直接建模细胞分布能有效提升WSI分类性能。
conclusion: 细胞空间分布是WSI分析的有效语义，该方案为细胞级特征在数字病理学中的应用提供新范式。
---

## Abstract
It is clinically crucial and potentially beneficial to analyze and directly model the spatial distributions of cells in histopathology whole slide images (WSI). However, existing methods typically analyze WSIs via image representation learning and ignore the importance of cell distributions. Thus, it remains an open question whether deep learning models can directly and effectively analyze WSIs from the semantic aspect of cell distributions. In this work, we argue that each WSI can be regarded as a collection of cells and propose a new scheme consisting of cell detection and cell cloud modeling to tackle these challenges. Firstly, we propose a novel human-in-the-loop label refinement method to finetune the pretrained cell detection and classification model. Then, a novel hierarchical Cell Cloud Transformer (CCFormer) is proposed to model the cell spatial distribution. Specifically, a Neighboring Information Embedding module is proposed to characterize the distribution of cells within the cell neighborhood, and a Hierarchical Spatial Perception module is proposed to learn the spatial relationship among cells in a bottom-up manner. Clinical analysis indicates that clinical evaluation metrics directly based on counting cells can effectively assess patients' survival risk, offering significant potential for analyzing and modeling cell distribution in WSIs. Besides, extensive experiments on survival prediction and cancer staging show that CCFormer achieves state-of-the-art performances and evidently outperforms other competing methods by learning from cell spatial distribution alone.

---

## 论文详细总结（自动生成）

## 论文总结：从组织病理学图像到细胞云：使用层次化细胞变换器学习切片表示

### 1. 核心问题与整体含义（研究动机和背景）
- **问题背景**：在全切片组织病理图像（WSI）分析中，细胞的**空间分布**（如细胞类型、密度、排列方式）具有重要的临床意义，可直接反映肿瘤微环境、疾病进展等信息。
- **现有方法的局限**：当前主流方法基于图像块（patch）或图像特征表示进行学习，本质上是对图像像素或纹理建模，**忽略了细胞本身的分布语义**，无法显式利用细胞级信息。
- **研究动机**：探索是否可以直接从细胞分布的角度对WSI进行建模，使深度学习模型能够像病理医生一样，直接基于细胞的“集体行为”做出判断。
- **整体含义**：将WSI重新定义为“细胞云”（cell cloud），即一组带有空间位置和类别信息的细胞集合，并提出一套从细胞检测到表示学习的完整流程，直接挖掘细胞空间分布中的关键语义。

### 2. 方法论：核心思想与关键技术细节
- **总体方案**：提出 **“细胞检测 + 细胞云建模”** 两阶段框架。
  - **细胞检测阶段**：采用 **人在回路标签优化（human-in-the-loop label refinement）** 方法，对预训练的细胞检测与分类模型进行微调，提升细胞检测准确性。
  - **细胞云建模阶段**：设计 **层次化细胞变换器（Hierarchical Cell Transformer, CCFormer）** 对检测到的细胞集合进行表示学习。
- **关键技术模块**：
  - **邻近信息嵌入（Neighboring Information Embedding）**：对每个细胞，刻画其邻域内其他细胞的分布特征，将局部细胞构成信息编码为向量。
  - **层次化空间感知模块（Hierarchical Spatial Perception）**：以自底向上的方式分层次聚合细胞间的空间关系，逐步提取从细胞级、细胞群级到切片级的表示。
- **最终输出**：得到整张WSI的切片级表示，可直接用于生存预测、癌症分期等下游任务。

### 3. 实验设计：数据集、场景与对比方法
- **下游任务**：生存预测（survival prediction）和癌症分期（cancer staging）。
- **对比基准**：与现有基于图像表示的方法进行对比，文中提到达到 state-of-the-art 性能。
- **亮点**：强调 **仅使用细胞空间分布信息（不使用图像纹理或补丁特征）** 即可明显优于其他竞争方法。
- **注**：由于提供的文本仅为摘要和元数据，未列出具体数据集名称（如TCGA、CPTAC等）、评估指标（如C-index、AUC）、对比方法名称等细节。

### 4. 资源与算力
- 原文摘要及元数据中**未提及任何GPU型号、数量、训练时长或显存消耗等算力信息**，无法进行总结。

### 5. 实验数量与充分性
- 从摘要可推断，实验至少覆盖：
  - 两个不同任务（生存预测、癌症分期）。
  - 与多个现有方法的对比（声称达到SOTA）。
  - 可能包含消融实验以验证各模块作用（如邻近嵌入、层次感知模块），但具体消融细节未在元数据中给出。
- **评估**：基于可获取的信息，实验设计在任务多样性上较合理，且强调仅用细胞分布的对比具有创新性；但由于缺少具体数据集数量、样本量、统计检验等细节，**实验的充分性和公平性无法完全判断**，需查阅完整论文确认。

### 6. 主要结论与发现
- **细胞的空間分布** 是WSI分析的有效语义源，可直接用于强性能的切片级表示学习。
- 临床分析表明，**基于简单细胞计数的临床指标**就能有效评估患者的生存风险，印证了细胞分布建模的重要性。
- 提出的CCFormer **仅依靠细胞云建模** 就在生存预测和癌症分期上取得最先进水平，并显著优于基于图像表示的方法。
- 此方法为**细胞级特征在数字病理学中的直接应用开辟了新范式**。

### 7. 优点：方法与实验设计的亮点
- **视角创新**：将WSI从图像重新定义为“细胞云”，直接对细胞分布建模，更贴近病理医生的诊断逻辑。
- **端到端方案**：构建了从细胞检测（带人在回路优化）到层次化细胞变换器的完整流程，结构清晰。
- **高效表示**：不依赖图像纹理，仅从细胞坐标和类别学习切片表示，可能降低对染色颜色、扫描仪差异的敏感性。
- **临床可解释性**：底层基于可计数的细胞对象，更易与临床知识（如免疫细胞浸润、肿瘤细胞比例）关联。

### 8. 不足与局限
- **信息缺失严重**：仅基于摘要和元数据，无法获知：
  - 细胞检测模型的鲁棒性及标签优化成本；
  - 具体数据集规模与多样性（如器官部位、染色类型）；
  - 是否处理了细胞重叠、检测误差传播问题；
  - 与其他最新MIL或图网络方法的详细对比；
  - 跨中心泛化能力。
- **潜在局限**：
  - 细胞检测本身可能引入误差，影响后续建模；
  - 细胞云建模丢弃了亚细胞或组织区域形态信息，可能在某些依赖组织结构的疾病中性能受限；
  - 计算复杂度：层次化变换器在处理数十万细胞时的可扩展性未提及。
- **偏差风险**：如果仅使用公开数据集（如TCGA），可能存在机构内验证偏差；缺少外部独立验证。

（完）
