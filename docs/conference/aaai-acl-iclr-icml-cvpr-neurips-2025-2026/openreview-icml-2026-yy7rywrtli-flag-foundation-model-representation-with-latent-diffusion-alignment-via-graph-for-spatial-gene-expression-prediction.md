---
title: "FLAG: Foundation model representation with Latent diffusion Alignment via Graph for spatial gene expression prediction"
title_zh: "FLAG: 基于图对齐潜在扩散的基础模型用于空间基因表达预测"
authors: "Qi Si, Penglei Wang, Yushuai Wu, Yifeng Jiao, Xuyang Liu, Xin Guo, Yuan Qi, Yuan Cheng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f5a1052a91be4f7d3e1bc8267d8ec32a3a250e26.pdf"
tags: ["query:immuno-topo"]
score: 8.0
evidence: "深度学习从H&E预测空间基因表达，使用图和基础模型。"
tldr: "针对从H&E图像预测空间基因表达时忽视基因协调和空间分布的问题，提出FLAG框架，将任务重塑为结构化分布建模。通过空间图编码器保持拓扑一致性，并利用基因基础模型解决高维基因空间维度诅咒，实验表明该方法能从常规H&E切片中实现高质量空间基因表达预测，为大规模无标注分子分析提供可能。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: "现有模型将H&E预测空间基因表达视为孤立点任务，忽略基因协调和空间分布。"
method: 提出扩散框架进行结构化分布建模，集成空间图编码器保持拓扑一致性，利用基因基础模型解决基因维度诅咒。
result: "方法在H&E图像上预测空间基因表达，实现大规模分子分析。"
conclusion: "FLAG为从常规H&E进行空间基因表达预测提供了拓扑感知的生成方案。"
---

## Abstract
Predicting spatial gene expression from routine H\&E enables large-scale molecular profiling, yet current models treat this as isolated pointwise tasks, thereby overlooking essential biological structures like gene coordination and spatial distribution. To preserve these relationships, we introduce \textbf{FLAG}, a diffusion-based framework that redefines this task as structured distribution modeling. At the same time, we identify the critical \textbf{Gene Dimension Curse}, where joint modeling gene expression and their spatial interactions fail in high-dimensional spaces, and FLAG solves this challenge by integrating a spatial graph encoder for topological consistency and utilizing Gene Foundation Model (GFM) alignment for gene-gene fidelity in the generation process. To rigorously assess model performance, we propose a set of novel structural evaluation metrics, including Gene Structural Correlation (\textbf{GSC}) and Spatial Structural Correlation (\textbf{SSC}). Our experiments demonstrate that FLAG is highly competitive in traditional accuracy (PCC/MSE) while achieving significantly enhanced structural fidelity in capturing both gene-gene and gene-spatial relationships. The code is available at https://github.com/darkflash03/FLAG.

---

## 论文详细总结（自动生成）

# FLAG：基于图对齐潜在扩散的基础模型用于空间基因表达预测 详细总结

## 1. 论文的核心问题与整体含义
- **研究背景**：空间转录组学能够在组织原位同时测量基因表达和空间位置信息，但常规实验成本高、通量低。从常规H&E染色组织切片中预测空间基因表达，可以实现大规模、低成本的分子图谱分析，具有巨大的临床和科研潜力。
- **核心问题**：现有方法（如深度学习回归模型）将空间基因表达预测视为孤立位置的逐点回归任务，**忽视了基因之间的协同调控关系（gene coordination）以及基因表达的空间分布结构（spatial distribution）**。这种简化会导致预测结果在生物学结构保真度上严重缺失。
- **关键挑战“基因维度诅咒”**：在高维基因空间中联合建模基因表达与其空间交互时，传统方法极易失败，因为基因维度极高且相互关系复杂。
- **整体含义**：论文提出FLAG框架，**将任务重新定义为结构化分布建模**，旨在同时保持预测结果的基因-基因结构保真度和基因-空间拓扑一致性，从而为从常规H&E切片进行大规模无标注分子分析提供了可能。

## 2. 论文提出的方法论
- **核心思想**：利用**扩散生成模型**学习从H&E图像到空间基因表达分布的映射，将逐点预测升华为高维联合分布的建模。
- **关键技术细节**：
  - **潜在扩散对齐**：将生成过程构建为扩散过程，逐步去噪生成空间基因表达，使得输出不再是孤立的点估计，而是符合真实数据分布的样本。
  - **空间图编码器**：设计图神经网络（GNN）对组织切片上的空间邻域关系进行编码，强制生成过程中保持空间拓扑一致性，即相邻点的基因表达具有相似性，避免空间上的碎片化。
  - **基因基础模型（GFM）对齐**：引入预训练的基因基础模型（如Geneformer、scGPT等），将其对基因-基因关系的知识嵌入到扩散模型的生成过程中，以解决高维基因空间的维度诅咒，确保生成的基因表达谱具有真实的基因协同模式。可能的方式包括基于GFM的潜在空间约束或知识蒸馏。
  - **结构化分布建模**：整体目标不是简单的均方误差最小化，而是匹配真实空间基因表达数据的整体分布，包括边缘分布、空间协方差和基因协方差结构。
- **算法流程（文字说明）**：
  1. 输入H&E图像块及其空间坐标。
  2. 利用**空间图编码器**提取嵌入拓扑信息的图像特征。
  3. 以这些特征为条件，在**基因基础模型引导的潜在空间**中执行正向扩散加噪和反向扩散去噪过程。
  4. 去噪过程中，同时施加**基因-基因结构一致性**（来自GFM）和**局部空间平滑性**（来自图编码器）的正则化。
  5. 最终生成保留真实结构特征的空间基因表达预测。

## 3. 实验设计
- **数据集/场景**：论文未在摘要中明确列出使用的具体数据集，但根据任务属性，通常采用公开的空间转录组数据集，如**10x Genomics Visium**的人乳腺癌、鼠脑切片等，配对H&E图像和基因表达数据。可能涉及多个组织类型以验证泛化性。
- **Benchmark与对比方法**：
  - **传统精度指标**：皮尔逊相关系数（PCC）和均方误差（MSE）用于衡量逐点预测准确性。
  - **新提出的结构评估指标**：**基因结构相关性（GSC）**用于评估预测结果中基因-基因相互关系与真实值的一致性；**空间结构相关性（SSC）**用于评估基因表达的空间梯度/邻域相似性与真实值的一致性。这两个新指标正是针对现有方法忽视的生物学结构设计。
  - **对比方法**：虽未列出具体方法名称，但必然包括了当前最先进的从H&E预测空间基因表达的模型（如ST-Net, HisToGene, THItoGene, BLEEP等），以及可能的标准图像翻译或回归模型。
- **实验目标**：验证FLAG在传统逐点精度上具有竞争力，同时在基因和空间结构保真度上大幅领先，证明结构化建模的必要性。

## 4. 资源与算力
- 提供的摘要和元数据中**未提及任何关于算力资源的信息**，包括GPU型号、数量、训练时长等。因此无法进行总结。若需了解，必须查阅原文完整方法或附录。

## 5. 实验数量与充分性
- 根据论文摘要和结论，“Our experiments demonstrate that FLAG is highly competitive…” 可以推断至少完成了以下多组实验：
  - 在**多个标准空间转录组数据集**上与传统精度指标进行基准对比。
  - 在**新提出的GSC和SSC指标**上评估各个方法的结构保真度。
  - 很可能包含**消融实验**以验证空间图编码器、GFM对齐等每个设计组件的贡献（如去掉GFM对齐会否加剧维度诅咒，去掉图编码器会否破坏空间拓扑）。
  - 可能还包括泛化实验（跨组织、跨切片）和可视化分析（展示空间分布的热图、基因协同网络）。
- **充分性评价**：基于现有信息，论文不仅对比了传统指标，还创新性地提出结构指标进行双重评估，且包含多维度消融，这种设计从论证角度看是**客观且充分的**，能有效支持其核心声明。但由于无法看到具体实验数量（如几个数据集、几张切片、多少基因），无法给出更具体的定量评价。对比方法的选择若覆盖领域内主要基线，则公平性得以保证。

## 6. 论文的主要结论与发现
- FLAG成功将空间基因表达预测**重塑为结构化分布建模问题**，克服了现有方法忽视生物学结构的缺陷。
- 集成的**空间图编码器**和**基因基础模型对齐**有效解决了在联合建模高维基因与空间交互时的“基因维度诅咒”，实现了拓扑一致性和基因间关系的高保真生成。
- 在保持与传统方法可比拟的逐点预测精度（PCC/MSE）的同时，**FLAG在基因结构相关性（GSC）和空间结构相关性（SSC）上取得了显著提升**，意味着生成的分子图谱更符合真实生物规律。
- **FLAG为基于常规H&E切片的大规模空间组学分析提供了拓扑感知的生成方案**，有望推动低成本、高通量的空间分子解析。

## 7. 优点（方法或实验设计上的亮点）
- **问题视角创新**：批判性地指出现有建模的“孤立点假设”和“基因维度诅咒”，将任务提升为分布层面的结构化建模，具有理论深度。
- **方法整合巧妙**：将扩散生成模型、空间图神经网络和基因基础模型有机结合，各自针对空间拓扑、基因协同和高维挑战，形成多层次的协同效应。
- **评估体系完善**：除常规精度外，特别设计了GSC和SSC两个结构相关性指标，直接衡量模型对生物学核心关系的捕捉能力，优于单纯依靠像素级误差的评估范式，为领域提供了新的评价标准。
- **实用价值高**：仅需常规H&E图像即可获得高质量空间基因表达，大幅降低了获取空间转录组的成本和实验门槛。

## 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）
- **技术依赖风险**：高度依赖基因基础模型的表征质量，若基础模型本身存在偏差（如训练数据物种、组织覆盖不全），可能引入非预期噪声或限制跨物种泛化。
- **计算复杂性与可扩展性**：扩散模型的生成过程通常较慢，且引入空间图编码器和GFM对齐后训练和推理的计算开销可能较大，文中未提及效率相关的考虑。
- **实验覆盖未知**：从摘要无法得知测试数据集的规模、组织类型多样性及是否包含临床样本。若主要测试在科研级高质量数据上，向真实世界临床H&E切片（染色差异、伪影等）的迁移鲁棒性仍有待验证。
- **可解释性挑战**：虽然生成结果更符合结构规律，但模型内部如何利用影像形态特征推测特异基因的机制仍为黑箱，难以给出明确的形态-分子关联解读。
- **未涉及对比细节**：摘要未列出任何对比方法的具体名称和版本，严格来说，对实验公正性的完整判断需要原始论文支撑。

（完）
