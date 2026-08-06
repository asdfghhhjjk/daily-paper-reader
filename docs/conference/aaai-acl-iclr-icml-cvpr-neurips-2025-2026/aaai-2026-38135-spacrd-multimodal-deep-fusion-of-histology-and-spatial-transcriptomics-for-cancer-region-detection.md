---
title: "SpaCRD: Multimodal Deep Fusion of Histology and Spatial Transcriptomics for Cancer Region Detection"
title_zh: SpaCRD：组织学与空间转录组学的多模态深度融合用于癌症区域检测
authors: "Shuailin Xue, Jun Wan, Lihua Zhang, Wenwen Min"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38135/42097"
tags: ["query:immuno-topo"]
score: 7.0
evidence: 融合组织学和空间转录组学进行癌症区域检测，实现TME分析
tldr: SpaCRD通过深度融合组织学图像与空间转录组学数据，准确检测癌症组织区域，从而促进肿瘤微环境分析和治疗反应评估，为精准肿瘤学提供新工具。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 478}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1834, \"height\": 959}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 393}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 662, \"height\": 429}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 412}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 419}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 430}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1829, \"height\": 763}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 820}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 284}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 669, \"height\": 327}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 228}]"
motivation: 传统基于组织学的检测方法易因形态相似性产生假阳性，难以精确识别癌症区域。
method: 提出多模态深度融合框架，有效整合组织学图像与空间转录组学数据。
result: 在跨样本和跨平台条件下，SpaCRD显著提高了癌症区域检测的准确性。
conclusion: 融合空间转录组学可提升癌症区域检测精度，为TME分析提供更可靠基础。
---

## Abstract
Accurate detection of cancer tissue regions (CTR) enables deeper analysis of the tumor microenvironment and offers crucial insights into treatment response. Traditional CTR detection methods, which typically rely on the rich cellular morphology in histology images, are susceptible to a high rate of false positives due to morphological similarities across different tissue regions. The groundbreaking advances in spatial transcriptomics (ST) provide detailed cellular phenotypes and spatial localization information, offering new opportunities for more accurate cancer region detection. However, current methods are unable to effectively integrate histology images with ST data, especially in the context of cross-sample and cross-platform/batch settings for accomplishing the CTR detection. To address this challenge, we propose SpaCRD, a transfer learning-based method that deeply integrates histology images and ST data to enable reliable CTR detection across diverse samples, platforms, and batches. Once trained on source data, SpaCRD can be readily generalized to accurately detect cancerous regions across samples from different platforms and batches. The core of SpaCRD is a category-regularized variational reconstruction-guided bidirectional cross-attention fusion network, which enables the model to adaptively capture latent co-expression patterns between histological features and gene expression from multiple perspectives. Extensive benchmark analysis on 23 matched histology-ST datasets spanning various disease types, platforms, and batches demonstrates that SpaCRD consistently outperforms existing eight state-of-the-art methods in CTR detection.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- 研究背景与核心问题：
  - 癌组织区域（Cancer Tissue Regions, CTR）的准确检测是肿瘤微环境分析和制定治疗策略的关键步骤。
  - 传统方法依赖病理学家人工标注或基于组织学图像的异常检测算法，前者耗时昂贵，后者因不同组织的形态相似性和染色质量不一致而假阳性率高。
  - 空间转录组学（ST）提供了高分辨率的细胞表型与空间定位信息，但ST数据本身存在显著的背景噪声，且基于标记基因的泛化性受限于先验知识。
  - 已有部分多模态融合方法未能有效整合组织学图像和ST数据，难以跨样本、跨平台/批次泛化。
- 整体含义：提出一种基于迁移学习和多模态深度融合的框架SpaCRD，通过有效对齐并融合组织学与空间转录组学特征，实现跨样本、跨平台/批次的高精度、可泛化的癌区域检测。

### 2. 方法论
- 核心思想：
  - 利用迁移学习和对齐学习将组织学与ST数据映射到共享表示空间，再通过双向交叉注意力融合及变分重建机制学习紧凑且类别可分的多模态嵌入，最后用高斯混合模型确定阈值输出癌症似然分数。
- 关键技术细节与流程（均以文字描述）：
  - **第一阶段：模态对齐表示学习**
    - 使用病理基础模型UNI提取组织学图像patch的特征（跳过微调），得到图像嵌入`Ximg`。
    - 对ST基因表达进行归一化得到`Xgene`。
    - 设计两个三层MLP编码器（图像编码器`fc1`与基因编码器`fc2`）将两种模态映射到相同维度，并通过对比学习损失（InfoNCE的双向变体，权重`α=0.5`）拉近同一空间位置的图像‑基因对，推远非配对表示。
  - **第二阶段：VRBCA融合网络（类别正则化变分重建引导的双向交叉注意力融合）**
    - 构建双向交叉注意力（BCA）模块：一个**基因引导的交叉注意力**和另一个**H&E引导的交叉注意力**，均采用多头注意力（m个头），输入包含本点对齐特征及邻居点特征，以综合建模局部空间交互。输出融合后的多模态表示`h*`。
    - 类别正则化变分自编码器（RVAE）：将融合嵌入编码为均值`μ`和对数方差`log σ²`，通过重参数化采样`z`，解码器重建原始嵌入。损失包含重建损失与类别条件KL散度（`β=0.5`），其中类特定高斯先验的均值`μ_yi`是可学习的。
  - **第三阶段：癌症似然判别器**
    - 将编码器输出的`μ`和`log σ²`拼接后送入两层MLP，进行二分类（癌or正常）。
    - 分类损失为BCE与融合损失`L_fused`的加权和（`γ=0.1`）。
    - 推理时使用双组分高斯混合模型（GMM）在预测分数分布上自动寻找交界点作为分类阈值。
  - 整体训练由对比损失、融合损失和分类损失联合优化。

### 3. 实验设计
- 数据集：
  - 总计5个数据集，包含23个配对的H&E–ST组织切片。
  - **跨样本评估**：两个多切片数据集——STHBC（人乳腺癌，8个切片，编号A‑H）、CRC（结直肠癌，12个切片，编号A1‑G2）。
  - **跨平台/批次评估**：在STHBC数据集上训练，然后测试于三个不同平台/批次的数据集——ViHBC（Visium平台）、IDC（Visium平台）、XeHBC（Xenium平台），共11个乳腺癌切片及相应的结直肠癌数据。
- Benchmark方法（8种SOTA）：
  - 多模态类：MEATRD、STANDS、SpaCell‑Plus（SpaCell的增强版）、iStar、TESLA（前两者基于视觉异常检测，后两者依赖先验知识）；
  - 纯ST类：STAGE、Spatial‑ID；
  - 纯图像类：SimpleNet。
- 评价指标：AUC、AP（平均精度）、F1分数、KS距离（衡量健康与肿瘤区域概率分布的分离程度）。

### 4. 资源与算力
- 硬件：所有实验均在一块NVIDIA RTX 3090（24GB）GPU上进行。
- 软件：PyTorch 2.1.1，Python 3.11.5。
- 关于训练时长、具体epoch数等文中未给出明确说明，仅给出了网络架构等补充材料，但在主文中未展示具体耗时。

### 5. 实验数量与充分性
- 实验规模：
  - **主实验**：在23个组织切片上完成跨样本和跨平台/批次测评，每个实验独立运行5次并报告均值±标准差。
  - **对比方法**：8种基线，与SpaCRD直接比较。
  - **消融实验**：
    - 评估不同组织学特征提取器（UNI, Swin‑Tiny, ResNet50, HIPT）在全部数据集上的性能。
    - 评估不同模态输入（纯图像、纯ST）及融合模块缺失的影响（去掉BCA、去掉RVAE、去掉整个VRBCA、去掉对比学习CL）。
  - **超参数敏感性分析**：11个乳腺癌数据集上测试了`α`, `β`, `γ`, 邻居点数。
  - **额外分析**：小样本训练鲁棒性分析、模型效率（参数、内存、运行时间）、下游癌严重程度分层、潜在病变区域发现。
- 评价：实验设计全面且系统，覆盖多种疾病类型、平台和批次；消融和敏感性实验有力支撑模块有效性；多次重复运行保证统计可靠性；比较对象丰富，包括近期多模态和纯单模态方法，实验充分且客观公平。

### 6. 主要结论与发现
- SpaCRD在跨样本和跨平台/批次条件下均显著超越所有基线方法，平均AUC、AP、F1提升约12%‑14%。
- VRBCA模块通过双向注意力与变分重建有效融合两种模态，减小模态差异并滤除噪声，产生更紧凑、类别可分的嵌入。
- KS距离分析证实SpaCRD预测的癌/正常分数分布分离度最大，表明其具有更好的辨别力。
- SpaCRD不仅能够精确检测癌区域，还能对癌严重程度进行分层（如区分侵袭性癌与原位癌），并发现某些被人工标注为正常但高表达癌标记基因的潜在病变区域，具有辅助临床决策的潜力。
- 即使训练样本量极少（<10%），SpaCRD仍保持稳定性能，展示出强大的泛化能力和数据效率。

### 7. 优点
- **新颖的融合机制**：双向交叉注意力协同邻居特征，捕获局部多模态交互；类别条件变分自编码器在融合过程中嵌入类别先验，既能降噪又能增强类间区分度。
- **跨平台跨批次的鲁棒泛化**：采用迁移学习与对比对齐策略，有效缓解技术和批次效应，这是现有ST‑组织学融合方法的重要短板。
- **无监督阈值确定**：利用GMM自动寻找分类阈值，减少对人为阈值的依赖。
- **生物学可解释性**：通过预测分数能够识别潜在早期病变，并为癌变严重程度提供分层信息，有助于下游生物学发现。
- **全面的实验验证**：在23个真实数据集、多种平台和肿瘤类型上对比8种SOTA方法，消融及敏感性分析详实，结果说服力强。

### 8. 不足与局限
- **计算效率未详述**：虽然提供了参数量和内存对比，但没有给出明确的训练时间或吞吐量数据，实际部署成本不够清晰。
- **依赖高质量组织学特征提取器**：UNI作为特征提取器起到了关键作用，更换为其他提取器后跨平台性能大幅下降，方法对病理基础模型的依赖较强。
- **类别先验需有标注数据**：变分自编码器的类特定先验需要标签`yi`，因此方法仍是有监督的，虽然在测试时可通过GMM决策，但训练依然需要部分标注的癌/正常标签。
- **空间范围限制**：VAE部分主要对单个spot的重建进行约束，尽管BCA使用了邻居特征，但未在潜在空间中显式建模更大尺度的组织结构，可能遗漏长程空间依赖。
- **实验覆盖面可扩展**：目前仅验证了乳腺癌和结直肠癌，对其他癌种的泛化性未做测试；另外，所有数据均为特定ST平台（10X Visium等），未涉及其它ST技术。
- **潜在批次效应**：尽管在跨平台测试中取得优秀成绩，但若训练和测试平台差异过大（例如探针捕获原理完全不同的原位测序技术），可能需要重新校准对齐策略。

（完）
