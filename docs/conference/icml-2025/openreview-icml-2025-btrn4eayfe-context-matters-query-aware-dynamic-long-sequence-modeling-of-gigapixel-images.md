---
title: "Context Matters: Query-aware Dynamic Long Sequence Modeling of Gigapixel Images"
title_zh: 语境至关重要：千兆像素图像的查询感知动态长序列建模
authors: "Zhengrui Guo, Qichen Sun, Jiabo MA, Lishuang Feng, Jinzhuo Wang, Hao Chen"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=BtRn4eayfE"
tags: ["query:pathology-ai"]
score: 8.0
evidence: Querent框架实现高效的全切片图像长序列建模
tldr: 全切片图像分析面临图块数量巨大导致的Transformer计算瓶颈。现有近似方法牺牲了模型能力。本文提出Querent框架，通过查询感知的动态长上下文建模，实现了对标准自注意力的理论有界近似，同时保持实际效率。该方法在计算病理学任务上取得高效且准确的性能，为全切片图像分析提供了实用的长序列建模方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 850, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1724, \"height\": 979, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 774, \"height\": 682, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 834, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 854, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-btrn4eayfe/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 857, \"height\": 353, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-btrn4eayfe/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1776, \"height\": 920, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-btrn4eayfe/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1775, \"height\": 856, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-btrn4eayfe/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 583, \"label\": \"Table\"}]"
motivation: Transformer在全切片图像分析中因二次复杂度而难以应用。
method: 提出Querent框架，通过对每个查询自适应选择相关上下文进行动态长序列建模。
result: 在多个计算病理学基准上以更低计算成本达到全注意力精度。
conclusion: Querent为全切片图像的高效长序列建模提供了新途径。
---

## Abstract
Whole slide image (WSI) analysis presents significant computational challenges due to the massive number of patches in gigapixel images. While transformer architectures excel at modeling long-range correlations through self-attention, their quadratic computational complexity makes them impractical for computational pathology applications. Existing solutions like local-global or linear self-attention reduce computational costs but compromise the strong modeling capabilities of full self-attention. In this work, we propose **Querent**, *i.e.*, the **quer**y-awar**e** long co**nt**extual dynamic modeling framework, which achieves a theoretically bounded approximation of full self-attention while delivering practical efficiency. Our method adaptively predicts which surrounding regions are most relevant for each patch, enabling focused yet unrestricted attention computation only with potentially important contexts. By using efficient region-wise metadata computation and importance estimation, our approach dramatically reduces computational overhead while preserving global perception to model fine-grained patch correlations. Through comprehensive experiments on biomarker prediction, gene mutation prediction, cancer subtyping, and survival analysis across over 10 WSI datasets, our method demonstrates superior performance compared to the state-of-the-art approaches. Codes are available at https://github.com/dddavid4real/Querent.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题**：全切片图像（Whole Slide Image, WSI）包含成千上万的图块（patches），标准Transformer的自注意力机制计算复杂度为二次（O(n²)），无法直接处理。
- **现有方案局限**：线性注意力（如Nyströmformer）或局部-全局注意力（如HIPT）虽降低了计算成本，但牺牲了全自注意力的建模能力，或依赖固定的空间模式，无法适应病理特征的高度可变性和上下文依赖性。
- **核心洞见**：不同查询图块关注的相关区域不同（例如，查肿瘤边界时，肿瘤-基质交界区比远处正常组织更相关），因此注意力应当动态、自适应地选择每个查询最相关的上下文。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出**Querent**框架，通过**查询感知的动态稀疏注意力**，实现全自注意力的有界近似，同时保持线性复杂度。
- **关键技术细节**：
  1. **区域级元数据汇总**：将WSI划分为若干区域（每区K个图块），计算每个区域的最小和最大特征向量，并通过可学习投影网络将其映射到共享嵌入空间。
  2. **区域重要性估计**：对每个查询图块，利用区域元数据计算重要性得分（取查询与区域最小/最大投影向量的点积绝对值的最大值），选择top-K最相关区域。
  3. **查询感知的选择性注意力**：仅对查询与所选区域内的图块计算密集自注意力，复杂度从O(N²)降至O(N·K·p)（p为每区图块数）。
  4. **特征聚合**：通过可学习的注意力池化，将增强后的图块特征聚合为切片级表示，用于分类或生存预测。
- **理论保证**：定理3.1证明，在合理条件下（注意力分数随空间距离指数衰减、区域直径足够小、区域间距离足够大等），查询感知注意力的Frobenius范数误差被有界常数项控制，实现全注意力的近似。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：共使用11个公开WSI数据集，涵盖四类任务：
  - 生物标志物预测：BCNB-ER（n=1038）
  - 基因突变预测：TCGA-LUAD TP53（n=469）
  - 癌症亚型分类：UBC-OCEAN（5亚型，n=527）
  - 生存分析：8个TCGA子集（BRCA、UCEC、STAD、LUAD、LUSC、SKCM、KIRC、KIRP）
- **基准**：5折交叉验证，分类任务报告ACC、AUC、F1分数；生存任务报告C-Index。
- **对比方法**：
  - 简单池化方法：Mean Pooling、Max Pooling
  - MIL方法：ABMIL、DS-MIL、CLAM-SB、DTFD、WiKG、MambaMIL
  - 基于Transformer的方法：TransMIL、HIPT、HistGen、RRT-MIL、LongMIL
- **统一设置**：所有方法均使用PLIP（病理视觉-语言基础模型）提取512维图块特征。

### 4. 资源与算力

- 论文在实现细节中提到了训练配置：使用AdamW优化器，学习率分类任务1e-4、生存任务2e-4，batch size为1 WSI per GPU，训练50个epoch，梯度裁剪最大范数1.0。但未明确说明GPU型号、数量及总训练时长。因此，算力信息不完整。

### 5. 实验数量与充分性

- **实验数量**：在3个分类任务（含消融实验）和8个生存分析任务上进行了全面评估，共11个数据集；另外单独做了区域汇总策略消融、区域重要性估计消融、区域大小消融、计算效率对比。
- **充分性**：实验覆盖了多种典型CPath任务，对比方法涵盖主流MIL和Transformer变体，消融实验设计合理（对比了min/max/mean/mean-std等汇总策略，以及随机选择、侧网络等重要性估计方法），结果具有统计显著性（p<0.005）。整体公平客观。

### 6. 论文的主要结论与发现

- Querent在所有分类任务上均达到SOTA：BCNB-ER ACC 0.836、AUC 0.848；TCGA-LUAD TP53 ACC 0.678、AUC 0.706；UBC-OCEAN ACC 0.835、AUC 0.956（比第二名分别高1.2%和1.0%）。
- 在8个TCGA生存分析子集上，平均C-Index 0.670，显著高于第二名（WiKG和MambaMIL的0.647），并在其中6个子集上取得最佳。
- 消融实验表明：min-max汇总策略优于单一min/max/mean/mean-std（相关性0.975 vs 0.897-0.959）；查询感知的区域选择优于随机选择或侧网络（UBC-OCEAN上ACC提升8.9%）；区域大小在16-24时最优。
- 计算效率：对100k图块，Querent仅需1GB内存和500 GFLOPs，而全自注意力需要37GB和10,000 GFLOPs，实现了近线性缩放。

### 7. 优点

- **方法创新**：提出查询感知的动态稀疏注意力，首次实现全自注意力的理论有界近似，同时保持实际效率，填补了计算病理学中高效长序列建模的空白。
- **理论严谨**：提供了详细的定理证明，阐明近似误差有界条件，增强了方法的可信度。
- **实验全面**：覆盖多种任务和数据集，消融实验深入，对比方法广泛，结果统计显著。
- **效率优异**：内存和计算成本极低，使大规模WSI处理可行。

### 8. 不足与局限

- **实验覆盖**：尽管数据集多样，但全部来自公开数据集（BCNB、TCGA、UBC-OCEAN），未在真实临床部署场景下验证；且仅使用PLIP一种特征提取器，未测试其他基础模型（如UNI、CONCH）。
- **超参数敏感性**：区域大小K、所选区域数K等超参数依赖经验调节，理论中虽有条件但未给出自动调优策略。
- **区域划分硬固定**：区域划分基于空间网格，未考虑组织学边界（如肿瘤区域与正常区域边界），可能将异质性组织混入同一区域。
- **资源信息缺失**：未报告具体GPU型号、数量及训练总时间，影响可复现性。
- **应用限制**：目前仅用于研究，临床落地需要额外验证和监管审批。

（完）
