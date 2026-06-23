---
title: Deep Neural Cellular Potts Models
title_zh: 深度神经细胞Potts模型
authors: "Koen Minartz, Tim D'Hondt, Leon Hillmann, Jörn Starruß, Lutz Brusch, Vlado Menkovski"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=3xznpzabYQ"
tags: ["query:profile"]
score: 5.0
evidence: 细胞动力学与形态学建模
tldr: 细胞Potts模型是模拟细胞群体时空动态的强大方法，但传统模型依赖物理启发的哈密顿量，难以捕捉真实复杂性。本文提出NeuralCPM，通过神经网络哈密顿量在观测数据上直接训练，能同时整合领域知识与数据驱动表达。该模型尊重细胞动力学的通用对称性，为生物形态发生研究提供了更准确的仿真工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 859, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 694, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 775, \"height\": 667, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 660, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 851, \"height\": 1001, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 855, \"height\": 1162, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1778, \"height\": 547, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1738, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1754, \"height\": 1205, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 887, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1746, \"height\": 2042, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xznpzabyq/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1752, \"height\": 2044, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 836, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 766, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 863, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 712, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 637, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 635, \"height\": 198, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 636, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 635, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 638, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1034, \"height\": 473, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1781, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xznpzabyq/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1638, \"height\": 551, \"label\": \"Table\"}]"
motivation: 传统细胞Potts模型依赖近似哈密顿量，无法全面模拟真实细胞复杂性。
method: 提出NeuralCPM，用神经网络架构构建可训练的哈密顿量，并整合领域知识。
result: 模型在观测数据上训练，能更准确模拟细胞集体动力学。
conclusion: NeuralCPM为细胞形态与微环境研究提供了可学习的仿真框架。
---

## Abstract
The cellular Potts model (CPM) is a powerful computational method for simulating collective spatiotemporal dynamics of biological cells.
To drive the dynamics, CPMs rely on physics-inspired Hamiltonians. However, as first principles remain elusive in biology, these Hamiltonians only approximate the full complexity of real multicellular systems.
To address this limitation, we propose NeuralCPM, a more expressive cellular Potts model that can be trained directly on observational data.
At the core of NeuralCPM lies the Neural Hamiltonian, a neural network architecture that respects universal symmetries in collective cellular dynamics.
Moreover, this approach enables seamless integration of domain knowledge by combining known biological mechanisms and the expressive Neural Hamiltonian into a hybrid model.
Our evaluation with synthetic and real-world multicellular systems demonstrates that NeuralCPM is able to model cellular dynamics that cannot be accounted for by traditional analytical Hamiltonians.

---

## 论文详细总结（自动生成）

# 论文《Deep Neural Cellular Potts Models》详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **背景**：细胞迁移与多细胞自组织是胚胎发育、癌症转移等关键生物过程。细胞Potts模型（CPM）通过物理启发的**哈密顿量（能量函数）** 驱动随机动力学，是模拟集体细胞行为的主流方法。
- **问题**：生物系统中的“第一原理”难以确定，传统CPM的哈密顿量依赖专家手工设计，仅能近似真实复杂性，且对每个新应用场景都需要重新设计，既费力又受限于符号表达形式。
- **目标**：提出一种可学习的CPM，能够直接从观测数据中拟合哈密顿量，同时保持细胞动力学生物学一致性，并允许整合已有的领域知识。

## 2. 方法论：核心思想、技术细节与流程
- **核心思想**：将CPM的哈密顿量参数化为**神经网络**（称为 Neural Hamiltonian），从而利用深度能量模型（Deep EBM）的训练框架直接优化哈密顿量，使其诱导的稳态分布匹配观测数据的分布。
- **Neural Hamiltonian 架构**：
  - **对称性约束**：哈密顿量需对细胞的**置换**和网格的**平移**保持不变性。
  - **流程**：输入为离散网格状态 \(x\)，先进行 one-hot 编码，得到每个细胞对应的独立网格；然后通过多个 **NH 层**处理，每层包含：
    1. 细胞独立 CNN（\(\phi^l\)）产生每个细胞的嵌入；
    2. 排列不变聚合（求和）得到全局上下文网格 \(A\)；
    3. 细胞间交互 CNN（\(\psi^l\)）结合个体嵌入与全局上下文；
    4. 可选局部池化。
  - 最后对所有细胞和空间维度进行全局池化，得到不变表示，再经 MLP 输出标量哈密顿量值。
- **生物学信息整合（闭包模型）**：
  - 将 Neural Hamiltonian 作为**闭包项**叠加在可解释的符号哈密顿量之上：
    \[
    H_{\theta}(x) = w_S \cdot H_{\theta_S}^{\text{symbolic}}(x) + w_{NN} \cdot H_{\theta_{NN}}^{\text{neural}}(x)
    \]
  - 符号部分通常包含接触能量和体积约束，提供强先验；神经部分负责表达超出手工函数的高阶交互。
- **训练算法**：
  - 目标：最小化负对数似然 \(\min_\theta E_{p^*}[-\log p_\theta(x)]\)，其中 \(p_\theta(x) \propto e^{-H_\theta(x)}\)。
  - 梯度：\(\nabla_\theta \mathcal{L} = E_{p^*}[\nabla_\theta H_\theta(x)] - E_{p_\theta}[\nabla_\theta H_\theta(x)]\)。
  - 使用持久化对比散度（PCD），从数据初始化 MCMC 链，每步用**近似并行 CPM 采样器**（算法 2）生成负样本，加速训练。损失函数中加入能量正则项 \(\lambda (H_\theta(x^+)^2 + H_\theta(x^-)^2)\)。

## 3. 实验设计：数据集、基准与对比方法
- **数据集 / 场景**：
  1. **合成细胞分选数据**：使用经典哈密顿量（式 4）生成四种分选模式（A、B、D、F），每类 128 个快照，用于验证参数学习能力。
  2. **Cellular MNIST**：合成数据，细胞在外部势能引导下形成手写数字结构（类似 MNIST），共 1280 个样本。用于测试表达力。
  3. **双极轴向组织（真实生物学）**：Toda et al. (2018) 的实验室观测（6 次重复 + 时间序列），以及基于 Morpheus 生成的合成配置（1000 个样本，通过设定目标坐标生成，再随机旋转）。用于评估模型在真实数据上的泛化能力。
- **对比方法**（共 8 种，含消融）：
  - 分析型：细胞分选哈密顿量、细胞分选 + 外部势能（学习势能）。
  - 神经型：CNN 哈密顿量、1 层 NH + CNN、纯 Neural Hamiltonian（NH）、NH + 闭包（核心模型）。
  - 消融对照：GNN + 闭包、NH 无交互 + 闭包、NH 无池化 + 闭包（附录 C.2）。
- **评价指标**：
  - 生物合理性：\(p_{\text{volume}}\)（体积在训练数据范围 ±10% 内）、\(p_{\text{unfragmented}}\)（最多 3 个碎片细胞）。
  - 集体结构质量：Cellular MNIST 使用**分类器得分（CS）**；双极轴向组织使用**轴向排列 RMSE**（沿主轴与正交轴方差的比例）。

## 4. 资源与算力
- 论文未明确说明使用的 GPU 型号、数量或总算力。
- 唯一提及：每个训练运行在 24 小时后终止（若未收敛则手动选取最佳模型）。附录 B.1 给出超参数表（批大小 16，蒙特卡洛步数 0.5~1.0，并行翻转数 50~100）。
- 结论：**缺乏详细的算力报告**，但这在早期方法论论文中较常见。

## 5. 实验数量与充分性
- **实验组数**：主实验 3 个场景，每个场景对比 7~8 种模型（含基线），总计约 8×3=24 组模拟。附录中包含参数拟合的鲁棒性分析（5 次随机初始化的均值和标准差）、消融研究（GNN、无交互、无池化）以及额外定性结果。
- **充分性**：
  - 合成数据验证了算法能正确恢复已知参数（RMSE 低，收敛快）。
  - 两个表达力场景均展示了 NH+闭包的优势，消融实验证明对称性架构和闭包项的必要性。
  - 真实数据实验通过与 Toda et al. (2018) 的 6 次重复及时间序列对比，证明了模型能复现实验观测的自组织动态。
- **公平性**：变模型架构（CNN、NH 等）保持相似的通道数和层数，但未统一计算量；训练使用相同超参数（学习率、批次等），但模型收敛速度不同，作者在定性上确保选出最佳模型。总体而言，比较较为公平。

## 6. 主要结论与发现
1. **Neural Hamiltonian 能够学习传统 CPM 无法表达的复杂集体动态**：在 Cellular MNIST 中，NH+闭包在维持生物合理性的同时获得了最高的分类器得分（CS=4.35），而纯分析模型 CS 仅约 2.47~3.11。
2. **对称性约束至关重要**：使用 CNN 或 GNN 替代对称性架构会导致生物指标显著下降（CNN 的 \(p_{\text{volume}}=0\)），证明置换+平移不变性是有效建模的前提。
3. **闭包建模提升训练稳定性与生物一致性**：纯 NH 在双极轴向组织实验中出现训练发散，而 NH+闭包稳定收敛，且生物一致性指标最优（\(p_{\text{volume}}=0.77\), \(p_{\text{unfragmented}}=1.00\)，轴向排列 RMSE=37.3 远低于其他模型）。
4. **学习的模型能预测真实细胞动态**：NeuralCPM 模拟的自组织时间进程与 Toda et al. (2018) 的显微镜观测高度吻合（图 7(b)），尽管训练数据仅包含合成最终配置，但模型在时间维度上展现了泛化能力。

## 7. 优点：方法与实验设计的亮点
- **方法创新**：首次将深度能量模型（EBM）框架引入 CPM，使得哈密顿量可以通过数据驱动方式进行学习，突破了手工设计的局限。
- **对称性感知架构**：设计了一类新的神经网络模块（NH 层），同时保证对细胞置换和平移的等变性，适用于网格上的多细胞状态，优于简单的 CNN 或 GNN 方案。
- **生物学先验融合**：通过可学习的闭包形式，无缝集成领域知识，既保留了传统哈密顿量的强约束（细胞体积、接触能），又赋予模型更高表达力，训练也更稳定。
- **理论与实验联系紧密**：不仅使用合成数据，还直接与真实实验数据对比，验证模型能预测未见的动态路径，体现了应用的现实价值。
- **开源代码**：提供完整实现（JAX/Equinox），便于复现与扩展。

## 8. 不足与局限
- **计算效率低**：MCMC 采样需要大量前向传播，即使采用近似并行采样器，训练仍耗时（单次运行可达 24 小时）。作者未提供具体加速比或对多 GPU 的扩展性分析。
- **规模限制**：实验中细胞数量 ≤100，网格尺寸 ≤200²。对于大规模组织模拟（如数千细胞、高分辨率网格），全局感受野的 NH 架构不现实，且采样成本会急剧上升。
- **平衡分布假设**：模型假设系统处于热力学平衡，对于主动迁移、非平衡态（如趋化、有丝分裂）等过程不适用。作者提出需发展条件哈密顿量以考虑历史信息。
- **评价指标可能不够全面**：生物合理性指标（体积、碎片化）较粗，未检验更精细的形态特征（例如细胞长宽比、极性）；CS 依赖于一个自行训练的 MNIST 分类器，其偏置可能影响比较。
- **对合成训练数据的依赖**：双极轴向组织实验使用合成配置而非真实观测进行训练，合成数据可能简化了噪声和异构性，模型在真实数据上的表现仍有一定差距（图 7(a) 的方差分数略高于真实）。
- **缺少与其他机器学习方法的直接比较**：未对比基于时间序列的自动回归模型（如 Minartz et al., 2022, 2023），只对比了哈密顿量替代架构，因此无法确定 NeuralCPM 相对于其他学习型仿真器的总体优势。

（完）
