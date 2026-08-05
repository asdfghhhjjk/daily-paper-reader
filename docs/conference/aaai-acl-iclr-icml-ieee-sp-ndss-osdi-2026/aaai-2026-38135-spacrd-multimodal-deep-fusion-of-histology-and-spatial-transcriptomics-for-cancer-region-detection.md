---
title: "SpaCRD: Multimodal Deep Fusion of Histology and Spatial Transcriptomics for Cancer Region Detection"
title_zh: SpaCRD：融合组织学和空间转录组学的多模态深度方法用于癌症区域检测
authors: "Shuailin Xue, Jun Wan, Lihua Zhang, Wenwen Min"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38135/42097"
tags: ["query:tme-evidence"]
score: 9.0
evidence: 融合组织学和空间转录组学进行癌症区域检测，从组织病理图像中分析肿瘤微环境。
tldr: SpaCRD针对传统基于组织学的癌症区域检测易产生假阳性的问题，提出一种融合组织学图像与空间转录组学数据的多模态深度方法。该方法利用空间转录组学提供的细胞表型和空间定位信息，通过跨样本、跨平台的对齐和融合策略，实现更准确的癌症区域检测。实验表明，多模态融合能有效降低假阳性率，为肿瘤微环境的深入分析和治疗反应评估提供了更可靠的基础。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1834, \"height\": 959, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 662, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 430, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1829, \"height\": 763, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 820, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 669, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 228, \"label\": \"Table\"}]"
motivation: 单纯依靠组织学图像形态相似性易导致癌症区域误检，空间转录组学可提供细胞表型信息来改善。
method: 设计跨模态对齐与融合网络，整合组织学图像特征和空间转录组学中的基因表达与空间定位数据。
result: 多模态融合显著降低了癌症检测的假阳性率，并在跨样本和跨平台场景下表现出良好泛化能力。
conclusion: 融合组织学与空间转录组学能提升癌症区域检测精度，为肿瘤微环境分析提供更丰富的证据。
---

## Abstract
Accurate detection of cancer tissue regions (CTR) enables deeper analysis of the tumor microenvironment and offers crucial insights into treatment response. Traditional CTR detection methods, which typically rely on the rich cellular morphology in histology images, are susceptible to a high rate of false positives due to morphological similarities across different tissue regions. The groundbreaking advances in spatial transcriptomics (ST) provide detailed cellular phenotypes and spatial localization information, offering new opportunities for more accurate cancer region detection. However, current methods are unable to effectively integrate histology images with ST data, especially in the context of cross-sample and cross-platform/batch settings for accomplishing the CTR detection. To address this challenge, we propose SpaCRD, a transfer learning-based method that deeply integrates histology images and ST data to enable reliable CTR detection across diverse samples, platforms, and batches. Once trained on source data, SpaCRD can be readily generalized to accurately detect cancerous regions across samples from different platforms and batches. The core of SpaCRD is a category-regularized variational reconstruction-guided bidirectional cross-attention fusion network, which enables the model to adaptively capture latent co-expression patterns between histological features and gene expression from multiple perspectives. Extensive benchmark analysis on 23 matched histology-ST datasets spanning various disease types, platforms, and batches demonstrates that SpaCRD consistently outperforms existing eight state-of-the-art methods in CTR detection.

---

## 论文详细总结（自动生成）

# 论文总结：SpaCRD——融合组织学与空间转录组学的癌症区域检测

## 1. 核心问题与研究动机
- **研究问题**：癌症组织区域（CTR）的准确检测是肿瘤微环境分析和治疗决策的基础。传统方法主要依赖组织学图像中的细胞形态，但由于不同组织区域形态学相似性高（如炎症与肿瘤边缘）和染色质量不稳定，导致假阳性率上升。
- **研究动机**：空间转录组学（ST）能够同时提供全转录本表达与空间位置信息，为区分形态相似但分子状态不同的区域提供了新机遇。然而，现有方法难以有效融合组织学图像与 ST 数据，尤其是在跨样本、跨平台/批次检测时存在严重的批次异质性和模态差异。
- **整体含义**：本文提出一种基于迁移学习的多模态深度融合框架，旨在利用对齐的组织学图像与基因表达特征，实现跨样本、跨平台/批次的稳健癌症区域检测，从而为临床诊断和肿瘤微环境分析提供更可靠的自动化工具。

## 2. 方法论（核心思想与关键技术细节）
- **总体框架**：SpaCRD 由三个阶段构成：
  - **阶段 I：模态对齐表示学习**  
    - 使用病理基础模型 **UNI**（大规模组织学预训练）提取每个空间位点的图像块特征（\( \mathbf{x}_i^{img} \)）。
    - 设计轻量级 MLP 编码器分别处理图像特征和归一化的基因表达向量，通过对比学习（InfoNCE 双向损失）将两种模态映射到共享嵌入空间，拉近同一位点的表示，推远不同位点。
  - **阶段 II：VRBCA 融合网络**  
    - **双向交叉注意力（BCA）**：以基因引导注意力和 H&E 引导注意力分别计算查询、键、值，通过多头注意力捕捉邻域位点间的跨模态交互，生成融合多模态表示 \( \mathbf{h}_i^* \)。
    - **类别正则化变分自编码器（RVAE）**：在 VAE 的隐空间中为肿瘤 / 正常位点分别设置可学习的均值中心 \( \mu_{y_i} \)，通过重构融合表示和拉近同类样本到对应中心来学习紧凑的类别特异性嵌入，同时去噪。
  - **阶段 III：癌症似然估计**
    - 将 RVAE 编码器输出的均值与对数方差拼接，通过两层 MLP 分类器预测癌症似然分数。
    - 推理时，使用双组分高斯混合模型（GMM）自适应确定分类阈值。
- **关键公式（文字说明）**：
  - 对比损失：\( \mathcal{L}_{\text{contrast}} = \alpha \mathcal{L}_{\text{img→gene}} + (1-\alpha) \mathcal{L}_{\text{gene→img}} \)。
  - 融合表示的重构损失加 KL 散度正则：\( \mathcal{L}_{\text{fused}} = \frac{1}{n}\sum_i [\| \hat{\mathbf{h}}_i^* - \mathbf{h}_i^* \|^2 + \beta \cdot D_{KL}^{\text{cls}}(q_i\|p_{y_i})] \)，其中后验分布 \( q_i \) 被拉向类别特定的高斯先验。
  - 最终分类损失：\( \mathcal{L}_{\text{cls}} = \mathcal{L}_{\text{BCE}} + \gamma \mathcal{L}_{\text{fused}} \)。

## 3. 实验设计
- **数据集与场景**：共使用 5 个数据集、23 张匹配的组织学-ST 组织切片：
  - **跨样本评估**：乳腺癌 STHBC（8 张切片）、结直肠癌 CRC（12 张切片），采用留一交叉验证。
  - **跨平台/批次评估**：在 ST 平台（STHBC）上训练，在 Visium 平台（ViHBC、IDC）和 Xenium 平台（XeHBC）上测试。
- **对比方法**（8 个前沿基准）：五类多模态方法（MEATRD、STANDS、SpaCell、iStar、TESLA），两类纯 ST 方法（STAGE、Spatial-ID），一类纯图像方法（SimpleNet）。
- **评价指标**：AUC、AP、F1-score、KS 距离（衡量健康与肿瘤区域的分布分离度）。

## 4. 资源与算力
- **硬件**：单块 NVIDIA RTX 3090 GPU（24 GB 显存）。
- **软件**：PyTorch 2.1.1，Python 3.11.5。
- **训练时长与能耗**：论文未明确报告单次训练的具体小时数或总能耗，但指出采用留一交叉验证，结合多个数据集的实验，计算开销在可接受范围内（详见补充材料的效率分析部分）。

## 5. 实验数量与充分性
- **主要实验组数约**：
  - 跨样本 20 个测试场景（8 个乳腺癌 + 12 个结直肠癌）。
  - 跨平台/批次 3 个测试场景（ViHBC、IDC、XeHBC）。
  - 消融实验：特征提取器对比（4 种）、模态与模块对比（6 种）、超参数敏感性分析（4 个超参数）、邻近位点数量影响。
  - 毒理 / 下游分析：癌症严重程度分层、潜在癌变区域识别。
  - 小样本训练效率分析。
- **实验充分性评价**：
  - 覆盖多癌种、多平台、跨样本的广泛基准，对比方法包含多种范式，实验设计较全面。
  - 消融覆盖核心组件（对比学习、BCA、RVAE、UNI 特征提取器）和重点超参数，能够支撑模块有效性结论。
  - 采用多次独立运行（5 次）报告均值和标准差，提升了结果的可信度。
  - 不足之处在于未公开极端低资源或不同组织来源的迁移测试，但整体实验设置较为客观、公平。

## 6. 主要结论与发现
- SpaCRD 在所有跨样本和跨平台/批次实验中，AUC、AP、F1 等指标均显著优于 8 种对比方法，平均 AUC 提升约 13.5%（跨样本）和 12.1%（跨平台）。
- VRBCA 融合模块能够有效捕捉跨模态共表达模式并过滤噪声，生成的类别特异性嵌入明显改善癌症与健康组织的分布分离（KS 距离中位数 0.754 vs 第二名 0.494）。
- 模型具备癌症严重程度分层的潜力（对浸润癌、原位癌、正常组织给出梯度的似然分数），并能发现标注为正常但已高表达肿瘤标志物的潜在“高风险”位点，反映出较强的生物学感知能力。
- 迁移学习策略有效缓解了技术批次效应，使在单一平台训练的模型可直接泛化到多个平台和批次。

## 7. 优点
- **创新性融合机制**：首次将迁移学习与双向交叉注意力、类别正则化 VAE 结合用于跨平台癌症区域检测，解决了模态差异和批次效应问题。
- **模块设计精巧**：对比学习对齐模态，BCA 实现局部邻域交互建模，RVAE 在隐空间引入类别结构，使特征紧凑且可分离。
- **实验评估扎实**：涵盖 23 张实际切片、多个平台和两个癌种，对比方法多样，指标全面，可信度高。
- **临床潜在价值**：不仅能检测癌症区域，还能对癌变程度进行分层，并挖掘潜在早期分子异常区域，具有转化研究前景。
- **开源代码**：提供完整实现，有利于复现和后续研究。

## 8. 不足与局限
- **对预训练模型的依赖**：组织学特征提取依赖 UNI 病理基础模型，若目标域的组织染色或分辨率与预训练数据差异过大，迁移效果可能下降，且缺乏针对性的微调策略探讨。
- **数据跨度与稀有癌症**：在实验中，所有训练和测试数据均来自乳腺癌和结直肠癌，未验证其他癌种（如鳞癌、胶质瘤等）或罕见肿瘤的泛化能力。
- **极端批次效应的鲁棒性**：虽然表现好于基线，但在部分跨平台实验中（如 IDC 和 CRC 某些切片），AUC 仍低于 0.9，提示在更强烈的技术变异性下性能仍有提升空间。
- **计算量未透明**：未给出具体的训练时长和推理吞吐量数据，实际部署中的实时性需要额外评估。
- **阈值依赖外部**：推理阶段使用 GMM 自适应阈值，尽管能自动确定，但在噪声较大或癌症比例极低时，双组分假设可能不成立，影响稳定性。
- **生物学可解释性有限**：尽管展示了癌症严重程度分层，但融合过程产生的嵌入并未直接与特定信号通路或细胞类型关联，解释性仍较弱。

（完）
