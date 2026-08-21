---
title: Do Pathology Foundation Models Encode Disease Progression? A Pseudotime Analysis of Visual Representations
title_zh: 病理基础模型是否编码疾病进展？视觉表示的伪时间分析
authors: "Pritika Vig, Renchin Wu, William Lotter"
date: 2026-01-23
pdf: "https://openreview.net/pdf/3c36acdfda826af2f5aabe662e70dca5b42dede3.pdf"
tags: ["query:cell-path"]
score: 4.0
evidence: 病理基础模型表征的伪时间分析，探索疾病进展
tldr: 该研究关注病理视觉基础模型是否在潜在表示中编码连续的疾病进展过程。采用从单细胞转录组学借鉴的扩散伪时间方法，分析基础模型对离散采样图像的学习是否隐含疾病转变的连续结构。这一探索有助于理解模型是否捕捉到生物学动态，可能提升泛化能力并支持疾病进展的定量分析，进而推动计算病理学基础模型的发展。
source: ICML-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 病理基础模型在分类任务上表现优异，但其表征是否编码连续疾病进展尚不清楚。
method: 使用扩散伪时间方法探测病理基础模型的视觉表示，分析疾病进展的连续结构。
result: 初步探讨了基础模型潜在空间是否隐含疾病状态转变的连续性。
conclusion: 编码疾病进展的基础模型可能更好地反映生物学，支持鲁棒泛化。
---

## Abstract
Vision foundation models trained on discretely sampled images achieve strong performance on classification benchmarks, yet whether their representations encode the continuous processes underlying their training data remains unclear. This question is especially pertinent in computational pathology, where we posit that models whose latent representations implicitly capture continuous disease progression may better reflect underlying biology, support more robust generalization, and enable quantitative analyses of features associated with disease transitions. Using diffusion pseudotime, a method developed to infer developmental trajectories from single-cell transcriptomics, we probe whether foundation models organize disease states along coherent progression directions in representation space. Across four cancer progressions and six models, we find that all pathology-specific models recover trajectory orderings significantly exceeding null baselines, with vision-only models achieving the highest fidelities $(\tau > 0.78$ on CRC-Serrated). Model rankings by trajectory fidelity on reference diseases strongly predict few-shot classification performance on held-out diseases ($\rho = 0.92$), and exploratory analysis shows cell-type composition varies smoothly along inferred trajectories in patterns consistent with known stromal remodeling. Together, these results demonstrate that vision foundation models can implicitly learn to represent continuous processes from independent static observations, and that trajectory fidelity provides a complementary measure of representation quality beyond downstream performance. While demonstrated in pathology, this framework could be applied to other domains where continuous processes are observed through static snapshots.

---

## 论文详细总结（自动生成）

# 论文总结：病理基础模型是否编码疾病进展？视觉表示的伪时间分析

## 1. 论文的核心问题与整体含义

- **核心问题**：在离散采样图像上训练的视觉基础模型，其潜在表示是否编码了训练数据背后的连续生物过程？特别是在计算病理学中，模型是否在表示空间中隐式地捕捉到疾病进展的连续轨迹？
- **研究动机**：病理基础模型在分类任务上表现优异，但现有评估主要基于离散标签和下游任务准确率，缺乏对模型内部表征是否反映生物学连续动态的考察。
- **整体含义**：如果基础模型能够编码疾病进展，则说明模型不仅记忆了离散类别，还学到了更本质的生物学结构；这可能带来更强的泛化能力，并支持与疾病转变相关的定量分析。

## 2. 论文提出的方法论

- **核心思想**：借鉴单细胞转录组学中用于推断发育轨迹的**扩散伪时间（diffusion pseudotime）**方法，来探测病理基础模型的视觉表示是否将疾病状态沿着连贯的进展方向组织在表示空间中。
- **关键技术细节**（文字说明）：
  1. 将病理图像输入基础模型，提取视觉表示向量。
  2. 基于表示向量之间的相似度构建样本间的图结构（或转移概率矩阵），模拟扩散过程。
  3. 利用扩散伪时间算法计算每个样本在连续轨迹上的伪时间排序。
  4. 将推断出的伪时间顺序与真实疾病进展阶段进行比较，采用**轨迹保真度（trajectory fidelity, τ）** 等指标衡量恢复程度。
  5. 将轨迹保真度作为表示质量的补充度量，并与下游少样本分类性能进行关联分析。
- **关键公式/流程**：文中未给出具体公式，但可概括为：`表示空间 → 相似度图 → 扩散过程 → 伪时间排序 → 与真实进展比较 → τ`。摘要中的关键量化指标包括 `τ > 0.78`（CRC-Serrated 上最优视觉-only模型）和 `ρ = 0.92`（模型排名与下游性能的秩相关）。

## 3. 实验设计

- **数据集/场景**：
  - 覆盖 **4 种癌症进展**，其中明确提到 **CRC-Serrated**（结直肠锯齿状病变相关进展），其余 3 种在摘要中未具体列出。
  - 涉及 **6 个模型**，包括病理专用基础模型和视觉-only 基础模型。
- **Benchmark 与评价指标**：
  - 使用 **扩散伪时间** 推断疾病轨迹，并以 **轨迹保真度 τ** 作为主要衡量指标。
  - 以 **零基线（null baseline）** 作为显著性参照。
  - 通过 **模型在参考疾病上的轨迹保真度排名** 与 **在 held-out 疾病上的少样本分类性能** 之间的秩相关（`ρ = 0.92`）来评价轨迹保真度的预测能力。
- **对比方法**：
  - 对比不同病理专用模型与视觉-only模型。
  - 对比零基线以检验轨迹恢复是否显著优于随机。
  - 还进行了探索性分析：**细胞类型组成沿推断轨迹的平滑变化**是否与已知基质重塑模式一致。

## 4. 资源与算力

- 论文摘要和元数据中**未明确说明**使用的 GPU 型号、数量、训练时长、显存消耗或推理算力。
- 由于本研究主要基于预训练基础模型的特征提取与伪时间分析，可能算力需求低于大规模预训练，但具体资源配置需要查阅论文正文或附录才能确认。

## 5. 实验数量与充分性

- **可见实验规模**：
  - 至少涵盖 **4 种癌症进展 × 6 个模型** 的轨迹恢复实验。
  - 包含与零基线的显著性检验。
  - 包含下游少样本分类性能与轨迹保真度的相关性分析。
  - 包含细胞类型组成沿轨迹变化的探索性分析。
- **充分性评估**：
  - 从摘要看，实验覆盖了多疾病、多模型和下游任务关联，设计较为系统。
  - 但**细节不足**：未说明是否有消融实验、不同伪时间参数或距离度量的敏感性分析、多次随机重复的统计结果等。
  - **公平性**：使用统一零基线作为对照，且跨模型比较，相对公平；但不同模型训练数据分布和规模可能影响轨迹保真度，若未控制则可能引入偏差。

## 6. 论文的主要结论与发现

- **病理专用模型能恢复疾病进展轨迹**：所有病理专用模型均恢复出显著优于零基线的轨迹排序。
- **视觉-only模型表现最佳**：在 CRC-Serrated 上，视觉-only模型达到最高轨迹保真度（`τ > 0.78`）。
- **轨迹保真度可预测下游性能**：模型在参考疾病上的轨迹保真度排名与在 held-out 疾病上的少样本分类性能强烈相关（`ρ = 0.92`），表明该指标可作为表示质量的补充度量。
- **生物学一致性**：细胞类型组成沿推断轨迹平滑变化，且模式与已知的基质重塑相符。
- **总体结论**：视觉基础模型能够从独立的静态观测中隐式学习连续过程的表示；轨迹保真度提供了超越下游性能的表示质量评估维度。

## 7. 优点

- **方法新颖**：首次将单细胞转录组学的扩散伪时间方法迁移到病理视觉表示分析中，思路跨领域且创新。
- **关注连续生物学过程**：超越传统离散分类评估，直接探究表示空间中的连续动态结构。
- **提出补充度量**：轨迹保真度不仅描述表示质量，还能预测下游少样本泛化性能，具有实际价值。
- **多模型、多疾病验证**：在 4 种癌症进展和 6 个模型上验证，增强结论的普适性。
- **生物学可解释性**：通过细胞类型组成的平滑变化，将表示空间轨迹与真实基质重塑联系起来，增加生物学可信度。

## 8. 不足与局限

- **细节缺失**：摘要未提供具体数据集名称、模型架构、伪时间实现细节、超参数设置和统计检验方法，难以完全复现。
- **疾病覆盖有限**：仅 4 种癌症进展，且摘要只明确 CRC-Serrated，其他类型未知；可能限制结论推广到非肿瘤或非进展性疾病。
- **伪时间方法潜在敏感性**：基于图构建和扩散过程的伪时间推断可能对距离度量、近邻数和图权重敏感，文中未提及鲁棒性验证。
- **下游关联证据单一**：`ρ = 0.92` 的相关性仅展示一个设置，需在更多数据集和任务上验证其稳定性。
- **模型比较公平性存疑**：病理专用模型与视觉-only模型在训练数据、规模和预训练策略上可能不同，可能影响轨迹保真度比较。
- **临床应用未验证**：目前仅为概念验证，尚未在实际临床诊断或预后任务中验证其效用。
- **潜在偏差风险**：零基线的构造方式、真实进展标签的可靠性、图像采样偏差等未充分说明，可能影响结论强度。

（完）
