---
title: "SpaCRD: Multimodal Deep Fusion of Histology and Spatial Transcriptomics for Cancer Region Detection"
title_zh: "SpaCRD: 组织学与空间转录组学多模态深度融合用于癌区检测"
authors: "Shuailin Xue, Jun Wan, Lihua Zhang, Wenwen Min"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38135/42097"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 检测组织学图像中的癌症区域以实现更深入的肿瘤微环境分析
tldr: SpaCRD融合组织学图像与空间转录组学数据，用于精确的癌组织区域检测，解决了仅依赖形态学易产生假阳性的问题。该方法利用多模态深度学习，在跨样本和跨平台场景中有效整合两种数据，提高了检测准确性。实验表明，该方法优于传统方法，为肿瘤微环境分析和治疗反应预测提供了可靠基础，推动了计算病理学中重要区域识别的发展。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 478}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1834, \"height\": 959}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 393}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 662, \"height\": 429}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 412}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 419}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 430}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1829, \"height\": 763}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 820}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 284}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 669, \"height\": 327}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 228}]"
motivation: 传统癌区检测依赖组织学形态易误判，空间转录组学提供细胞表型和定位信息但融合困难。
method: 提出多模态深度融合网络，协同组织学图像和空间转录组学数据，实现跨样本、跨平台的有效整合。
result: 在多个数据集上显著提高癌组织区域检测准确率，降低假阳性。
conclusion: 多模态融合提升癌区检测可靠性，为肿瘤微环境分析和治疗研究提供有力工具。
---

## Abstract
Accurate detection of cancer tissue regions (CTR) enables deeper analysis of the tumor microenvironment and offers crucial insights into treatment response. Traditional CTR detection methods, which typically rely on the rich cellular morphology in histology images, are susceptible to a high rate of false positives due to morphological similarities across different tissue regions. The groundbreaking advances in spatial transcriptomics (ST) provide detailed cellular phenotypes and spatial localization information, offering new opportunities for more accurate cancer region detection. However, current methods are unable to effectively integrate histology images with ST data, especially in the context of cross-sample and cross-platform/batch settings for accomplishing the CTR detection. To address this challenge, we propose SpaCRD, a transfer learning-based method that deeply integrates histology images and ST data to enable reliable CTR detection across diverse samples, platforms, and batches. Once trained on source data, SpaCRD can be readily generalized to accurately detect cancerous regions across samples from different platforms and batches. The core of SpaCRD is a category-regularized variational reconstruction-guided bidirectional cross-attention fusion network, which enables the model to adaptively capture latent co-expression patterns between histological features and gene expression from multiple perspectives. Extensive benchmark analysis on 23 matched histology-ST datasets spanning various disease types, platforms, and batches demonstrates that SpaCRD consistently outperforms existing eight state-of-the-art methods in CTR detection.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：癌组织区域（CTR）的准确检测对肿瘤微环境分析、治疗策略制定至关重要。
- **现有痛点**：
  - 传统方法依赖组织学图像（H&E）的细胞形态，易因不同区域形态相似而出现高假阳性。
  - 空间转录组学（ST）提供细胞表型与空间定位，但数据噪声大，且仅依赖标记基因的方法受限于先验知识不全。
  - 当前多模态融合方法（如简单拼接、视觉异常检测范式）未能有效整合组织学与ST，且难以跨样本、跨平台/批次泛化。
- **论文目标**：提出一种基于迁移学习与多模态深度融合的框架，可靠地在不同样本、平台、批次间检测癌区。

### 2. 方法论：核心思想与关键技术细节
- **总体框架**：SpaCRD 包含三个阶段：
  1. **模态对齐表示学习**：用病理基础模型 UNI 提取组织学特征，通过基于 CLIP 的双向对比损失将图像特征与基因表达对齐到同一隐空间。
  2. **VRBCA 融合网络**：使用双向交叉注意力（BCA）分别以基因指导图像和图像指导基因进行跨模态交互，同时融合近邻点位信息；再通过类别正则化变分自编码器（RVAE）对融合表示进行去噪与结构化。
  3. **癌变似然估计**：利用 VRBCA 编码器输出的潜在均值和方差，送入两层 MLP 分类器，结合二元交叉熵与融合损失训练；推理时采用高斯混合模型自动确定阈值。
- **关键公式与流程**（文字说明）：
  - 特征提取：图像块通过 UNI 得到 `x_img`，基因表达归一化为 `x_gene`。
  - 对比对齐：轻量 MLP 编码器分别映射，计算缩放点积相似度矩阵，双向 InfoNCE 损失加权组合。
  - 双向交叉注意力：对每个点，将其与邻居的特征构成输入矩阵，分别执行基因指导与图像指导的交叉注意力，拼接中心点输出，通过 MLP 得到 `h*`。
  - 类别正则化 VAE：编码融合表示得到潜在分布，解码重构，训练损失包含重构误差与类别条件 KL 散度（各类先验均值可学习）。
  - 分类损失：`L_cls = L_BCE + γ·L_fused`。

### 3. 实验设计
- **数据集**：
  - 共 23 对匹配的组织学-ST 数据集，涵盖乳腺癌和结直肠癌，来自多个平台（ST、Visium、Xenium）和批次。
  - 具体：8 个乳腺癌（STHBC A-H）、12 个结直肠癌（CRC A1-G2）用于跨样本评估；ViHBC（Visium）、XeHBC（Xenium）、IDC（Visium）用于跨平台/批次评估。
- **对比方法**（8 种 SOTA）：
  - 多模态：MEATRD、STANDS、SpaCell、iStar、TESLA
  - 仅 ST：STAGE、Spatial-ID
  - 仅图像：SimpleNet
- **评估指标**：AUC、AP、F1-score，以及 KS 距离（衡量癌与非癌预测得分分布分离度）。

### 4. 资源与算力
- 论文明确提及：所有实验在单块 NVIDIA RTX 3090 GPU（24 GB 显存）上运行。
- 开发环境：PyTorch 2.1.1，Python 3.11.5。
- 训练时长未明确指出，但提供了详细架构与超参设置（补充材料），效率分析见原文附录。

### 5. 实验数量与充分性
- **核心实验组数**：
  - 跨样本 CTR 检测：20 个数据集上的留一法验证（12 结直肠 + 8 乳腺癌），每项重复 5 次，给出均值与标准差。
  - 跨平台/批次 CTR 检测：以 STHBC 为源域，测试 ViHBC、IDC、XeHBC 三个不同平台数据集。
  - 消融实验：覆盖全数据集（11 乳腺癌 + 12 结直肠），比较不同特征提取器（UNI、ResNet50、Swin-Tiny、HIPT）、模态缺失（仅图像、仅 ST）、模块移除（无 BCA、无 RVAE、无 VRBCA、无对比学习）的 4 组消融。
  - 敏感度分析：11 个乳腺癌数据集上对超参 α、β、γ 及邻居点数进行扫描。
  - 效率分析：参数量、运行时间、内存对比。
  - 小样本训练分析：用少于 10% 的训练点仍保持稳定的跨平台性能。
  - 下游分析：XeHBC 上的癌严重程度分层、IDC 中潜在癌变区域发现。
- **充分性评价**：
  - 数据集覆盖面广（多疾病、多平台），对比方法涵盖单模态与多模态 SOTA，评估指标丰富，重复实验保证稳定性。
  - 消融实验全面，敏感性与效率分析到位，实验设计较客观、公平。

### 6. 主要结论与发现
- SpaCRD 在所有 23 个数据集上均取得最优 AUC、AP、F1-score，平均比次优方法提升约 12%–14%。
- 在跨平台/批次场景下优势显著，证明有效缓解了技术/批次效应。
- 预测得分能有效区分浸润性癌、原位癌与正常组织，且可能揭示标注为良性但基因表达异常的高风险区域。
- 消融实验证实了 UNI 特征提取器、对比对齐、VRBCA 各模块均不可或缺。

### 7. 优点（方法与实验设计的亮点）
- **创新性融合**：首次将多模态深度融合与迁移学习结合用于癌区检测，提出双向交叉注意力加类别正则化 VAE 的紧凑嵌入。
- **泛化性强**：设计了模态对齐和跨平台泛化能力，在多个平台和批次上保持高性能。
- **生物学可解释性**：不仅能检测癌区，还可分层严重程度，并发现潜在的高风险区域，具有一定临床应用前景。
- **实验严谨**：数据集多样、对比方法广泛、指标综合、多轮重复、附有详细分析（效率、小样本、超参）。

### 8. 不足与局限
- **手动标注依赖**：训练仍需要癌区/正常标注，且标注可能不完美，影响模型上限。
- **计算资源**：虽在单卡 3090 上可跑，但基于 UNI 提取特征可能前期预处理耗时，整体推理效率未详述。
- **数据覆盖有限**：仅评估了乳腺癌和结直肠癌，其他癌种推广性待验证。
- **潜在偏差**：源域 STHBC 为特定乳腺癌数据集，迁移至其他癌种效果未知；模型可能学到具体染色模式而非通用癌特征。
- **应用限制**：方法依赖配对的组织学-ST 数据，实际临床中 ST 数据获取成本高，部署受限。
- **超参敏感**：部分超参（如 γ）对性能有一定影响，虽然进行了敏感性分析，但最佳设置可能随数据集变化。

（完）
