---
title: "M2OST: Many-to-one Regression for Predicting Spatial Transcriptomics from Digital Pathology Images"
title_zh: M2OST：从数字病理图像预测空间转录组学的多对一回归
authors: "Hongyi Wang, Xiuju Du, Jing Liu, Shuyi Ouyang, Yen-Wei Chen, Lanfen Lin"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/32830/34985"
tags: ["query:profile"]
score: 8.0
evidence: 从数字病理图像预测空间转录组学以推断组织微环境
tldr: 现有方法忽略病理图像金字塔多尺度信息，M2OST提出多对一回归模型，利用多尺度视觉信息从数字病理图像直接预测空间转录组学表达，在肿瘤微环境分析中降低成本并提高准确性。
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 821, \"height\": 795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 872, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1841, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 264, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1850, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1805, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1836, \"height\": 380, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32830/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32830/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 873, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32830/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1833, \"height\": 671, \"label\": \"Table\"}]"
motivation: 空间转录组获取昂贵，需从病理图像直接预测。
method: 提出多对一回归框架，利用金字塔多尺度视觉信息。
result: 实验结果展示模型在基因表达预测上的准确性。
conclusion: 为数字病理图像推断组织微环境提供经济高效方案。
---

## Abstract
The advancement of Spatial Transcriptomics (ST) has facilitated the spatially-aware profiling of gene expressions based on histopathology images. Although ST data offers valuable insights into the micro-environment of tumors, its acquisition cost remains expensive. Therefore, directly predicting the ST expressions from digital pathology images is desired. Current methods usually adopt existing regression backbones along with patch-sampling for this task, which ignores the inherent multi-scale information embedded in the pyramidal data structure of digital pathology images, and wastes the inter-spot visual information crucial for accurate gene expression prediction. To address these limitations, we propose M2OST, a many-to-one regression Transformer that can accommodate the hierarchical structure of the pathology images via a decoupled multi-scale feature extractor. Unlike traditional models that are trained with one-to-one image-label pairs, M2OST uses multiple images from different levels of the digital pathology image to jointly predict the gene expressions in their common corresponding spot. Built upon our many-to-one scheme, M2OST can be easily scaled to fit different numbers of inputs, and its network structure inherently incorporates nearby inter-spot features, enhancing regression performance. We have tested M2OST on three public ST datasets and the experimental results show that M2OST can achieve state-of-the-art performance with fewer parameters and floating-point operations (FLOPs).

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：空间转录组学技术能揭示组织微环境中的基因表达空间分布，但其获取成本高昂。直接从成本较低、常规生成的数字病理图像预测基因表达具有重要价值，但当前方法存在两个主要局限：
  - 忽略病理图像本身固有的金字塔多尺度数据结构。
  - 浪费了点与点之间的视觉信息，而这些信息对提升预测精度至关重要。
- **整体含义**：论文旨在提出一种新的许多对一回归框架，利用数字病理图像的层级结构信息，更精确、低成本地从病理图像中预测空间基因表达。

### 2. 论文提出的方法论
- **核心思想**：将ST预测从传统的一对一图像-标签回归问题，重新定义为**多对一建模问题**。使用来自WSI不同放大倍数的多个图像块，共同预测其对应的同一个中心点的基因表达。
- **关键技术细节**：
  1. **Deformable Patch Embedding (DPE)**：针对高级别病理图像，采用不同的补丁尺寸生成精细的“点内”和粗糙的“点周围”标记，确保焦点集中在目标点上。
  2. **Intra‑Level Token Mixing Module (ITMM)**：基于ViT和随机掩码自注意力机制，用于从每个级别的序列中学习尺度内特征。
  3. **Cross‑Level Token Mixing Module (CTMM)**：通过全连接交叉注意力，在不改变各序列长度和解耦网络参数的前提下，实现不同尺度序列间的信息交互。
  4. **Cross‑Level Channel Mixing Module (CCMM)**：采用对序列长度不敏感的“压缩-激励”操作，混合来自不同尺度特征在通道维度上的信息。
- **算法流程**：多尺度图像块通过DPE生成标记序列，附加类别标记后，依次经过ITMM、CTMM和CCMM构成的编码器进行解耦式多尺度特征提取，最后将所有类别标记拼接并送入回归头进行预测。

### 3. 实验设计
- **数据集与场景**：在三个公开ST数据集上进行评估，分别为：
  - 人类乳腺癌数据集。
  - 人类HER2阳性乳腺肿瘤数据集。
  - 人类皮肤鳞状细胞癌数据集。
- **Benchmark与对比方法**：将PCC和RMSE作为主要评价指标，与广泛的方法进行了对比，包括：
  - **单尺度方法**：ResNet50、ViT‑B/16、Swin‑T、ConvNeXt‑T。
  - **多尺度方法**：CrossViT、用于特征提取的HIPT/iStar。
  - **ST专用方法**：DeepSpaCE、ST‑Net、HisToGene、Hist2ST、BLEEP。

### 4. 资源与算力
- **计算资源**：所有方法均在两块Nvidia RTX A6000（48G）GPU上进行训练。
- **训练时长**：论文未报告具体的训练总时长。

### 5. 实验数量与充分性
- **实验数量**：进行了多组实验，包括：
  - 三个数据集上的主流方法对比实验。
  - 对不同模型组件进行替换的消融实验。
  - 对不同的输入层级组合进行探索的实验。
  - 统计显著性检验。
  - 预测结果的可视化分析。
- **充分性与客观性**：实验设计较为充分和客观。对比了涵盖各种架构的主流和最新方法，确保了benchmark的广度。消融实验系统地验证了所提各个模块和许多对一方案的有效性。同时，使用统一的数据预处理和训练配置保证了对比的公平性。

### 6. 论文的主要结论与发现
- M2OST在所有三个数据集上均取得了最优的PCC性能，同时拥有更少的参数量和更低的FLOPs。
- 许多对一方案有效集成了多尺度信息和点周围视觉特征，显著优于仅使用最高放大倍数图像的一对一方法。
- 解耦式的多尺度特征提取模块在提升性能的同时，保持了模型的计算高效性。
- 与需要整张切片输入的slide-level方法相比，基于图像块的patch-level方法预测效果更好，说明单点基因表达主要与其对应组织区域相关。

### 7. 优点
- **新颖的建模角度**：将ST预测定义为许多对一问题，自然融合了病理图像的多尺度特性。
- **灵活高效的模型设计**：M2OST结构可轻松缩放以适应不同数量的输入，且能部分更新参数，具有很好的灵活性。
- **计算高效**：通过解耦设计显著降低了计算成本，在性能和效率上均优于现有最优方法。
- **详实的实验验证**：通过全面的对比和消融实验，充分证明了其方法的优势。

### 8. 不足与局限
- **训练时间未报告**：论文未提及模型的训练时间，无法完整评估其训练成本。
- **应用范围待拓展**：实验仅限于三种癌症类型的数据集，其在其他组织类型上的通用性有待验证。
- **缺乏讨论**：未对失败案例进行分析，也未讨论当输入图像质量差异较大时模型的鲁棒性。

（完）
