---
title: "A Cross Modal Knowledge Distillation & Data Augmentation Recipe for Improving Transcriptomics Representations through Morphological Features"
title_zh: 一种利用形态特征改善转录组表征的跨模态知识蒸馏与数据增强方案
authors: "Ihab Bendidi, Yassir El Mesbahi, Alisandra Kaye Denton, Karush Suri, Kian Kenyon-Dean, Auguste Genovesio, Emmanuel Noutahi"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=w7lm8AjzH6"
tags: ["query:pathology-ai"]
score: 6.0
evidence: 利用显微镜图像形态特征增强转录组学
tldr: 转录组学提供可解释的基因信息，而显微镜图像蕴含丰富形态特征但难以解释。本文提出跨模态知识蒸馏框架，利用弱配对数据将形态信息整合到基因表达表示中，同时通过数据增强缓解数据稀缺问题。实验表明，该方法能显著提升转录组学表征的预测能力，揭示了形态与基因表达的关联，对数字病理学中细胞形态分析有参考价值。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-w7lm8ajzh6/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 855, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-w7lm8ajzh6/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1773, \"height\": 872, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-w7lm8ajzh6/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1766, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-w7lm8ajzh6/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 841, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-w7lm8ajzh6/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1725, \"height\": 1010, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-w7lm8ajzh6/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1730, \"height\": 1034, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-w7lm8ajzh6/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1774, \"height\": 534, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-w7lm8ajzh6/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-w7lm8ajzh6/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1741, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-w7lm8ajzh6/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1773, \"height\": 1026, \"label\": \"Table\"}]"
motivation: 转录组学与显微图像模态互补，但弱配对数据稀缺限制多模态学习。
method: 提出跨模态知识蒸馏框架，对齐并绑定模态，用形态特征丰富基因表达表示。
result: 增强的转录组表征在预测任务上性能提升。
conclusion: 该方法有效融合形态与基因数据，推动细胞功能理解。
---

## Abstract
Understanding cellular responses to stimuli is crucial for biological discovery and drug development. Transcriptomics provides interpretable, gene-level insights, while microscopy imaging offers rich predictive features but is harder to interpret. Weakly paired datasets, where samples share biological states, enable multimodal learning but are scarce, limiting their utility for training and multimodal inference. We propose a framework to enhance transcriptomics by distilling knowledge from microscopy images. Using weakly paired data, our method aligns and binds modalities, enriching gene expression representations with morphological information. To address data scarcity, we introduce (1) *Semi-Clipped*, an adaptation of CLIP for cross-modal distillation using pretrained foundation models, achieving state-of-the-art results, and (2) *PEA* (**P**erturbation **E**mbedding **A**ugmentation), a novel augmentation technique that enhances transcriptomics data while preserving inherent biological information. These strategies improve the predictive power and retain the interpretability of transcriptomics, enabling rich unimodal representations for complex biological tasks.

---

## 论文详细总结（自动生成）

# 论文核心问题与整体含义（研究动机和背景）

- **核心问题**：转录组学（gene expression）数据具有基因级可解释性，但预测能力较弱；显微镜图像蕴含丰富的形态学特征，预测能力强但难以直接解释。两类模态互补，但严格配对（同一生物重复）的多模态数据极其稀缺，大规模采集不切实际。弱配对数据（共享相同细胞系和扰动条件但不来自同一重复）虽然可获取，但数据量依然有限，限制了多模态学习和推断的扩展。
- **整体含义**：本文旨在利用有限的弱配对显微镜-转录组数据，将形态学知识“蒸馏”到转录组表征中，从而在不牺牲转录组可解释性的前提下显著提升其预测能力。最终实现仅需输入转录组数据就能获得富含形态信息的强大表征，支撑药物发现等下游任务。

# 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

## 核心思想
- **跨模态知识蒸馏**：以显微镜图像为教师模态，转录组为学生模态。冻结预训练好的图像编码器，训练一个轻量适配器将转录组嵌入映射到图像嵌入空间，使用对比学习（CLIP损失）实现对齐。这种方法避免了对大量配对数据的需求，且仅单向传递知识。
- **生物学启发数据增强**：提出PEA（Perturbation Embedding Augmentation），将原本用于后处理的批次校正方法改造为训练时的随机数据增强，在保持生物学信息的同时引入合理变异，缓解弱配对数据稀缺。

## 关键技术细节

### Semi-Clipped
- 使用预训练且冻结的图像编码器 $E_T$（Phenom-1）和转录组编码器 $E_S$（scVI 等）。仅训练转录组适配器 $f_S$（三层MLP，含ReLU）。
- 损失函数：CLIP 对比损失，训练时随机选取同一扰动条件下的一个图像-转录组对为正样本，同批次其他样本为负样本。
- 公式（文字说明）：计算对齐后转录组嵌入 $h_S = f_S(z_S)$ 与图像嵌入 $z_T$ 之间的余弦相似度，通过温度参数缩放的 softmax 交叉熵优化。

### PEA
- 定义一组批次校正变换 $A$（包括中心化、缩放、典型变异归一化 TVN 及其变体）。训练时对每个转录组样本 $z_S$：
  1. 从 $A$ 中随机选择一个变换 $A$；
  2. 随机丢弃 $A$ 的部分步骤（增加随机性）；
  3. 随机抽取若干对照样本（未受扰动的控制样本）用于校正；
  4. 应用变换得到增强嵌入 $z_{S,A}$，再输入适配器。
- 教师模态使用固定批次校正（TVN）以聚焦相关信号。
- 推理时也对转录组嵌入应用批次校正以对齐训练分布。

### 算法流程（伪代码）
1. 每批数据：用冻结编码器提取 $z_S$ 和 $z_T$；
2. 随机选择批次校正方法 $A$，随机丢弃部分步骤 → $A'$；
3. 随机抽取控制样本子集 $X_S^{(c)}$，应用 $A'$ 得 $z_S^a$；
4. 适配器计算对齐嵌入 $h_S = f_S(z_S^a)$；
5. 对图像嵌入应用 TVN 得 $z_T^b$；
6. 计算 CLIP 损失，反向传播更新 $f_S$。

# 实验设计：数据集、场景、基准与对比方法

## 数据集
- **训练集**：HUVEC-CMPD，包含 130,000 个阵列式批量转录组样本和 20,000 张显微镜图像，均来自 HUVEC 细胞，涵盖 1,700 种化学扰动（各 3 个浓度）。转录组与图像按扰动和浓度弱配对。
- **评估集**（三个 OOD 数据集）：
  1. **HUVEC-KO**：约 300 个 CRISPR 基因敲除的 HUVEC 批量转录组数据（12 万样本），与训练集无实验重叠，测试泛化到未见过实验和遗传扰动。
  2. **LINCS**：L1000 平台（不同量化方法）的 443,000 样本，涵盖 31 种细胞系、5,157 个 CRISPR 敲除，测试量化方法迁移。
  3. **SC-RPE1**：来自视网膜色素上皮细胞的单细胞转录组数据（247,914 样本），测试从批量到单细胞的泛化。

## 基准任务
- **已知生物关系召回**：通过基因嵌入余弦相似度计算预测关系，与 CORUM、HuMAP、StringDB、Reactome、SIGNOR 五个数据库的标注对比，指标为平均召回率。
- **转录组可解释性保持**：综合结构完整性分数（保留控制-扰动结构）和斯皮尔曼相关系数（基因表达预测一致性），二者平均。

## 对比方法
- **跨模态蒸馏基线**：CLIP、SigClip、VICReg、DCCA（无标签对齐方法）；KD、SHAKE、C2KD（有标签蒸馏方法）。所有方法均使用相同预训练编码器和可训练适配器，蒸馏方法还额外预训练适配器分类器。
- **数据增强基线**：MWO、scVI 去噪、MDWGAN-GP、scGFT，以及它们的组合，与 PEA 单独及联合比较。

# 资源与算力

- 论文明确提到：在放大版数据集（130 万弱配对样本）上，使用单个 NVIDIA H100 GPU 训练仅需 19 小时。**未明确说明原始数据集（13 万样本）的具体训练时长**，但推测耗时更短。
- 训练配置：batch size 1024，150 个 epoch，学习率 0.001，温度 0.1。适配器为轻量 MLP（三层），冻结骨干网络，整体计算效率高。

# 实验数量与充分性

- **实验数量**：包含核心对比（图2a、2b）、训练选择分析（图1）、超参数消融（图3）、PEA 组件消融（表2）、跨方法 PEA 改进（表1，每个方法 15 seeds）、维恩图分析（图4）、通路富集分析（附录表3）。多个图表展示不同 OOD 数据集结果。
- **充分性与公平性**：
  - 使用了多个独立种子（5 或 15）并报告均值和标准差，部分实验使用 Wilcoxon 符号秩检验验证显著性（p < 0.05）。
  - 严格控制变量：所有方法基于同样预训练编码器，超参数通过网格搜索优化。
  - OOD 设置覆盖实验变异、量化方法变化、单细胞适应，较为全面。
  - 但是，仅使用 HUVEC 一种细胞类型训练，未测试跨细胞系迁移；仅与经典多模态对齐/蒸馏基线对比，未与更近期的多模态融合方法（如直接拼接、交叉注意力）比较。

# 论文的主要结论与发现

1. **Semi-Clipped 优于现有蒸馏方法**：在三个 OOD 数据集上，Semi-Clipped（无增强）的已知生物关系召回率均超过或持平所有有标签和无标签方法，同时保持转录组可解释性。
2. **PEA 显著提升性能且与现有增强互补**：单独使用 PEA 即可使召回率提升 17%~55%；与其他生物增强联合使用时效果最佳（总提升 25%~69%）。PEA 跨四种不同蒸馏方法均带来统计显著提升。
3. **无标签方法优于有标签方法**：基于 CLIP 的无标签对齐方法普遍优于依赖扰动标签的蒸馏方法，说明弱标签不足以捕捉细胞复杂状态。
4. **Semi-Clipped 产生新的生物学洞察**：其独家检索的关系（排除单项模态）富集了细胞周期和翻译后修饰相关通路，表明融合可揭示模态独立的协同信息。
5. **批次校正可转化为有效数据增强**：将后处理步骤随机化并用于训练，能够引入合理变异而不破坏生物学信息。

# 优点：方法或实验设计上的亮点

- **创新性**：
  - 首次将 CLIP 对比学习与冻结预训练模型结合用于弱配对、低数据量下的跨模态生物知识蒸馏。
  - 创造性将批次校正重新设计为数据增强（PEA），既保留生物学信号又增加多样性。
- **实用性**：
  - 训练轻量适配器，计算开销小（单 GPU 19 小时），便于大规模应用。
  - 推理时仅需转录组单模态输入，避免了同时采集两种模态的困难。
- **实验严谨性**：
  - 多 OOD 设置，全面评估泛化能力。
  - 统计显著性检验（Wilcoxon）、多种子平均、组件消融，增强了结论可靠性。
- **生物学洞察**：通过维恩图和 GSEA 揭示了跨模态融合带来的新生物学通路，证明非简单加和效应。

# 不足与局限

- **配对策略局限**：训练时随机从同一扰动组选择正对，若组内样本存在较大差异（如不同浓度下生物学状态不同），可能稀释对齐质量。论文指出需要更好的匹配策略。
- **数据与模态覆盖不足**：
  - 仅训练于一种细胞系（HUVEC），未在多种细胞类型上验证训练集泛化。
  - 仅使用了显微镜图像和批量转录组，未探索其他模态（如蛋白质组、代谢组）。
  - OOD 数据集虽覆盖不同变异源，但数量有限（仅三个），且均为转录组验证，缺乏对图像模态的独立测试。
- **基线选择有限**：未与端到端多模态融合方法（如直接双编码器交叉注意力）或更现代的对比学习变体（如 SigLIP、ALBEF）比较。
- **对预训练模型依赖性**：Semi-Clipped 的性能受限于图像和转录组预训练编码器的质量。如果基础编码器不够好，蒸馏效果可能打折。
- **可解释性保持的局限性**：在 LINCS 和 SC-RPE1 上，转录组可解释性得分略低于纯转录组基线，虽其他蒸馏方法更差，但仍有提升空间。
- **缺乏真实生物学验证**：提升的召回率是对已知数据库的匹配，而“新发现”的通路（如细胞周期）虽有趣，但缺少独立实验验证这些关系是否确实可靠。

（完）
