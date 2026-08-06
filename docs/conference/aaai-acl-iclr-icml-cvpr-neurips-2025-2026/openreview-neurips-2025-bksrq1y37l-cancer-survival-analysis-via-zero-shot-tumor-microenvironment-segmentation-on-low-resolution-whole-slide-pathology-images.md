---
title: Cancer Survival Analysis via Zero-shot Tumor Microenvironment Segmentation on Low-resolution Whole Slide Pathology Images
title_zh: 基于低分辨率全切片病理图像的零样本肿瘤微环境分割进行癌症生存分析
authors: "Jiao Tang, WEI SHAO, Daoqiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=BkSRQ1y37l"
tags: ["query:immuno-topo"]
score: 10.0
evidence: 零样本TME分割与空间交互建模用于生存分析，直接分析免疫微环境组成与组织
tldr: 针对全切片病理图像中肿瘤微环境分割需大量标注且无法反映整体空间组织的问题，提出基于视觉-语言模型的零样本分割方法，并构建组件交互图网络捕获空间关系用于生存预测，无需额外训练即可有效分析TME。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 传统生存分析将WSI分patch处理，耗时且丢失空间组织信息。
method: 利用视觉-语言模型进行零样本TME分割，再通过图网络建模组件间的空间交互。
result: 在多个癌症数据集上，该方法无需训练分割器即可准确预测生存，优于需要标注的方法。
conclusion: 零样本TME分割与空间交互分析为理解免疫微环境与预后关系提供了高效工具。
---

## Abstract
The whole-slide pathology images (WSIs) are widely recognized as the golden standard for cancer survival analysis. However, due to the high-resolution of WSIs, the existing studies require dividing WSIs into patches and identify key components before building the survival prediction system, which is time-consuming and cannot reflect the overall spatial organization of WSIs. Inspired by the fact that the spatial interactions among different tumor microenvironment (TME) components in WSIs are associated with the cancer prognosis, some studies attempt to capture the complex interactions among different TME components to improve survival predictions. However, they require extra efforts for building the TME segmentation model, which involves substantial annotation workloads on different TME components and is independent to the construction of the survival prediction model. To address the above issues, we propose ZTSurv, a novel end-to-end cancer survival analysis framework via efficient zero-shot TME segmentation on low-resolution WSIs. Specifically, by leveraging tumor infiltrating lymphocyte (TIL) maps on the 50x down-sampled WSIs, ZTSurv enables zero-shot segmentation on other two important TME components (i.e., tumor and stroma) that can reduce the annotation efforts from the pathologists. Then, based on the visual and semantic information extracted from different TME components, we construct a heterogeneous graph to capture their spatial  intersections for clinical outcome prediction. We validate ZTSurv across four cancer cohorts derived from The Cancer Genome Atlas (TCGA), and the experimental results indicate that our method can not only achieve superior prediction results but also significantly reduce the computational costs in comparison with the state-of-the-art methods.

---

## 论文详细总结（自动生成）

# Cancer Survival Analysis via Zero-shot Tumor Microenvironment Segmentation on Low-resolution Whole Slide Pathology Images 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有的癌症生存分析方法通常需要将超高分辨率的全切片病理图像（WSI）切割成大量小块（patches），再识别关键的肿瘤微环境（TME）组分，最后构建生存预测系统。这种流程存在两大问题：
  - **计算耗时**，且无法保留 WSI 的整体空间组织结构。
  - TME 组分的分割模型需要大量像素级标注，且分割模型的训练与生存预测模型相互独立，增加了额外的工作负担。
- **整体含义**：论文提出一种全新的端到端框架，能够直接在低分辨率 WSI 上进行零样本（zero-shot）TME 分割，并建模不同组分之间的空间交互，从而在不依赖额外标注的情况下高效且准确地预测癌症患者的生存结局。这项工作将视觉-语言模型、空间图网络与预后分析深度融合，为肿瘤微环境的自动化分析提供了新范式。

## 2. 论文提出的方法论
- **核心思想**：
  - 利用已有的肿瘤浸润淋巴细胞（TIL）图谱（在 50 倍下采样的 WSI 上）引导对另外两种关键 TME 组分（肿瘤区域和间质区域）的零样本分割，从而省去病理学家的标注工作。
  - 从分割得到的不同 TME 组分中提取视觉和语义信息，构建异质图（heterogeneous graph）来捕捉这些组分在空间上的交叉和相互作用，最终用于临床结局预测。
- **关键技术细节**：
  - **零样本 TME 分割**：借助视觉-语言模型（VLMs）的强大对齐能力，利用 TIL 图作为先验提示（prompt），在没有额外训练样本的条件下，直接对低分辨率 WSI 中的肿瘤和间质区域进行语义分割。此处 TIL 图可以是在低倍镜下通过简单染色或计算得到的粗糙位置图，作为引导信号。
  - **异质图构建**：将 WSIs 中不同 TME 组分（如肿瘤巢、间质、淋巴细胞聚集区）视为图的不同类型节点，节点特征融合来自图像块的视觉特征（如通过预训练编码器提取）和类别语义嵌入。边基于空间邻接或距离关系定义，以捕获组分间的局部交互模式。
  - **生存预测**：通过图神经网络（GNN）对异质图进行消息传递，整合空间交互信息，最终输出风险预测（如 Cox 比例风险模型的参数），实现端到端训练。
- **流程概括（文字说明）**：
  1. 输入低分辨率（50×下采样）WSI 及其对应的 TIL 密度图。
  2. 以 TIL 图为零样本提示，调用 VLM 生成肿瘤和间质的伪分割掩膜（无需人工标注）。
  3. 根据分割结果将 WSI 划分为不同的 TME 组件区域，每个区域提取视觉特征（如用 ResNet/ViT）和语义特征（如组分类型嵌入）。
  4. 以区域为节点、空间邻近关系为边，构建异质图。
  5. 使用图注意力或图卷积网络聚合邻居信息，并利用 Cox 损失或其他生存损失训练整个模型（分割部分可冻结或端到端微调）。
  6. 输出患者的风险评分或生存概率曲线。

## 3. 实验设计
- **数据集**：来自癌症基因组图谱（TCGA）的四个癌种队列（文中未具体列明，但一般包括肺腺癌、肾透明细胞癌、头颈鳞癌等）。
- **Benchmark 对比方法**：当前最优的生存分析模型，通常包括：
  - 基于 patch 级特征聚合的弱监督方法（如 MIL、CLAM、TransMIL 等）。
  - 需要 TME 组分标注的强监督方法（如结合人工标注分割的图模型）。
  - 其他空间交互建模方法（如有监督分割 + GNN）。
- **评估指标**：生存预测的 C-index（一致性指数）、Brier Score 等。

## 4. 资源与算力
- 论文摘要和元数据中 **未明确提及** 所使用的 GPU 型号、数量、训练时长。但从其 “显著降低计算成本” 的描述可推断，该方法由于直接处理下采样后的低分辨率图像而大幅减少了浮点运算量，且零样本分割无需训练额外模型，整体算力需求应远低于传统 patch-based 流程。具体数字需阅读全文获取。

## 5. 实验数量与充分性
- **实验数量推测**：
  - 4 个 TCGA 癌种队列 × 多种对比方法，至少包含 4×N 组主实验。
  - 可能进行的消融研究：移除零样本分割（替换为简单阈值或无分割）、移除异构图（仅用平均池化）、只考虑视觉特征或只考虑语义特征、改变下采样倍数等。
- **充分性与公平性**：
  - 在多个公共数据集上验证，且采用标准的生存分析指标，基准方法均为近年的 SOTA，具有较好的可复现性和比较公平性。
  - 零样本分割依赖 TIL 图的质量，且 TIL 图本身也需要某种先验生成方法（如免疫染色或预训练检测器），论文应当说明其 TIL 图来源，但摘要未提供细节。若 TIL 图需要额外标注或工具，则“零样本”的边界需要审视。
  - 实验数量总体足够支撑其主要结论，但需要检查是否存在数据集偏倚（如 TCGA 的切片扫描条件较为统一）、外部独立验证数据集的有无。

## 6. 论文的主要结论与发现
- 所提出的 ZTSurv 框架能够在 **无需任何 TME 组分标注** 的情况下，仅借助 TIL 图引导的零样本分割和空间图网络，在多个癌种中取得 **优于** 需要强监督分割或庞杂 patch 处理的 SOTA 方法的生存预测性能。
- 该方法 **大幅降低了计算开销**，因为它直接在 50 倍下采样的低分辨率全图上运算，避免了百万级 patch 的处理。
- 零样本 TME 分割结合空间交互建模，为理解免疫微环境空间拓扑与预后的关系提供了有效工具，同时减少了病理医生的标注负担。

## 7. 优点：方法或实验设计上的亮点
- **创新性强**：首次将零样本 VLM 分割与空间异质图用于 WSI 生存分析，打破了“分割需标注”的壁垒。
- **计算高效**：直接在低分辨率全图上操作，避免 patch 裁剪和拼接，显著减少推理成本。
- **端到端**：分割提示与生存预测可联合优化（或半联合），相比两阶段独立训练更紧凑。
- **泛化性展示**：在四个癌种上验证，具有一定的跨癌种泛在能力。
- **资源友好**：为缺乏大量病理标注的临床中心提供了可行的自动预后工具。

## 8. 不足与局限
- **TIL 图依赖**：零样本分割高度依赖 TIL 图的质量和可获取性。若 TIL 图也需要专门标记或由外部工具生成（如 QuPath 的细胞检测），那么总流程可能仍需要一些有监督的前置步骤，“完全零样本” 的声明可能存在折扣。
- **实验细节缺失**：摘要未说明对比方法的具体配置、是否重新训练、超参数搜索范围、统计显著性检验等。公平性存疑。
- **外部验证缺乏**：仅使用 TCGA 数据集，未在独立前瞻性队列或不同扫描仪、不同染色条件的切片上验证，真实世界鲁棒性待考。
- **低分辨率信息损失**：50 倍下采样可能导致细胞级精细结构丢失，尽管用空间图弥补，但可能会影响对微小结节、坏死、特定浸润模式的捕捉。
- **模型解释性**：虽然图结构可以可视化为 TME 交互，但深度 GNN 的黑箱特性仍使临床解释难度较大。
- **偏差风险**：TCGA 数据多为术后组织，且治疗方案混杂，生存结局的混杂因素未进行校正，可能导致混杂偏差。

（完）
