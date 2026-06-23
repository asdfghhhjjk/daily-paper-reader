---
title: "Distributed Parallel Gradient Stacking(DPGS): Solving Whole Slide Image Stacking Challenge in Multi-Instance Learning"
title_zh: 分布式并行梯度堆叠：解决全切片图像多实例学习中的堆叠挑战
authors: "Boyuan Wu, ZEFENG WANG, Xianwei Lin, Jiachun Xu, Jikai Yu, Zhou Shicheng, Hongda Chen, Lianxin Hu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=ss5JNmJDkW"
tags: ["query:wsi-mil"]
score: 7.0
evidence: 全切片图像多实例学习堆叠方法
tldr: "全切片图像分析常被建模为多实例学习问题，但现有方法因实例长度不一致导致堆叠困难、性能下降。本文提出分布式并行梯度堆叠框架DPGS，首次实现无损MIL数据堆叠，并搭配深度模型梯度压缩加速分布式训练。在Camelyon16和TCGA-Lung数据集上，训练速度提升高达31倍，通信量减少99.2%，准确率提升9.3%。该方法为病理切片弱监督学习提供了高效解决方案。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ss5jnmjdkw/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 864, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ss5jnmjdkw/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1720, \"height\": 907, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ss5jnmjdkw/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 825, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ss5jnmjdkw/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1570, \"height\": 777, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ss5jnmjdkw/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 825, \"height\": 483, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ss5jnmjdkw/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ss5jnmjdkw/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1756, \"height\": 884, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ss5jnmjdkw/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 856, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ss5jnmjdkw/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 821, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ss5jnmjdkw/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 849, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ss5jnmjdkw/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 780, \"height\": 567, \"label\": \"Table\"}]"
motivation: 现有MIL方法因实例长度不一致导致非堆叠数据，降低性能和效率。
method: 提出DPGS框架实现无损MIL数据堆叠，并引入深度模型梯度压缩加速分布式训练。
result: "在Camelyon16和TCGA-Lung上训练速度提升31倍，通信量减少99.2%，准确率提升9.3%。"
conclusion: DPGS有效解决了WSI堆叠问题，显著提升MIL训练效率和精度。
---

## Abstract
Whole Slide Image (WSI) analysis is framed as a Multiple Instance Learning (MIL) problem, but existing methods struggle with non-stackable data due to inconsistent instance lengths, which degrades performance and efficiency. We propose a Distributed Parallel Gradient Stacking (DPGS) framework with Deep Model-Gradient Compression (DMGC) to address this. DPGS enables lossless MIL data stacking for the first time, while DMGC accelerates distributed training via joint gradient-model compression. Experiments on Camelyon16 and TCGA-Lung datasets demonstrate up to 31× faster training, up to a 99.2% reduction in model  communication size at convergence, and up to a 9.3% improvement in accuracy compared to the baseline. To our knowledge, this is the first work to solve non-stackable data in MIL while improving both speed and accuracy.

---

## 论文详细总结（自动生成）

### 分布式并行梯度堆叠：解决全切片图像多实例学习中的堆叠挑战——详细中文总结

#### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：全切片图像分析被建模为多实例学习问题。但因每个“包”中实例数量不一致（非堆叠数据），现有MIL方法无法将不同长度的包堆叠成批次，只能逐个顺序处理，导致（1）GPU并行效率极低，训练时间过长；（2）单包梯度估计不稳定，模型收敛困难。
- **整体含义**：本文首次提出能实现**无损MIL数据堆叠**的框架，将分布式计算、梯度堆叠与模型-梯度联合压缩相结合，在不改变模型架构的前提下，同时提升训练速度和分类精度，为大规模病理切片弱监督学习提供了高效解决方案。

#### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：  
  利用分布式并行计算，将变长的包分配到多个子模型上并行计算梯度，然后在主服务器上对梯度求平均，模拟传统批处理堆叠的效果，从而绕过数据堆叠的物理限制。
- **关键技术细节**：
  - **分布式并行梯度堆叠（DPGS）**：  
    - 将模型参数复制到P个子进程，每个子进程处理一个包（含变长实例），独立计算损失和梯度。  
    - 子进程将梯度发送给主服务器，不清除本地模型状态。  
    - 主服务器对所有子进程的梯度求平均（堆叠函数S），更新全局参数，再广播给所有子进程。  
    - 数学上证明：若损失函数为均值，DPGS得到的平均梯度与将多个包直接堆叠为小批量得到的梯度完全等价（公式(5)-(8)），因此DPGS是**无损**的。
  - **深度模型-梯度压缩（DMGC）**：  
    - 在DGC（Deep Gradient Compression）基础上改进：不仅对梯度做top-k稀疏化，还对模型权重增量（即每次更新的变化量）进行压缩。  
    - 每个子进程维护本地残差，只有超过阈值的梯度被传输，其余积累到下一次。  
    - “虚拟批次”效应：经过T次本地积累后，等效于使用了T倍大的批次，学习率自动遵循线性缩放规则（公式(10)）。  
    - 通信量减少99.2%（在99.99%丢弃率下仍保持收敛）。
  - **算法流程**（Algorithm 1）：  
    - 训练服务器循环：解压模型增量 → 更新全局θ → 对每个子进程：取子集、计算梯度、加残差、top-k掩码、裁剪、压缩、发送梯度到主服务器。  
    - 主服务器循环：接收并解压各子进程梯度 → 平均 → 更新θ → 计算θ增量并压缩 → 广播给所有训练服务器。

#### 3. 实验设计：数据集、基准、对比方法
- **数据集**：
  - **Camelyon16**：两个特征版本：多尺度特征（实例特征长度512）和ImageNet预训练特征（256）。训练集160包，测试集239包（官方划分）。
  - **TCGA-Lung**：两个特征版本：多尺度特征（1024）和UNI2提取特征（1536）。训练534包，测试512包（随机8:2划分）。
- **基准方法**：  
  - 经典MIL：ABMIL、MeanMIL、TransMIL、CLAM-MB、ACMIL、RRTMIL。  
  - 两种传统堆叠策略：**Padding**（零填充对齐长度）、**Sampling**（随机选取固定数量实例）。
  - 基线模式：无DPGS（单GPU顺序训练） vs 带DPGS+DMGC。
- **对比指标**：准确率（%）和收敛时间（秒），收敛定义为总损失低于所有试验的95分位值。

#### 4. 资源与算力
- **明确说明**：实验使用 **4个节点，每个节点4×NVIDIA V100 GPU（32GB）**，网络带宽 **1000 Mbps**（压缩实验中使用20Mbps、10Mbps等受限带宽）。  
- 非并行基线使用**单GPU**；DPGS+DMGC使用4个节点（4GPU / 单节点多进程亦可）。  
- 未说明整体训练总时长或总GPU小时数，但给出了各方法收敛时间数值（秒级）。

#### 5. 实验数量与充分性
- **实验组数丰富**：  
  - 4个数据集变体（Camelyon16×2, TCGA-Lung×2）× 6种经典MIL方法 × 3种堆叠策略（Pad/Sampling/DPGS） + 消融实验 + 带宽影响实验 + 丢弃率实验 + 节点扩展实验 + 单vs多节点对比 → 合计超过50个实验配置。  
  - 消融实验：对比DMGC vs DGC vs 无压缩（表5）。  
  - 带宽影响：6种带宽下分别测试无压缩、DGC、DMGC（图5）。  
  - 丢弃率影响：从0.01%到100%共13个丢弃率（表6）。  
  - 节点数扩展：K=1~8，不同丢弃率（图3）。  
  - 单机多进程vs多机多GPU（表4）。
- **充分性评价**：实验设计较为全面，覆盖了不同特征提取器、不同数据集规模、不同模型架构、不同堆叠策略、不同压缩方法、不同网络带宽以及不同节点数，消融和对比充分。但所有实验仅在两个公开数据集上进行，缺乏更多癌症类型或更大规模数据验证。

#### 6. 论文的主要结论与发现
- **DPGS+DMGC显著优于所有基线**：  
  - 训练速度提升最高31倍（ABMIL on TCGA-Lung Multiscale：636.3s → 20.0s）。  
  - 准确率提升最高9.3%（MeanMIL on Camelyon16 Multiscale：61.71% → 71.33%）。  
  - 通信量减少99.2%，且在高丢弃率（99.99%）下仍保持收敛。  
- **DPGS可应用于单机多进程**（表4），无需多GPU，且内存内通信效率更高。  
- **最优批次大小存在折中**（图4）：过大或过小均导致性能下降，且与数据集复杂度相关。  
- **DMGC在低带宽下优势更突出**（图5）：相比DGC加速平均1.73倍，相比无压缩加速3.08倍。

#### 7. 优点
- **方法原创性**：首次提出通过梯度堆叠而非数据堆叠解决MIL的变长问题，思路新颖，且数学上证明等价性。  
- **通用性强**：不改变任何MIL模型结构，可即插即用于现有方法（ABMIL、TransMIL等），适应性强。  
- **双重效率提升**：既加速训练（并行+压缩），又提高精度（更稳定的梯度估计）。  
- **压缩策略优化**：DMGC联合压缩梯度和模型参数增量，在极端丢弃率下仍保持收敛，通信减少幅度大。  
- **实验设计全面**：覆盖多种数据集、特征、模型、堆叠策略、带宽和节点规模，消融实验完整。

#### 8. 不足与局限
- **实验覆盖有限**：仅使用Camelyon16和TCGA-Lung两个公开数据集，缺少更多癌症类型（如乳腺癌、结直肠癌）或更大规模WSI数据集验证。  
- **同步通信开销**：文中指出同步梯度聚合仍会限制GPU利用率，尤其在节点数超过4时效率进入平台期（图3）。未来需探索异步分布式方案。  
- **未讨论模型性能上限**：未与全监督方法或更强的前沿MIL方法（如MIL-VT、WSI-Transformer）对比，仅与经典ABMIL、TransMIL等对比。  
- **收敛时间定义**：基于损失下降至95分位，可能受初始化和随机性影响，不够标准化。  
- **压缩稀疏性影响**：高丢弃率下虽保持收敛，但训练时间反而增加（表6中0.01%丢弃率耗时5256s vs 1%丢弃率355s），说明极端压缩可能增加迭代次数，实际收益需权衡。  
- **无开源代码或复现细节**：论文未提供代码链接，可复现性存疑。

（完）
