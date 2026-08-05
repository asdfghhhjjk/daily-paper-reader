---
title: "SpaCRD: Multimodal Deep Fusion of Histology and Spatial Transcriptomics for Cancer Region Detection"
title_zh: SpaCRD：组织学与空间转录组学的多模态深度融合用于癌症区域检测
authors: "Shuailin Xue, Jun Wan, Lihua Zhang, Wenwen Min"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38135/42097"
tags: ["query:profile"]
score: 4.0
evidence: 融合组织学与空间转录组学进行癌症区域检测和肿瘤微环境分析
tldr: 针对传统组织学图像癌症检测假阳性高的问题，提出SpaCRD框架，深度融合组织学图像与空间转录组学数据，利用细胞表型和空间定位信息提升癌症区域检测精度，促进肿瘤微环境分析。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 478}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1834, \"height\": 959}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 393}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 662, \"height\": 429}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 412}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 419}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 430}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1829, \"height\": 763}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 820}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 284}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 669, \"height\": 327}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 228}]"
motivation: 解决组织学图像中因形态相似导致的癌症区域误检问题。
method: 设计多模态融合网络整合组织学与空间转录组数据。
result: 在癌症区域检测任务上优于单一模态方法。
conclusion: 该方法展示了多模态数据在计算病理中的潜力。
---

## Abstract
Accurate detection of cancer tissue regions (CTR) enables deeper analysis of the tumor microenvironment and offers crucial insights into treatment response. Traditional CTR detection methods, which typically rely on the rich cellular morphology in histology images, are susceptible to a high rate of false positives due to morphological similarities across different tissue regions. The groundbreaking advances in spatial transcriptomics (ST) provide detailed cellular phenotypes and spatial localization information, offering new opportunities for more accurate cancer region detection. However, current methods are unable to effectively integrate histology images with ST data, especially in the context of cross-sample and cross-platform/batch settings for accomplishing the CTR detection. To address this challenge, we propose SpaCRD, a transfer learning-based method that deeply integrates histology images and ST data to enable reliable CTR detection across diverse samples, platforms, and batches. Once trained on source data, SpaCRD can be readily generalized to accurately detect cancerous regions across samples from different platforms and batches. The core of SpaCRD is a category-regularized variational reconstruction-guided bidirectional cross-attention fusion network, which enables the model to adaptively capture latent co-expression patterns between histological features and gene expression from multiple perspectives. Extensive benchmark analysis on 23 matched histology-ST datasets spanning various disease types, platforms, and batches demonstrates that SpaCRD consistently outperforms existing eight state-of-the-art methods in CTR detection.

---

## 论文详细总结（自动生成）

### SpaCRD：组织学与空间转录组学的多模态深度融合用于癌症区域检测

#### 1. 论文的核心问题与整体含义
- **研究动机**：癌症组织区域（CTR）的准确检测对肿瘤微环境分析和治疗反应评估至关重要。
- **背景与挑战**：
  - 传统基于组织学图像的方法因不同组织区域形态相似而假阳性率较高。
  - 空间转录组学（ST）提供了丰富的细胞表型和空间定位信息，但现有方法无法有效融合组织学图像与ST数据。
  - 跨样本、跨平台/批次的泛化存在巨大挑战，受到批间异质性和模态差异的限制。
- **整体含义**：提出 **SpaCRD**，一种基于迁移学习的深度融合框架，能够可靠地在多样化样本、平台和批次中实现CTR检测，有望提升临床诊断和生物医学研究的精度。

#### 2. 论文提出的方法论
- **核心思想**：通过迁移学习对齐不同模态，再结合双向交叉注意力与类别正则化变分重建，学习稳健的跨模态融合表示用于CTR分类。
- **三个关键阶段**：
  - **（一）模态对齐表示学习**：
    - 使用预训练的病理基础模型 **UNI** 提取组织学图像块特征。
    - 采用基于 CLIP 的对比学习，通过双向 InfoNCE 损失将图像和基因表达嵌入对齐到共享空间，减少模态间隙。
  - **（二）VRBCA 融合网络**：
    - **双向交叉注意力（BCA）**：基因引导和图像引导的交叉注意力模块，利用各点及其空间邻域的特征进行多视角交互融合，生成多模态表示。
    - **类别正则化变分自编码器（RVAE）**：对融合表示编码，通过引入类别特定的高斯先验（可学习的均值中心）和变分重建损失，鼓励产生去噪且类别紧凑的潜在嵌入。
  - **（三）癌症似然判别**：
    - 利用变分编码器输出的均值和对数方差，经过两层 MLP 预测癌症概率。
    - 训练损失 = 二进制交叉熵 + 融合损失（重建误差 + KL 散度正则化）。
    - 推理时用高斯混合模型（GMM）自动确定分类阈值。

#### 3. 实验设计
- **数据集**：总计 23 个匹配的组织学‑ST 数据集，涵盖：
  - 乳腺癌：STHBC（8个切片，跨样本评估）、10XHBC、ViHBC（Visium平台）、XeHBC（Xenium平台）、IDC，用于跨平台/批次评估。
  - 结直肠癌：12个CRC切片（跨样本评估）。
- **场景设置**：
  - **跨样本检测**：同平台样本间的留一验证。
  - **跨平台&批次检测**：在 STHBC（ST平台）上训练，直接迁移到 Visium 和 Xenium 等不同平台的标本上测试。
- **基准方法**：8种SOTA方法，包括多模态方法（MEATRD、STANDS、SpaCell、iStar、TESLA）、ST方法（STAGE、Spatial‑ID）和图像方法（SimpleNet）。
- **评估指标**：AUC、AP、F1‑score；分布分离度（KS距离）。

#### 4. 资源与算力
- **硬件**：单张 **NVIDIA RTX 3090 GPU**（24 GB 显存）。
- **软件**：PyTorch 2.1.1，Python 3.11.5。
- **训练时长**：正文未明确给出具体训练时间或总内存消耗，但提到在补充材料中进行了参数数目、运行时间和显存占用的效率分析。

#### 5. 实验数量与充分性
- **实验规模**：
  - 23个数据集上的全基准对比（20个跨样本 + 3个跨平台/批次），均重复5次并报告均值与标准差。
  - 消融实验：涵盖不同视觉特征提取器（UNI、ResNet、Swin‑T、HIPT）、输入模态（仅图像/仅ST）、融合模块组件（BCA、RVAE、CL）的逐一拆除。
  - 敏感性分析：对比损失权重 α、KL正则化系数 β、分类损失权重 γ、邻域大小等超参数的影响。
  - 效率与鲁棒性分析：参数/内存/运行时间对比（补充材料）、小样本训练稳定性分析。
  - 下游生物学分析：癌症严重程度分层（侵袭癌vs.原位癌vs.正常）和潜在病灶标记基因验证。
- **充分与公平性**：
  - 实验设计全面，覆盖了两类癌症、多平台和多批次，对比方法涵盖多种技术路线，且统一评价指标和随机种子，结果客观可靠。

#### 6. 论文的主要结论与发现
- SpaCRD 在所有跨样本和跨平台/批次测试中均**显著超越**8种SOTA方法，平均AUC、AP、F1提升约10%–14%。
- 在跨平台泛化任务（Visium/Xenium）上，模型仍表现优异，**缓解了平台和批次效应**。
- SpaCRD 能够**区分癌症的严重程度**（侵袭性癌平均得分0.91，原位癌0.64，正常0.17），而对比方法无法有效分离。
- 模型识别出的部分病理标注为正常但得分较高的斑点，其乳腺癌标志基因（ERBB2、CCND1）表达上调，暗示**检测到潜在的早期病变区域**。
- 消融实验证实了UNI提取器、双向交叉注意力和变分重建正则化等组件的关键作用。

#### 7. 优点
- **首次将迁移学习与多模态深度融合**用于癌症区域检测，实现了跨平台/批次的稳定泛化。
- **VRBCA网络**设计精巧，通过双向注意力和类别正则化变分重建有效抑制ST噪声并缩窄模态鸿沟。
- **实验扎实**：覆盖23个数据集、多种平台与两种癌症，与8种经典及最新方法对比，并进行了细致的模块化消融和下游生物学验证。
- **潜在临床价值**：不仅能检测癌症区域，还能对恶性程度分层并发现可疑区域，为病理诊断提供额外信息。
- 代码开源，增强了可复现性。

#### 8. 不足与局限
- **数据噪声依赖**：模型假设训练源数据有精确的癌症标注，若源标注存在噪声或错误，可能影响迁移学习效果。
- **癌症类型限制**：仅验证了乳腺癌和结直肠癌，未见对其他组织或更复杂癌症类型的测试，泛化性边界未知。
- **计算效率细节缺失**：文中未给出具体训练/推理时间和显存占用，仅说明在补充材料中，无法直接评估实际部署代价。
- **GMM阈值依赖**：推理阶段使用二分量GMM确定分类阈值，在样本量极少或分布复杂时可能不稳定，缺乏端到端的柔性边界。
- **未与其他SOTA深度融合方法对比**：2024‑2025年不断有新方法涌现，虽然比对了8种方法，但基线选择的时效性和广度仍可讨论。
- **模态假设**：需要配准良好的组织学图像和ST表达数据，若存在配准误差或切片质量差异，可能影响特征对齐效果。

（完）
