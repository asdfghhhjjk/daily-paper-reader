---
title: "CellFlux: Simulating Cellular Morphology Changes via Flow Matching"
title_zh: "CellFlux: 通过流匹配模拟细胞形态变化"
authors: "Yuhui Zhang, Yuchang Su, Chenyu Wang, Tianhong Li, Zoe Wefers, Jeffrey J Nirschl, James Burgess, Daisy Ding, Alejandro Lozano, Emma Lundberg, Serena Yeung-Levy"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=3NLNmdheIi"
tags: ["query:pathology-ai"]
score: 6.0
evidence: 模拟细胞形态变化的生成模型
tldr: CellFlux利用流匹配生成受化学和基因扰动影响的细胞形态变化图像，有效区分实际扰动效应与实验批次效应。模型在多个扰动数据集上生成了生物学上有意义的细胞图像，为细胞形态学参数分析提供了合成数据生成工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1773, \"height\": 674, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 463, \"height\": 288, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1768, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1755, \"height\": 983, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1771, \"height\": 766, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 538, \"height\": 320, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 788, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1308, \"height\": 1750, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1315, \"height\": 1840, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1306, \"height\": 1795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1743, \"height\": 1672, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1741, \"height\": 1646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3nlnmdheii/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1766, \"height\": 894, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-3nlnmdheii/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1772, \"height\": 616, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3nlnmdheii/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1692, \"height\": 1149, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3nlnmdheii/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 732, \"height\": 1490, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3nlnmdheii/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1686, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3nlnmdheii/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1602, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3nlnmdheii/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1348, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3nlnmdheii/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 875, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3nlnmdheii/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1582, \"height\": 383, \"label\": \"Table\"}]"
motivation: 构建能够准确模拟细胞行为的虚拟细胞是计算生物学的长期目标。
method: 提出基于流匹配的图像生成模型，建模未扰动到扰动状态的分布变换。
result: 在三个扰动数据集上生成忠实于扰动特异性形态变化的细胞图像。
conclusion: CellFlux为细胞形态学模拟提供了有效工具，可助力形态参数分析。
---

## Abstract
Building a virtual cell capable of accurately simulating cellular behaviors in silico has long been a dream in computational biology. We introduce CellFlux, an image-generative model that simulates cellular morphology changes induced by chemical and genetic perturbations using flow matching. Unlike prior methods, CellFlux models distribution-wise transformations from unperturbed to perturbed cell states, effectively distinguishing actual perturbation effects from experimental artifacts such as batch effects—a major challenge in biological data. Evaluated on chemical (BBBC021), genetic (RxRx1), and combined perturbation (JUMP) datasets, CellFlux generates biologically meaningful cell images that faithfully capture perturbation-specific morphological changes, achieving a 35% improvement in FID scores and a 12% increase in mode-of-action prediction accuracy over existing methods. Additionally, CellFlux enables continuous interpolation between cellular states, providing a potential tool for studying perturbation dynamics. These capabilities mark a significant step toward realizing virtual cell modeling for biomedical research. Project page: https://yuhui-zh15.github.io/CellFlux/.

---

## 论文详细总结（自动生成）

# 论文结构化总结：CellFlux: Simulating Cellular Morphology Changes via Flow Matching

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：构建一个能够在计算机中准确模拟细胞行为的“虚拟细胞”（virtual cell），特别是预测细胞在化学药物或基因扰动下的形态变化，从而加速药物发现、个性化医疗和基础细胞生物学研究。
- **背景与动机**：
  - 计算生物学长期追求虚拟细胞，希望快速预测新化合物或基因修饰的细胞响应，减少实验成本和时间。
  - 大规模高内涵筛选实验已生成海量细胞图像数据（TB/PB级别），但存在**批次效应**等系统性偏差，使真实扰动效应与实验伪影混淆。
  - 现有生成模型（如基于GAN、扩散模型的方法）要么忽略对照（control）细胞图像，要么使用次优的分布变换方式（如扩散模型中先加噪声再生成），无法有效分离批次效应，也缺乏对扰动态之间连续变化的能力。
- **研究含义**：提出一种新的方法CellFlux，利用流匹配（flow matching）直接从对照分布到扰动分布进行变换，显著提升生成图像质量与生物学保真度，并为研究扰动动态提供了新工具。

## 2. 论文提出的方法论

### 核心思想
- 将细胞形态预测建模为**分布到分布**的映射问题：源分布为同一批次中未扰动（对照）细胞的图像分布，目标分布为施加特定扰动（化学/基因）后的细胞图像分布。
- 利用**流匹配**（Flow Matching）学习一个连续的速度场（velocity field），通过求解常微分方程（ODE）将源分布平滑地转换为目标分布。
- 相比于其他方法（如GAN需要额外组件、扩散模型使用噪声-图像双阶段映射），流匹配天然适合进行分布间直接、可逆的连续变换。

### 关键技术细节
- **条件流匹配**：在速度场中纳入扰动条件 \(c\)，学习条件速度场 \(v_\theta(x_t, t, c)\)，使变换针对特定扰动。
- **噪声增强**：以概率 \(p_e\) 向源样本添加高斯噪声，防止过拟合，使速度场更平滑。
- **无分类器引导**（Classifier-Free Guidance, CFG）：训练时随机丢弃条件 \(c\)，推理时通过插值条件/无条件预测增强生成保真度。
- **神经网络架构**：使用U-Net实现速度场，时间 \(t\) 用傅立叶特征编码，扰动条件 \(c\) 通过可学习嵌入网络注入U-Net各层。

### 算法流程（文字说明）
- **训练**：
  1. 从对照分布 \(p_0\) 采样 \(x_0\)，从扰动分布 \(p_1(\cdot|c)\) 采样 \(x_1\)，采样时间 \(t \sim U[0,1]\)。
  2. 线性插值得到中间状态 \(x_t = (1-t)x_0 + t x_1\)，真实速度 \(v = x_1 - x_0\)。
  3. 对 \(x_0\) 以概率 \(p_e\) 添加噪声，以概率 \(p_c\) 丢弃条件。
  4. 优化损失 \(\|v_\theta(x_t, t, c) - (x_1 - x_0)\|_2^2\)。
- **推理**：
  1. 给定对照图像 \(x_0\) 和扰动条件 \(c\)。
  2. 使用CFG计算速度：\(v_\theta^{CFG} = \alpha v_\theta(x_t, t, c) + (1-\alpha)v_\theta(x_t, t, \emptyset)\)。
  3. 从 \(t=0\) 到 \(1\) 逐步更新 \(x_t \leftarrow x_t + \Delta t \cdot v_\theta^{CFG}\)，最终得到预测的扰动图像 \(x_1\)。

## 3. 实验设计

### 数据集
- **BBBC021**: 化学扰动数据集，MCF-7乳腺癌细胞，含26种扰动（对应113个化合物及多种浓度），共98K图像，3通道（DNA、F-actin、beta-tubulin）。
- **RxRx1**: 基因扰动数据集（CRISPR敲除），HUVEC细胞，含1,042种基因扰动，共171K图像，6通道。
- **JUMP (CPJUMP1)**: 化学+基因组合扰动，U2OS和A549细胞，含747种扰动，共424K图像，5通道。
- 所有图像均经预处理（照明校正、以细胞核为中心裁剪为96×96、过滤低质量图像）。

### 评测场景与指标
- **图像质量**：FID（Fréchet Inception Distance）、KID（Kernel Inception Distance），计算整体（overall）和每个扰动条件平均（conditional）的分数。
- **生物学保真度**：在BBBC021上训练MoA（Mode of Action）分类器，使用生成图像预测药物作用模式，评估准确率、宏F1和加权F1。
- **分布外（OOD）泛化**：在BBBC021上留出部分扰动（未在训练集中出现），测试生成能力和MoA预测。
- **批次效应校正**：比较使用同批次对照 vs 不同批次对照作为初始化的效果。
- **消融实验**：分别去掉条件、CFG、噪声增强三个组件，观察性能变化。
- **其他**：跨数据集迁移（将BBBC021训练的模型直接应用于RxRx1和JUMP）、CellProfiler特征（核大小）定量比较、插值轨迹可视化。

### 对比方法
- **PhenDiff** (MICCAI'24)：基于扩散模型，先将对照图像映射到噪声再生成目标图像。
- **IMPA** (Nature Communications'25)：基于GAN，使用AdaIN层将对照图像风格样式迁移到目标。
- **MorphoDiff** (ICLR'25)：扩散模型但未使用对照图像（额外比较）。
- 均为公开有代码的方法，且只有前两者使用了对照图像（与CellFlux设定一致）。

## 4. 资源与算力
- **GPU**：4块 NVIDIA A100 GPU。
- **训练时长**：
  - BBBC021：约8小时（100 epochs）。
  - RxRx1：约16小时（100 epochs）。
  - JUMP：约36小时（100 epochs）。
- **批次大小**：128。
- **学习率**：1e-4，使用Adam优化器。

## 5. 实验数量与充分性
- **实验数量**：至少包括3个数据集主实验（每个数据集多个指标）、OOD泛化实验（8种未见过扰动）、Batch effect定量研究、消融实验（3个变体）、跨数据集迁移定性展示、CellProfiler核大小比较（3种扰动）、MoA分类实验、插值轨迹可视化。
- **充分性与公平性**：
  - 对比了两种最相关的基线，复现其官方代码，在相同数据预处理和评估协议下测试。
  - 使用多种指标（FID/KID/MoA分类/CellProfiler特征）从分布距离和生物学语义两方面评估，避免单一指标偏差。
  - 消融实验验证了各组件贡献。
  - 考虑了实际应用中重要的OOD和批次效应问题。
  - 评估了不同样本数量下FID/KID的稳定性（附录表5）。
  - 总体上实验设计全面，条件控制较好。

## 6. 论文的主要结论与发现
1. CellFlux在图像质量（FID/KID）上全面超越现有方法，改善幅度达21%~45%，在三个数据集上始终最优（BBBC021 FID: 18.7, RxRx1 FID: 33.0, JUMP FID: 9.0）。
2. 生成图像能准确反映扰动的生物学效应，MoA精度71.2%，接近真实图像（72.4%），比最佳基线（63.7%）提升12%。
3. 具备良好的分布外泛化能力，对未见过化合物仍能生成合理形态，MoA准确率43.2%远高于基线（16.0%）。
4. 通过条件于同批次对照，有效消除批次效应，同批次初始化相比不同批次在条件FID和MoA上分别改善14%和48%。
5. 流匹配的可逆性使双向插值成为可能，能生成从对照到扰动及反向的连续变化序列，为动态响应研究提供潜在工具。
6. 跨数据集迁移实验表明模型具有一定基础性，可在不同细胞类型和扰动集上零样本应用。

## 7. 优点
- **问题建模新颖**：将形态预测视为分布到分布的映射，并采用流匹配这一自然解决方案，优于GAN/扩散模型中加噪声或AdaIN等间接方式。
- **对照图像的充分利用**：通过条件于同一批次的对照细胞，有效分离真实扰动效应与批次效应，这在现有工作中常被忽视。
- **多维度评估**：不仅用FID/KID衡量图像质量，还通过MoA分类、CellProfiler特征分析检验生物学语义，评估维度丰富。
- **可解释性与可操作性**：连续速度场支持双向插值和批效应校正，为研究人员提供了可视化扰动轨迹和消除实验偏差的工具。
- **实验充分，消融清晰**：各组件（条件、CFG、噪声增强）均有消融证明其必要性。
- **开源且可复现**：提供项目页面、代码、预训练模型，推动领域发展。

## 8. 不足与局限
- **数据偏差**：仅使用了少数癌细胞系（MCF-7、HUVEC、U2OS、A549），可能无法代表正常生理或更多组织类型的细胞，存在欠覆盖风险。
- **插值轨迹的生物有效性未验证**：虽然模型能生成连续中间状态，但这些状态在实际生物学过程中是否存在尚缺乏实验证据（论文也承认这一局限，并给出未来验证方向如剂量插值、时间点插值）。
- **训练数据破坏性采样**：由于细胞固定染色是破坏性的，无法获得同一细胞扰动前后的配对样本，模型只能从分布级学习，可能丢失单细胞级别的精细信息。
- **性能与数据规模相关**：在RxRx1（基因扰动）上改善幅度较小（5-12%），作者归因于每类扰动图像数量少，说明模型对小样本扰动类别的泛化仍有改进空间。
- **算力需求**：训练需4×A100 (8~36小时)，对于更大规模数据集（如TB级）可能需要更多资源，限制了部分实验室的复现门槛。
- **仅支持像素空间建模**：当前直接在96×96像素上使用U-Net，未探索潜在空间（如autoencoder latent），可能限制了高分辨率或大规模图像的扩展性。
- **缺乏临床/体外验证**：MoA分类是在已有标签上训练的分类器，并未在真实生物学功能实验中进行验证，因此生成的图像能否真正反映细胞生理变化仍需进一步确认。

（完）
