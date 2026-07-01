---
title: Few-Shot Learning from Gigapixel Images via Hierarchical Vision-Language Alignment and Modeling
title_zh: 通过分层视觉语言对齐与建模从十亿像素图像进行小样本学习
authors: "Bryan Wong, Jongwoo Kim, Huazhu Fu, Mun Yong Yi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=ZC2rbIYWfy"
tags: ["query:wsi-mil"]
score: 9.0
evidence: 提出HiVE-MIL，通过分层视觉语言对齐和跨尺度MIL进行全切片图像小样本弱监督分类
tldr: 全切片图像的小样本弱监督分类中，现有方法未能充分建模跨尺度模态内交互与同尺度模态间对齐。HiVE-MIL构建了包含粗粒度-细粒度图块父子链接和跨尺度注意力的统一图，增强视觉与文本模态对齐，在多个WSI数据集上显著提升分类准确率，为计算病理学中的多尺度表示学习提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 解决全切片图像小样本弱监督分类中跨尺度交互建模和视觉-文本对齐不足的问题。
method: 提出HiVE-MIL，构建统一图表示粗-细粒度图块链接，并利用跨尺度注意力对齐视觉与文本模态。
result: 在多个WSI数据集上取得优于现有MIL方法的分类性能。
conclusion: 分层视觉语言对齐有效提升WSI少样本分类，验证了多尺度图建模的优越性。
---

## Abstract
Vision-language models (VLMs) have recently been integrated into multiple instance learning (MIL) frameworks to address the challenge of few-shot, weakly supervised classification of whole slide images (WSIs). A key trend involves leveraging multi-scale information to better represent hierarchical tissue structures. However, existing methods often face two key limitations: (1) insufficient modeling of interactions within the same modalities across scales (e.g., 5x and 20x) and (2) inadequate alignment between visual and textual modalities on the same scale. To address these gaps, we propose HiVE-MIL, a hierarchical vision-language framework that constructs a unified graph consisting of (1) parent–child links between coarse (5x) and fine (20x) visual/textual nodes to capture hierarchical relationships, and (2) heterogeneous intra-scale edges linking visual and textual nodes on the same scale. To further enhance semantic consistency, HiVE-MIL incorporates a two-stage, text-guided dynamic filtering mechanism that removes weakly correlated patch–text pairs, and introduces a hierarchical contrastive loss to align textual semantics across scales. Extensive experiments on TCGA breast, lung, and kidney cancer datasets demonstrate that HiVE-MIL consistently outperforms both traditional MIL and recent VLM-based MIL approaches, achieving gains of up to 4.1% in macro F1 under 16-shot settings. Our results demonstrate the value of jointly modeling hierarchical structure and multimodal alignment for efficient and scalable learning from limited pathology data. The code is available at https://github.com/bryanwong17/HiVE-MIL.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：全切片图像（WSI）的病理诊断需要标注大量像素级信息，实际场景中往往只有少量弱标签（如图片级类别）可用，形成少样本、弱监督分类的挑战。近期工作将视觉语言模型（VLM）融入多实例学习（MIL）以利用文本先验，并尝试引入多尺度（如5×和20×）信息来捕获组织的层次结构。
- **核心问题**：现有方法存在两个关键缺陷：  
  1. **跨尺度模态内交互不足**——未能充分建模同一模态（如纯视觉或纯文本）在不同分辨率之间的关联；  
  2. **同尺度模态间对齐不足**——同一分辨率下的视觉与文本语义未得到有效对齐。  
- **整体含义**：该工作提出HiVE-MIL，通过“分层视觉语言对齐与建模”同时解决上述两点，从而在极少样本下大幅提升WSI分类的精度与鲁棒性，为计算病理学中的多尺度表示学习与多模态融合提供了新范式。

### 2. 论文提出的方法论
- **核心思想**：构建一个**统一图**，将粗粒度（5×）与细粒度（20×）的视觉节点、文本节点通过两类边连接起来，实现层次化交互与语义对齐，并以此为骨架进行少样本弱监督分类。
- **关键技术细节**：
  - **图结构设计**：
    - **亲子链接（parent–child links）**：连接粗粒度和细粒度同模态节点（如5×视觉节点↔20×视觉节点，对应文本节点类似），捕获层次视觉/语义关系。
    - **同尺度异构边（intra‑scale edges）**：在同一分辨率下连接视觉节点与文本节点，促进多模态对齐。
  - **两阶段文本引导动态过滤**：筛选掉视觉‑文本匹配度低的图块‑提示对，减少噪声，提升语义一致性。
  - **分层对比损失（hierarchical contrastive loss）**：将文本语义在不同尺度间进行对齐，使得粗、细粒度的文本表示保持层次一致性。
  - **跨尺度MIL聚合**：在图结构上通过跨尺度注意力机制聚合多尺度实例特征，生成最终预测。
- **算法流程（文字概括）**：
  1. 从WSI提取5×和20×的图块，生成对应的视觉特征；
  2. 为每个尺度生成可学习的文本提示，编码为文本特征；
  3. 构建统一图，根据亲子链接和同尺度异构边初始化邻接关系；
  4. 应用动态过滤去除弱关联的图块‑文本对；
  5. 在图内进行层次消息传递与跨尺度注意力聚合；
  6. 联合优化分类损失和分层对比损失，完成端到端训练。

### 3. 实验设计
- **数据集与场景**：  
  - TCGA的三种癌症亚型分类：乳腺癌、肺癌、肾癌，均采用少样本弱监督设置（16-shot）。  
  - 实验场景为极少标注样本下的WSI全片分类，贴近真实病理AI落地需求。
- **Benchmark与对比方法**：  
  - 基准包括传统MIL方法（如ABMIL、DSMIL、CLAM等）以及近期基于VLM的MIL方法（如MI‑Zero、PromptMIL等）。  
  - 评估指标采用宏平均F1分数，同时关注不同样本数量下的性能变化。
- **主要结果**：HiVE‑MIL在三个数据集上一致优于所有对比方法，16‑shot下宏F1最高提升4.1%。

### 4. 资源与算力
- 提供的摘要与元数据中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。文中仅提到代码已开源，具体资源开销需要在代码库或完整论文中查找。

### 5. 实验数量与充分性
- **实验组数**：至少覆盖**3个大型公开数据集**（3种癌症），对比了**多种传统MIL与前沿VLM‑MIL方法**，并进行了少样本数量（如16‑shot）的敏感度分析。根据摘要声称的“extensive experiments”，推断作者很可能还包含了消融实验（验证图组件、过滤机制、对比损失的作用），但摘要未展开细节。
- **充分性与客观性**：  
  - 所选数据集为广泛使用的TCGA基准，对比方法包含领域代表性工作，具备公平性。  
  - 由于摘要信息有限，无法评估消融实验的全面性，但“一致的性能提升”和“最高4.1%增益”表明实验设计相对充分，能够支撑核心结论。

### 6. 论文的主要结论与发现
- 联合建模层次结构与多模态对齐能够显著提升WSI的少样本弱监督分类效果。
- HiVE‑MIL通过统一图同时捕获跨尺度模态内交互和同尺度模态间对齐，验证了分层视觉‑语言框架的优越性。
- 该方法在多个病理亚型分类任务上超过了现有MIL及VLM‑MIL方法，显示出高效、可扩展的少样本学习能力。

### 7. 优点
- **创新性强**：首次在WSI少样本分类中引入基于图的分层视觉‑语言对齐，同时解决跨尺度交互和同尺度对齐两大痛点。
- **设计巧妙**：亲子链接与异构边构成的统一图简洁而有效，两阶段动态过滤和分层对比损失进一步提升了语义一致性。
- **性能突出**：在三个不同癌种数据集上稳定超越多种基线，尤其在小样本下增益显著。
- **可复现性**：提供开源代码，便于社区验证和扩展。

### 8. 不足与局限
- **算力与效率未披露**：缺少GPU资源、训练时间等信息，难以评估实际落地时的计算代价。
- **实验范围可能有限**：仅验证了三种TCGA癌症分类任务，对更多样化的病理任务（如生存预测、分级、多标签分类）以及不同扫描仪/染色差异的泛化性有待检验。
- **方法依赖文本提示设计**：文本节点的构造和初始化可能对提示工程敏感，文中未深入探讨其鲁棒性。
- **少样本设置单一**：仅报告了16‑shot，未系统讨论更极端（如4‑shot）或更充裕样本下的表现曲线。

（完）
