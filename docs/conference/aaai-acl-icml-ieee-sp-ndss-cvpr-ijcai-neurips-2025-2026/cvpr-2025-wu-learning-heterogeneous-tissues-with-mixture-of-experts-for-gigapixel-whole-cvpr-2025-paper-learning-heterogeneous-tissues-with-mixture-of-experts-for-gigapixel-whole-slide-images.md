---
title: Learning Heterogeneous Tissues with Mixture of Experts for Gigapixel Whole Slide Images
title_zh: 用专家混合模型学习千兆像素全切片图像中的异质组织
authors: "Wu, Junxian, Chen, Minheng, Ke, Xinyi, Xun, Tianwang, Jiang, Xiaoming, Zhou, Hongyu, Shao, Lizhi, Kong, Youyong"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wu_Learning_Heterogeneous_Tissues_with_Mixture_of_Experts_for_Gigapixel_Whole_CVPR_2025_paper.pdf"
tags: ["query:cell-graph"]
score: 4.0
evidence: 专家混合模型学习WSI异质组织，非细胞级特征
tldr: 本文针对千兆像素全切片图像中组织异质性和领域知识缺失的问题，提出病理感知专家混合模块PAMoE。该模块可即插即用，通过将不同组织路由到对应专家来学习特定肿瘤内组织的特征。方法有望提升WSI分析的可扩展性，并能发现新的预后相关因素，但未直接使用细胞分割和分类结果。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 759}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 837, \"height\": 833}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1498, \"height\": 820}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1472, \"height\": 996}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 694, \"height\": 554}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1802, \"height\": 659}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1797, \"height\": 373}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1797, \"height\": 246}]"
motivation: 千兆像素WSI分析面临复杂组织环境和缺乏目标驱动领域知识的问题。
method: 提出即插即用的病理感知专家混合模块（PAMoE），训练专家成为特定肿瘤内组织的专家，并学习路由。
result: 摘要未完整，预期提高WSI分析的可扩展性和识别新预后因素的能力。
conclusion: PAMoE为WSI组织异质性建模提供了新方法，但未聚焦细胞级特征。
---

## Abstract
Analyzing gigapixel Whole Slide Images (WSIs) is challenging due to the complex pathological tissue environment and the absence of target-driven domain knowledge. Previous methods incorporated pathological priors to mitigate this issue but relied on additional inference steps and specialized workflows, restricting scalability and the model's capacity to identify novel outcome-related factors. To address these challenges, we propose a plug-and-play Pathology-Aware Mixture-of-Experts (PAMoE) module, which based on mixture of experts to learn pathology-related knowledge and extract useful information. We train the experts to become 'specialists' in specific intratumoral tissues by learning to route each tissue to its mapped expert. In addition, to reduce the impact of irrelevant content on the model, we introduce a new routing rule that discards patches in which none of the experts express interest, which helps the model better capture the relationships between relevant patches. Through a comprehensive evaluation of PAMoE on survival task, we demonstrate that 1) Our module enhances the performance of baseline models in most cases, and 2) The sparse expert processing across different tissues enhances the learning of patch representations by addressing tissue heterogeneity.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：千兆像素级全切片图像（WSI）是癌症病理诊断的金标准。弱监督多实例学习（MIL）常将 WSI 切分为大量 patch，用预训练编码器提取特征后再聚合成幻灯片级表示。
- **核心问题**：
  - WSI 中病理组织高度异质，存在肿瘤、间质、免疫浸润、坏死等多种组织类型，以及复杂的组织间相互作用。
  - 许多任务（如预后预测、分期、亚型分类）需要从全景角度整合瘤内异质性和组织间关系，而传统注意力聚合方法更偏向“大海捞针”式任务（如微转移检测）。
  - 已有工作通过病理先验（如聚类原型、异构图）改善这一点，但往往依赖额外推理步骤或专用工作流，限制了可扩展性和发现新预后因素的能力。
- **整体含义**：该论文希望在不依赖推理阶段额外先验的前提下，让模型端到端地学习并利用组织异质性，从而提升 WSI 分析性能，并增强可解释性。

## 2. 论文提出的方法论

- **核心思想**：提出即插即用的 **病理感知专家混合模块 PAMoE**（Pathology-Aware Mixture-of-Experts）。
  - 基于 MoE 结构，训练不同专家成为特定瘤内组织的“专家”。
  - 通过将不同组织 patch 路由到对应专家，实现对异质病理组织的感知和处理。
  - 引入专家选择路由（Expert Choice Routing），由专家主动选择感兴趣的 patch，未被任何专家选择的 patch 被丢弃，从而过滤无关内容。

- **关键技术细节**：
  - **专家选择路由**：
    - 传统 MoE 为每个 token 分配 top-k 专家；PAMoE 反过来让每个专家选择 top-k 个 patch。
    - 设输入 patch 特征 `X ∈ R^{n×d}`，路由网络为 MLP `g(·)`，输出分配概率 `S = g(X) ∈ R^{m×n}`。
    - 每个专家沿 patch 维度选择 top `k = n × c / m` 个 patch，其中 `c` 为容量因子，`m` 为专家数。
    - 对选择结果进行 softmax 归一化，未被选中的 patch 权重为 0，可被后处理移除。
    - 输出为各专家输出的加权和，保留被选中 patch 的特征。
  - **病理感知监督**：
    - 先利用 CONCH 预训练模型对随机采样的 10% patch 进行分类，选取肿瘤、间质、免疫浸润、坏死四类组织。
    - 对每类组织取特征平均，得到先验原型 `P = {p_ω}`。
    - 将 PAMoE 中的专家分为 **先验监督专家** 和 **自由专家**。
    - 对每个 patch 与原型计算余弦相似度，再 softmax 得到先验选择概率 `prob_ω`。
    - 对先验监督专家的路由概率 `s_ω` 与 `prob_ω` 计算交叉熵损失 `LPAMoE`，约束专家偏好与病理组织类型对齐。
    - 总损失：`L = L_task + α · LPAMoE`。
  - **与经典模型集成**：将 TransMIL、LongViT、PatchGCN 等模型中的全连接层替换为 PAMoE 层。

## 3. 实验设计

- **数据集**：
  - 在 5 个 TCGA 癌症数据集上进行生存预测实验：COAD、LGG、LUAD、PAAD、BRCA。
- **任务与评价指标**：
  - 主要任务是生存预测，损失函数采用 Cox 回归损失。
  - 评价指标为 C-index（一致性指数），报告均值 ± 标准差。
- **对比方法**：
  - 经典 MIL 方法：ABMIL、AttnMISL。
  - Transformer / 上下文方法：CaMIL、TransMIL、LongViT。
  - 图方法：PatchGCN。
  - 基于病理先验的 SOTA 方法：PANTHER（原型聚类）、HEAT（异构图 + Hover-net 分类先验）。
- **实验设置**：
  - 所有方法统一使用 UNI 作为 patch 特征编码器。
  - 采用相同的 5 折交叉验证划分。
  - AttnMISL 和 PANTHER 配置为 16 个原型。
  - PAMoE 默认设置：4 个先验监督专家、2 个自由专家、容量因子 `c=2.0`、`α=0.1`。

## 4. 资源与算力

- 论文中 **未明确给出具体 GPU 型号、数量、训练时长或显存消耗**。
- 仅在致谢中提到“由东南大学大数据计算中心支持”。
- 在限制部分提到“受硬件条件限制，未能在更大规模模型上探索 PAMoE”，说明实验中确实存在算力约束，但未披露具体配置。

## 5. 实验数量与充分性

- **实验规模**：
  - 主实验覆盖 5 个癌症数据集、8 个对比方法/变体。
  - 对 TransMIL、LongViT、PatchGCN 三种基线分别进行集成实验。
  - 消融实验包括：
    - 专家数量与先验/自由专家比例（表 2）。
    - MoE 架构必要性，对比 CSA 层（表 3）。
    - 先验损失超参数 `α` 的影响（图 5）。
  - 论文还提及在补充材料中进行更多消融：专家选择路由、跳跃连接和 class token 处理、原型获取替代方式、CONCH 作为编码器、容量因子、patch 丢弃比例、自由专家分析等。
- **充分性与客观性**：
  - 实验覆盖面较广，尤其消融实验较充分。
  - 统一使用 UNI 特征编码器和相同数据划分，具有一定公平性。
  - 但存在潜在的偏差风险：不同方法使用的病理先验来源不同（PAMoE 使用 CONCH 分类器、HEAT 使用 Hover-net、PANTHER 使用聚类中心），可能影响公平性。
  - 仅涉及生存预测任务，未在其他下游任务（如分型、分级）上验证。

## 6. 论文的主要结论与发现

- PAMoE 在多数情况下能提升 baseline 模型性能，尤其是基于 Transformer 的模型（TransMIL、LongViT）。
- 对 PatchGCN 的提升有限且不稳定，表明当实例交互局限于局部邻域时，PAMoE 的优势受限。
- 作者提出假设：PAMoE 的收益主要来自不同专家以不同方式映射 patch，扩展了潜空间，使模型能捕捉更多样的全局交互；这种交互需要 Transformer 全局自注意力支持。
- 可视化结果显示：
  - 先验监督专家的偏好与预期的组织类型一致（如肿瘤、坏死、间质、浸润）。
  - 自由专家表现出更分散的偏好，倾向于探索新模式。
- 消融表明：
  - 加入先验监督专家通常优于相同总数但无监督的 MoE。
  - 仅使用固定余弦相似度分配的 CSA 层不如可学习的 PAMoE 灵活。
  - 适度的 `α` 值能提升性能，证明先验损失有效。

## 7. 优点

- **即插即用**：PAMoE 无需专门工作流设计，可较方便地集成到多种经典 WSI 分析方法中。
- **端到端推理**：推理阶段不需要额外病理先验或分类器，减少了部署复杂度。
- **自然过滤噪声**：通过专家选择路由，未被任何专家选中的 patch 被丢弃，可降低无关背景和组织对模型的干扰。
- **可解释性较好**：专家选择偏好可以可视化，对应到具体病理组织类型，帮助理解模型行为。
- **实验较丰富**：多数据集、多基线、多消融，且统一了特征编码器和交叉验证划分。

## 8. 不足与局限

- **任务单一**：仅在生存预测任务上验证，未展示在分类、分级、亚型预测等任务上的表现。
- **数据集局限**：只使用 5 个 TCGA 数据集，缺乏外部独立队列验证，泛化性尚未充分证明。
- **先验依赖与公平性**：
  - PAMoE 在训练阶段依赖 CONCH 分类器获得组织先验，这会引入额外的领域知识。
  - 对比方法使用的先验来源不同，可能影响对比公平性。
- **对非 Transformer 结构提升有限**：
  - PatchGCN + PAMoE 结果不一致，说明该方法不一定适用于局部交互为主的模型。
- **算力披露不足**：
  - 未给出具体 GPU、显存、训练时间等信息，难以评估复现成本。
- **超参数敏感性**：
  - 容量因子 `c`、先验损失权重 `α`、专家数量等均需调节，且可能随数据集变化。
- **组织类别固定**：
  - 先验类别限定为肿瘤、间质、浸润、坏死四类，可能无法覆盖所有癌种或任务中的关键组织类型。
- **未在大规模模型上验证**：
  - 作者明确提到受硬件限制，未探索更大模型上的表现。

（完）
