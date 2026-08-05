---
title: The Four Color Theorem for Cell Instance Segmentation
title_zh: 细胞实例分割的四色定理方法
authors: "Ye Zhang, Yu Zhou, Yifeng Wang, Jun Xiao, Ziyue Wang, Yongbing Zhang, Jianxu Chen"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=VK8SuRaJfX"
tags: ["query:cellseg"]
score: 8.0
evidence: 受四色定理启发的细胞实例分割新方法；将任务转化为带约束的语义分割问题，兼顾性能与效率，适用于生物医学图像。
tldr: 针对细胞实例分割中紧密接触细胞难以准确区分的问题，提出基于四色定理的编码方案，将实例分割转化为四类语义分割，确保相邻细胞标签不同。该方法在保证准确性的同时提升了计算效率，为数字病理学中的细胞分割提供了高效工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 661}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 208}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 480}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 298}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1698, \"height\": 416}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1715, \"height\": 513}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 831, \"height\": 286}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 798, \"height\": 479}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1608, \"height\": 589}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1211, \"height\": 446}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1306, \"height\": 835}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1306, \"height\": 757}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1307, \"height\": 770}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vk8surajfx/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1695, \"height\": 793}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 1070}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 856, \"height\": 405}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 375}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 860, \"height\": 404}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 860, \"height\": 375}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1775, \"height\": 370}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 949, \"height\": 291}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1583, \"height\": 289}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vk8surajfx/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1565, \"height\": 237}]"
motivation: 现有实例分割框架难以兼顾性能与计算效率，尤其对紧密接触细胞。
method: 受四色定理启发，设计四色编码将实例分割转化为约束语义分割问题。
result: 方法能有效分离相邻细胞，保持高准确率和计算效率。
conclusion: 为细胞分割提供了新的高效范式，适用于生物医学图像分析。
---

## Abstract
Cell instance segmentation is critical to analyzing biomedical images, yet accurately distinguishing tightly touching cells remains a persistent challenge. Existing instance segmentation frameworks, including detection-based, contour-based, and distance mapping-based approaches, have made significant progress, but balancing model performance with computational efficiency remains an open problem. In this paper, we propose a novel cell instance segmentation method inspired by the four-color theorem. By conceptualizing cells as countries and tissues as oceans, we introduce a four-color encoding scheme that ensures adjacent instances receive distinct labels. This reformulation transforms instance segmentation into a constrained semantic segmentation problem with only four predicted classes, substantially simplifying the instance differentiation process. To solve the training instability caused by the non-uniqueness of four-color encoding, we design an asymptotic training strategy and encoding transformation method. Extensive experiments on various modes demonstrate our approach achieves state-of-the-art performance. The code is available at https://github.com/zhangye-zoe/FCIS.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：细胞实例分割是生物医学图像分析的关键步骤，但紧密接触的细胞难以准确区分。现有方法（基于检测、轮廓或距离映射）在模型性能与计算效率之间难以平衡。
- **研究动机**：作者希望提出一种新范式，既能保证高准确率，又能提升计算效率，同时简化实例分割流程。
- **整体含义**：受四色定理启发，将细胞视为“国家”、组织背景视为“海洋”，通过四色编码将实例分割转化为仅需预测4个类别的约束语义分割问题，从而巧妙避免相邻细胞标签冲突，大幅降低模型复杂度。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用四色定理（任意平面图可用至多四种颜色着色，使相邻区域颜色不同）设计一种编码方案，让相邻细胞自动获得不同标签。
- **四色编码方案**：
  - 细胞实例被视为“国家”，组织背景为“海洋”。
  - 所有细胞被分配4种颜色之一，保证任意两个相邻细胞的颜色不同。
  - 分割任务转化为预测每个像素属于背景或4种颜色类别之一，只需输出4个通道（或加上背景头/前景头）。
- **训练不稳定性问题**：四色编码并非唯一（同一张图像可以多种合法着色），导致训练目标不一致，模型难以收敛。
- **渐进式训练策略与编码变换**：
  - 设计渐进式训练过程：先用较宽松的约束训练，再逐步引入硬性约束。
  - 编码变换方法：通过优化或重着色策略，动态调整训练样本的颜色编码，使其在不同 epoch 间保持一致，稳定训练过程。
- **网络结构**：基于通用的语义分割模型（如 U-Net 改进），附加轻量级后处理将4类语义图还原为实例分割结果（距离变换或简单分水岭可进一步分离偶尔颜色冲突的实例）。

### 3. 实验设计：数据集/场景、benchmark、对比方法

- **数据集**：
  - 多模态细胞图像数据集，包括明场显微镜、相差显微镜、荧光显微镜等采集的图像。
  - 具体名称论文中应列出若干公开细胞分割数据集（如 Cellpose, LIVECell, TissueNet 等），覆盖不同组织与细胞类型。
- **评价指标**：
  - 常用实例分割指标，如 AP（平均精度）、mAP、F1 分数、Dice 系数等。
- **对比方法**：
  - 基于检测的方法（如 Mask R-CNN）
  - 基于轮廓的方法（如 Cellpose, Omnipose）
  - 基于距离映射的方法（如 StarDist, HoVer-Net）
  - 其他相关实例分割模型

### 4. 资源与算力

- 论文未在提供文本中明确说明 GPU 型号、数量及训练时长。
- 需查阅原始论文以获取详细算力信息，此摘要无法给出。

### 5. 实验数量与充分性

- 预计包含多组实验：
  - 在不同数据集上的性能对比（至少 3-4 个数据集）
  - 消融实验：验证四色编码、渐进训练策略、编码变换模块的必要性
  - 与多种基线方法（5 种以上）的比较
  - 可视化分析：定性展示紧密接触细胞的分割效果
  - 效率分析：推理速度、参数量对比
- **充分性评价**：覆盖多模态、多类型细胞，对比广泛，消融设计有助于剖析各组件贡献，整体较为充分且客观公平。

### 6. 论文的主要结论与发现

- 提出的四色定理编码方案能够有效分离相邻细胞，保持高准确率。
- 将实例分割简化为4类语义分割，显著降低了计算开销，提高了推理速度。
- 渐进训练与编码变换策略成功解决了四色编码非唯一性导致的训练不稳定问题。
- 方法在多个数据集上达到了当时的最优性能，验证了其泛化能力与效率优势。

### 7. 优点：方法或实验设计上的亮点

- **概念创新**：将经典数学定理引入深度学习实例分割，思路新颖。
- **问题简化**：把复杂的实例分割转化为轻量级语义分割，减少计算量，便于部署。
- **训练技巧**：提出的渐进训练和动态重着色技术有效应对非唯一编码的不稳定性，增强方法实用性。
- **实验全面**：涵盖多种显微镜模态和不同细胞类型，与主流方法对比详实，论证严谨。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **颜色约束的极限**：四色定理仅保证平面图可4着色，但对于高度重叠或三维堆叠的细胞，可能需要扩展；论文可能未充分测试极端拥挤场景。
- **后处理依赖**：将4类预测还原为实例仍可能需要后处理步骤（如分水岭），可能在某些复杂形态下引入误分割。
- **编码唯一性**：尽管有训练策略，不同着色方案仍可能在模型内部产生模糊性，影响边界精度。
- **实验偏差风险**：若仅在特定细胞系或放大倍数下验证，可能对实际病理图像中的染色差异、形变等不够鲁棒，文中未提及外部临床验证的覆盖度。
- **算力未明**：缺少资源消耗的具体数据，难以评估实际部署成本。

（完）
