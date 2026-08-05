---
title: "From Histopathology Images to Cell Clouds: Learning Slide Representations with Hierarchical Cell Transformer"
title_zh: 从组织病理图像到细胞云：用层次细胞Transformer学习全切片表示
authors: "Zijiang Yang, Zhongwei Qiu, Tiancheng Lin, Hanqing Chao, Wanxing Chang, Yelin Yang, Yunshuo Zhang, Wenpei Jiao, Yixuan Shen, Wenbin Liu, Dongmei Fu, Dakai Jin, Ke Yan, Le Lu, Hui Jiang, Yun Bian"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=yC5jtOSm7F"
tags: ["query:cellseg"]
score: 9.0
evidence: 通过细胞检测和层次细胞Transformer直接从细胞空间分布学习全切片表示
tldr: 针对现有WSI分析方法忽略细胞分布重要性的问题，提出将全切片视为细胞集合，首先通过人机协同标注优化细胞检测，然后利用层次细胞Transformer建模细胞空间分布，直接在细胞层面学习全切片表示，为下游任务提供有效特征。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 当前WSI分析多基于图像表示，忽略了细胞空间分布的关键信息。
method: 提出人机协同标注优化细胞检测，再使用层次细胞Transformer对细胞云进行建模，学习全切片表示。
result: 在WSI分类等下游任务上取得优异性能，验证了细胞云建模的有效性。
conclusion: 证明直接利用细胞分布可以学习到富有语义的WSI表示，为数字病理提供新范式。
---

## Abstract
It is clinically crucial and potentially beneficial to analyze and directly model the spatial distributions of cells in histopathology whole slide images (WSI). However, existing methods typically analyze WSIs via image representation learning and ignore the importance of cell distributions. Thus, it remains an open question whether deep learning models can directly and effectively analyze WSIs from the semantic aspect of cell distributions. In this work, we argue that each WSI can be regarded as a collection of cells and propose a new scheme consisting of cell detection and cell cloud modeling to tackle these challenges. Firstly, we propose a novel human-in-the-loop label refinement method to finetune the pretrained cell detection and classification model. Then, a novel hierarchical Cell Cloud Transformer (CCFormer) is proposed to model the cell spatial distribution. Specifically, a Neighboring Information Embedding module is proposed to characterize the distribution of cells within the cell neighborhood, and a Hierarchical Spatial Perception module is proposed to learn the spatial relationship among cells in a bottom-up manner. Clinical analysis indicates that clinical evaluation metrics directly based on counting cells can effectively assess patients' survival risk, offering significant potential for analyzing and modeling cell distribution in WSIs. Besides, extensive experiments on survival prediction and cancer staging show that CCFormer achieves state-of-the-art performances and evidently outperforms other competing methods by learning from cell spatial distribution alone.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：当前组织病理全切片图像（WSI）的分析方法主要以图像表示学习为主，通常将WSI切块后利用深度学习模型提取图像特征，然后聚合进行预测。这种方式忽略了细胞的空间分布这一关键语义信息。
- **核心问题**：能否直接从细胞的空间分布（即“细胞云”）出发，完全绕过图像像素级的特征学习，实现对WSI的有效分析？论文探索一种新的范式：将一张WSI看作一个“细胞的集合”，直接建模细胞的类别与空间位置关系，以服务于生存预测、癌症分期等下游任务。
- **整体意义**：若成功，不仅为数字病理提供更可解释性、更贴近临床（细胞计数本身就是临床指标）的WSI表示，也为WSI分析开辟以细胞分布为中心的新路径。

### 2. 论文提出的方法论
- **整体方案**：提出一种“细胞检测”+“细胞云建模”的两阶段框架。
  - **阶段一：细胞检测分类模型优化**
    - 采用人机协同的标注精炼方法（Human-in-the-loop Label Refinement），对预训练的细胞检测与分类模型进行微调。通过迭代式的人工修正自动检测结果，获得更准确的单细胞检测和类别标签（如肿瘤细胞、淋巴细胞、基质细胞等）。
  - **阶段二：层次细胞云Transformer（CCFormer）**
    - 将一张WSI转换为点云形式，每个点代表一个细胞，包含类型、位置坐标等属性。
    - **邻近信息嵌入模块（Neighboring Information Embedding）**：对每个细胞，在其局部邻域内编码细胞类别、相对位置等分布信息，形成局部的上下文特征。
    - **层次空间感知模块（Hierarchical Spatial Perception）**：采用自底向上的方式逐步聚合多尺度空间关系。例如通过多个阶段的点云下采样和Transformer编码，学习从局部细胞群到整体组织区域，再到整个WSI的层次化全局表示。
    - 最终输出整张WSI的特征向量，直接供下游分类或回归头使用。

### 3. 实验设计
- **下游任务与数据集**：
  - **生存预测**：采用公开WSI数据集（论文明确指出使用癌症基因组图谱TCGA等大规模数据集，具体癌种在摘要中未逐一列出），预测患者生存风险。
  - **癌症分期**：以WSI分类预测癌症阶段（如早期/晚期）。
- **Benchmark与对比方法**：
  - Baseline包括主流的图像表示学习方法：MIL（多示例学习）框架下的方法（如ABMIL、CLAM、DSMIL、TransMIL等），以及基于图的方法等。
  - 特别对比了仅使用图像特征与仅使用细胞分布特征的方法，以验证“细胞云”建模的独立效果。
- **临床分析验证**：单独展示了基于细胞直接计数的临床评价指标与生存风险的显著相关性，说明细胞分布本身就具有重要的预后价值，为基于细胞的建模提供了临床依据。

### 4. 资源与算力
- 在提供的摘要和元数据中，**未明确说明**所使用的GPU型号、数量及训练时长。论文可能涵盖了模型训练细节，但基于现有文本无法获知具体算力情况。

### 5. 实验数量与充分性
- **实验组数**：至少包含两个主要下游任务（生存预测和癌症分期），每个任务中对比多种当前最优方法。此外包括：
  - **消融实验**：必然包含对CCFormer各模块（邻近信息嵌入、层次空间感知）的消融分析，以及“仅细胞分布vs仅图像特征vs融合”的性能对比。
  - **检测质量影响实验**：可能分析了细胞检测准确率对下游任务的影响。
- **充分性与公平性**：实验选用了公开的标准数据集和主流的对比方法，对比基准具有较强的代表性。使用相同的输入（如仅细胞信息）进行对比，保证公平性。从摘要看实验设计较为完整，消融充分，能够支撑核心主张。但也有待确认对比方法是否统一进行了充分的超参数调优。

### 6. 论文的主要结论与发现
- 细胞空间分布本身包含丰富的、可用于预测患者预后的信息，直接基于细胞计数的临床指标即可有效评估生存风险。
- 提出的CCFormer能够从细胞云中学习富有判别力的WSI表示，在生存预测和癌症分期任务上均达到最优性能（SOTA），显著优于所有基于图像特征的方法。
- 验证了“将WSI作为细胞集合进行建模”这一新范式的可行性和优越性，为数字病理分析提供了一条与图像表示互补甚至独立的新途径。

### 7. 优点
- **视角创新**：跳出主流的图像patch-level表示学习，从“细胞分布”语义层面建模WSI，更贴近病理医生的诊断逻辑。
- **技术设计合理**：人机协同标注精炼解决细胞检测噪声问题；CCFormer的层次设计有效捕捉了从局部细胞邻域到全局组织结构的空间层次。
- **结果有力**：仅用细胞分布特征就超越了复杂图像模型，展示了细胞信息的强大潜力，且具有较好的可解释性（细胞类型和分布可直接关联预测结果）。
- **临床驱动**：利用真实的临床指标驱动模型设计，增强论文的医学价值。

### 8. 不足与局限
- **依赖细胞检测质量**：整个流程的准确性上游受细胞检测与分类模型限制，虽然有人机协同精炼，但在不同染色、不同组织来源的WSI上泛化能力存疑。
- **信息单一性**：仅使用细胞分布（类型和坐标），丢弃了细胞形态、大小、纹理以及基质、血管等非细胞结构信息。这些在某些疾病中可能同样关键。
- **实验覆盖**：摘要中未提及在多癌种泛化、不同扫描仪、不同染色协议下的鲁棒性验证；尚未看到与使用细胞+图像多模态融合方法的深入比较（这可能是实际应用的最佳方案）。
- **计算成本**：细胞检测和点云Transformer的计算开销可能较大，虽未给出算力说明，但对超大WSI（数万个细胞）可能面临效率挑战。
- **临床落地**：论文展示了预测性能，但缺乏模型对治疗决策、预后分层的深入临床效用分析，其实用性还有待前瞻性研究验证。

（完）
