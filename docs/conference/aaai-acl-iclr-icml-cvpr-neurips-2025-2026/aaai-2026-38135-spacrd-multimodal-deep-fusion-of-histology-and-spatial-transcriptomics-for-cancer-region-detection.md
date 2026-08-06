---
title: "SpaCRD: Multimodal Deep Fusion of Histology and Spatial Transcriptomics for Cancer Region Detection"
title_zh: "SpaCRD: 组织学与空间转录组学多模态深度融合用于癌症区域检测"
authors: "Shuailin Xue, Jun Wan, Lihua Zhang, Wenwen Min"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38135/42097"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 深度融合组织学与空间转录组学用于肿瘤微环境分析
tldr: 提出一种结合组织学图像与空间转录组学的多模态深度融合方法，用于精确检测癌症组织区域，支持深入的肿瘤微环境分析。通过跨模态融合克服了仅靠组织学形态容易产生的假阳性问题，实验表明所提方法在跨样本和跨平台场景下具有优越的准确性和泛化能力，为肿瘤微环境空间解析提供了强大工具。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 478}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1834, \"height\": 959}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 393}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 662, \"height\": 429}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 412}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 419}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 430}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1829, \"height\": 763}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 820}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 284}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 669, \"height\": 327}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 228}]"
motivation: 解决传统仅依赖组织学图像进行癌症区域检测时形态相似性导致的高假阳性率问题。
method: 构建多模态深度融合框架，同时提取组织学形态特征与空间转录组学基因表达模式，通过特征对齐与融合实现跨模态协同检测。
result: 在多个公开数据集上显著提升了癌症区域检测精度，并展现出跨样本与跨平台的良好泛化性。
conclusion: 融合组织形态与分子空间信息可大幅提升肿瘤区域检测的可靠性，为计算病理学中肿瘤微环境研究开辟新途径。
---

## Abstract
Accurate detection of cancer tissue regions (CTR) enables deeper analysis of the tumor microenvironment and offers crucial insights into treatment response. Traditional CTR detection methods, which typically rely on the rich cellular morphology in histology images, are susceptible to a high rate of false positives due to morphological similarities across different tissue regions. The groundbreaking advances in spatial transcriptomics (ST) provide detailed cellular phenotypes and spatial localization information, offering new opportunities for more accurate cancer region detection. However, current methods are unable to effectively integrate histology images with ST data, especially in the context of cross-sample and cross-platform/batch settings for accomplishing the CTR detection. To address this challenge, we propose SpaCRD, a transfer learning-based method that deeply integrates histology images and ST data to enable reliable CTR detection across diverse samples, platforms, and batches. Once trained on source data, SpaCRD can be readily generalized to accurately detect cancerous regions across samples from different platforms and batches. The core of SpaCRD is a category-regularized variational reconstruction-guided bidirectional cross-attention fusion network, which enables the model to adaptively capture latent co-expression patterns between histological features and gene expression from multiple perspectives. Extensive benchmark analysis on 23 matched histology-ST datasets spanning various disease types, platforms, and batches demonstrates that SpaCRD consistently outperforms existing eight state-of-the-art methods in CTR detection.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：癌症组织区域检测对肿瘤微环境分析和治疗响应评估至关重要。传统方法依赖组织学图像的细胞形态，但因不同组织区域的形态相似性（如炎症与肿瘤），导致假阳性率较高。空间转录组学可提供细胞表型与空间位置信息，有望提升检测精度，但现有方法难以在跨样本、跨平台 / 批次场景下有效融合组织学图像和 ST 数据。
- **整体含义**：该研究旨在通过迁移学习和多模态深度融合，构建一个能泛化到不同样本、技术平台和实验批次的癌症区域检测框架，以克服形态歧义和 ST 数据噪声，实现更鲁棒、准确的检测。

### 2. 论文提出的方法论
- **总体框架（SpaCRD）**：分为三阶段训练 —— 模态对齐表征学习、VRBCA 融合网络和癌症似然估计。
- **模态对齐表征学习**：
  - 使用病理基础模型 UNI 提取组织学图像块特征（无需微调）。
  - 采用类似 CLIP 的对比学习策略，通过轻量 MLP 编码器将图像特征和基因表达向量映射到共享隐空间，最小化双向 InfoNCE 损失，对齐配对样本，缩小模态鸿沟。
- **VRBCA 融合网络**：
  - **双向交叉注意力（BCA）**：构建基因引导和图像引导两个交叉注意力模块，对每个 spot 及其邻居的两种模态特征进行交叉建模，输出融合后的多模态表示。
  - **类别正则化变分自编码器（RVAE）**：对融合表示进行变分重建，并引入类别特定的高斯先验（类别正则化），迫使隐空间按癌 / 非癌类别聚集，同时去除噪声，生成紧凑、类一致的嵌入。训练目标包含重建损失和类别 KL 散度。
- **癌症似然判别器**：
  - 将 RVAE 编码器输出的均值与对数方差拼接，输入两层 MLP 预测癌症概率；损失函数为 BCE 损失与融合损失加权和。
  - 推理时用双分量高斯混合模型（GMM）自动确定分类阈值。

### 3. 实验设计
- **数据集**：总计 23 个配对的组织学 - ST 数据集。
  - **乳腺癌**：STHBC（8 个切片，跨样本）、10XHBC、XeHBC、IDC（跨平台 / 批次，平台包括 ST、Visium、Xenium）。
  - **结直肠癌**：CRC A1–G2（12 个切片，跨样本）。
- **评估场景**：
  - **跨样本检测**：留一法交叉验证（在 STHBC 和 CRC 上）。
  - **跨平台 / 批次检测**：在 STHBC 上训练，在 ViHBC、XeHBC、IDC 上测试。
- **对比方法**：8 种 SOTA 方法，包括多模态（MEATRD, STANDS, SpaCell-Plus, iStar, TESLA）、纯 ST（STAGE, Spatial-ID）和纯图像（SimpleNet）。
- **评价指标**：AUC、AP、F1-score，并引入 KS 距离衡量健康 / 肿瘤区域预测得分的分布分离程度。

### 4. 资源与算力
- **硬件**：单张 NVIDIA RTX 3090 GPU（24 GB 显存）。
- **软件环境**：PyTorch 2.1.1，Python 3.11.5。
- **训练时长**：论文未明确给出具体的单次训练耗时或总实验耗时，仅指出计算开销在可接受范围，并在补充材料中进行了效率分析。

### 5. 实验数量与充分性
- **实验组数**：
  - 跨样本：20 组（12 个 CRC + 8 个 STHBC 切片）留一验证。
  - 跨平台 / 批次：3 组（ViHBC, XeHBC, IDC）。
  - 消融实验：5 组模块 / 模态消融（仅图像、仅 ST、去除 BCA、去除 RVAE、去除 CL）。
  - 特征提取器消融：3 种替换（ResNet50, Swin-Tiny, HIPT）。
  - 超参数敏感性分析：涉及 α, β, γ 及邻居数。
  - 下游分析：癌症严重程度分层、潜在病变区域检测。
- **充分性与公平性**：覆盖两大癌种、多种平台，对比方法全面，所有实验重复 5 次并报告均值和标准差，消融和敏感性分析详尽，实验设计客观、公平。

### 6. 论文的主要结论与发现
- SpaCRD 在所有数据集和场景下均显著优于 8 种基线方法，跨样本平均 AUC 提升约 13.5%，跨平台 / 批次提升约 12.1%。
- VRBCA 模块能有效融合多模态数据，类别正则化可促进类内紧凑性，双向交叉注意力充分利用了基因 - 图像双重信号。
- 通过迁移学习，SpaCRD 有效缓解了批次效应，展现出强大的跨平台泛化能力。
- 癌症似然得分能区分浸润癌、原位癌和正常组织，并能在标注正常的区域中识别出高表达癌标志基因的潜在早期病变，具有辅助风险分层的潜力。

### 7. 优点
- **新颖的融合设计**：双向交叉注意力与类别正则化 VAE 的组合，在特征交互和噪声过滤上兼具优势。
- **泛化能力强**：通过迁移学习和隐空间对齐，在无目标域微调的情况下直接实现跨平台检测。
- **实验验证充分**：涵盖多种癌种、平台，与多个 SOTA 方法对比，消融和敏感性分析完备，并提供代码。
- **生物学可解释性**：预测分数与癌症严重程度及标志基因表达高度相关，可发现潜在病变。

### 8. 不足与局限
- **训练时长未明确**：论文未给出具体训练耗时，影响对方法实际部署可行性的判断。
- **癌种覆盖面有限**：仅测试了乳腺癌和结直肠癌，对其他癌症类型或正常组织中的罕见病变检测效果未知。
- **依赖配对数据**：训练需成对的组织学图像和 ST 数据，限制了在不提供 ST 数据的常见病理场景下的应用。
- **显著性依赖预训练模型**：方法性能高度依赖 UNI 病理基础模型，更换为非病理专用或轻量级提取器后性能下降明显，可能限制在非标准染色或低资源环境的使用。
- **标注质量依赖**：模型训练依赖病理学家手动标注的真值，可能存在标注主观性或边界模糊问题，影响模型学习。
- **阈值自动选取**：GMM 假设分布为双高斯分量，在非平衡或极端分布下可能失效。

（完）
