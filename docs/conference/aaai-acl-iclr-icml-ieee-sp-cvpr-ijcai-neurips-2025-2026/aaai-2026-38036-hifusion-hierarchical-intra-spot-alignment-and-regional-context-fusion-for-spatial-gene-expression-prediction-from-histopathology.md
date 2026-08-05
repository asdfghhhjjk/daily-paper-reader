---
title: "HiFusion: Hierarchical Intra-Spot Alignment and Regional Context Fusion for Spatial Gene Expression Prediction from Histopathology"
title_zh: HiFusion：面向组织病理学空间基因表达预测的层次化点内对齐与区域上下文融合
authors: "Ziqiao Weng, Yaoyu Fang, Jiahe Qian, Xinkun Wang, Lee A D Cooper, Weidong Cai, Bo Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38036/41998"
tags: ["query:profile"]
score: 5.0
evidence: "从H&E全切片图像预测空间基因表达，通过层次化点内建模和区域上下文融合；融合跨点空间特征进行全局预测，类似于跨斑块信息融合。"
tldr: "针对从H&E全切片图像预测空间基因表达时难以捕捉点内异质性和形态噪声的问题，提出HiFusion框架。它通过层次化点内建模提取精细形态特征，并利用区域上下文融合整合周围组织信息。实验表明该方法能有效融合跨图像点的空间特征，实现准确的基因表达预测，为数字病理学中的空间分析提供了新工具。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1836, \"height\": 871}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 892}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1796, \"height\": 816}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1830, \"height\": 491}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 351}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 209}]"
motivation: 现有方法无法捕捉点内的复杂生物异质性，且融合上下文时易受形态噪声影响。
method: 提出HiFusion，包含层次化点内建模模块和区域上下文融合模块。
result: "在H&E全切片图像上准确预测空间基因表达，优于现有方法。"
conclusion: HiFusion有效融合多尺度空间特征，提升了从组织形态预测基因表达的能力。
---

## Abstract
Spatial transcriptomics (ST) bridges gene expression and tissue morphology but faces clinical adoption barriers due to technical complexity and prohibitive costs. While computational methods predict gene expression from H&E-stained whole-slide images (WSIs), existing approaches often fail to capture the intricate biological heterogeneity within spots and are susceptible to morphological noise when integrating contextual information from surrounding tissue. To overcome these limitations, we propose HiFusion, a novel deep learning framework that integrates two complementary components. First, we introduce the Hierarchical Intra-Spot Modeling module that extracts fine-grained morphological representations through multi-resolution sub-patch decomposition, guided by a feature alignment loss to ensure semantic consistency across scales. Concurrently, we present the Context-aware Cross-scale Fusion module, which employs cross-attention to selectively incorporate biologically relevant regional context, thereby enhancing representational capacity. This architecture enables comprehensive modeling of both cellular-level features and tissue microenvironmental cues, which are essential for accurate gene expression prediction. Extensive experiments on two benchmark ST datasets demonstrate that HiFusion achieves state-of-the-art performance across both 2D slide-wise cross-validation and more challenging 3D sample-specific scenarios. These results underscore HiFusion’s potential as a robust, accurate, and scalable solution for ST inference from routine histopathology.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：空间转录组学（Spatial Transcriptomics, ST）能够将基因表达与组织形态联系起来，但面临实验成本高、技术复杂、难以大规模临床推广的挑战。因此，研究者希望直接从常规的苏木精-伊红（H&E）染色全切片图像（WSIs）预测空间基因表达。
*   **现有方法的局限**：
    *   难以同时捕捉spot内部的精细形态学细节和全局组织上下文。
    *   通常将每个spot视为同质整体，忽略了spot内部可能包含的不同细胞类型、细胞核纹理和亚细胞结构等层次化信息。
    *   在整合周围组织区域的上下文信息时，缺乏对生物学相关性的显式建模，容易引入形态噪声，导致表示能力次优。
*   **研究动机**：设计一个能够显式建模spot内部多尺度形态异质性，并智能融合区域组织上下文信息的鲁棒框架，从而提升从组织病理学图像预测空间基因表达的准确性。

### 2. 论文提出的方法论
HiFusion 是一个双分支框架，核心包含两个模块：

*   **层次化点内建模模块 (Hierarchical Intra-Spot Modeling, HISM)**
    *   **核心思想**：将每个spot图像分解为多个不重叠的子块（sub-patch），形成层级结构（如1×1原始spot，2×2子块，7×7子块），分别提取多尺度特征，以捕捉从组织级到细胞级的形态模式。
    *   **关键细节**：
        *   Level-0输入为原始spot图像 \(X_i^S\)，经过共享编码器 \(f_\theta\) 提取全局特征 \(F_0^S\)。
        *   Level-1和Level-2输入分别为 \(p \times p\) 和 \(q \times q\) 的非重叠子块（\(q > p\)，实际使用 \(p=2, q=7\)），所有子块通过同一个编码器提取特征。
        *   将子块特征按原始空间位置重新拼接，并通过双线性插值对齐到 \(F_0^S\) 的分辨率，得到 \(\tilde{F}_1^S, \tilde{F}_2^S\)。
        *   **特征对齐损失 (Feature Alignment Loss)**：通过最小化 \(\tilde{F}_s^S\) 与 \(F_0^S\) 之间的差异，强制不同尺度特征在语义上保持一致，公式为 \( \mathcal{L}_{align} = \sum_{s=1}^{2} \| \tilde{F}_s^S - F_0^S \|_1 \)。

*   **上下文感知的跨尺度融合模块 (Context-Aware Cross-Scale Fusion, CCF)**
    *   **核心思想**：利用交叉注意力机制，以周围区域特征作为查询（query），自适应选择与目标spot生物学相关的精细形态特征进行融合，并抑制噪声。
    *   **关键细节**：
        *   **区域上下文编码**：提取一个比spot更大的邻域图像 \(X_i^N\)，经过轻量编码器 \(f_\psi\) 和全局平均池化得到区域查询特征 \(Q_i^N\)。
        *   **多尺度特征融合**：为来自HISM的三个尺度的特征 \(F_s^S\) 分配可学习的权重，加权求和得到融合的spot表示 \(F_{fused}^S\)。
        *   **交叉注意力**：将 \(F_{fused}^S\) 经自适应平均池化和形状变换后作为键（Key）和值（Value），将 \(Q_i^N\) 作为查询（Query），进行多头交叉注意力计算。
        *   **残差连接与预测**：将注意力输出与原始查询 \(Q_i^N\) 相加，再通过LayerNorm和全连接层预测基因表达向量 \(\hat{y}_i\)。

*   **损失函数**：总损失 \(\mathcal{L}_{total} = \mathcal{L}_{main} + \mathcal{L}_{aux} + \lambda \mathcal{L}_{align}\)。主回归损失和辅助回归损失均为均方误差（MSE），分别用于最终预测和三个尺度的独立预测。

### 3. 实验设计
*   **数据集/场景**：
    *   **HER2**：包含36张WSIs，13,620个ST spots，来自HER2阳性乳腺肿瘤样本。
    *   **ST-Data**：包含16个样本的41,544个spots的乳腺癌数据集。
    *   均预测表达量最高的250个基因。
*   **评估协议（Benchmarks）**：
    *   **2D Slide-wise 交叉验证**：4折交叉验证，确保同一患者的样本不跨训练/测试集。
    *   **3D Sample-specific 验证**：更具挑战性的样本内验证，使用每个患者的第一层组织切片训练，剩余层测试。
*   **对比方法**：
    *   局部模型：ST-Net， EGN
    *   全局/上下文模型：HisToGene， His2ST， TRIPLEX， ASIGN-2D， ASIGN-3D（当前SOTA模型）
*   **评估指标**：均方误差（MSE）、平均绝对误差（MAE）、皮尔逊相关系数（PCC）。

### 4. 资源与算力
*   **硬件**：使用单块 NVIDIA RTX 4090 GPU 进行所有实验。
*   **训练细节**：优化器为 Adam（momentum=0.9，weight_decay=1e-5），初始学习率 3e-4，采用余弦退火调度器（最小学习率 1e-6），总共训练 50 个 epoch，批次大小为 32。

### 5. 实验数量与充分性
*   **实验数量**：
    *   在 2 个数据集、2 种验证协议下与 7 个基线模型进行对比（主实验）。
    *   对 HISM 模块进行多组消融实验（不同分解级别组合、是否使用特征对齐损失）。
    *   对 CCF 模块进行两组消融实验（spot token 数量、邻域图像大小）。
    *   对特定癌标志基因（ERBB2, KRT19, CD74）的预测性能及空间分布进行可视化分析。
    *   与 ASIGN-3D 等高级 3D 预测策略进行对比分析。
*   **充分性与公正性**：实验设计全面，覆盖了多个公开基准、主流SOTA方法和不同泛化场景。消融实验系统评估了各个模块及其关键参数的影响。所有基线模型均在相同条件下重新训练和评估，保证了比较的公平性。

### 6. 论文的主要结论与发现
*   HiFusion 在 2D 和 3D 两种评估范式下均取得了最优性能，显著优于现有方法。
*   发现 3D sample-specific 的学习范式（单层训练，多层预测）在患者内泛化能力更强，且优于复杂的跨患者 3D 对齐方法（如 ASIGN-3D），这源于患者间的组织病理学和基因表达存在较大差异，跨患者训练可能引入噪声。
*   层次化 spot 内部分解能有效提升性能，其中“1×1（原始）+ 2×2 + 7×7”的组合效果最佳，能够互补地捕捉不同尺度的空间粒度。
*   特征对齐损失强化了跨尺度的语义一致性，对性能有正向贡献。
*   上下文区域并非越大越好，中等大小（2倍spot尺寸）效果最佳，过大的区域会引入无关噪声。

### 7. 优点
*   **创新性强**：首次将层次化点内分解与基于交叉注意力的上下文选择性融合相结合，有效解决了spot内异质性建模和上下文智能整合的难题。
*   **方法论扎实**：通过特征对齐损失确保多尺度语义一致性，利用残差交叉注意力动态融合区域与局部信息，设计严谨。
*   **实验评估全面**：不仅采用了常规的2D交叉验证，还引入了更具挑战性的3D样本内验证，并从定量、定性、消融等多个维度进行了详尽分析，揭示了区域大小、3D学习策略等非平凡发现。
*   **临床转化潜力大**：能够从廉价、常规的H&E图像准确预测空间基因表达和癌症标志物分布，为临床提供了一种经济、可扩展的解决方案。

### 8. 不足与局限
*   **区域上下文整合路径单一**：论文指出，目前通过单分支设计整合区域上下文，未来可探索更高效、更具表达力的机制来提取和融合组织区域的细粒度生物学特征。
*   **基因覆盖范围有限**：受限于计算量和数据，仅预测了表达量最高的250个基因，未能预测全基因组表达，可能忽略了部分重要的低丰度基因。
*   **模型泛化性验证有限**：仅在两种乳腺癌数据集上进行了验证，其对其他组织类型、疾病模型的跨数据集泛化能力尚不明确。
*   **生物学可解释性缺失**：虽然展示了预测能力，但未对模型学习到的多尺度形态特征与特定生物学功能之间的关联进行深入的可解释性分析。

（完）
