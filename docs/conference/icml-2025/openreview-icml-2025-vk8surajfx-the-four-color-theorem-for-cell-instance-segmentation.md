---
title: The Four Color Theorem for Cell Instance Segmentation
title_zh: 细胞实例分割的四色定理
authors: "Ye Zhang, Yu Zhou, Yifeng Wang, Jun Xiao, Ziyue Wang, Yongbing Zhang, Jianxu Chen"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=VK8SuRaJfX"
tags: ["query:cellseg"]
score: 9.0
evidence: 基于四色定理的细胞实例分割方法
tldr: 细胞实例分割中紧密相邻细胞的区分是长期挑战。现有检测、轮廓或距离图方法难以平衡性能与效率。本文受四色定理启发，将细胞视为国家，组织为海洋，引入四色编码方案确保相邻实例标签不同。该方法将实例分割转化为仅有四类的约束语义分割问题，大幅简化了分割流程。实验表明该方法在多个细胞数据集上取得了高效准确的实例分割结果。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 661, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 208, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 298, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1698, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1715, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 831, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 798, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1608, \"height\": 589, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1211, \"height\": 446, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1306, \"height\": 835, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1306, \"height\": 757, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1307, \"height\": 770, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1695, \"height\": 793, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 1070, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 856, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 860, \"height\": 404, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 860, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1775, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 949, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1583, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1565, \"height\": 237, \"label\": \"Table\"}]"
motivation: 现有细胞实例分割方法在相邻细胞区分上表现不佳且计算复杂。
method: 提出四色编码方案，将实例重标注为四类语义标签，用语义分割网络直接输出实例。
result: 在多个公共细胞数据集上实现了优于现有方法的准确率和速度。
conclusion: 四色定理为细胞实例分割提供了一种简洁高效的解决思路。
---

## Abstract
Cell instance segmentation is critical to analyzing biomedical images, yet accurately distinguishing tightly touching cells remains a persistent challenge. Existing instance segmentation frameworks, including detection-based, contour-based, and distance mapping-based approaches, have made significant progress, but balancing model performance with computational efficiency remains an open problem. In this paper, we propose a novel cell instance segmentation method inspired by the four-color theorem. By conceptualizing cells as countries and tissues as oceans, we introduce a four-color encoding scheme that ensures adjacent instances receive distinct labels. This reformulation transforms instance segmentation into a constrained semantic segmentation problem with only four predicted classes, substantially simplifying the instance differentiation process. To solve the training instability caused by the non-uniqueness of four-color encoding, we design an asymptotic training strategy and encoding transformation method. Extensive experiments on various modes demonstrate our approach achieves state-of-the-art performance. The code is available at https://github.com/zhangye-zoe/FCIS.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：细胞实例分割是生物医学图像分析的基础任务，但现有方法（检测型、轮廓型、距离图型）在处理紧密相邻细胞时普遍存在性能瓶颈，且面临模型复杂度高、后处理繁琐、泛化能力不足等问题。如何在保证分割精度的同时降低计算开销，是领域内长期未解决的挑战。
- **核心含义**：本文提出一种受四色定理启发的全新范式，将细胞视为“国家”、组织背景视为“海洋”，通过仅需四种颜色的编码方案，将实例分割转化为一个四类别的约束语义分割问题，从而大幅简化区分相邻实例的难度，同时提升模型效率和鲁棒性。

### 2. 论文提出的方法论

- **核心思想**：利用四色定理（任意平面地图的相邻区域只需四种颜色即可区分）来编码细胞实例，使得每个相邻细胞被赋予不同颜色标签，将实例分割转化为仅含4个语义类别的分割任务。
- **关键技术细节**：
    1. **贪心编码算法**：为每张图像构建细胞邻接图，按顺序为每个细胞分配可用最小颜色（1-4），生成四色分割掩模。
    2. **渐近训练策略**：网络输出5通道（1背景+4颜色），先通过二分类（前景/背景）提取空间语义，再对前景区域进行四色分类，避免直接多类训练带来的类不平衡问题。
    3. **负采样正交约束**：对相邻细胞的特征进行负采样，通过余弦相似度损失（`L_ort`）增强特征区分性，确保相邻细胞编码不同。
    4. **编码转换模块**：针对四色编码的非唯一性（替换、交换、规则修改），设计两个卷积层将网络预测映射到最小颜色表示，消除歧义，稳定训练。
- **损失函数**：`L_total = L_sem + 2·L_ort + 1·L_cls`，其中`L_sem`是二分类语义损失（CE+Dice），`L_cls`是转换后的四色分类损失。

### 3. 实验设计

- **使用的数据集**：四个不同模态的生物医学图像数据集：
  - **BBBC006v1**（荧光染色，696×520像素，462/153/153划分）
  - **DSB2018**（荧光染色，256×256~520×696，380/67/50划分）
  - **PanNuke**（H&E染色，256×256，2656/2523/2722划分）
  - **YeaZ**（明场+相差，300/20/29划分）
- **Benchmark方法**：8种主流细胞分割方法，包括检测型（DoNet）、轮廓型（DCAN、NucleiSegNet、GeSegNet）、距离图型（HoverNet、CPP-Net、CellPose）以及SAM基础模型（Un-SAM）。
- **评估指标**：DICE、AJI（聚合Jaccard指数）、DQ（检测质量）、SQ（分割质量）、PQ（全景质量）。

### 4. 资源与算力

- 文中明确提及使用 **NVIDIA A100 GPU** 进行实验，代码基于PyTorch实现。
- 未具体说明GPU数量、训练轮次耗时或算力消耗（如总GPU小时数），仅提到训练200个epochs，学习率0.01等超参数。

### 5. 实验数量与充分性

- **实验数量**：主实验在4个数据集上与8种方法对比；消融实验在DSB2018和PanNuke上分别测试了渐近训练、编码转换、负采样三个模块的贡献；同时进行了收敛性分析、可视化比较以及超参数（采样率、损失权重）的消融。
- **充分性**：实验覆盖不同成像模态（荧光、H&E、明场），对比方法涵盖主流三类框架，消融设计合理，结果报告了多个指标（DICE、AJI、DQ、SQ、PQ），整体上充分且客观，验证了方法的有效性和泛化能力。

### 6. 论文的主要结论与发现

- 基于四色定理的方法（FCIS）在所有四个数据集上均达到 **最先进（SOTA）** 或接近SOTA的性能，同时参数量（39.75M）和计算成本（58.03G FLOPs）低于多数对比方法。
- 直接使用四色编码作为监督会导致训练不稳定，而渐近训练策略和编码转换模块有效解决了该问题，显著提升收敛速度和分割质量。
- 负采样正交约束是性能提升的关键，能够强制相邻细胞获得不同特征表示。

### 7. 优点

- **方法新颖性**：首次将四色定理引入细胞实例分割，将复杂实例区分问题转化为简单的多类语义分割，颠覆传统范式。
- **理论支撑**：提供了贪心算法全局最优性定理和编码兼容性定理，论证了方法在细胞分布场景下的适用性。
- **实验全面性**：在多种细胞图像模态上进行了系统评估，与多种主流方法公平对比，消融实验严谨。
- **实用潜力**：模型复杂度低、后处理简化，易部署于实际生物医学分析流程，且代码已开源。

### 8. 不足与局限

- **数据集覆盖**：未在3D细胞图像或低信噪比的活细胞成像数据集上验证，泛化性有待进一步确认。
- **稀疏细胞情况**：当图像中细胞极少或拓扑结构特殊时，四色编码的冗余性可能导致学习信号不足，文中未详述应对策略。
- **训练复杂性**：非唯一性编码的处理引入了额外模块（渐近训练、编码转换、负采样），增加了超参数调优负担。
- **与最新基础模型的对比**：仅对比了Un-SAM，未与更多基于视觉基础模型（如SAM、CellSAM）的微调版本对比，可能低估前沿性能。
- **应用范围**：当前仅针对细胞核实例分割，未拓展到细胞分类、跟踪等下游任务，功能单一。

（完）
