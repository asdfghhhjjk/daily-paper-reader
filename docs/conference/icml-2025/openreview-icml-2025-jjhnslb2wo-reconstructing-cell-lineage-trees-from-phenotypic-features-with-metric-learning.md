---
title: Reconstructing Cell Lineage Trees from Phenotypic Features with Metric Learning
title_zh: 利用度量学习从表型特征重建细胞谱系树
authors: "Da Kuang, GuanWen Qiu, Junhyong Kim"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=JjhnSLb2wO"
tags: ["query:cellseg"]
score: 4.0
evidence: 度量学习用于细胞谱系和类型分类
tldr: 提出利用度量学习从细胞表型特征重建谱系树的方法，无需基因工程标记。通过对比学习将表型特征嵌入度量空间，推断细胞分化关系。实验表明该方法能准确分类细胞类型并重建谱系，为理解发育过程提供新工具，但对病理图像中的细胞分类仅为间接相关。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 691, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1338, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 824, \"height\": 259, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1773, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 830, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 518, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1560, \"height\": 935, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1756, \"height\": 1073, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1511, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1529, \"height\": 703, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1257, \"height\": 786, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1764, \"height\": 2210, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1767, \"height\": 679, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1771, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1779, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1777, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1766, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1766, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1777, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1778, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1779, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 864, \"height\": 669, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1766, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jjhnslb2wo/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1770, \"height\": 418, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 842, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 836, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1469, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1780, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1824, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1409, \"height\": 1031, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1688, \"height\": 515, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1383, \"height\": 1644, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1516, \"height\": 513, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1505, \"height\": 979, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1509, \"height\": 978, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1388, \"height\": 1166, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 932, \"height\": 834, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1655, \"height\": 1236, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1655, \"height\": 1232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1506, \"height\": 981, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jjhnslb2wo/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1511, \"height\": 978, \"label\": \"Table\"}]"
motivation: 现有细胞谱系追踪方法受限于基因工程标记，在多种生物中不可行。
method: 采用度量学习将细胞表型特征映射到嵌入空间，通过相似性推断细胞谱系关系。
result: 在多个单细胞数据集上成功重建细胞谱系树，细胞分类准确率高。
conclusion: 基于度量学习的表型特征分析可实现无标记的细胞谱系重建与分类。
---

## Abstract
How a single fertilized cell gives rise to a complex array of specialized cell types in development is a central question in biology. The cells replicate to generate cell lineages and acquire differentiated characteristics through poorly understood molecular processes. A key approach to studying developmental processes is to infer the tree graph of cell lineage histories, which provides an analytical framework for dissecting individual cells' molecular decisions during replication and differentiation (i.e., acquisition of specialized traits). Although genetically engineered lineage-tracing methods have advanced the field, they are either infeasible or ethically constrained in many organisms. By contrast, modern single-cell technologies can measure high-content molecular profiles (*e.g.*, transcriptomes) in a wide range of biological systems. Here, we introduce *CellTreeQM*, a novel deep learning method based on transformer architectures that learns an embedding space with geometric properties optimized for tree-graph inference. By formulating the lineage reconstruction problem as tree-metric learning, we systematically explore weakly supervised training settings at different levels of information and present the *Cell Lineage Reconstruction Benchmark* to facilitate comprehensive evaluation. This benchmark includes (1) synthetic data modeled via Brownian motion with independent noise and spurious signals; (2) lineage-resolved single-cell RNA sequencing datasets. Experimental results show that *CellTreeQM* recovers lineage structures with minimal supervision and limited data, offering a scalable framework for uncovering cell lineage relationships. To our knowledge, this is the first method to cast cell lineage inference explicitly as a metric learning task, paving the way for future computational models aimed at uncovering the molecular dynamics of cell lineage. Code and benchmarks are available at: https://kuang-da.github.io/CellTreeQM-page

---

## 论文详细总结（自动生成）

# 论文总结：利用度量学习从表型特征重建细胞谱系树

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：理解单个受精卵如何通过细胞分裂和分化产生多种特化细胞类型，是发育生物学的核心问题。重建细胞谱系树（即细胞分裂历史的树状图）是解析这一过程的关键工具。
- **现有方法的局限**：黄金标准方法（如基于CRISPR-Cas9的遗传谱系追踪）需要基因工程改造，在许多生物中不可行或受伦理限制。
- **本文切入点**：现代单细胞技术能测量高内涵分子谱（如转录组），但能否从这些表型数据中提取谱系信息尚不明确。本文尝试回答这一问题，提出一种基于度量学习的深度学习框架，直接从转录组数据重建细胞谱系树。

## 2. 方法论

### 核心思想
- **问题重定义**：将细胞谱系树重建转化为**树度量学习**问题。目标学习一个嵌入空间，使得该空间中细胞间的欧氏距离近似于真实谱系树中的路径距离（additive tree metric）。
- **关键假设**：假定谱系树上的马尔可夫过程产生的表型数据，其期望平方欧氏距离矩阵是加性（additive）的。学习嵌入函数 \( f \)  使得 \( \|f(x_i) - f(x_j)\| \approx D_T(i,j) \)。

### 关键技术细节
1. **Transformer 骨干网络**：使用无位置编码的Transformer编码器处理无序的细胞输入，输出低维嵌入向量。
2. **四元组损失（Quartet Loss）**：基于树度量的四点条件（Four-Point Condition）。对于任意四个叶子 i,j,k,l，计算三个距离和 \( S_1 = d_{ij}+d_{kl} \), \( S_2 = d_{ik}+d_{jl} \), \( S_3 = d_{il}+d_{jk} \)。在完美树度量中两个最大和相等，最小和更小。损失函数包含两部分：
   - **L_close**：鼓励两个最大和相等（\( |S_1 - S_2| \)）。
   - **L_push**：强制最小和小于前两者平均值一定边际（\( [S_3 - (S_1+S_2)/2 + m_0]_+ \)）。
3. **偏差损失（Deviation Loss）**：约束学习后的嵌入空间距离矩阵不偏离原始数据距离矩阵太远，防止退化。
4. **特征门控（Feature Gating）**：利用Gumbel-Softmax实现离散化特征选择，抑制噪声基因，突出谱系相关基因。
5. **最终优化目标**：\( \mathcal{L} = \mathcal{L}_{\text{additivity}} + \lambda \Omega + \lambda_{\text{spar}} \text{sparsity} \)。
6. **树构建**：使用Neighbor-Joining (NJ) 算法从学习到的距离矩阵重建谱系树。

### 监督与弱监督设置
- **监督**：所有四元组的真实拓扑已知。
- **弱监督**：
  - **高级分区**：知道树叶属于少数几个大分支（如已知细胞系粗分类），由此可推断部分四元组拓扑。
  - **部分叶子标记**：仅部分细胞有谱系标签。
- **无监督**：完全无标签，仅利用数据自身估计四元组排序。

## 3. 实验设计

### 数据集与基准（Benchmark）
- **合成数据**：基于布朗运动模拟信号特征（加性距离属性），添加独立高斯噪声和来自“替代树”的混淆特征（anti-signal），可系统调控信噪比。
- **真实数据**：
  - **C. elegans**：唯一拥有完整胚胎谱系的模式生物。使用Pack et al. (2019)和Large et al. (2024)的转录组图谱，构建三个规模：Small (102叶), Mid (183叶), Large (295叶)。
  - **CRISPR 数据集**：来自Chan et al. (2019)的mESC克隆数据（3435 NT T1和T6），作为额外验证。

### 对比方法
- **Triplet Loss**：基于四元组中最近对作为锚点-正例，最远为负例。
- **Quadruplet Loss**：扩展Triplet Loss，引入第二个负例，加强全局距离结构。
- **直接重构（Direct Reconstruction）**：使用原始欧氏距离直接通过NJ重建。

### 评估指标
- **Robinson–Foulds距离（RF）**：拓扑差异，0表示完全一致。
- **Quartet距离（QD）**：四元组拓扑正确比例，0表示完全一致。
- **相对改善率**：\( \Delta\% RF = (RF_{base} - RF_{recon}) / RF_{base} \)。

## 4. 资源与算力

- **论文未明确说明**：未提及使用的GPU型号、数量、训练时长等硬件信息。仅在附录中提到C. elegans Large数据集因计算成本高只运行一次，但未给出具体时间或资源细节。这可能会影响实验可重复性评估。

## 5. 实验数量与充分性

- **实验数量**：非常丰富。
  - 监督设置：在3个C.elegans数据集和合成数据上比较CellTreeQM、Triplet、Quadruplet，并包含特征门控（-G）和标签置换（-p）检验。
  - 弱监督-高级分区：在Small、Mid、Large三个规模上测试Level 1-3，多次重复（Small 10次，Mid 3次，Large 1次）。
  - 弱监督-部分叶子标记：在Small、Mid上测试已知比例30%/50%/80%，Small重复10次，Mid重复5次。
  - 无监督：仅在一个小模拟数据集上展示概念验证。
  - 消融实验：对损失函数组件进行单独和组合测试。
  - 额外验证：CRISPR数据集上的高级分区实验。
  - 重建方法比较：比较NJ、UPGMA、FastME、Ward、Single linkage等。
- **充分性与公平性**：
  - 多次重复并报告均值和标准差，统计严谨。
  - 采用标签/基因/细胞置换的零假设实验，验证方法不是过拟合。
  - 对比基线（Triplet, Quadruplet）实现合理，超参数类似。
  - 但弱监督部分在C. elegans Large上只运行一次，统计说服力稍弱；部分叶子标记在较低比例（30%）下所有方法效果差，表明场景难度高，但论文如实报告。
- **总体评价**：实验设计系统、覆盖面广、对比公平，可以认为充分支持文章结论。

## 6. 主要结论与发现

- CellTreeQM在监督和弱监督设置下**显著优于**Triplet和Quadruplet损失，尤其在全局树拓扑恢复上优势明显（RF改善率高）。
- 特征门控（-G）能进一步改善性能，尤其在合成数据中能有效剔除噪声。
- 标签置换实验表明，CellTreeQM学到的是**真实谱系信号**而非数据伪影。
- 高级分区弱监督（知道粗粒度分支）是实用的：仅知道Level 1或2即可大幅改善RF。
- 部分叶子标记弱监督在已知比例>50%时有效，但30%时所有方法几乎无改善，表明该场景极具挑战。
- 无监督在合成小数据上有潜力，但在真实数据上表现有限，仍需更优策略。
- **首次将谱系重建明确视为度量学习问题**，为后续工作提供新范式。

## 7. 优点

1. **问题定义新颖**：将树重建转化为度量空间学习，避免了直接优化NP难的拓扑搜索。
2. **损失函数设计精巧**：四元组损失直接基于树度量的四点条件，理论依据强，优于对比学习中的通用损失。
3. **特征门控增强可解释性**：能自动筛选谱系相关基因，有助于后续生物学发现。
4. **基准构建完整**：提供合成和真实数据的多规模基准，涵盖多种噪声和弱监督场景，便于后续方法比较。
5. **实验系统全面**：覆盖监督、两种弱监督、无监督，并包含消融、置换检验、多种重建方法比较，结论可靠。
6. **代码和基准开源**：促进可重复性和社区贡献。

## 8. 不足与局限

1. **计算资源未报告**：未说明GPU型号、训练时间等，可能影响可重复性。
2. **损失函数超参数敏感**：包含多个权重（\( \lambda, m_0, \lambda_{spar} \)），调参成本较高，论文未给出鲁棒性分析。
3. **依赖NJ算法**：NJ在复杂噪声下可能失败，论文未探索更鲁棒的树推断方法（如贝叶斯或图神经网络）。
4. **真实数据仅限线虫**：C. elegans是唯一有完整谱系的模型，向人类或其他物种推广需谨慎，且CRISPR数据集作为验证规模较小。
5. **部分叶子标记场景实用性低**：在已知比例30%时几乎无效，而实际中可能更少。
6. **无监督表现有限**：仅在合成小数据上有效，真实数据上RF改善微乎其微，离实际应用有距离。
7. **弱监督高级分区需要先验知识**：实际中生物学家可能无法知道精准的分区级别，限制了直接应用。
8. **特征门控受限于信号-噪声相关性**：论文指出真实数据中“噪声”可能与信号相关，门控效果减弱。

（完）
