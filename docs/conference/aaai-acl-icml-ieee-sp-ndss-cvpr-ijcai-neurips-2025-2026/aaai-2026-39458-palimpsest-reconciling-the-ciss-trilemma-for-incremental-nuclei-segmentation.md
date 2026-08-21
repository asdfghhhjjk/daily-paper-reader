---
title: "Palimpsest: Reconciling the CISS Trilemma for Incremental Nuclei Segmentation"
title_zh: Palimpsest：调和增量式细胞核分割中的CISS三难困境
authors: "Jiajia Li, Huisi Wu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39458/43419"
tags: ["query:cell-path"]
score: 8.0
evidence: "提出组织病理学中增量式细胞核分割方法，直接支撑H&E全切片图像的细胞核分割"
tldr: "Palimpsest针对组织病理学中类别增量式细胞核分割面临的三难问题，即稳定性、可塑性和模型大小限制。该方法在无样本约束下，通过参数保守合成和相似度感知质心重校准等机制解耦冲突需求。实验表明其能在学习新类别细胞核的同时保持旧类别性能，且模型规模不变。该工作为H&E全切片图像中细胞核分割的持续学习提供了关键支持。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 847, \"height\": 470}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1807, \"height\": 716}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 540}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1840, \"height\": 806}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 858, \"height\": 465}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 850, \"height\": 570}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 883, \"height\": 478}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39458/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 868, \"height\": 570}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 475}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1838, \"height\": 565}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 898, \"height\": 285}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 280}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39458/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 886, \"height\": 331}]"
motivation: 临床诊断需要模型持续学习新类别细胞核，但现有方法在稳定性、可塑性和存储方面存在冲突。
method: 提出参数保守合成模块、相似度感知质心重校准和双区域正则化等机制。
result: 在无样本增量场景下有效缓解遗忘，实现新类核的准确分割。
conclusion: 为组织病理学细胞核分割的类增量学习提供了新框架，促进下游细胞分析。
---

## Abstract
Adapting computational pathology models to evolving clinical diagnostics via Class-Incremental Semantic Segmentation (CISS) is critical. However, this task imposes a unique CISS Trilemma: a simultaneous failure to preserve the intricate tissue background (stability), distinguish morphologically similar new nuclei (plasticity), and maintain a constant model size (scalability), all under a strict exemplar-free constraint. To resolve this, we introduce Palimpsest, a novel framework that systematically decouples these conflicting demands. Palimpsest integrates three synergistic mechanisms: a Parameter-Conserving Synthesis (PCS) module merges lightweight adapters to ensure scalability; a novel Similarity-Aware Centroid Recalibration (SCR) module executes differentiated recalibration to counteract non-uniform foreground drift, securing plasticity; and an Adaptive Residual Shading (ARS) module performs logit-space decoupling to preserve background integrity, ensuring stability. Extensive experiments on two histopathology datasets demonstrate that Palimpsest significantly outperforms state-of-the-art methods, achieving a superior stability-plasticity balance, particularly in challenging long-term incremental scenarios.

---

## 论文详细总结（自动生成）

# Palimpsest 论文总结

## 1. 核心问题与整体含义

- **研究背景**：计算病理学中，细胞核分割是癌症诊断、分级和预后评估的重要基础任务。临床实践中新型病理实体不断出现，传统深度模型难以持续适应，因此需要引入类别增量式语义分割（Class-Incremental Semantic Segmentation, CISS）。
- **核心问题**：论文提出并形式化了组织病理学场景下的 **CISS 三难困境（CISS Trilemma）**：
  - **稳定性（Stability）**：必须同时保留旧前景类别和复杂的组织背景结构；
  - **可塑性（Plasticity）**：必须区分形态高度相似的新细胞核类别；
  - **可扩展性（Scalability）**：模型规模必须保持恒定，满足临床资源受限环境；
  - 同时受严格 **无旧样本约束（exemplar-free）** 限制，不能回放患者历史数据。
- **现有方法局限**：
  - 知识蒸馏类方法以整体正则化保留旧知识，但会抑制对新类别的细粒度学习能力；
  - 架构扩展类方法能隔离参数保证稳定性，但参数量随任务数线性增长，不利于临床部署；
  - 现有无样本重校准方法多采用均匀漂移补偿，忽视了形态相似类别间非均匀的特征漂移。

## 2. 方法论

Palimpsest 将增量学习过程解耦为两个阶段：**Intra-Task Adaptation（任务内适应）** 和 **Inter-Task Consolidation（任务间整合）**，每个阶段用专门机制解决三难中的不同方面。

### 2.1 Intra-Task Adaptation：平衡可塑性与背景稳定性

- 冻结主特征提取器 Φ，注入轻量级任务特定适配器 \(A_t\) 学习新类特征。
- **可塑性**：通过瓶颈结构的 adapter 得到新特征表示，仅对新类别像素计算交叉熵损失 \(L_{new}\)。
- **背景稳定性**：引入 **Adaptive Residual Shading (ARS)** 模块 \(B_t\)，在 logit 空间学习负残差，将新类别从背景中“雕刻”出来，而不直接修改共享特征空间：
  \[
  \mu_{b,t}(x) = \mu_{b,0}(\Phi(x)) + \sum_{j=1}^{t} B_j(\Phi(x))
  \]
  训练时使用 margin-based 损失 \(L_{ARS}\)，使 \(B_t\) 仅在新类别像素上产生强负信号，避免破坏稳定背景表示。
- **前景稳定性**：引入 **Foreground Feature Consistency (FFC)** 损失 \(L_{FFC}\)，利用旧模型生成的伪标签选择旧类像素，最小化当前与旧特征表示之间的 L2 距离，防止新 adapter 对旧前景特征产生扰动。
- 总损失：
  \[
  L_{total} = L_{new} + \lambda_{ARS} L_{ARS} + \lambda_{FFC} L_{FFC}
  \]

### 2.2 Inter-Task Consolidation：可扩展性与长期稳定性

- **Parameter-Conserving Synthesis (PCS)**：
  - 将新训练 adapter \(A_t\) 与上一阶段统一 adapter \(\bar{A}_{t-1}\) 进行加权融合：
    \[
    \bar{\theta}_t = (1-\alpha_t)\bar{\theta}_{t-1} + \alpha_t \theta_t,\quad \alpha_t = 1/t
    \]
  - 实现恒定的 \(O(1)\) 模型参数规模，但融合会引入非均匀特征漂移。
- **Similarity-Aware Centroid Recalibration (SCR)**：
  - 在无旧样本条件下，对特征漂移进行差异化校正，分三步：
    1. **漂移估计**：利用当前任务验证数据，计算新类原型在合并前后的平均位移向量 \(\Delta_t\)；
    2. **影响调制**：基于旧类原型与新类原型之间的余弦相似度，为每个旧类 \(c'\) 计算调制因子 \(s_{c'}\)；
    3. **差异化重校准**：更新旧类原型：
       \[
       P'_{c'} = P_{c'} + s_{c'} \cdot \Delta_t
       \]
  - 校正后的原型直接作为旧类的分类器权重，无需重训练，从而恢复前景稳定性。

## 3. 实验设计

- **数据集**：
  - **MoNuSAC**：包含多种器官的 4 种细胞类型（上皮细胞、淋巴细胞、巨噬细胞、中性粒细胞），用于测试多类别灾难性遗忘；
  - **CoNSeP**：结直肠癌组织切片，细胞核形态相似、密集排列，用于测试细粒度区分能力；原始类别合并为 3 类（上皮、梭形、其他）。
- **增量协议**：
  - 采用 **overlapped setting**，模拟临床非穷尽标注：新任务训练数据中只显式标注新类，旧类被归为背景；
  - 设置如 MoNuSAC 的 1-1、2-1、2-2、3-1，CoNSeP 的 1-1、2-1 等场景。
- **对比方法**：
  - Finetune、LwF、MiB、PLOP、EWF、BalConpas、InSeg，以及联合训练上界 Joint。
- **评价指标**：
  - Old Dice、New Dice、Mean Dice（%），取 3 个随机种子平均。

## 4. 资源与算力

- 文中提到实验使用 **PyTorch** 框架，在 **NVIDIA 2080Ti GPU** 上运行；
- **未明确说明** GPU 数量、具体训练时长、单卡/多卡配置或总计算开销。

## 5. 实验数量与充分性

- **实验数量较丰富**：
  - 两个公开病理数据集 × 多个增量协议；
  - 与 7 个主流方法及联合训练上界进行对比（表 1、表 2）；
  - 核心组件消融（表 3）；
  - 损失组件消融（表 4）；
  - 不同重校准策略对比（表 5）；
  - 还包含 t-SNE 特征可视化、激活图对比、融合系数 \(\alpha\) 分析、定性分割结果等。
- **充分性与客观性**：
  - 实验覆盖多数据集、多协议、多粒度消融，对比方法覆盖主流 SOTA，且使用随机种子取平均，整体较为客观；
  - 但缺少统计显著性检验，部分结果差异较小，随机波动风险未被量化；
  - 仅在两个 H&E 病理数据集上验证，场景覆盖有限。

## 6. 主要结论与发现

- Palimpsest 通过机制解耦，系统性地解决了 CISS 三难：
  - **PCS** 保证常数模型规模；
  - **ARS** 在 logit 空间保护背景完整性；
  - **SCR** 对不同类别进行差异化漂移校正，提升旧类别稳定性。
- 在 MoNuSAC 和 CoNSeP 上均显著优于现有方法，尤其在长期增量场景下稳定性-可塑性平衡更优。
- 消融实验证明三个组件具有协同作用，单独使用 PCS 会导致严重特征漂移，加入 ARS 和 SCR 后才能恢复性能。
- SCR 的相似度感知差异化重校准明显优于无校准、随机校准和均匀校准策略。

## 7. 优点

- **问题定义清晰**：首次将组织病理学 CISS 中的稳定性、可塑性、可扩展性冲突形式化为三难问题，动机直观且贴合临床需求。
- **方法设计针对性强**：三个模块各司其职，PCS 解决规模问题，ARS 解决背景稳定性，SCR 解决合并引起的非均匀前景漂移。
- **符合实际约束**：全程无旧样本回放，满足患者隐私要求；推断时保持 \(O(1)\) 复杂度，利于临床部署。
- **实验设置贴近现实**：overlapped 协议模拟非穷尽标注临床工作流，增加了任务难度和可信度。
- **可复现性较好**：提供代码仓库，并与多个主流方法进行公平对比。

## 8. 不足与局限

- **SCR 的简化假设**：
  - 用单一全局漂移向量近似所有类别的漂移，当多个新类影响差异较大时可能不够精确；
  - 余弦相似度到漂移幅度的线性映射未必能捕获非线性类间动态；作者在论文中也承认这一点。
- **实验覆盖有限**：
  - 仅在两个 H&E 染色病理数据集上验证，缺乏对其他染色、器官、模态（如免疫组化、多重荧光）的泛化证据；
  - 增量类别数较少（2–4 类），未测试大规模类别增量场景。
- **统计严谨性不足**：
  - 未报告方差、置信区间或显著性检验，部分性能提升幅度较小；
  - 未系统分析超参数（\(\lambda_{ARS}\)、margin、adapter 瓶颈维度等）的敏感性。
- **部署相关成本未讨论**：
  - 未报告训练时间、显存占用、推断延迟等实际资源开销；
  - PCS 的融合权重 \(\alpha_t\) 固定为 \(1/t\)，缺乏自适应机制。

（完）
