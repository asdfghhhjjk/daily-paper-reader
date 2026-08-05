---
title: "SpaCRD: Multimodal Deep Fusion of Histology and Spatial Transcriptomics for Cancer Region Detection"
title_zh: "SpaCRD: 组织学与空间转录组学的多模态深度融合用于癌区域检测"
authors: "Shuailin Xue, Jun Wan, Lihua Zhang, Wenwen Min"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38135/42097"
tags: ["query:cellseg"]
score: 4.0
evidence: 融合组织学图像和空间转录组学检测癌组织区域，助力肿瘤微环境分析。
tldr: 传统癌组织区域(CTR)检测依赖组织学图像中的细胞形态，但形态相似性易导致假阳性。空间转录组学(ST)技术可提供详细的细胞表型和空间定位信息，为更准确的CTR检测带来新机遇。SpaCRD提出多模态深度融合方法，有效整合组织学图像和ST数据，解决跨样本、跨平台场景下的对齐和融合难题。实验结果表明，该方法在CTR检测任务上显著优于单模态方法，具有更好的泛化性和鲁棒性，为下游肿瘤微环境分析奠定了基础。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 478}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1834, \"height\": 959}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 393}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 662, \"height\": 429}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 412}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 419}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38135/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 430}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1829, \"height\": 763}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 820}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 284}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 669, \"height\": 327}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38135/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 228}]"
motivation: 传统CTR检测仅靠组织学图像易产生假阳性，空间转录组学提供细胞表型信息可改善。
method: 提出SpaCRD，深度融合组织学图像和空间转录组学数据进行癌区域检测。
result: 在跨样本和跨平台实验中，检测准确性和鲁棒性显著优于单一模态方法。
conclusion: SpaCRD通过多模态融合实现了更精确的癌区域检测，为肿瘤微环境分析奠定基础。
---

## Abstract
Accurate detection of cancer tissue regions (CTR) enables deeper analysis of the tumor microenvironment and offers crucial insights into treatment response. Traditional CTR detection methods, which typically rely on the rich cellular morphology in histology images, are susceptible to a high rate of false positives due to morphological similarities across different tissue regions. The groundbreaking advances in spatial transcriptomics (ST) provide detailed cellular phenotypes and spatial localization information, offering new opportunities for more accurate cancer region detection. However, current methods are unable to effectively integrate histology images with ST data, especially in the context of cross-sample and cross-platform/batch settings for accomplishing the CTR detection. To address this challenge, we propose SpaCRD, a transfer learning-based method that deeply integrates histology images and ST data to enable reliable CTR detection across diverse samples, platforms, and batches. Once trained on source data, SpaCRD can be readily generalized to accurately detect cancerous regions across samples from different platforms and batches. The core of SpaCRD is a category-regularized variational reconstruction-guided bidirectional cross-attention fusion network, which enables the model to adaptively capture latent co-expression patterns between histological features and gene expression from multiple perspectives. Extensive benchmark analysis on 23 matched histology-ST datasets spanning various disease types, platforms, and batches demonstrates that SpaCRD consistently outperforms existing eight state-of-the-art methods in CTR detection.

---

## 论文详细总结（自动生成）

## 一、论文的核心问题与整体含义

- **研究背景**：癌症组织区域（CTR）的精确检测是肿瘤微环境分析和制定治疗方案的关键步骤。传统方法依赖组织学图像中的细胞形态，但由于不同组织区域存在形态相似性、染色质量不稳定等问题，容易产生大量假阳性。
- **空间转录组学带来的机遇**：空间转录组学（ST）技术能够在保留空间位置信息的同时，全面解析组织切片的转录本，为更准确地识别癌症区域提供细胞表型和空间定位支撑。
- **现有挑战**：ST数据存在较高背景噪声，且现有融合组织学图像与ST数据的方法往往忽略跨模态交互与全局空间上下文，也难以适应跨样本、跨平台/批次场景下的分布差异，导致CTR检测的泛化能力不足。
- **本文目标**：提出基于迁移学习的多模态深度融合框架SpaCRD，旨在实现跨样本、跨平台/批次的可靠CTR检测，克服单模态局限和现有融合方法的缺陷。

## 二、论文提出的方法论

- **整体思路**：SpaCRD采用三阶段训练范式，通过模态对齐、深度融合和癌症似然估计，从组织学图像和ST数据中学习紧凑且类特定的多模态嵌入表示，最终输出每个测序点/区域的癌症可能性评分。
- **模态对齐表示学习**：
  - 使用病理专用的预训练基础模型UNI提取组织学图像块特征，获得图像嵌入。
  - 设计两个轻量MLP编码器分别处理图像特征和基因表达谱，并采用双向InfoNCE对比损失（图像到基因、基因到图像）将两种模态对齐到共享潜在空间，缩小模态差距。
  - 目标函数：\[ L_{\text{contrast}} = \alpha \cdot L_{\text{img→gene}} + (1-\alpha) \cdot L_{\text{gene→img}} \]，实验中 \(\alpha=0.5\)。
- **VRBCA深度融合网络**：
  - **双向交叉注意力（BCA）**：利用基因引导和图像引导的两个交叉注意力模块，同时考虑每个测序点及其空间邻居的特征，从多角度建模跨模态交互，生成初始多模态融合表示 \(h^*_i\)。
  - **类别正则化变分自编码器（RVAE）**：对融合表示进行变分重构，并引入类别特定的高斯先验（均值可学习），迫使潜在空间呈现类内紧凑、类间分离的结构，同时滤除噪声。训练目标包含重构误差和类别正则化的KL散度：
    \[
    L_{\text{fused}} = \frac{1}{n}\sum_{i=1}^{n} \left( \|\hat{h}^*_i - h^*_i\|^2 + \beta \cdot D^{\text{cls}}_{KL}(q_i \| p_{y_i}) \right)
    \]
  - 超参数 \(\beta=0.5\)。
- **癌症似然判别器**：将RVAE编码器输出的均值和对数方差拼接后输入两层MLP分类器，联合二元交叉熵损失和融合损失进行训练，最终使用混合高斯模型（GMM）自动确定分类阈值。
- **迁移学习应用**：通过对比学习和类别正则化隐空间对齐，SpaCRD将源数据学到的知识迁移到目标平台/批次样本，缓解跨域漂移。

## 三、实验设计

- **数据集**：共使用23个匹配的组织学图像-ST数据集，涵盖多种疾病类型、平台和批次。
  - 跨样本评估：11个乳腺癌数据集（STHBC A-H等）和12个结直肠癌数据集（CRC A1-G2）。
  - 跨平台/批次评估：源数据为ST平台（STHBC），目标数据包括Visium平台（ViHBC、IDC）和Xenium平台（XeHBC）。
- **对比方法**：与8种前沿方法对比，包括：
  - 多模态方法：MEATRD、STANDS、SpaCell-Plus、iStar、TESLA
  - 纯ST方法：STAGE、Spatial-ID
  - 纯图像方法：SimpleNet
- **评价指标**：AUC、AP、F1-score，以及用于衡量健康与肿瘤区域评分分布分离程度的KS距离。

## 四、资源与算力

- 所有实验均在单个NVIDIA RTX 3090 GPU（24GB显存）上完成。
- 软件环境：PyTorch 2.1.1，Python 3.11.5。
- 论文未明确提及单次训练的具体时间或总训练时长，但提供了推断时间、内存占用等效率分析（详见附录）。

## 五、实验数量与充分性

- **主要实验组数**：
  - 跨样本CRC和STHBC各12和8个数据集的留一交叉验证，共20组对比结果（表1、表2）。
  - 跨平台/批次评估：在3个不同平台数据集上测试，并与8个基线对比。
  - 消融实验：特征提取器替换（4种）、模态/模块去除（5种设置）、超参数敏感性分析（\(\alpha,\beta,\gamma\)和邻居数量）、小样本训练影响。
  - 下游分析：癌变严重程度分层、潜在病灶区域检测等。
- **实验充足性与客观性**：
  - 数据集覆盖广：23个独立组织切片，跨两种癌症类型和三种ST平台，评价全面。
  - 对比方法多样：包含近期多模态、单模态及异常检测范式的方法。
  - 所有定量结果均报告5次独立运行的平均值和标准差，统计稳健。
  - 消融实验系统性检验了每一个关键组件和超参数的贡献，结论可靠。
  - 公平性：基线方法按照原始论文设置或作者提供的配置运行，输入数据统一预处理。

## 六、论文的主要结论与发现

- SpaCRD在所有跨样本、跨平台/批次设置中，AUC、AP和F1均显著优于其他8种SOTA方法，平均提升约12%–14%。
- 通过KS距离和分数分布可视化，SpaCRD对健康与肿瘤区域的分离效果最佳，验证了其类别正则化设计的有效性。
- 消融实验证明：UNI病理特征提取器、双向交叉注意力融合、RVAE的去噪和类特定先验以及对比对齐模块均对性能有重要贡献。
- SpaCRD能够对癌症严重程度进行分层（如浸润性癌 > 原位癌 > 正常组织），并可能发现人工注解遗漏但具有高癌变标志物表达的潜在病灶区域，展示了临床应用潜力。
- 小样本场景下，SpaCRD仍维持稳定性能，说明其数据效率和泛化能力强。

## 七、优点

- **创新的融合架构**：VRBCA将双向交叉注意力与类别正则化VAE相结合，从多角度捕获跨模态交互，并主动规范潜在空间结构，优于简单的拼接或重建误差方法。
- **强泛化能力**：通过对比学习对齐模态和类别先验，有效缓解了平台/批次效应，实现了跨域零样本/少样本迁移。
- **端到端与可解释性**：提供每个测序点的连续癌症似然评分，无需事先定义标记基因，且分数具有生物学可解释性（如强度与恶性程度关联）。
- **全面的实验验证**：覆盖23个数据集、多平台、多疾病类型，并与8个前沿方法对比，消融和鲁棒性分析充分。
- **公开代码与可复现性**：论文提供了代码链接，并详细说明了模型配置和超参数。

## 八、不足与局限

- **对病理图像特征提取器的依赖**：性能高度依赖UNI等大规模预训练模型，若替换为自然图像预训练的ResNet或ViT，跨平台性能大幅下降，可能限制在缺乏病理专用基础模型时的应用。
- **源数据标注依赖**：迁移学习仍需一定量的带标注源数据，对于全新癌症类型或缺乏组织学-ST配对标注的情况，仍需重新训练或微调。
- **ST数据噪声处理**：尽管RVAE能滤除部分噪声，但若ST数据质量极差（如基因捕获效率过低），对齐和融合效果可能下降，论文未深入探讨此极端情况。
- **空间尺度限制**：当前实验基于10X Visium/Xenium等点级数据，对于更高分辨率（如亚细胞）ST技术和更精细的组织结构检测能力未验证。
- **计算成本**：相较于部分基线，SpaCRD的参数量和推理内存占用可能较高（文中承认但称其可接受），在超大规模组织切片上部署可能存在效率瓶颈。
- **临床转化距离**：论文仅展示了回顾性分析中的潜在病灶发现，尚未进行前瞻性临床验证或与病理医生诊断的一致性研究。

（完）
