---
title: "unMORE: Unsupervised Multi-Object Segmentation via Center-Boundary Reasoning"
title_zh: "unMORE: 通过中心-边界推理实现无监督多目标分割"
authors: "Yafei YANG, Zihui Zhang, Bo Yang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=vF5F7cL76i"
tags: ["query:cellseg"]
score: 6.0
evidence: 基于中心-边界推理的无监督多目标分割方法
tldr: unMORE提出了一种无监督的多目标分割流水线，通过显式学习三层次物体中心表示和多物体推理模块，能够发现复杂真实图像中的多个物体。该方法无需标注即可实现实例分割，对于细胞实例分割等任务具有潜在应用价值。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 455, \"height\": 328, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1736, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1721, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1703, \"height\": 314, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1424, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1637, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1577, \"height\": 821, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1765, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 191, \"height\": 188, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1504, \"height\": 1797, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1771, \"height\": 219, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1413, \"height\": 847, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1422, \"height\": 867, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1425, \"height\": 872, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1421, \"height\": 809, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1425, \"height\": 808, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vf5f7cl76i/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 800, \"height\": 597, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1757, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1774, \"height\": 440, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 851, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 876, \"height\": 197, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1772, \"height\": 477, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1586, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1759, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1582, \"height\": 481, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1344, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1391, \"height\": 608, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1784, \"height\": 527, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1384, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1754, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1765, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-vf5f7cl76i/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1452, \"height\": 2117, \"label\": \"Table\"}]"
motivation: 现有无监督分割方法只能处理简单合成对象或少量真实对象，难以应对复杂场景。
method: 提出两阶段流水线：第一阶段学习物体中心、边界和区域表示；第二阶段利用物体先验进行多目标推理。
result: 在复杂真实图像上实现了优于现有方法的分割性能。
conclusion: unMORE展示了无监督多目标分割的潜力，可拓展至细胞分割等任务。
---

## Abstract
We study the challenging problem of unsupervised multi-object segmentation on single images. Existing methods, which rely on image reconstruction objectives to learn objectness or leverage pretrained image features to group similar pixels, often succeed only in segmenting simple synthetic objects or discovering a limited number of real-world objects. In this paper, we introduce unMORE, a novel two-stage pipeline designed to identify many complex objects in real-world images. The key to our approach involves explicitly learning three levels of carefully defined object-centric representations in the first stage. Subsequently, our multi-object reasoning module utilizes these learned object priors to discover multiple objects in the second stage. Notably, this reasoning module is entirely network-free and does not require human labels. Extensive experiments demonstrate that unMORE significantly outperforms all existing unsupervised methods across 6 real-world benchmark datasets, including the challenging COCO dataset, achieving state-of-the-art object segmentation results. Remarkably, our method excels in crowded images where all baselines collapse. Our code and data are available at https://github.com/vLAR-group/unMORE.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将基于您提供的论文内容，对《unMORE: Unsupervised Multi-Object Segmentation via Center-Boundary Reasoning》进行结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）

*   **核心问题**：论文聚焦于**无监督多目标分割**这一极具挑战性的任务。旨在从单张真实世界图像中，自动发现并分割出多个复杂的物体，且完全无需任何人工标注（如边界框、分割掩膜）进行训练。
*   **研究动机**：现有方法存在明显局限性，主要分为两类：
    *   **基于重建的槽位方法**（如Slot Attention及其变体）：通过图像重建目标驱动瓶颈结构学习物体表征，在简单合成数据集上表现出色，但难以泛化到复杂真实图像。
    *   **基于自监督特征的方法**（如TokenCut, CutLER, DINOSAUR）：利用自监督模型（如DINO/v2）的特征来分组像素。虽然取得了更优结果，但它们通常只关注于少量物体，且存在**欠分割**问题（例如将邻近的多个物体错误地合并为一个），因为它们倾向于简单地将相似特征聚类，而缺乏区分物体边界与中心的能力。
*   **整体含义**：本文提出了一种全新的范式，模拟人类“先学习物体概念，再进行场景推理”的认知过程，试图从根本上解决“什么是物体”（物体性定义）和“如何发现它们”（物体搜索策略）这两个核心难题。

### 2. 论文提出的方法论：核心思想、关键技术细节

论文提出了一个名为 **unMORE** 的**两阶段流水线**，核心思想是先学习显式的物体中心表征，再基于这些表征进行无网络的多目标推理。

**第一阶段：物体中心表征学习（Object-Centric Representation Learning）**
*   **目标**：训练一个**物体性网络（Objectness Network）**，使其学习以下三个层次显式定义的物体表征。这些表征是模仿人类对物体的认知（是否存在、在哪里、什么形状）。
    *   **物体存在性得分（Object Existence Score, $f_e$）**：一个标量，判断图像/图像块中是否包含有效物体。
    *   **物体中心场（Object Center Field, $f_c$）**：为物体内部每个像素分配一个指向物体边界框中心的单位方向向量。这是后续分离多个物体中心的关键。
    *   **物体边界距离场（Object Boundary Distance Field, $f_b$）**：为每个像素分配一个到最近物体边界的归一化有符号距离值。物体内部为正，外部为负。
*   **关键技术**：
    *   **训练数据生成**：利用自监督模型（DINO/v2）和VoteCut方法，从ImageNet图像中自动提取单物体掩膜，以此作为“伪标签”来定义上述三种表征。同时，通过裁剪背景区域生成负样本，增强网络对背景的判别力。
    *   **网络架构**：使用ResNet50预测存在性得分，使用DPT-large（常用于密集预测）作为共享主干，连接两个独立CNN头部分别预测中心场和边界距离场。
    *   **损失函数**：结合交叉熵损失、L2损失和L1损失对三个任务进行联合优化。

**第二阶段：多目标推理模块（Multi-Object Reasoning Module）**
*   **目标**：利用训练好并冻结的物体性网络，在复杂场景图像中自动发现多个物体。此模块**完全无需神经网络**，也无需人工标签。
*   **算法流程**（网络-free的迭代推理过程）：
    1.  **初始化（Step #0）**：在场景图像上均匀采样大量不同尺度和长宽比的初始边界框候选。
    2.  **存在性检查（Step #1）**：将每个候选框裁剪并缩放后输入物体性网络，丢弃（$f_e$得分低于阈值）不包含物体的候选框。
    3.  **中心推理与分裂（Step #2）**：对于高分候选框，分析其中心场$f_c$。这是解决**欠分割**（多物体挤在一个框内）的核心步骤。
        *   设计一个**反中心核**（5x5）与中心场进行卷积，生成**反中心图**。反中心图的高值像素表示该点位于多个物体之间。
        *   如果反中心图最大值超过阈值$\tau_c$，则认为该候选框包含多个物体，并在此位置将候选框分裂成四个子候选框（上、下、左、右），然后递归回到Step #1。
        *   否则，进入下一步。
    4.  **边界推理（Step #3）**：对于仅包含单个物体的候选框，利用其边界距离场$f_b$来微调边界框的位置和大小，以解决**过/欠拟合**问题。
        *   分析候选框四条边框上的$f_b$值。正的最大距离值表示该边框有背景需要收缩，负值表示物体被切掉需要扩张。
        *   基于梯度信息，迭代地调整边界框的四条边，直到收敛，从而得到一个紧贴物体的精确边界框。
    5.  **后处理**：对所有收敛的边界框应用非极大值抑制（NMS）去除冗余。最终，通过合并中心场和边界距离场信息生成物体的分割掩膜。
*   **可选步骤：训练检测器**：利用上述步骤发现的高置信度物体作为伪标签，可以作为监督信号来训练一个单独的类别无关检测器（如Cascade Mask R-CNN），从而进一步提升性能和效率。

### 3. 实验设计：数据集、基准与对比方法

*   **数据集**：
    *   **主要评估集**：**COCO 2017 val 增强版（COCO\*）**。作者指出COCO官方val集存在大量未标注物体，因此他们手动补充标注了197个新类别和10336个新实例，使评价更公平。该数据集是评估的核心。
    *   **其他零样本迁移测试集**：COCO20K、LVIS、PASCAL VOC、KITTI、Object365、OpenImages，共6个，涵盖了自动驾驶、通用物体、长尾分布等多种场景，全面检验模型泛化能力。
*   **基准（Benchmark）**：COCO* 验证集上的标准指标，包括边界框AP/AR（AP_box, AR_box）和掩膜AP/AR（AP_mask, AR_mask）。
*   **对比方法**：共分为三类，确保比较的广泛性和公平性：
    *   **Group 1：无需可学习模块的直接发现方法**（FreeMask, MaskCut, VoteCut）。这些方法不涉及网络训练，直接利用DINO特征进行分割。
    *   **Group 2：使用可学习模块的直接发现方法**（DINOSAUR, FOUND, **unMORE_disc**）。这些方法训练了某种形式的网络，但最终推理方式类似。
    *   **Group 3：额外训练检测器的方法**（UnSAM, CutLER, CuVLER, **unMORE**）。这些方法使用自发现伪标签先训练检测器，再用检测器推断，是目前的主流方式。实验包括了多种训练设置（如是否联合ImageNet伪标签、是否多轮训练等）。

### 4. 资源与算力

文中明确提到了**资源与算力**信息，总结如下：
*   **训练物体性网络**：使用4块NVIDIA V100 GPU。存在性模型训练100K次迭代，中心/边界模型训练50K次迭代。
*   **训练最终检测器（unMORE）**：使用8块GPU，训练25K次迭代，耗时约**30小时**。相比之下，基线方法CutLER/CuVLER需要约60-75小时。
*   **直接发现推理（unMORE_disc）**：每张图片平均耗时45.3秒，比MaskCut（33.7秒）慢，但比VoteCut（5.1秒）慢很多。这是其主要效率瓶颈。
*   **最终检测器推理（unMORE）**：与基线方法速度相当（0.1秒/张）。

### 5. 实验数量与充分性

论文的实验非常充分且设计严谨：
*   **数量众多**：在7+个数据集（包括自建的COCO*）上进行了评估，对比了10+种现有方法，并测试了多种训练设置。大量的定性结果（可视化）也印证了定量数据。
*   **客观公平**：
    *   针对COCO*数据集，论文详尽对比了三大类方法及其多种变体设置，提供了全面的指标（不同IoU阈值下的AP/AR）。
    *   **消融实验**深入分析了三个表征各自的重要性，证明边界距离场贡献最大，三者结合最优。
    *   对多目标推理模块中的关键超参数（如阈值）进行了敏感性分析，证明方法对参数不特别敏感，稳定性好。
    *   对训练数据增强（随机裁剪）和不同来源的粗糙掩膜质量都做了消融，进一步验证了组件设计的必要性。

### 6. 论文的主要结论与发现

1.  **性能显著超越SOTA**：unMORE在COCO\*验证集上，无论是直接发现（**unMORE_disc**）还是训练检测器后（**unMORE**），各项指标均大幅超越所有现有无监督方法，实现了新的最优结果。
2.  **在拥挤场景中表现突出**：当图像中物体数量增多时（≥5个），unMORE的优势更加明显，而基线方法（如VoteCut, CuVLER）的性能则急剧下降。这表明该方法特别擅长处理**多物体粘连和重叠**的难题。
3.  **强零样本泛化能力**：在COCO20K、LVIS、KITTI、VOC等6个未见过的数据集上，unMORE几乎在所有指标上均取得最高分，证明了其强大的泛化能力。
4.  **核心价值在于显式表征**：通过显式学习物体中心、边界等结构信息，一劳永逸地解决了“什么是物体”的问题，使得后续的推理过程（多目标发现）变得简单、高效且无需额外训练。

### 7. 优点：方法或实验设计上的亮点

*   **方法论创新性强**：提出了一个优雅、简洁且极度有效的“学习-推理”两阶段范式。用预定义的显式表征（存在性、中心场、边界场）替代了黑盒式的隐式表征学习，使得整个过程高度可解释、可控制。
*   **模块化设计，推理无网络**：多目标推理模块完全基于规则（卷积、分裂、迭代更新），不依赖任何可学习的参数。这种设计不仅避免了训练中的过拟合风险，也使推理过程极其灵活直观。
*   **对技术难点的解决思路清晰**：
    *   用**中心场反卷积核**巧妙解决了**欠分割**问题。
    *   用**边界距离场梯度**优雅地解决了边界框**微调**（过/欠拟合）问题。
*   **实验设计严谨细致**：主动发现并解决数据集标注不完整的问题（创建COCO\*），并对大量参数和设置做了详尽的消融研究，结论可信度高。
*   **自包含性强**：从伪标签生成、物体性网络训练到多目标推理和最终检测器训练，整个流程构成了一个不需要任何人工标注的完整闭环。

### 8. 不足与局限

*   **计算效率瓶颈**：**第一阶段的直接发现推理（unMORE_disc）速度较慢**。因为需要处理大量初始候选框并进行迭代式中心分裂和边界微调，推理时间远大于基于简单特征相似度的方法，不适合实时处理。虽然训练检测器（unMORE）后速度恢复正常，但前期伪标签生成的开销较大。
*   **无法区分高度交叠的相似物体**：文中承认在失败案例分析中指出，对于纹理过于相似且严重重叠的物体，该方法依然难以正确分离。这表明纯粹基于视觉几何线索的方法有其局限。
*   **依赖第一阶段粗糙掩膜质量**：物体性网络的训练依赖于最初由VoteCut生成的ImageNet粗糙掩膜。虽然消融实验表明方法对这些掩膜质量具有鲁棒性，但更好的初始化方法理论上能进一步提升性能上限。
*   **跨域泛化能力未验证**：论文主要测试了自然场景图像。文中明确提到，对于存在**显著领域差异**的数据（如医学图像），从自然图像中习得的物体先验可能不适用，这是一个应用限制。
*   **多个超参数依赖人工设定**：推理过程中的几个关键阈值（$\tau_e$, $\tau_c$, $\tau_{adjust}$）需要人工设置。虽然敏感性分析表明方法对参数不敏感，但这依然引入了额外的手工调参环节。

（完）
