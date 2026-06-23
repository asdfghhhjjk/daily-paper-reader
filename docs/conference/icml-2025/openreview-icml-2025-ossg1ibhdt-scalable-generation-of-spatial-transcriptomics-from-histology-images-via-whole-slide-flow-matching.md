---
title: Scalable Generation of Spatial Transcriptomics from Histology Images via Whole-Slide Flow Matching
title_zh: 通过全切片流匹配从组织学图像可扩展生成空间转录组
authors: "Tinglin Huang, Tianyu Liu, Mehrtash Babadi, Wengong Jin, Rex Ying"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Ossg1IbHDT"
tags: ["query:pathology-ai"]
score: 7.0
evidence: 全切片图像分析用于空间转录组生成
tldr: 空间转录组技术受限于低通量和实验设施。现有预测方法未建模细胞间相互作用且编码器存在内存瓶颈。本文提出STFlow，利用流匹配在全切片组织学图像上生成空间转录组数据。该方法显式建模细胞间交互并引入可扩展编码器，大幅提升了预测效率与准确性。该工作为从组织学图像推断基因表达谱提供了新的高效途径。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1765, \"height\": 943, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 637, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 832, \"height\": 628, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1774, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 862, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1780, \"height\": 684, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1593, \"height\": 575, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1766, \"height\": 868, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 770, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 855, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 858, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1062, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1766, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1234, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1597, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1419, \"height\": 513, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1416, \"height\": 513, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1421, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1414, \"height\": 433, \"label\": \"Table\"}]"
motivation: 现有空间转录组预测方法忽略细胞间相互作用且受限于编码器内存瓶颈。
method: 提出STFlow，基于流匹配框架，在全切片图像上生成空间转录组，显式建模细胞间相互作用。
result: 在多个数据集上生成了高质量的空间转录组，超越现有方法。
conclusion: STFlow为从组织学图像高效推断基因表达提供了可扩展方案。
---

## Abstract
Spatial transcriptomics (ST) has emerged as a powerful technology for bridging histology imaging with gene expression profiling. However, its application has been limited by low throughput and the need for specialized experimental facilities. Prior works sought to predict ST from whole-slide histology images to accelerate this process, but they suffer from two major limitations. First, they do not explicitly model cell-cell interaction as they factorize the joint distribution of whole-slide ST data and predict the gene expression of each spot independently. Second, their encoders struggle with memory constraints due to the large number of spots (often exceeding 10,000) in typical ST datasets. Herein, we propose STFlow, a flow matching generative model that considers cell-cell interaction by modeling the joint distribution of gene expression of an entire slide. It also employs an efficient slide-level encoder with local spatial attention, enabling whole-slide processing without excessive memory overhead. On the recently curated HEST-1k and STImage-1K4M benchmarks, STFlow substantially outperforms state-of-the-art baselines and achieves over 18% relative improvements over the pathology foundation models.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：空间转录组（Spatial Transcriptomics, ST）能够将组织学图像与基因表达谱在空间上关联，但传统ST技术通量低、依赖专用实验设备。现有方法尝试从全切片组织学图像（WSI）直接预测基因表达，以加速这一过程。
- **现有局限**：
  - 大多数方法将每个“斑块”（spot）独立预测基因表达，**未显式建模细胞间的相互作用**（如某些基因调控邻近细胞中基因的表达）。
  - 编码器处理含数万个斑块的全切片时存在**内存瓶颈**，难以扩展到大规模WSI。
- **本文目标**：提出STFlow，一种基于**流匹配（Flow Matching）**的生成模型，能够**联合建模全切片所有斑块的基因表达联合分布**，同时利用**高效局部空间注意力**实现可扩展的全切片处理。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 核心思想
- 将传统的回归任务重新定义为生成任务：从先验分布采样“初始表达猜测”，通过迭代去噪逐步逼近真实表达。
- 在每一次去噪步骤中，显式利用**细胞间相互作用**（通过局部空间注意力结合基因表达差异和空间关系）来更新每个斑块的表达预测。

### 关键技术细节

1. **病理基础模型（Pathology Foundation Model）**：使用预训练的大规模病理图像模型（如UNI）提取每个斑块的视觉特征，之后冻结权重。

2. **先验分布（Prior Distribution）**：分析发现基因表达数据具有**稀疏性和过度离散性**（零膨胀、方差>均值），因此选择**零膨胀负二项分布（ZINB）**作为先验，由均值μ、分散参数ϕ和零膨胀概率π控制。

3. **流匹配学习框架**：
   - **训练阶段（Algo.1）**：
     - 从ZINB中采样噪声 \(Y_0\)，均匀采样时间步 \(t \in [0,1]\)。
     - 线性插值：\(Y_t = t \cdot Y + (1-t) \cdot Y_0\)。
     - 去噪网络 \(f_\theta\) 输入（坐标C、图像特征I、噪声表达\(Y_t\)、时间t），预测去噪后的表达 \(\hat{Y}\)。
     - 损失函数：MSE(\(Y, \hat{Y}\))。
   - **推理阶段（Algo.2）**：
     - 从ZINB中采样初始表达 \(Y_0\)。
     - 对于S个步长（实验中S=5），逐步插值：\(Y_{t_2} = Y_{t_1} + (\hat{Y} - Y_{t_1})/(1-t_1) \cdot (t_2 - t_1)\)。
     - 最终步输出 \(\hat{Y}\) 作为预测。

4. **去噪器架构 \(f_\theta\)**：
   - **局部空间上下文**：只对每个斑块的k近邻（k=8）计算注意力，降低计算复杂度（O(Nk)）。
   - **E(2)-不变空间注意力**：利用**框架平均（Frame Averaging, FA）**实现旋转、平移、反射不变性。具体：将方向向量投影到PCA提取的四个正交框架上，对每个框架进行MLP编码后取平均，得到不变的空间关系表示 \(C'_{i \to j}\)。
   - **注意力计算**：使用MLP注意力，将查询、键、空间编码、基因表达差异拼接后计算权重：
     \[
     A_{ij} = \mathrm{Softmax}_i\left( \mathrm{MLP}\left( [Z_{Q,i} \| Z_{K,j} \| C'_{i \to j} \| (Y_{t,i} - Y_{t,j}) ] \right) \right)
     \]
   - **更新**：聚合邻居表示，更新斑块表示和基因表达，各层输出的表达取平均作为最终预测。

5. **不变性保证**：空间注意力基于帧平均，保证E(2)-不变；病理基础模型经过大尺度数据增强，对图像层面的E(2)变换鲁棒。

## 3. 实验设计：数据集、基准与对比方法

### 数据集与基准
- **HEST-1k**：包含10个器官/癌症子数据集（IDC, PRAD, PAAD, SKCM, COAD, READ, CCRCC, HCC, LUNG, LYMPH），采用患者分层交叉验证（k折）。
- **STImage-1K4M**：选取7个器官（Breast, Brain, Skin, Mouth, Stomach, Prostate, Colon），随机8:1:1拆分训练/验证/测试。
- **评价指标**：对log1p归一化后的top 50高变基因计算Pearson相关系数，报告均值和标准差（3个随机种子）。

### 对比方法
- **基于点的方法**：Ciga、UNI、Gigapath（使用Random Forest作为回归头）、STNet、BLEEP。
- **基于切片的方法**：Gigapath-slide、HisToGene、TRIPLEX。
- **消融变体**：STFlow w/o FM（去掉流匹配）、STFlow w/o FA（去掉框架平均）。
- **E(2)架构变体**：EGNN、E2CNN（替换STFlow的注意力模块）。
- **不同病理基础模型**：Ciga、UNI、Gigapath作为视觉特征提取器。

### 额外实验
- **生物标志物预测**：在IDC（GATA3, ERBB2）、LUNG（UBE2C）、SKCM（VWF）上预测4个标志基因表达。
- **不同先验分布**：零分布、标准高斯分布 vs. ZINB。
- **不同细化步数**：S=1,2,5,10,16。
- **效率比较**：推理时间和GPU内存（与HisToGene、TRIPLEX对比）。
- **超参数研究**：ZINB参数的网格搜索。

## 4. 资源与算力

- **硬件环境**：单台Linux服务器，AMD EPYC 7763 64核CPU、1024GB RAM、8块RTX A6000-48GB GPU。
- **训练细节**：所有模型训练100个epoch，使用Adam优化器，学习率5e-4（经{1e-3,5e-4,1e-4}调优），梯度裁剪1.0，早停（20个epoch无改善则停止）。
- **文中未明确给出具体训练时长或总GPU小时数**，但指出STFlow参数量仅1.147M，显著少于HisToGene（149M）和TRIPLEX（13.767M），推理速度更快。

## 5. 实验数量与充分性

### 实验数量
- **主要结果**：在17个数据集（HEST-1k的10个 + STImage-1K4M的7个）上对比了8种基线，共报告了14个表格（包括正文和附录）。
- **生物标志物**：4个基因 × 多个模型。
- **消融实验**：针对流匹配、框架平均、不同病理模型、不同E(2)架构、不同先验、不同步数等共5组以上消融。
- **效率对比**：生成一张图（图5）对比推理时间和内存。
- **超参数研究**：ZINB的μ和ϕ共9种组合。

### 充分性与公平性
- **充分性**：覆盖了多种器官、多种技术（Visium, Xenium）、多种评估维度，实验内容全面，消融实验验证了每个核心模块的贡献。
- **客观性**：所有结果均报告多次运行（3个随机种子）的均值和标准差；患者分层拆分避免数据泄露；超参数通过网格搜索或调优确定。
- **公平性**：基线的实现和超参数均参照官方代码或文献设定，并统一使用相同的病理基础模型（如UNI）以隔离变量。性能对比基于公开基准。
- **不足**：仅使用两个公开数据集，未涉及其他来源或不同物种的数据；生物标志物预测只选了4个基因，样本量有限。

## 6. 主要结论与发现

1. **全切片流匹配建模有效**：STFlow在HEST-1k和STImage-1K4M共17个数据集上均优于所有基线，平均Pearson相关系数达到0.415（HEST-1k），较最强的病理基础模型UNI（0.344）**相对提升约18%**。
2. **细胞-细胞相互作用建模是关键**：去除流匹配或框架平均后性能显著下降（例如在IDC上从0.587降至0.580或0.580）。
3. **ZINB先验优于零或高斯先验**：ZINB分布更符合基因表达数据的稀疏性和过度离散特征。
4. **迭代细化提升预测精度**：从单步预测（S=1）增加到多步（S=5）带来明显提升，更多步数（S=10,16）收益饱和。
5. **高效性与可扩展性**：STFlow参数量少（1.147M），推理时间和内存消耗远低于同类切片级方法（如HisToGene、TRIPLEX），适合标准WSI（>10,000 spots）。
6. **临床潜力**：在GATA3、ERBB2、UBE2C、VWF四个生物标志物上取得最高相关系数，可视化显示预测表达模式与真实高度一致。

## 7. 优点

- **方法创新**：
  - 首次将**流匹配**应用于全切片空间转录组预测，替代传统一步回归，通过迭代优化显式建模基因-基因和细胞-细胞关系。
  - 引入**E(2)-不变空间注意力**，基于框架平均方法，在保留方向向量的同时实现旋转/平移/反射不变性，且计算高效。
  - **ZINB先验**的设计充分利用了基因表达的统计特性。
- **实验设计**：
  - 在**大规模、多器官、双基准**上验证，结果具有统计意义。
  - 消融实验系统全面，每个模块的必要性都得到证明。
  - 与多种SOTA方法（包括不同视觉backbone）对比，展示通用兼容性。
- **实用价值**：
  - 参数量少、运行速度快，可部署到实际病理工作流中。
  - 在生物标志物预测上表现突出，有潜力辅助临床诊断。

## 8. 不足与局限

- **超参数依赖网格搜索**：ZINB的μ、ϕ、π需要手动调优，论文未提供自动估计方法（如利用VAE拟合经验分布）。
- **固定细化步数**：S=5在多个数据集上接近最优，但最优步数可能因数据集而异，论文未深入讨论自适应步数策略。
- **通用性局限**：仅使用H&E染色的病理图像，未测试其他染色或不同分辨率下效果；仅涉及人类癌症组织，未验证在正常组织或小鼠等模型上的表现。
- **计算资源需求**：虽然方法本身高效，但训练仍需要A6000级GPU（显存需求取决于最大WSI尺寸），论文未明确给出具体训练时间，限制了可复现性。
- **评价指标单一**：仅使用Pearson相关系数，未引入MSE、SSIM或生物学意义指标（如通路富集一致性等）。
- **数据偏倚风险**：STImage-1K4M中某些器官样本量极少（如Skin仅4例，Stomach 12例），模型在这些小样本上的表现可能不稳定。
- **未报告失败案例**：例如READ、HCC等数据集上所有方法相关系数均很低（0.1-0.2），STFlow虽然领先但绝对数值仍不高，论文未深入分析原因。

（完）
