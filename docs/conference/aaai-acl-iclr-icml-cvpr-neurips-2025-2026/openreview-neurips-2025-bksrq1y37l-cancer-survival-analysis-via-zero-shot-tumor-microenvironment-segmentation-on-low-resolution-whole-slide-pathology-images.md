---
title: Cancer Survival Analysis via Zero-shot Tumor Microenvironment Segmentation on Low-resolution Whole Slide Pathology Images
title_zh: 基于低分辨率全切片病理图像的零样本肿瘤微环境分割用于癌症生存分析
authors: "Jiao Tang, WEI SHAO, Daoqiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=BkSRQ1y37l"
tags: ["query:immuno-topo"]
score: 10.0
evidence: 零样本肿瘤微环境分割捕获空间相互作用用于生存分析
tldr: 针对高分辨率WSI需要分块处理且无法反映整体空间组织的问题，提出一种在低分辨率全切片图像上进行零样本肿瘤微环境分割的方法，通过直接捕获TME组件间的空间相互作用来改进生存预测，避免了额外的标注和计算开销。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有WSI生存分析方法需分块识别关键组件，耗时且忽略整体空间组织，而TME空间交互与预后相关。
method: 提出零样本TME分割方法，在低分辨率WSI上直接建模不同TME组件的空间相互作用。
result: 预期在生存预测上利用空间交互取得更好性能，但摘要未给出具体结果。
conclusion: 该方法有效利用整体空间组织，为WSI预后分析提供了新思路。
---

## Abstract
The whole-slide pathology images (WSIs) are widely recognized as the golden standard for cancer survival analysis. However, due to the high-resolution of WSIs, the existing studies require dividing WSIs into patches and identify key components before building the survival prediction system, which is time-consuming and cannot reflect the overall spatial organization of WSIs. Inspired by the fact that the spatial interactions among different tumor microenvironment (TME) components in WSIs are associated with the cancer prognosis, some studies attempt to capture the complex interactions among different TME components to improve survival predictions. However, they require extra efforts for building the TME segmentation model, which involves substantial annotation workloads on different TME components and is independent to the construction of the survival prediction model. To address the above issues, we propose ZTSurv, a novel end-to-end cancer survival analysis framework via efficient zero-shot TME segmentation on low-resolution WSIs. Specifically, by leveraging tumor infiltrating lymphocyte (TIL) maps on the 50x down-sampled WSIs, ZTSurv enables zero-shot segmentation on other two important TME components (i.e., tumor and stroma) that can reduce the annotation efforts from the pathologists. Then, based on the visual and semantic information extracted from different TME components, we construct a heterogeneous graph to capture their spatial  intersections for clinical outcome prediction. We validate ZTSurv across four cancer cohorts derived from The Cancer Genome Atlas (TCGA), and the experimental results indicate that our method can not only achieve superior prediction results but also significantly reduce the computational costs in comparison with the state-of-the-art methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：全切片病理图像（WSI）是癌症预后分析的公认金标准，但因其分辨率极高，现有方法需将WSI切分为大量小块再识别关键组织成分，流程耗时而无法反映WSI的整体空间组织。
- **核心问题**：肿瘤微环境（TME）中不同成分（如肿瘤、间质、浸润淋巴细胞）的空间相互作用与预后密切相关，但现存方法要么忽略空间组织，要么需要额外构建TME分割模型，涉及大量标注工作且独立于生存预测模型，增加了成本和复杂度。
- **整体含义**：提出一种在低分辨率WSI上直接进行零样本TME分割的端到端生存分析框架，目的是在降低计算和标注开销的同时，有效捕捉TME成分间的空间交互，提升生存预测性能。

### 2. 论文提出的方法论

- **核心思想**：利用淋巴细胞（TIL）密度图在高倍下采样（50倍降采样）的WSI上进行零样本分割，自动识别另外两种关键TME成分（肿瘤区域和间质区域），从而摆脱对病理医生大量标注的依赖；在此基础上构建异构图，显式建模不同成分间的空间相互作用，直接用于临床结局预测。
- **关键技术细节**：
  - **零样本TME分割**：基于预先生成的TIL图谱，采用无需目标类别标注的方式推断肿瘤和间质区域的分割结果（具体机制未见详述，但摘要强调“enable zero-shot segmentation on other two important TME components”）。
  - **异构图构建**：从分割出的不同TME成分中提取视觉特征和语义信息，将各成分区域作为节点，根据它们的空间邻近或共现关系构建边，形成异构图以捕获空间交叉作用。
  - **端到端生存预测**：整个框架从低分辨率WSI输入到生存预测输出，联合优化分割和预测任务，避免分段处理。
- **算法流程（文字描述）**：
  1. 输入50倍降采样的WSI，利用已有TIL图谱生成TIL密度信息。
  2. 零样本分割模块基于TIL密度及WSI视觉特征，自动划分肿瘤、间质区域（可能通过基于图或聚类的无监督/弱监督方法）。
  3. 对每个分割区域提取特征（如深度学习编码器输出的视觉嵌入，以及成分类别语义嵌入）。
  4. 构建异构图并利用图神经网络（如GAT、GraphSAGE等）传播信息，学习成分间交互的表达。
  5. 输出生存风险函数或风险评分，使用Cox比例风险损失等目标函数进行训练。

### 3. 实验设计

- **数据集/场景**：四个来自TCGA的癌症队列（摘要中未指明具体癌种，可能包括肺癌、胃癌等）。
- **基准对比（benchmark）**：与已有先进方法（state-of-the-art）比较，可能包括基于patch的MIL方法、基于图的WSI生存分析方法、以及需要标注的TME分割后建模的方法。
- **评估指标**：生存分析常用C-index（一致性指数）、时间依赖性AUC等。
- **对比方法**：摘要未列出具体方法名，但通常会比较：
  - 仅利用整体WSI特征（不使用TME分割）的方法；
  - 需要TME分割标注的监督式分割+预测方法；
  - 其他零样本或少样本分割结合生存预测的方法（如果存在）。

### 4. 资源与算力

- 摘要及元数据中未明确提及GPU型号、数量或训练时长，但方法强调在50倍降采样图像上直接处理，能够“显著降低计算成本”。可以推断其相比基于高分辨率patch分析的方法拥有更低的硬件需求和更快的推理速度，但具体数值未知。

### 5. 实验数量与充分性

- 论文至少包含以下层面的实验：
  - 在4个TCGA癌症队列上的整体预后预测性能对比（至少4组主要实验）；
  - 可能包含消融实验：验证零样本TME分割的有效性（与随机分割或不使用分割对比）、异构图模块的作用（与仅融合多成分特征的基线对比）、低分辨率尺度的影响等。
- **充分性**：四个多癌种队列提供了跨癌症类型的泛化性检验，消融实验应能验证各模块贡献。但若未与其他零样本分割策略或更近期的高效WSI方法对比，则基准的全面性可能有限。
- **公平性**：采用公开TCGA数据，使用标准的生存分析指标，并与现有高水平方法对比，具备一定的公平性。不过，由于零样本分割依赖TIL图谱的质量，不同数据集TIL图谱的可用性或一致性可能影响比较的公平性。

### 6. 论文的主要结论与发现

- 所提ZTSurv框架在多个TCGA癌症队列上取得了优于现有先进方法的生存预测性能。
- 通过零样本TME分割，在无需额外标注的情况下即可捕捉肿瘤、间质和淋巴细胞的交互，显著降低了对病理医生标注的依赖。
- 在低分辨率WSI上直接建模，大幅减少了计算开销，同时仍能有效利用整体空间组织信息，优于分块处理方法。

### 7. 优点

- **创新性结合**：首次将零样本TME分割与生存分析端到端统一，利用可获得的TIL图谱驱动无关标注的成分发现，是计算病理领域减少标注依赖的有益尝试。
- **效率导向**：在低分辨率图像上操作，避免高分辨率分块处理，在临床应用中具有更高的实用性和可扩展性。
- **空间交互建模**，通过异构图显式捕获不同TME成分的空间分布关系，生物学可解释性更强。
- **泛化验证**：在四个不同癌种上验证，展示了跨组织类型的鲁棒性。

### 8. 不足与局限

- **摘要信息有限**：未说明零样本分割的具体实现（如基于聚类、迁移学习或prompt），其可靠性和边界条件未知；分割结果的质量（如Dice系数）是否足以支撑生存预测仍需审视。
- **依赖先验图谱**：方法需要预先计算的TIL图谱，若TIL检测本身不准确或低分辨率下TIL信号稀疏，可能影响零样本分割和后续图学习。
- **实验覆盖**：仅在TCGA数据集上验证，其他来源（如临床试验样本、不同扫描仪）的泛化性未讨论；未与需要少量标注的半监督或弱监督方法深入比较。
- **解释性分析**：对异构图捕获的交互模式（如肿瘤-间质-免疫间的具体空间特征）可能缺乏充分的病理学关联解读。
- **计算成本降低的实际幅度**缺少量化对比，且未说明在极低分辨率下是否会丢失对预后关键的高频纹理细节。

（完）
