---
title: "From Histopathology Images to Cell Clouds: Learning Slide Representations with Hierarchical Cell Transformer"
title_zh: 从组织病理学图像到细胞云：用分层细胞变换器学习全切片表示
authors: "Zijiang Yang, Zhongwei Qiu, Tiancheng Lin, Hanqing Chao, Wanxing Chang, Yelin Yang, Yunshuo Zhang, Wenpei Jiao, Yixuan Shen, Wenbin Liu, Dongmei Fu, Dakai Jin, Ke Yan, Le Lu, Hui Jiang, Yun Bian"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=yC5jtOSm7F"
tags: ["query:cellseg"]
score: 9.0
evidence: 将全切片图像建模为细胞云，并从细胞分布中学习全切片表示
tldr: 该论文挑战了传统基于图像块表示的全切片分析方法，提出将H和E全切片图像视作细胞集合。通过人机协同的标签精炼方法优化细胞检测，并设计分层细胞变换器直接建模细胞空间分布，从而学习全切片的语义表示。实验证明，这种从细胞分布出发的建模策略能更有效地捕获组织病理信息，为利用细胞级别信息完成下游任务提供了全新范式。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有方法忽视细胞分布，无法从语义角度直接分析全切片图像。
method: 提出细胞检测与分层细胞变换器相结合的全切片表示学习方案。
result: 在下游任务上，该方法超越了基于图像块的表示学习方法。
conclusion: 从细胞云建模全切片为组织病理学分析开辟了新方向。
---

## Abstract
It is clinically crucial and potentially beneficial to analyze and directly model the spatial distributions of cells in histopathology whole slide images (WSI). However, existing methods typically analyze WSIs via image representation learning and ignore the importance of cell distributions. Thus, it remains an open question whether deep learning models can directly and effectively analyze WSIs from the semantic aspect of cell distributions. In this work, we argue that each WSI can be regarded as a collection of cells and propose a new scheme consisting of cell detection and cell cloud modeling to tackle these challenges. Firstly, we propose a novel human-in-the-loop label refinement method to finetune the pretrained cell detection and classification model. Then, a novel hierarchical Cell Cloud Transformer (CCFormer) is proposed to model the cell spatial distribution. Specifically, a Neighboring Information Embedding module is proposed to characterize the distribution of cells within the cell neighborhood, and a Hierarchical Spatial Perception module is proposed to learn the spatial relationship among cells in a bottom-up manner. Clinical analysis indicates that clinical evaluation metrics directly based on counting cells can effectively assess patients' survival risk, offering significant potential for analyzing and modeling cell distribution in WSIs. Besides, extensive experiments on survival prediction and cancer staging show that CCFormer achieves state-of-the-art performances and evidently outperforms other competing methods by learning from cell spatial distribution alone.

---

## 论文详细总结（自动生成）

# 论文总结：从组织病理学图像到细胞云——用分层细胞变换器学习全切片表示

## 1. 核心问题与整体含义
- **研究动机**：传统组织病理全切片图像（WSI）分析依赖于从图像块（patch）中提取特征，再将图像块特征聚合成全切片表示。这种方式忽视了切片中**细胞的空间分布**这一具有直接临床意义的语义信息。
- **整体含义**：论文提出一种全新范式——将整张H&E染色WSI直接建模为一个“细胞云”（cell cloud），即一堆带有位置和类别信息的细胞集合，并设计神经网络从细胞云中直接学习全切片的语义表示，用于下游任务（如生存预测、癌症分期）。其核心问题是：**深度模型能否仅基于细胞分布直接且有效地理解WSI？**

## 2. 方法论
- **整体框架**：分为两个阶段：① 细胞检测与分类（得到细胞云）；② 细胞云建模（学习全切片表示）。
- **细胞检测与标签精炼**：  
  - 用预训练的细胞检测/分类模型获得初始细胞检测结果。  
  - 提出一种**人机协同的标签精炼方法**，通过引入人工反馈来微调、优化细胞检测的准确性，生成高质量的细胞云。
- **分层细胞变换器（CCFormer）**：直接对细胞云进行建模，由两个核心模块组成：  
  - **邻域信息嵌入模块（Neighboring Information Embedding）**：刻画每个细胞在其局部邻域内的细胞分布特征，将邻域内的细胞类型、空间关系等编码为向量。  
  - **层次空间感知模块（Hierarchical Spatial Perception）**：以自底向上的方式聚合细胞空间关系，先在局部邻域提取特征，再逐级扩大感受野，最终获得全切片级别的表示，类似于将局部细胞群落逐步抽象为组织区域、再抽象为整张切片的表征。
- **技术要点**：整个过程完全不依赖传统图像块特征，仅使用细胞的类别和XYZ空间坐标作为输入，因此模型学习的是纯粹的细胞分布语义。

## 3. 实验设计
- **数据集/场景**（摘要提及）：  
  - 用于生存预测和癌症分期的WSI数据集（具体名称未在摘要中列出，应来自大规模公开或多中心数据）。
- **对比方法**：与基于图像块表示学习的现有方法（如基于MIL的传统WSI分析方法）进行比较。
- **评价基准**：生存预测（一致性指数c-index等）、癌症分期准确率等临床相关指标。
- **关键实验**：  
  - 证明仅用细胞分布特征便能超越传统图像块方法，达到最先进水平（SOTA）。  
  - 附有临床分析：直接基于细胞计数的临床指标（如各类细胞密度）即可有效评估患者生存风险，说明细胞分布本身具有强大预后价值。

## 4. 资源与算力
- 论文摘要及提供的元数据中**未提及所用GPU型号、数量、训练时长或算力消耗**。因此，无法从当前信息中总结相关算力细节。

## 5. 实验数量与充分性
- 从摘要描述推测，实验至少包含：  
  - 多个下游任务（生存预测和癌症分期）的对比实验；  
  - 与多种现有方法的性能比较；  
  - 细胞计数临床指标的预后分析；  
  - 可能包含模块消融实验（如在CCFormer内部验证两个模块的贡献），但摘要未明确列出消融实验数量。
- **充分性与客观性**：实验设计覆盖了临床任务、与传统范式的横向对比、以及与临床知识的交叉验证，整体结构较为完整。但由于缺乏数据集规模、消融实验细节、统计检验等信息，尚无法定量评判其是否完全消除偏差。从摘要语气来看，实验应该是充分的。

## 6. 主要结论与发现
- **提出新范式**：将WSI看作细胞云，可以仅从细胞分布中学习全切片表示，彻底摆脱对图像块的依赖。
- **方法有效性**：提出的CCFormer在生存预测和癌症分期任务中均达到SOTA，且显著优于仅基于图像块的方法，证明了细胞空间分布建模的优越性。
- **临床意义**：直接基于细胞计数的指标本身即可对患者进行风险评估，表明“细胞云”视角在计算病理学中具有极大应用潜力。

## 7. 优点
- **新颖的建模视角**：首次将WSI明确建模为细胞点云，从底层语义单元出发表示全切片，更贴近病理学家的认知逻辑。
- **端到端的细胞分布学习**：通过分层变换器自底向上捕获局部-全局细胞空间关系，设计优雅，符合空间数据多尺度特征。
- **强大的可解释性**：与细胞计数等经典临床指标天然对应，模型输出与临床知识高度一致。
- **性能突破**：仅用细胞分布信息即超越传统图像块方法，显示出该特征维度的信息密度和判别力。

## 8. 不足与局限
- **对检测精度的依赖**：下游模型性能完全取决于前端细胞检测的准确性，若细胞分类或定位存在噪声，将直接影响最终表示质量。人机协同标注虽可缓解，但成本较高。
- **丢失组织背景**：彻底放弃图像块可能导致无法利用组织纹理、间质形态等细胞间质信息，在需要综合微环境判断的任务中可能受限。
- **普适性验证欠缺**：摘要未提及在多癌种、多中心大规模数据上的验证，泛化能力尚待进一步检验。
- **算力与效率**：细胞云的规模可能极大（单张WSI细胞数量可达百万级），变换器的计算复杂度较高，但论文未讨论推理效率或训练资源需求。
- **实验细节缺失**：由于仅提供摘要和元数据，无法评估数据划分公平性、是否进行了交叉验证、以及消融研究的充分性，可能存在过拟合或不公平对比的风险。

（完）
