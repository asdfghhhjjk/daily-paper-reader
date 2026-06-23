---
title: Bayesian Inference for Correlated Human Experts and Classifiers
title_zh: 关联人类专家和分类器的贝叶斯推断
authors: "Markelle Kelly, Alex James Boyd, Sam Showalter, Mark Steyvers, Padhraic Smyth"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=sw2pUzbTf1"
tags: ["query:cellseg"]
score: 4.0
evidence: 结合分类器与专家的贝叶斯框架，应用于医学分类
tldr: 该论文提出一个通用贝叶斯框架，通过联合潜变量建模专家相关性，能够在少量专家查询下推断后验标签，并在医学分类任务上展示了实用性，可改进细胞核分类等应用中的标签质量。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-sw2puzbtf1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 680, \"height\": 2151, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sw2puzbtf1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 690, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sw2puzbtf1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 690, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sw2puzbtf1/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 639, \"height\": 524, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 988, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 870, \"height\": 602, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 825, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 836, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 346, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 970, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 794, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 817, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sw2puzbtf1/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 811, \"height\": 253, \"label\": \"Table\"}]"
motivation: 机器学习常需结合模型输出和专家意见，但专家查询成本高。
method: 通过联合潜变量建模专家相关性，进行基于模拟的专家查询决策和后验推断。
result: 在多个医学分类数据集上大幅减少专家查询次数同时保持准确性。
conclusion: 该框架为结合人机协同分类提供了高效方案，可应用于细胞分类。
---

## Abstract
Applications of machine learning often involve making predictions based on both model outputs and the opinions of human experts. In this context, we investigate the problem of querying experts for class label predictions, using as few human queries as possible, and leveraging the class probability estimates of pre-trained classifiers. We develop a general Bayesian framework for this problem, modeling expert correlation via a joint latent representation, enabling simulation-based inference about the utility of additional expert queries, as well as inference of posterior distributions over unobserved expert labels. We apply our approach to two real-world medical classification problems, as well as to CIFAR-10H and ImageNet-16H, demonstrating substantial reductions relative to baselines in the cost of querying human experts while maintaining high prediction accuracy.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

在许多实际应用中，机器学习系统需要与人类专家协作完成分类任务。例如，在医疗影像诊断中，多个放射科医生对同一图像可能给出不同意见，而获取所有专家的投票成本高昂。论文旨在解决以下问题：如何利用预训练分类器的概率输出，**以最少的专家查询次数**，准确预测一组人类专家的集体投票结果（如多数投票共识）。核心挑战在于专家之间可能存在相关性（例如，某些专家总是倾向于一致），而分类器与专家之间也可能存在分布偏移。论文提出了一个通用的贝叶斯框架，通过联合潜变量建模专家与分类器的相关性，实现在线序贯查询策略，从而在保持高精度的同时大幅降低查询成本。

### 2. 论文提出的方法论：核心思想、关键技术

- **核心思想**：将每个专家和分类器对输入 \(x\) 的预测（或潜在置信度）映射到低维潜变量空间（通过 logistic 正态变换），并假设这些潜变量服从多元正态分布，从而捕获专家之间、专家与分类器之间的相关性。通过贝叶斯推断（MCMC）学习全局参数（均值、协方差），然后基于观测到的部分专家投票和分类器输出，对未观测的专家投票进行后验模拟，并预测共识结果。
- **关键技术细节**：
  - **潜变量建模**：对于每个专家 \(i\) 和分类器 \(j\)，将其概率向量 \(\theta\) 通过加性logistic变换 \(\gamma(\theta) = [\log(\theta_1/\theta_K), ..., \log(\theta_{K-1}/\theta_K)]\) 转化为实值 logits \(z\)。所有 agent（\(M\) 个分类器 + \(H\) 个专家）的 logits 联合服从多元正态分布：\(z \sim \mathcal{N}(\mu, \Sigma)\)。
  - **投票生成**：专家的硬投票 \(y_i\) 从温度参数化后的分类分布中采样：\(y_i | \theta_i, \tau \sim \text{Categorical}(\text{softmax}(\theta_i/\tau))\)，其中 \(\tau\) 为温度（全局参数）。
  - **后验推断**：使用 MCMC（3条链，每条1500次warm-up + 2000次采样）从已观测数据（之前样本的专家投票和分类器输出）中学习 \(\mu, \Sigma, \tau\) 的后验。
  - **未观测投票预测**：给定当前样本的分类器输出 \(z_M\) 和已观测专家投票 \(y_O\)，通过算法1（条件模拟）从后验预测分布中采样 \(y_U\)，进而计算共识 \(y^*\) 的后验概率。
  - **主动查询策略**：采用信息增益（等价于最小化期望熵）选择下一个要查询的专家（算法2）。查询停止条件为模型对共识预测的误差概率低于预设阈值 \(e\)。
- **算法流程**：
  1. 初始化全局参数后验。
  2. 对每个新样本 \(x^{(t)}\)：
     - 获取分类器输出 \(z_M\)。
     - 循环：计算当前候选专家集合中每个专家的期望信息增益，选择最优专家查询。
     - 更新已观测集 \(O\)，重评估共识后验熵。
     - 若后验误差低于阈值则停止查询，输出共识预测。
     - 使用该样本的观测数据更新全局参数后验（在线学习，降低更新频率）。

### 3. 实验设计

- **数据集**：
  - 真实医疗图像：**ChestX-Ray**（二分类，5位放射科医生，810张图片）、**Chaoyang**（四分类，3位病理学家，2139张图片）。
  - 模拟专家数据集：**CIFAR-10H**（三分类，3个合成专家）、**ImageNet-16H**（三分类，3个合成专家）。合成专家通过组合多个匿名标注者的标签，注入类间能力差异（如对一个类准确率低）。
- **Baseline方法**：
  - **INFEXP + ϵ-greedy**：基于Showalter et al. (2024) 的贝叶斯方法，但通过ϵ-greedy选择专家（按观测准确率排序）。
  - **Confusion matrices + calibration**：扩展Kerrigan et al. (2021) 的方法，为每个专家学习混淆矩阵，并利用校准技术预测共识。
- **评估指标**：**错误率 vs. 平均专家查询次数**（误差-成本曲线）。每个数据集使用12个不同的250样本序列（在线学习），取平均结果。阈值 \(e\) 系统变化以绘制曲线。

### 4. 资源与算力

论文在实验细节（Appendix D）中提及：**使用NVIDIA GeForce 2080Ti GPU，实验持续数天**。未提供具体训练小时数或模型参数量。MCMC使用3条链、每条1500次warm-up+2000次采样，共6000个后验样本。参数更新频率：前20个样本每个样本更新，之后每10个样本更新一次直至100，之后每50个样本更新一次。算力要求中等到较高，但未提供精确量化。

### 5. 实验数量与充分性

- **实验数量**：覆盖4个数据集，每个数据集在12个随机序列上运行，取平均。共 \(4 \times 12 = 48\) 个主实验组（每组包含多个阈值下的误差-成本点）。
- **额外实验**：
  - 校准分析（Table 1）：报告了不同阈值下的期望校准误差（ECE），验证了模型不确定性校准良好（ECE通常<1%）。
  - 探索-利用分析（Table 2）：对比前50个和后50个样本的平均查询数，显示初期探索多、后期利用少。
  - 分布偏移实验（Figure 4）：在ImageNet-16H上模拟噪声水平突变，使用滑动窗口（大小50）适应，观察查询数自适应增加。
  - 替代聚合函数（Figure 5）：在ChestX-Ray上测试“任何专家投票为1”和“全体一致”函数。
- **充分性与公平性**：
  - 实验设计合理：在线学习场景下，方法对数据顺序敏感，12次随机打乱取平均可减小偏差。
  - 与两个baseline对比公平：baseline已从原始方法调整到当前问题设置。
  - 未在text或tabular数据上测试，但问题本身聚焦图像分类，覆盖面可接受。
  - 合成专家可能不完全反映真实专家相关性，但两个真实医疗数据集增强了说服力。

### 6. 论文的主要结论与发现

- 所提出的贝叶斯方法在所有四个数据集上均能**以最少的专家查询次数达到0%错误率**，而两种baseline要么无法达到0%错误（confusion+calibration），要么需要更多查询（INFEXP）。
- 模型的不确定性估计**校准良好**（ECE<1%），使得阈值 \(e\) 能够有效控制实际错误率。
- 在线学习体现了**探索-利用平衡**：初期查询较多，后期快速下降。
- 在**分布偏移**下，模型能自动增加查询次数以适应新的数据分布。
- 支持**灵活的聚合函数**（如“任意投票”、“全票一致”），可适应不同决策需求。

### 7. 优点

- **方法论创新**：首次针对不完全可交换的、相关的专家群体，提出一个统一的贝叶斯框架，同时建模分类器与专家之间的相关性，并进行主动查询选择。
- **实用性强**：无需专家数据预训练，可在线适应新分布；适用于高成本专家查询场景（如医疗）。
- **理论严谨**：基于后验模拟与信息论准则，提供可解释的查询策略。
- **实验全面**：覆盖真实医疗与模拟数据，包含校准、分布偏移、替代聚合函数等多种分析，验证了稳健性。

### 8. 不足与局限

- **计算成本**：MCMC采样在每个时间步（尽管更新频率降低）仍可能昂贵，对于超大规模问题（如大量专家或类别）可能不够高效。论文中也指出协方差矩阵 \( \Sigma \) 大小随 \( K, M, H \) 增长快。
- **实验覆盖有限**：仅限于图像分类任务；未在文本、表格数据或其他模态上验证。专家数量最多5人，类别最多4类，较大规模场景有待验证。
- **合成专家假设**：CIFAR-10H和ImageNet-16H的专家是人工构造的，可能不完全反映真实专家行为模式。真实医疗数据中专家数目少、差异大，但实验仍显示出优势。
- **未考虑不同查询成本**：假设所有专家查询成本相同，但实际中专家资历不同可能成本不同，文中提到这是未来方向。
- **与baseline的比较**：baseline方法（INFEXP+ϵ-greedy和confusion+calibration）可能并非该问题最优，但论文已说明这是现有相关方法的最佳适配。未与“随机查询”或“全量查询”等更简单的基线对比（但通过误差-成本曲线隐含对比）。
- **停止规则依赖校准**：虽然校准良好，但若模型严重失准，阈值 \(e\) 可能无法保证实际误差。

（完）
