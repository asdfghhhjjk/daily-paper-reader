---
title: "Palimpsest: Reconciling the CISS Trilemma for Incremental Nuclei Segmentation"
title_zh: Palimpsest：调和增量式细胞核分割的CISS三难困境
authors: "Jiajia Li, Huisi Wu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39458/43419"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 计算病理中的细胞核分割直接对应HE切片细胞分割要求
tldr: 为适应病理诊断中不断出现的新细胞核类别，本文提出Palimpsest框架，通过参数保留合成、相似度感知质心重校准和背景感知知识蒸馏，在无样本约束下化解增量学习的稳定性、可塑性和可扩展性冲突。实验证明该方法在多个细胞核分割数据集上有效平衡三方需求，为持续学习的病理模型提供了可行方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 847, \"height\": 470}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1807, \"height\": 716}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 540}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1840, \"height\": 806}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 858, \"height\": 465}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 850, \"height\": 570}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 883, \"height\": 478}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 868, \"height\": 570}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 475}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1838, \"height\": 565}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 898, \"height\": 285}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 280}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 886, \"height\": 331}]"
motivation: 计算病理模型需适应新细胞核类别，但增量分割面临稳定性、可塑性和可扩展性三难困境。
method: 提出Palimpsest框架，通过参数保留合成、相似度感知质心重校准和背景感知背景蒸馏解耦冲突。
result: 在增量细胞核分割任务上平衡了三方面需求，实现了高效无样本学习。
conclusion: Palimpsest系统性地解决了CISS三难困境，推动了病理模型持续适应新临床需求。
---

## Abstract
Adapting computational pathology models to evolving clinical diagnostics via Class-Incremental Semantic Segmentation (CISS) is critical. However, this task imposes a unique CISS Trilemma: a simultaneous failure to preserve the intricate tissue background (stability), distinguish morphologically similar new nuclei (plasticity), and maintain a constant model size (scalability), all under a strict exemplar-free constraint. To resolve this, we introduce Palimpsest, a novel framework that systematically decouples these conflicting demands. Palimpsest integrates three synergistic mechanisms: a Parameter-Conserving Synthesis (PCS) module merges lightweight adapters to ensure scalability; a novel Similarity-Aware Centroid Recalibration (SCR) module executes differentiated recalibration to counteract non-uniform foreground drift, securing plasticity; and an Adaptive Residual Shading (ARS) module performs logit-space decoupling to preserve background integrity, ensuring stability. Extensive experiments on two histopathology datasets demonstrate that Palimpsest significantly outperforms state-of-the-art methods, achieving a superior stability-plasticity balance, particularly in challenging long-term incremental scenarios.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：计算病理学中，细胞核分割模型需要持续适应新出现的病理类别，但直接采用类增量语义分割（Class‑Incremental Semantic Segmentation, CISS）会陷入 **CISS 三难困境**：
  - **稳定性**：需要精确保留复杂的组织背景以及旧类别知识；
  - **可塑性**：必须有效学习形态高度相似的新细胞核类别；
  - **可扩展性**：模型参数量和计算开销须保持恒定，以适应资源受限的临床部署。
- **额外约束**：受医疗隐私法规限制，禁止保存或回放任何历史患者数据（严格无样本约束）。
- **研究动机**：现有的知识蒸馏、架构扩展、无样本重校准等方法均无法同时解决上述三个冲突目标，因此需要一个解耦式框架，系统性地调和稳定性、可塑性和可扩展性之间的矛盾。

## 2. 论文提出的方法论
- **整体思路**：将每个增量任务的学习过程拆分为两个阶段——**任务内适应**与**任务间整合**，并引入三个协同模块分别应对不同需求。
- **任务内适应（Intra‑Task Adaptation）**
  - 冻结预训练特征提取器 Φ，注入轻量的 **任务专用适配器 `A_t`**（瓶颈结构，压缩比 r=16）来学习新类特征。
  - **自适应残差阴影模块（ARS）`B_t`**：直接在 logit 空间学习负向残差，以“划出”新类别区域，避免扰动背景表达。最终背景 logit 为固定基值加上所有历史残差之和，并采用 margin‑based 损失 `L_ARS` 约束。
  - **前景特征一致性损失 `L_FFC`**：利用上一模型对旧类像素生成伪标签，约束当前适配器输出与冻结统一适配器输出之间的 L2 距离，保护旧前景知识。
- **任务间整合（Inter‑Task Consolidation）**
  - **参数保留合成（PCS）**：将新训练好的适配器 `A_t` 按加权平均（权重 `α_t=1/t`）合并到统一的适配器 `Ā_t` 中，保证整个模型参数量恒定（O(1) 复杂度）。
  - **相似度感知质心重校准（SCR）**：
    1. 在当前任务验证集上，计算新旧原型差异的均值，得到一个全局漂移向量 `Δ_t`。
    2. 基于旧类别原型与新类别原型的余弦相似度，为每个旧类别计算影响因子 `s_{c'}`。
    3. 对每个旧类别原型进行区分性更新：`P'_{c'} = P_{c'} + s_{c'}·Δ_t`，并直接将其作为分类器权重，实现无样本重校准。

## 3. 实验设计
- **数据集**：
  - **MoNuSAC**：4 种多器官细胞核类型（上皮、淋巴细胞、巨噬细胞、中性粒细胞），用于评估多类别灾难性遗忘。
  - **CoNSeP**：结直肠癌密集且形态相似的细胞核，原始 7 类合并为 3 类（上皮、梭形、其他），检验细粒度区分能力。
- **增量协议**：采用临床现实中常见的“重叠标注”设置（训练数据中未标注的旧类被归为背景），设计多种 `N_old–N_new` 场景（如 3‑1、2‑1、2‑2 等）。
- **基线方法**：包括朴素微调、LwF、MiB、PLOP、EWF、BalConpas、InSeg 等主流 CISS 方法，以及联合训练上界（Joint）。
- **评估指标**：旧类 Dice（稳定性）、新类 Dice（可塑性）、所有已见类的平均 Dice（综合性能），均取三次随机种子平均。

## 4. 资源与算力
- **硬件**：使用 NVIDIA 2080Ti GPU 进行实验，文中未明确提及 GPU 数量，推测为单卡。
- **训练设置**：每个增量步骤训练 100 epochs，batch size 为 12，采用 SGD 优化器与余弦退火学习率调度，基于 ImageNet 预训练的 ResNet‑101 骨干网络。
- **时长**：论文未给出具体的总训练时长或每个任务耗时，但参照常见配置可认为计算量适中。

## 5. 实验数量与充分性
- **主要对比实验**：在 MoNuSAC 的 4 种增量场景（1‑1, 2‑1, 2‑2, 3‑1）和 CoNSeP 的 2 种场景（1‑1, 2‑1）中对比 7 种基线方法及上限，表格均报告 Dice 数值。
- **消融实验**：以 MoNuSAC 2‑1 为基准，逐步验证 PCS、ARS、SCR 组合效应；拆解三种损失函数的必要性；比较不同的重校准策略（无校准、随机、均匀、重放、SCR），共形成至少 5 组消融表。
- **定性分析**：提供分割结果可视化、t‑SNE 特征分布、激活图对比，以及对融合系数 α 的超参数分析。
- **公平性**：所有方法采用相同的骨干网络、评估协议和随机种子，具备可比性；但由于仅在两个特定病理数据集上验证，对更广泛临床场景的泛化性证据有限，不过实验设计在给定设定内已较为充分。

## 6. 论文的主要结论与发现
- Palimpsest 通过解耦设计成功调和了稳定性、可塑性和可扩展性冲突，在无样本约束下显著优于现有 CISS 方法。
- ARS 通过 logit 空间残差叠加有效保护复杂背景；PCS 实现恒定模型规模的同时引起特征漂移；SCR 利用相似度加权的漂移补偿精准恢复了旧类知识。
- 框架在长序列增量场景下仍能维持高平衡性能，显示出面向真实临床流式学习的潜力。

## 7. 优点
- **解耦式设计**：将三难困境中的每一方面指派给专门模块，思路清晰且因果明确。
- **病理特化机制**：ARS 利用 logit 空间的负残差避免破坏丰富的组织背景；SCR 针对病理中形态相似性导致的非均匀漂移进行区分性矫正，而非简单均匀修正。
- **完全无样本且模型大小恒定**：严格遵守隐私与部署约束，实用性高。
- **实验系统全面**：多场景、多基线、细粒度消融与可视化相结合，有力支撑每个设计选择。

## 8. 不足与局限
- **SCR 假设简化**：采用单一全局漂移向量，并假设特征相似度与漂移影响呈线性关系，无法捕获类间复杂的非线性交互，可能在大量新类别或极度异构的场景下失效。
- **数据集与类别规模有限**：仅在两个数据集上测试，类别数较少（3–4 类），未在包含数十种细胞类型的更大规模病理影像库中评估，泛化性有待进一步验证。
- **骨干网络单一**：所有实验基于 ResNet‑101，未展示在其他架构（如 Vision Transformer）上的适配能力。
- **缺少效率量化分析**：未详细报告训练/推理时间、显存占用与串行开销，难以直接评判临床部署的实时性。
- **可能存在的偏差风险**：伪标签生成、漂移估计均依赖前一模型的质量，在长序列中误差可能累积，但本文未对此进行深入讨论。

（完）
