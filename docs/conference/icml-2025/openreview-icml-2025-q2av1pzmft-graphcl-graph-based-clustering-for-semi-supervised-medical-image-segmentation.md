---
title: "GraphCL: Graph-based Clustering for Semi-Supervised Medical Image Segmentation"
title_zh: GraphCL：基于图聚类的半监督医学图像分割
authors: "Mengzhu Wang, houcheng su, Jiao Li, Chuan Li, Nan Yin, Li Shen, Jingcai Guo"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Q2av1PZmfT"
tags: ["query:cellseg"]
score: 6.0
evidence: 基于图聚类的半监督医学图像分割
tldr: 半监督医学图像分割中，现有方法仅依赖复杂训练策略而忽略数据图结构信息。本文提出GraphCL，在一体化深度模型中联合建模图数据结构，通过图聚类引导伪标签生成。该方法在多个医学图像分割基准上显著提升了分割精度，尤其适用于标注数据稀缺的场景。该框架可泛化至病理图像等医学图像分析任务。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-q2av1pzmft/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 823, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-q2av1pzmft/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1454, \"height\": 785, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-q2av1pzmft/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 836, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-q2av1pzmft/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 837, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-q2av1pzmft/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 838, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-q2av1pzmft/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 850, \"height\": 574, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-q2av1pzmft/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 629, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-q2av1pzmft/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 860, \"height\": 593, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-q2av1pzmft/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-q2av1pzmft/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1792, \"height\": 429, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-q2av1pzmft/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 853, \"height\": 274, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-q2av1pzmft/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 850, \"height\": 552, \"label\": \"Table\"}]"
motivation: 现有半监督分割方法未充分利用数据间的图结构关系。
method: 提出联合建模图数据结构的深度模型，通过图聚类利用未标注数据。
result: 在多个医学图像分割数据集上取得了半监督设置下的最优性能。
conclusion: 图结构信息能有效提升半监督医学图像分割的性能。
---

## Abstract
Semi-supervised learning (SSL) has made notable advancements in medical image segmentation (MIS), particularly in scenarios with limited labeled data and significantly enhancing data utilization efficiency. Previous methods primarily focus on complex training strategies to utilize unlabeled data but neglect the importance of graph structural information. Different from existing methods, we propose a graph-based clustering for semi-supervised medical image segmentation (GraphCL) by jointly modeling graph data structure in a unified deep model. The proposed GraphCL model enjoys several advantages. Firstly, to the best of our knowledge, this is the first work to model the data structure information for semi-supervised medical image segmentation (SSMIS). Secondly, to get the clustered features across different graphs, we integrate both pairwise affinities between local image features and raw features as inputs. Extensive experimental results on three standard benchmarks show that the proposed GraphCL algorithm outperforms state-of-the-art semi-supervised medical image segmentation methods.

---

## 论文详细总结（自动生成）

# 论文总结：GraphCL: Graph-based Clustering for Semi-Supervised Medical Image Segmentation

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：半监督医学图像分割（SSMIS）旨在利用少量标注数据和大量未标注数据提升分割性能。现有方法多依赖复杂的训练策略（如一致性正则化、自训练），但忽视了数据间的**图结构信息**（graph structural information）。医学图像中复杂生物结构和高敏感性使得建模数据内在的结构关系尤为重要，而先前工作未在SSMIS中探索图结构建模。
- **整体含义**：本文首次在SSMIS中引入图数据结构建模，通过图神经网络（GNN）捕捉样本间及体素间的结构相似性，并利用图聚类增强特征判别性，以缓解标注数据稀缺导致的分布不匹配问题。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：在统一深度模型中联合建模图数据结构，将医学图像特征转化为图节点，基于相似性构建邻接关系，并通过图卷积网络（GCN）传播结构信息，辅以图聚类损失优化。
- **关键技术细节**：
  - **双向复制粘贴框架（BCP）**：采用教师-学生网络框架，通过随机裁剪标注图像的 foreground 粘贴到未标注图像（及反向操作）生成混合图像 `X_in` 和 `X_out`，分别用伪标签和真实标签监督学生网络。
  - **结构感知对齐（SA）**：对每个 mini-batch，用CNN提取特征，通过数据结构分析器（DSA）生成结构分数，计算图邻接矩阵 `Â = X_sa * X_sa^T`，再用GCN进行特征传播：`Z = D^(-1/2) Â D^(-1/2) X W`，得到聚合结构信息的特征。
  - **图神经网络聚类**：对每个3D体素，提取深度特征构建相似性矩阵 `W = (F·F^T - max(F·F^T))/τ`，τ控制聚类灵敏度。将W作为邻接矩阵，用单层GCN和MLP得到聚类分配矩阵S，采用**相关聚类损失** `L_CC = -Tr(W S S^T)`，促进相似节点归入同一簇、不相似节点分离。
  - **总损失**：`L_all = L_in + L_out + κ * L_CC`，κ为聚类损失权重（实验中设为0.01）。
- **算法流程**：预训练学生网络→教师网络生成伪标签→混合样本双向监督→每步更新学生参数，教师参数通过指数移动平均（EMA）更新。

## 3. 实验设计
- **数据集**：
  - **LA（左心房分割）**：3D MRI，标注比例5%、10%。
  - **ACDC（心脏多结构分割）**：2D MRI，标注比例5%、10%。
  - **Pancreas-NIH（胰腺分割）**：3D CT，标注比例20%。
- **评价指标**：Dice↑、Jaccard↑、95% Hausdorff距离（95HD↓）、平均表面距离（ASD↓）。
- **对比方法**：
  - 全监督基线：V-Net / U-Net（用全部标注或部分标注）。
  - 半监督方法：UA-MT、SASSNet、DTC、URPC、MC-Net、SS-Net、BCP，以及DAN、ADVENT、CoraNet（仅胰腺数据集）。
- **实验设置**：采用与SS-Net一致的评估协议，确保公平比较。

## 4. 资源与算力
- 论文明确说明：
  - **LA数据集**：运行在 NVIDIA A800 GPU 上。
  - **ACDC和Pancreas-NIH**：运行在 NVIDIA 3090 GPU 上。
  - 未提及训练时长、GPU数量或并行策略等具体资源使用细节。

## 5. 实验数量与充分性
- **主要实验数量**：
  - 在3个数据集上进行了对比实验（LA、ACDC、Pancreas-NIH），每个数据集包含不同标注比例，共6组主要对比。
  - **消融实验**：对三个数据集均进行了组件消融（基线 vs +SA vs +L_CC vs 两者），共12组（含不同标注比例）。
  - **GCN层位置消融**：在ACDC上测试了1~5层位置，共10组。
  - **超参数敏感性**：在ACDC上对κ和τ进行扫描（κ=0,0.005,0.01,0.05,0.1；τ=2,4,6,8,10,12），两个标注比例，共20组。
  - 总计约48组独立实验，覆盖不同数据集、标注比例和超参数。
- **充分性与公平性**：
  - 对比方法均采用官方或广泛认可的设置，使用相同backbone（V-Net/U-Net）和训练策略。
  - 消融实验验证了各组件的独立贡献，GCN层位置实验提供了设计指导。
  - 敏感性实验展示了超参数鲁棒性。
  - **不足**：未在更多样化的医学模态（如病理图像、X光）上验证；未报告统计显著性检验；可视化分析（KDE和分割样例）仅展示定性结果，缺乏定量分析。

## 6. 主要结论与发现
- GraphCL在所有数据集和标注比例上全面优于现有半监督方法，尤其在标注数据极低（5%）时提升更显著（如LA上平均Dice提升1.73%，ACDC上提升1.85%）。
- 结构感知对齐（SA）和图聚类损失（L_CC）均能独立提升性能，两者结合效果最佳。
- GCN置于encoder较深层（第5层）性能最好，浅层效果较差甚至退化。
- τ=2时聚类效果最优，κ=0.01给出最佳平衡。
- 可视化表明GraphCL能更好对齐未标注与标注数据的特征分布，分割边界更精准。

## 7. 优点
- **方法创新性**：首次将图数据结构建模引入SSMIS，且图聚类可自动确定簇数量（k-less），无需预设聚类数。
- **技术融合巧妙**：将BCP双向混合框架、GCN特征传播、相关聚类损失在单一损失函数中联合优化，架构清晰。
- **实验充分且严格**：在三个不同模态/维度的医学数据集上验证，对比了主流半监督方法；消融、超参数、GCN位置等实验设计系统。
- **开源代码**：提供GitHub仓库，便于复现与扩展。

## 8. 不足与局限
- **实验覆盖有限**：仅针对心脏（LA/ACDC）和胰腺（Pancreas-NIH）数据集，未检验在脑部、肺部或多器官分割上的泛化性；未验证在自然图像任务上的迁移能力。
- **偏差风险**：所有实验均基于V-Net/U-Net backbone，未探索Transformer类backbone（如Swin UNet），图结构建模与不同backbone的兼容性未知。
- **应用限制**：
  - 教师-学生框架和BCP混合依赖预训练，计算复杂度较高（需预训练和自训练两阶段）。
  - 超参数τ和κ需手动调整，缺乏自适应机制。
  - 图构建基于mini-batch，未能建模跨batch长程依赖。
  - 未讨论图像尺寸或GPU内存限制对图规模的影响。
- **未提及统计显著性**：未报告标准差或p值，可能削弱结果可靠性的量化结论。

（完）
