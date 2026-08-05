---
title: "Palimpsest: Reconciling the CISS Trilemma for Incremental Nuclei Segmentation"
title_zh: 调和CISS三难困境的增量式细胞核分割框架Palimpsest
authors: "Jiajia Li, Huisi Wu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39458/43419"
tags: ["query:tme-evidence"]
score: 9.0
evidence: 增量式细胞核分割直接解决组织病理图像中的细胞分类与分割
tldr: 针对计算病理中类别增量语义分割面临的稳定性、可塑性和可拓展性三重困境，提出Palimpsest框架，通过参数保持合成、相似性感知质心重校准等机制解耦冲突，实现对组织病理图像中细胞核的持续、准确分割与分类。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 847, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1807, \"height\": 716, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1840, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 858, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 850, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 883, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 868, \"height\": 570, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 475, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1838, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 898, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 886, \"height\": 331, \"label\": \"Table\"}]"
motivation: 计算病理模型需适应不断演进的临床诊断，但类别增量语义分割存在稳定性、可塑性和可拓展性无法兼顾的困境。
method: 提出Palimpsest，集成参数保持合成模块、相似性感知质心重校准模块和伪特征重放模块，分别解决可拓展性、稳定性和可塑性问题。
result: 在多个细胞核分割数据集上的增量实验表明，Palimpsest有效平衡了三难困境，优于现有方法。
conclusion: 为计算病理中的细胞核持续分割提供了新框架，助力临床诊断模型的渐进式更新。
---

## Abstract
Adapting computational pathology models to evolving clinical diagnostics via Class-Incremental Semantic Segmentation (CISS) is critical. However, this task imposes a unique CISS Trilemma: a simultaneous failure to preserve the intricate tissue background (stability), distinguish morphologically similar new nuclei (plasticity), and maintain a constant model size (scalability), all under a strict exemplar-free constraint. To resolve this, we introduce Palimpsest, a novel framework that systematically decouples these conflicting demands. Palimpsest integrates three synergistic mechanisms: a Parameter-Conserving Synthesis (PCS) module merges lightweight adapters to ensure scalability; a novel Similarity-Aware Centroid Recalibration (SCR) module executes differentiated recalibration to counteract non-uniform foreground drift, securing plasticity; and an Adaptive Residual Shading (ARS) module performs logit-space decoupling to preserve background integrity, ensuring stability. Extensive experiments on two histopathology datasets demonstrate that Palimpsest significantly outperforms state-of-the-art methods, achieving a superior stability-plasticity balance, particularly in challenging long-term incremental scenarios.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在计算病理学中，通过**类别增量语义分割（Class-Incremental Semantic Segmentation, CISS）** 持续学习新出现的细胞核类型至关重要。然而，该任务面临一个独特的**CISS三难困境**：
  - **稳定性（Stability）**：模型必须保留对既往类别及复杂组织背景的分割能力，防止灾难性遗忘。
  - **可塑性（Plasticity）**：模型需有效学习形态高度相似的新细胞核类别。
  - **可扩展性（Scalability）**：模型参数量需保持恒定，以适应临床部署的资源限制。
  - 上述三者必须在严格的**无样本重放（exemplar‑free）约束**下同时满足，即出于患者隐私保护，禁止复用任何历史数据。
- **整体含义**：现有的蒸馏、架构扩展等方法均无法同时解决这三个冲突目标。论文提出 Palimpsest 框架，通过机制解耦，系统性地调和该三难困境，实现病理细胞核分割的可持续、轻量级增量学习。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将增量学习过程解耦为两个阶段，并分配专用模块分别应对可塑性、稳定性和可扩展性。
  - **阶段1：任务内适应（Intra‑Task Adaptation）** —— 解决可塑性与背景稳定性。
  - **阶段2：任务间整合（Inter‑Task Consolidation）** —— 解决可扩展性与前景稳定性。

- **关键技术细节**：
  - **参数高效适配器（PEFT Adapters）**：在冻结的主干网络上插入轻量级瓶颈适配器 \(A_t\)，仅训练少量参数以区分新类别，保证可塑性。适配器输出 \( z' = z + \sigma(z W_{\text{down}}) W_{\text{up}} \)。
  - **自适应残差遮罩（ARS）**：在 logit 空间学习负残差 \(B_t\)，从背景 logit 中“抠出”新类别区域，保持背景表征不被污染。背景 logit 定义为 \( \mu_{b,t}(x) = \mu_{b,0}(\Phi(x)) + \sum_{j=1}^{t} B_j(\Phi(x)) \)。使用基于边界的损失 \( \mathcal{L}_{\text{ARS}} \) 强制新类别像素产生强烈负信号，其他位置信号接近零。
  - **前景特征一致性（Foreground Feature Consistency, FFC）**：通过 \( \mathcal{L}_{\text{FFC}} \) 约束当前适配器与上一阶段合并适配器在旧类别像素上的 L2 特征距离，保护旧前景知识。
  - **参数保持合成（PCS）**：将新适配器权重以指数衰减系数 \( \alpha_t = 1/t \) 融合到统一适配器中：\( \bar{\theta}_t = (1-\alpha_t)\bar{\theta}_{t-1} + \alpha_t \theta_t \)，保持模型大小 \(O(1)\)。
  - **相似性感知质心重校准（SCR）**：针对 PCS 引起的特征漂移，利用当前任务数据估计全局漂移向量 \( \Delta_t \)，再根据新旧类别质心的余弦相似度计算调制因子 \( s_{c'} \)，对旧类别原型进行差异化校正 \( P'_{c'} = P_{c'} + s_{c'} \cdot \Delta_t \)。校正后的原型直接作为旧类别的分类器权重，全程无需历史数据。

- **训练损失**：  
  任务内适应阶段总损失为  
  \[
  \mathcal{L}_{\text{total}} = \mathcal{L}_{\text{new}} + \lambda_{\text{ARS}} \mathcal{L}_{\text{ARS}} + \lambda_{\text{FFC}} \mathcal{L}_{\text{FFC}}
  \]  
  其中 \(\mathcal{L}_{\text{new}}\) 为新类别像素交叉熵损失，\(\lambda_{\text{ARS}}\) 和 \(\lambda_{\text{FFC}}\) 为平衡超参数。

### 3. 实验设计：数据集、场景、对比方法

- **数据集**：
  - **MoNuSAC**：包含四种细胞核类型（上皮、淋巴、巨噬、中性粒细胞），多器官来源，用于测试多类别遗忘。
  - **CoNSeP**：结直肠癌组织中的形态相似、密集细胞核，原类别合并为三类（上皮、梭形、其他），突出细粒度区分挑战。
- **增量协议**：
  - 采用**重叠（overlapped）设定**，训练时新任务中未标注的旧类别被视为背景，贴近临床实际。
  - 任务划分记为“\(N_{\text{old}}\text{-}N_{\text{new}}\)”，如 1‑1（4步）、2‑1（3步）、3‑1（2步）等多种变体，重点测试长序列与一步新增多类的场景。
- **评价指标**：
  - 旧类别 Dice（Old）衡量稳定性，新类别 Dice（New）衡量可塑性，所有类别的平均 Dice（Mean）衡量综合性能。
- **对比方法**：
  - 微调（Finetune）、LwF、MiB、PLOP、EWF、BalConpas、InSeg，以及联合训练（Joint）作为理论上限。这些方法覆盖了知识蒸馏、重放、背景建模等 CISS 主流范式。

### 4. 资源与算力

- **硬件配置**：所有实验在 **NVIDIA 2080Ti GPU** 上完成。
- **训练细节**：每步增量训练为 100 轮，批量大小 12，采用 SGD 优化器与余弦退火学习率调度。
- **未明确提及**：论文未给出单次实验的 GPU 显存占用、具体训练耗时或 GPU 使用数量，仅提供了硬件型号和基本训练参数。

### 5. 实验数量与充分性

- **实验组数**：
  - **主对比实验**：在 MoNuSAC 上测试了 4 种增量协议（1‑1、2‑1、2‑2、3‑1），在 CoNSeP 上测试了 2 种（2‑1、1‑1），共 6 组对比，每组均与 7～8 个现有方法比较。
  - **消融研究**：在 MoNuSAC 2‑1 设定下，逐项移除 PCS、ARS、SCR 模块，分析其独立性；进一步消融了各损失项、合并系数 \(\alpha\)、重校准策略（无校准、随机、均匀、朴素重放、SCR）。
  - **可视化分析**：提供了分割结果定性对比、消融组图、t‑SNE 特征分布、激活图对比等。
- **公平性与充分性**：
  - 所有对比方法均使用相同的骨干网络（ResNet‑101）和相同的无样本重放约束，结果取 3 次随机种子平均，评估标准一致。
  - 消融实验设计系统，从模块级到损失函数级，验证了各组件贡献和设计选择的优劣，实验较为充分、客观。

### 6. 论文的主要结论与发现

- Palimpsest 在所有增量场景、两个数据集上均取得最优平均 Dice，尤其在长序列（4步 1‑1）和一次新增多类的困难设定下优势更明显（如 MoNuSAC 1‑1 协议 Mean Dice 达到 71.28%，相较最佳竞争对手提升约 2%）。
- 三组件的协同是核心：仅添加 PCS 会导致严重遗忘，加上 ARS 恢复背景稳定性，SCR 进一步大幅提升旧类别性能。
- 损失函数设计中，基于边界的 ARS 损失远优于标准 BCE 损失；前景特征一致性损失对稳定旧类别至关重要。
- 重校准策略方面，与均匀漂移校正相比，相似性感知的差异化校正显著更优，验证了细胞核形态相似性导致漂移是非均匀的。
- 框架整体在无样本回放的严格约束下，成功实现了稳定‑可塑‑恒参的平衡，且推理时维持 O(1) 复杂度。

### 7. 优点：方法或实验设计上的亮点

- **问题建模新颖**：首次将计算病理 CISS 抽象为三难困境，并针对性解耦，而非沿用单一策略的折衷。
- **机制高度解耦且专用**：ARS 在 logit 空间保护背景，SCR 在原型空间校正前景漂移，PCS 在参数空间控制规模，三个模块各司其职、互不干扰。
- **严格贴合临床需求**：全程无历史数据复用（exemplar‑free），模型规模恒定，推理复杂度不随任务数增长，真实满足医疗隐私与部署限制。
- **相似性感知重校准**：SCR 根据新旧类别相似度定制化校准，弥补了普遍假设均匀漂移的缺陷，对形态类似细胞核的增量学习尤为有效。
- **实验设计扎实**：覆盖多个数据集、多种增量协议，与多种 SOTA 方法公平对比，消融实验层层递进，可视化证据丰富，验证充分。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **漂移建模简化**：SCR 使用单一全局漂移向量 \(\Delta_t\)，当一次性增加多个不同性质的新类别时，可能无法精确表征各类别的独立漂移；相似度与漂移幅度之间的线性映射也可能不足以捕捉真实非线性关系。
- **数据集与类别多样性有限**：仅在两个公开数据集的少量细胞核类别上验证，且在 CoNSeP 上将原始类别合并为 3 类，简化了任务难度。未在大规模、更多样化的病理图谱或不同染色协议下测试。
- **超参数敏感性与普适性**：ARS 的边距 \(m\)、损失权重 \(\lambda_{\text{ARS}}\) 等需人工设定，未系统分析其对不同数据集和增量步长的鲁棒性；适配器瓶颈维度 \(r\) 的选取也缺乏讨论。
- **未与部分前沿方法对比**：未纳入某些基于动态架构或提示微调的最新 CISS 方法（如 CODA‑Prompt、DualPrompt 等），对比覆盖度可进一步扩展。
- **临床部署的具体开销未阐明**：虽然推理时模型大小恒定，但新增任务的训练成本（时间、计算量）及 SCR 所需当前任务验证集的计算开销未详细报告，不利于评估真实场景下的效率。
- **任务顺序影响未知**：未分析不同类别增量顺序对最终性能的影响，无法排除实验结论对任务划分顺序的敏感性。

（完）
