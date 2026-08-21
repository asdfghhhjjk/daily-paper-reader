---
title: "SpaCRD: Multimodal Deep Fusion of Histology and Spatial Transcriptomics for Cancer Region Detection"
title_zh: SpaCRD：组织学与空间转录组学多模态深度融合用于癌症区域检测
authors: "Shuailin Xue, Jun Wan, Lihua Zhang, Wenwen Min"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38135/42097"
tags: ["query:cell-graph"]
score: 5.0
evidence: 融合组织学与空间转录组进行癌症区域检测
tldr: 本文针对仅依赖组织学形态的癌症区域检测假阳性率高的问题，提出SpaCRD方法。该方法深度融合组织学图像和空间转录组数据，利用细胞表型与空间定位信息提高检测准确性。预期在跨样本和跨平台场景下也能有效，为肿瘤微环境分析提供更可靠的基础。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 478}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1834, \"height\": 959}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 393}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 662, \"height\": 429}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 412}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 419}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 430}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1829, \"height\": 763}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 820}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 284}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 669, \"height\": 327}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 228}]"
motivation: 传统基于组织学形态的癌症区域检测易因形态相似产生假阳性。
method: 提出SpaCRD，深度融合组织学图像与空间转录组数据，实现更准确的癌症区域检测。
result: 摘要未完整，预期降低假阳性并提高跨样本/跨平台泛化。
conclusion: 融合组织学与ST可提升癌症区域检测精度，对肿瘤微环境分析有助益。
---

## Abstract
Accurate detection of cancer tissue regions (CTR) enables deeper analysis of the tumor microenvironment and offers crucial insights into treatment response. Traditional CTR detection methods, which typically rely on the rich cellular morphology in histology images, are susceptible to a high rate of false positives due to morphological similarities across different tissue regions. The groundbreaking advances in spatial transcriptomics (ST) provide detailed cellular phenotypes and spatial localization information, offering new opportunities for more accurate cancer region detection. However, current methods are unable to effectively integrate histology images with ST data, especially in the context of cross-sample and cross-platform/batch settings for accomplishing the CTR detection. To address this challenge, we propose SpaCRD, a transfer learning-based method that deeply integrates histology images and ST data to enable reliable CTR detection across diverse samples, platforms, and batches. Once trained on source data, SpaCRD can be readily generalized to accurately detect cancerous regions across samples from different platforms and batches. The core of SpaCRD is a category-regularized variational reconstruction-guided bidirectional cross-attention fusion network, which enables the model to adaptively capture latent co-expression patterns between histological features and gene expression from multiple perspectives. Extensive benchmark analysis on 23 matched histology-ST datasets spanning various disease types, platforms, and batches demonstrates that SpaCRD consistently outperforms existing eight state-of-the-art methods in CTR detection.

---

## 论文详细总结（自动生成）

# SpaCRD 论文详细总结

## 1. 核心问题与整体含义

- **研究背景**：癌症组织区域（cancer tissue regions, CTR）的准确检测对肿瘤微环境分析、手术切缘判断、放疗剂量设计等临床和研究任务至关重要。
- **现有问题**：
  - 传统基于组织学图像的检测高度依赖细胞形态，但由于不同组织区域形态相似、染色质量不稳定，容易产生较多假阳性。
  - 人工标注成本高、耗时长，难以大规模应用。
  - 空间转录组（ST）可提供细胞表型和空间定位信息，但存在背景噪声、批次差异，单独使用ST的方法也常因噪声而性能受限。
- **核心挑战**：如何有效融合组织学图像与ST数据，特别是在跨样本、跨平台/批次场景下，仍能稳定、准确地进行CTR检测。
- **整体含义**：论文提出 **SpaCRD**，一个基于迁移学习的多模态深度融合框架，将组织病理图像与空间转录组数据深度整合，实现对不同样本、不同平台/批次癌症区域的高泛化检测。

---

## 2. 方法论

SpaCRD 主要由三个训练阶段组成：

### 2.1 模态对齐表示学习（Stage I）

- **组织学特征提取**：
  - 根据ST中每个spot的空间坐标，从组织学图像中裁剪对应图像patch。
  - 使用病理学基础模型 **UNI** 作为组织学图像特征提取器，获得H&E嵌入 `ximg_i`。
  - UNI在大规模病理数据上预训练，具有较好的细粒度组织学结构表征能力，且文中不进行微调以降低计算开销。
- **基因表达特征**：
  - 使用每个spot的标准化基因表达向量 `xgene_i`。
- **CLIP式对比学习对齐**：
  - 分别用轻量三层MLP编码器 `fc1`（图像编码器）和 `fc2`（基因编码器）将两种模态映射到共享潜在空间，得到 `himg_i` 和 `hgene_i`。
  - 通过缩放点积构建相似度矩阵，并计算两个方向的 InfoNCE 损失：
    - `L_img→gene`
    - `L_gene→img`
  - 总对比损失：`L_contrast = α × L_img→gene + (1-α) × L_gene→img`，实验中固定 `α=0.5`。
  - 目标是使同一空间位置的图像-基因配对在潜在空间中靠近，不同位置配对远离，从而减少模态差异，为后续融合提供稳定基础。

### 2.2 VRBCA 融合网络（Stage II）

VRBCA 全称为 **类别正则化变分重建引导的双向交叉注意力融合网络**，用于捕捉组织学与ST数据之间的潜在共表达模式。

- **双向交叉注意力（BCA）**：
  - 设计两个结构相同的交叉注意力模块：
    - **基因引导交叉注意力**：以H&E特征为query，基因特征为key/value。
    - **H&E引导交叉注意力**：以基因特征为query，H&E特征为key/value。
  - 每个模块包含多个注意力头，使用缩放点积注意力，并通过拼接、投影得到输出。
  - 对每个spot，输入还包括其邻近spot的特征（`{i1, ..., ik}`），以建模空间邻域交互。
  - 将两个方向的注意力输出在spot维度取首项后拼接，再通过MLP得到融合的多模态表示 `h*_i`。

- **类别正则化变分自编码器（RVAE）**：
  - 在VAE框架中引入可学习的类别特定潜在中心，使潜在空间具有语义结构。
  - 编码器 `f_enc` 输入融合表示 `h*_i`，输出均值 `μ_i` 和对数方差 `log σ²_i`。
  - 采样潜在变量 `z_i = μ_i + σ ⊙ ε`，`ε∼N(0,I)`，解码器 `f_dec` 重构 `ĥ*_i`。
  - 训练目标包含重建误差和类别条件KL散度：
    - `L_fused = (1/n) Σ [ ||ĥ*_i − h*_i||² + β·D_KL(q_i || p_yi) ]`
    - 其中 `q_i = N(μ_i, diag(σ²_i))` 为近似后验，`p_yi = N(μ_yi, I)` 为类别特定高斯先验，`β=0.5`。
  - 作用：过滤噪声、促进生成紧凑且类别一致的嵌入。

### 2.3 癌症似然判别器（Stage III）

- 将VRBCA编码器输出的均值 `μ_i` 和对数方差 `log σ²_i` 拼接后输入两层MLP分类器，预测每个spot为癌症的概率。
- 分类损失结合二值交叉熵（BCE）和融合损失：
  - `L_BCE = −(1/n) Σ [y_i log σ(ŷ_i) + (1−y_i) log(1−σ(ŷ_i))]`
  - `L_cls = L_BCE + γ × L_fused`，实验中 `γ=0.1`。
- **推理阈值自动确定**：对预测分数拟合两分量高斯混合模型（GMM），取两个高斯分量交点作为分类阈值，无需手动设定。

---

## 3. 实验设计

### 3.1 数据集

- 总计使用 **23个匹配的组织学-ST数据集（组织切片）**，涉及不同疾病类型、平台和批次。
- **跨样本评估数据集**：
  - **CRC**：12个结直肠癌数据集（CRC A1–G2），来自多切片研究 Valdeolivas et al. 2024。
  - **STHBC**：8个人乳腺癌数据集（STHBC A–H），来自 Andersson et al. 2021。
  - 采用 **留一交叉验证** 评估跨样本泛化能力。
- **跨平台/批次评估数据集**：
  - 在ST平台生成的 **STHBC** 上训练，在以下平台数据上测试：
    - **ViHBC**（Visium平台）
    - **IDC**（Visium平台）
    - **XeHBC**（Xenium平台）

### 3.2 对比方法

共对比 **8种SOTA方法**，包括：

- **多模态方法**：MEATRD、STANDS、SpaCell（表格中为SpaCell-Plus）、iStar、TESLA。
- **ST方法**：STAGE、Spatial-ID。
- **图像方法**：SimpleNet。

### 3.3 评估指标

- AUC、AP、F1-score、KS距离（用于评估健康与肿瘤预测分数分布分离程度）。
- 所有结果均报告5次独立运行的平均值和标准差。

---

## 4. 资源与算力

- **GPU**：使用单块 **NVIDIA RTX 3090 GPU（24GB）**。
- **软件环境**：PyTorch 2.1.1、Python 3.11.5。
- **训练时长**：论文正文未明确给出具体训练时长，仅说明详细网络结构、训练计划和实现设置见补充材料S5。
- 代码已公开：`https://github.com/wenwenmin/SpaCRD`。

---

## 5. 实验数量与充分性

- **主要基准实验**：
  - 12个CRC数据集 + 8个STHBC数据集上的跨样本留一验证。
  - 3个跨平台/批次测试数据集（ViHBC、IDC、XeHBC）。
- **可视化/下游分析**：
  - STHBC G、ViHBC、XeHBC、IDC等多个数据集上的癌症区域检测可视化。
  - 癌症严重程度分层分析（invasive cancer、carcinoma in situ、normal tissue）。
  - 潜在病变区域分析：对高预测分数但原标注为非癌的spot，检查乳腺癌标志基因表达（ERBB2、CCND1、ACTB）。
- **消融实验**：
  - 组织学特征提取器对比：UNI vs. ResNet50、Swin-Tiny、HIPT。
  - 模态和融合模块消融：仅图像、仅ST、去除BCA、去除RVAE、去除VRBCA、去除对比学习。
- **鲁棒性与效率分析**：
  - 超参数敏感性：α、β、γ、邻近spot数量。
  - 参数数量、运行时间、显存占用对比。
  - 小样本训练分析：训练集少于测试集10% spots时性能仍稳定。
- **充分性评价**：
  - 实验覆盖多个癌症类型（乳腺癌、结直肠癌）、不同平台（ST、Visium、Xenium）和批次。
  - 使用统一指标和多次运行均值±标准差，结果具有统计可比性。
  - 消融实验较完整，能够反映各模块贡献。
  - 但部分基线方法依赖先验知识或异常检测框架，可能与SpaCRD的监督/半监督设置存在差异，存在一定公平性讨论空间。

---

## 6. 主要结论与发现

- SpaCRD 在 **12个CRC和11个乳腺癌数据集** 上一致优于8种SOTA方法。
- **跨样本场景**：
  - 相比第二名方法，AUC、AP、F1平均分别提升约 **13.5%、14.1%、14.0%**。
- **跨平台/批次场景**：
  - 相比第二名方法，AUC、AP、F1平均分别提升约 **12.1%、11.8%、

11.9%**。
- **可视化结果**：在STHBC G、ViHBC、XeHBC、IDC等多个数据集上，SpaCRD预测的癌症区域与病理学家标注高度一致，能清晰区分浸润性癌、原位癌和正常组织，边界较准确。
- **潜在病变区域分析**：对SpaCRD给出高癌症概率但原始标注为非癌的spot进行分析，发现这些spot中ERBB2、CCND1、ACTB等乳腺癌相关标志基因表达显著升高，提示模型可能识别出早期或隐匿性病变，或纠正原有标注噪声。
- **消融实验结论**：
  - 融合组织学与ST数据比仅使用单一模态性能显著提升；
  - 去除BCA、RVAE、VRBCA或对比学习模块均会导致AUC、AP、F1下降，说明各模块对最终性能均有贡献；
  - 使用UNI作为组织学特征提取器优于ResNet50、Swin-Tiny和HIPT。
- **超参数与鲁棒性**：SpaCRD对损失权重α、β、γ以及邻近spot数量不敏感，在合理范围内性能波动小；在小样本训练（训练集spot数不足测试集10%）条件下仍保持较高性能，数据效率较高。
- **效率分析**：SpaCRD参数量、单次推理时间和GPU显存占用均处于较低水平，适用于大规模空间转录组数据分析。

---

## 7. 局限性与未来工作

- SpaCRD依赖配对的组织学图像和空间转录组数据，数据获取成本较高，且仍需要一定量的人工标注用于监督训练。
- 尽管在ST、Visium、Xenium等平台间展现出良好泛化能力，但面对更极端的批次差异或罕见癌症类型时，可能需要进一步域适应或微调。
- 论文中跨平台实验的训练数据来自单一平台（ST），未来可扩展到多平台联合训练，进一步提升跨平台稳定性。
- 对潜在病变区域的生物学验证仍有限，需结合更多独立实验或临床随访验证其可靠性。

---

## 8. 总结与评价

SpaCRD通过“对比学习模态对齐 + 类别正则化变分双向交叉注意力融合 + 癌症似然判别”的三阶段框架，有效整合组织病理图像与空间转录组数据，在跨样本和跨平台/批次场景下均显著优于现有方法。其模块设计合理、消融充分，且代码公开，具有较强的可复现性和实际应用潜力，为空间转录组指导的癌症区域检测提供了新的基准和思路。

（完）
