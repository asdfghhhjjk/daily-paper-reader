---
title: "M2OST: Many-to-one Regression for Predicting Spatial Transcriptomics from Digital Pathology Images"
title_zh: M2OST：从数字病理图像预测空间转录组学的多对一回归
authors: "Hongyi Wang, Xiuju Du, Jing Liu, Shuyi Ouyang, Yen-Wei Chen, Lanfen Lin"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/32830/34985"
tags: ["query:profile"]
score: 8.0
evidence: 从数字病理图像预测空间转录组学，将图像特征与组织微环境关联
tldr: 针对现有方法忽略数字病理图像金字塔多尺度信息和斑点间视觉信息的问题，本文提出M2OST框架，利用多对一回归融合多尺度特征，从数字病理图像预测空间转录组学表达。该方法在预测精度上优于现有方法，为从病理图像低成本推断组织微环境提供了有效途径，可支持下游分析任务。
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 821, \"height\": 795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 872, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1841, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 264, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1850, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1805, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32830/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1836, \"height\": 380, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32830/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32830/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 873, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32830/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1833, \"height\": 671, \"label\": \"Table\"}]"
motivation: 现有方法忽略数字病理图像的多尺度结构和斑点间信息。
method: 提出M2OST，利用金字塔数据结构和多尺度信息进行多对一回归。
result: 在空间转录组学预测任务上取得优于现有方法的性能。
conclusion: 为从病理图像推断组织微环境开辟了新路径。
---

## Abstract
The advancement of Spatial Transcriptomics (ST) has facilitated the spatially-aware profiling of gene expressions based on histopathology images. Although ST data offers valuable insights into the micro-environment of tumors, its acquisition cost remains expensive. Therefore, directly predicting the ST expressions from digital pathology images is desired. Current methods usually adopt existing regression backbones along with patch-sampling for this task, which ignores the inherent multi-scale information embedded in the pyramidal data structure of digital pathology images, and wastes the inter-spot visual information crucial for accurate gene expression prediction. To address these limitations, we propose M2OST, a many-to-one regression Transformer that can accommodate the hierarchical structure of the pathology images via a decoupled multi-scale feature extractor. Unlike traditional models that are trained with one-to-one image-label pairs, M2OST uses multiple images from different levels of the digital pathology image to jointly predict the gene expressions in their common corresponding spot. Built upon our many-to-one scheme, M2OST can be easily scaled to fit different numbers of inputs, and its network structure inherently incorporates nearby inter-spot features, enhancing regression performance. We have tested M2OST on three public ST datasets and the experimental results show that M2OST can achieve state-of-the-art performance with fewer parameters and floating-point operations (FLOPs).

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：空间转录组学（Spatial Transcriptomics, ST）能够在组织原位同时获取基因表达与空间信息，为揭示肿瘤微环境提供关键见解，但实验成本高昂、临床应用受限。数字病理图像（Whole Slide Images, WSIs）成本低且常规生成，因此直接从 WSIs 预测 ST 表达具有重要价值。
- **现有方法局限**：当前方法多采用单尺度病理图像 patch 进行“一对一”回归，忽略了 WSI 的金字塔多尺度数据结构，浪费了不同放大倍率所蕴含的细胞形态与组织区域信息；同时丢弃了 spot 周边的视觉上下文（inter-spot features），限制了预测精度。
- **整体含义**：将 ST 预测重新建模为 **多对一**（many-to-one）回归问题——利用同一 spot 在不同 WSI 层级上的多个图像 patch，联合预测该 spot 的基因表达谱，从而融入多尺度信息与 spot 间特征，提升预测性能并降低成本。

## 2. 方法论

### 2.1 总体框架
提出 **M2OST**（Many-to-one regression Transformer），输入为同一 spot 对应的三个层级的病理图像 patch（如 level 0、level 1、level 2），输出为该 spot 的基因表达向量。模型由 **Deformable Patch Embedding (DPE)** 与堆叠的 **M2OST Encoder** 组成，编码器内部解耦为 **Intra-Level Token Mixing (ITMM)**、**Cross-Level Token Mixing (CTMM)** 和 **Cross-Level Channel Mixing (CCMM)**。

### 2.2 关键技术细节

- **Deformable Patch Embedding (DPE)**  
  采用共享权重的 patch embedding，但针对高层级图像使用不同 patch size（如 p、p/2、p/4），使中心区域获得更细粒度的 token，从而在保留高效性的同时强调 spot 内部特征。生成的长度分别为 L、2L、3L 的 token 序列。

- **Intra-Level Token Mixing Module (ITMM)**  
  对每一个层级的 token 序列独立应用类似 ViT 的自注意力，并引入 Random Mask Self-Attention 增强泛化。加入可学习位置编码和 [cls] token。

- **Cross-Level Token Mixing Module (CTMM)**  
  实现跨层级 token 级信息交互。由于各层级序列长度不同，采用全连接式跨注意力：  
  \( \text{CTMM}(S_i) = \sum_{j \neq i} \omega_{ij} \cdot \sigma\!\left(\frac{Q_i K_j^T}{\sqrt{d_K}}\right) V_j \)  
  其中 \(\omega_{ij}\) 为可学习权重，\(\sigma\) 为 softmax。各层级保持原有序列长度。

- **Cross-Level Channel Mixing Module (CCMM)**  
  实现跨层级通道级交互。对每个序列先全局平均池化，拼接后经 squeeze-and-excitation 生成通道注意力权重，再拆分并乘回各自序列，完成长度不敏感的通道混合。

### 2.3 多对一扩展性
M2OST 的模块对序列长度不敏感，可灵活增减输入流以适应不同数量的 WSI 层级（如二对一、四对一），且训练时可部分更新参数，支持缺失某个层级输入的情形。

## 3. 实验设计

### 3.1 数据集
三个公开 ST 数据集：
- **HBC**（人乳腺癌） – 68 张 WSI，30,612 个 spots，26,949 基因；
- **HER2+**（HER2 阳性乳腺癌） – 36 张 WSI，13,594 个 spots，15,045 基因；
- **cSCC**（皮肤鳞状细胞癌） – 12 张 WSI，8,671 个 spots，16,959 基因。

所有 spot 直径约 100–110 μm，中心距 150–200 μm。训练/验证/测试划分：60%/10%/30%。

### 3.2 对比方法（Benchmark）
涵盖多种类型的回归模型：
- 标准 CNN/Transformer：ResNet50、ViT‑B/16、Swin‑T、ConvNeXt‑T
- 多尺度方法：CrossViT、HIPT/iStar
- 专用 ST 预测模型：ST‑Net、DeepSpaCE、HisToGene、Hist2ST、BLEEP

评估指标：所有 spot 的平均 Pearson 相关系数（PCC）和均方根误差（RMSE）。基因预处理：过滤低变异基因，保留 250 个空间高变基因，表达式经标准化和 log 变换。

## 4. 资源与算力

- **硬件**：训练使用两块 **NVIDIA RTX A6000 (48 GB)** GPU。
- **训练参数**：优化器 Adam，学习率 1e‑4，epochs 100；patch-level 方法 batch size 为 96，slide-level 方法 batch size 为 1。
- **训练时长**：论文未明确报告每个实验的总训练时间，仅提供了参数量和 FLOPs 对比（M2OST 参数量 6.81M，FLOPs 2.24G），并指出推理速度比 iStar 快 100 倍。

## 5. 实验数量与充分性

实验设计较为全面，主要包括：
- **主要对比实验**：3 个数据集 × 11 个方法（含 M2OST），共约 33 组结果，展示 PCC、RMSE、参数量和 FLOPs。
- **消融实验**：
  - 组件替换（去除/替换 DPE、ITMM、CTMM、CCMM），验证每个模块的有效性和效率。
  - 输入组合探索：从单层级到三对一的多种输入组合，证实多尺度输入的优势。
- **统计检验**：配对 t 检验证明 M2OST 相较其他方法具有统计显著性（p<0.05），并给出箱线图展示稳定性。
- **可视化分析**：通过 PCA 降维后的 ST 彩色图与单个关键基因（DDX5）的空间分布图，直观比较不同方法的预测质量。

以上实验设计具有内在一致性与可重复性，比较基准公平，分组合理，能够支撑论文结论。

## 6. 论文的主要结论与发现

- **多对一建模明显提升性能**：使用多个层级的图像联合预测 spot 基因表达，比单一层级（level 0）的 PCC 有显著提升（如 cSCC 从 49.31% 增至 50.50%）。
- **M2OST 以极小模型达到 SOTA**：参数量 6.81 M、FLOPs 2.24 G 的情况下，在三个数据集上 PCC 均超越所有对比方法，且在 HER2+ 和 cSCC 上优于 ST‑Net 超过 1 个百分点。
- **解耦多尺度特征提取高效且有效**：ITMM 负责层内表征，CTMM 负责层间交互，CCMM 负责通道混合，这种解耦设计在保持性能的同时大幅降低计算开销。
- **Patch-level 方法优于 Slide-level 方法**：实验表明逐个 spot 独立预测的效果优于一次性预测整张切片，这说明基因表达主要与对应组织区域相关，全局相关性对精度提升有限。
- **推理速度优势明显**：相比同样使用多尺度但分步操作的 iStar，M2OST 在相同显存限制下推理快 100 倍以上。

## 7. 优点

- **创新的问题建模**：将 ST 预测重新定义为多对一回归，充分利用 WSI 固有金字塔结构，补偿了传统 patch 采样丢失的周围信息。
- **高度灵活与解耦的架构**：可动态增减输入流，各模块不依赖固定的序列长度，训练时亦可部分更新，适配不同 WSI 扫描协议和缺失情况。
- **计算友好**：相比同性能级别方法，参数量和 FLOPs 极小（例如参数量不到 ST‑Net 的 1），推理延迟低。
- **实验扎实**：涵盖 3 个数据集、11 个对比方法、多组消融和统计验证，结果可信度高。

## 8. 不足与局限

- **基因覆盖范围有限**：仅预测预筛选的 250 个空间高变基因，未验证对全基因谱的预测能力，可能无法满足需要全转录组信息的场景。
- **通用性未充分检验**：数据集均为肿瘤组织（乳腺癌、皮肤癌），在正常组织或其他器官类型上的泛化性能未知。
- **输入层级组合依赖人工设定**：模型假设 spot 在各层级上具有准确的空间对应关系，实际临床 WSI 拼接与配准误差可能影响效果。
- **对高分辨率细节的捕捉**：尽管引入 DPE 强调 patch 中心区域，但高层级图像中单个 spot 可能包含过多背景，仍存在信息稀释的可能。
- **训练时长与资源消耗未精细记录**：仅给出硬件型号和基本超参数，缺乏具体的训练耗时和不同 batch size 下的效率分析。

（完）
