---
title: Learning Heterogeneous Tissues with Mixture of Experts for Gigapixel Whole Slide Images
title_zh: 利用专家混合模型学习异质性组织用于千兆像素全切片图像
authors: "Wu, Junxian, Chen, Minheng, Ke, Xinyi, Xun, Tianwang, Jiang, Xiaoming, Zhou, Hongyu, Shao, Lizhi, Kong, Youyong"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wu_Learning_Heterogeneous_Tissues_with_Mixture_of_Experts_for_Gigapixel_Whole_CVPR_2025_paper.pdf"
tags: ["query:cellseg"]
score: 7.0
evidence: 提出专家混合模型用于全切片图像分析，推进数字病理学
tldr: 针对千兆像素全切片图像分析中组织异质性和领域知识缺乏的挑战，提出病理感知专家混合模块PAMoE，通过门控机制将不同组织区域路由至对应专家，在无需额外先验的情况下学习组织特异性特征，在多个下游任务中展现出优于现有方法的性能，为可扩展的WSI分析提供了新范式，有望推动数字病理学中数据驱动的发现。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 759, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 837, \"height\": 833, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1498, \"height\": 820, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1472, \"height\": 996, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 694, \"height\": 554, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1802, \"height\": 659, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1797, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1797, \"height\": 246, \"label\": \"Table\"}]"
motivation: 千兆像素全切片图像分析缺乏目标驱动的领域知识引导。
method: 提出病理感知专家混合模块，将组织区域路由到特定专家学习。
result: 模型可学习组织异质性，识别新的预后相关因素，性能优越。
conclusion: 为WSI分析提供可插拔模块，提升模型可扩展性和可解释性。
---

## Abstract
Analyzing gigapixel Whole Slide Images (WSIs) is challenging due to the complex pathological tissue environment and the absence of target-driven domain knowledge. Previous methods incorporated pathological priors to mitigate this issue but relied on additional inference steps and specialized workflows, restricting scalability and the model's capacity to identify novel outcome-related factors. To address these challenges, we propose a plug-and-play Pathology-Aware Mixture-of-Experts (PAMoE) module, which based on mixture of experts to learn pathology-related knowledge and extract useful information. We train the experts to become 'specialists' in specific intratumoral tissues by learning to route each tissue to its mapped expert. In addition, to reduce the impact of irrelevant content on the model, we introduce a new routing rule that discards patches in which none of the experts express interest, which helps the model better capture the relationships between relevant patches. Through a comprehensive evaluation of PAMoE on survival task, we demonstrate that 1) Our module enhances the performance of baseline models in most cases, and 2) The sparse expert processing across different tissues enhances the learning of patch representations by addressing tissue heterogeneity.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：千兆像素全切片图像（WSI）分析面临两大挑战：
  - 复杂的病理组织环境（组织异质性，intratumoral heterogeneity）；
  - 缺乏与任务目标直接相关的领域知识引导。
- **现有方法局限**：先前工作（如 PANTHER、HEAT）通过引入病理先验（如聚类原型、组织分类器）来利用组织异质性，但依赖额外的推理步骤和专用工作流，限制了可扩展性以及模型发现新的预后相关因素的能力。
- **研究动机**：设计一种无需额外推理先验、可端到端学习并利用组织异质性的方法，从而更灵活地挖掘不同病理组织间的关系，提升 WSI 分析性能。

### 2. 论文提出的方法论
- **核心思想**：提出一种即插即用的**病理感知专家混合模块（PAMoE）**，基于 Mixture-of-Experts（MoE）架构，让不同专家“专精”于特定的瘤内组织类型，通过可训练的门控机制自动将组织块路由到对应专家，同时过滤与任务无关的噪声块。
- **关键技术细节**：
  - **专家选择路由（Expert Choice Routing）**：与传统 patch-选-expert 不同，PAMoE 让每个专家独立选择其感兴趣的 Top-k 个 patch，未被任何专家选中的 patch 被丢弃。这既解决了专家负载不平衡问题，又天然滤除了 MIL 流程中的无关实例。
  - **先验原型预提取**：利用预训练基础模型 CONCH 作为分类器，确定每个 patch 所属的瘤内组织类别（肿瘤、间质、免疫浸润、坏死、其他），并计算各类别实例的平均特征作为**先验原型**。
  - **专家选择的先验监督**：将 MoE 专家分为“先验监督专家”和“自由专家”。对先验监督专家，计算其选择概率与对应原型引导概率（余弦相似度经 softmax 归一化）之间的交叉熵损失 \(\mathcal{L}_{\text{PAMoE}}\)，引导专家偏好与病理先验一致。自由专家无监督约束，保留模型发现未知因素的能力。
  - **总损失**：\(\mathcal{L} = \mathcal{L}_{\text{task}} + \alpha \mathcal{L}_{\text{PAMoE}}\)，其中 \(\mathcal{L}_{\text{task}}\) 为下游任务（如生存预测）的损失，\(\alpha\) 为平衡超参数。
  - **模块集成**：PAMoE 可替换经典 WSI 分析方法（如 TransMIL、LongViT、PatchGCN）中的全连接层，作为即插即用组件。

### 3. 实验设计
- **任务与数据集**：在**生存预测**任务上验证，使用 5 个公开癌症数据集（COAD、LGG、LUAD、PAAD、BRCA），均来自 TCGA。
- **对比方法**：
  - 经典 MIL 方法：ABMIL、AttnMISL
  - Transformer 方法：CaMIL（含空间感知）
  - 引入先验的方法：PANTHER（原型引导）、HEAT（异质图+组织分类器）
  - 基线方法集成 PAMoE：PatchGCN+PAMoE、TransMIL+PAMoE、LongViT+PAMoE
- **统一设置**：所有方法均采用 UNI 作为实例特征编码器，相同 5 折交叉验证分割，评估指标为 C-index（均值±标准差）。

### 4. 资源与算力
- 论文正文和补充材料中**未明确提及**使用的 GPU 型号、数量或训练时长。仅声明因硬件限制未能在更大规模模型上探索 PAMoE。

### 5. 实验数量与充分性
- **主要实验组数**：
  - 与 5 种 SOTA 方法及 3 种基线的集成对比（表 1，共 8 个方法配置）。
  - 消融实验：
    - 专家数量与先验监督比例（表 2，3 种总数 × 3 种分配方式）。
    - MoE 架构的必要性对比（表 3，PAMoE vs. 余弦相似度分配 CSA）。
    - 损失超参数 α 的影响（图 5，5 个 α 值）。
    - 补充材料中包含更多消融：专家选择路由、跳跃连接与类别令牌处理、原型获取方式、使用 CONCH 作为编码器、容量因子、patch 丢弃比例分析、自由专家分析等。
- **实验充分性评价**：
  - 实验覆盖 5 种不同癌型，比较方法多样，消融维度丰富，能较全面验证模块的有效性。
  - 采用相同编码器、统一数据划分和指标，对比公平性较高。
  - 受限于硬件，未在更大型模型或更多样架构上测试，这是潜在的不足。

### 6. 论文的主要结论与发现
- **性能提升**：PAMoE 集成到基于 Transformer 的基线模型后，在大多数数据集上一致提升生存预测 C-index，且性能优于或相当 SOTA 方法。
- **有效性验证**：PAMoE 通过稀疏专家处理，有效应对组织异质性，增强了块表征学习；先验监督有助于专家形成与病理组织一致的偏好，自由专家则能探索新模式。
- **适用边界**：PAMoE 对基于 Transformer 的模型改进显著，但对以局部邻域交互为主的图网络模型（PatchGCN）提升有限。
- **可解释性**：专家热图可视化显示，监督专家能聚焦于对应的组织类型，自由专家偏好分散，表明模块可解释性和任务适应性。

### 7. 优点：方法或实验设计上的亮点
- **即插即用**：PAMoE 无需专用工作流，可轻松嵌入现有 MIL 模型（替换全连接层），具有良好通用性。
- **端到端学习**：训练中引入病理先验，但推断时无需额外先验信息或推理步骤，简化了预测流程。
- **噪声过滤机制**：专家选择路由天然丢弃无关 patch，有助于模型聚焦关键组织区域，减少噪声干扰。
- **专家解耦设计**：区分监督专家与自由专家，在利用先验的同时保留了模型发现新模式的灵活性。
- **实验全面**：在多个癌型上验证，涉及多种对比方法和消融设置，结果有说服力。
- **可解释性分析**：通过专家选择概率热图直观展示病理组织的路由偏好，增强模型透明度。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **架构适应局限**：对非 Transformer 架构（如图网络）的性能提升有限，未在更多样化架构上验证。
- **先验原型依赖外部模型**：原型提取依赖 CONCH 分类器，增加了前期计算开销；虽然讨论了替代方案，但默认设置仍引入额外模型。
- **参数敏感性**：容量因子 \(c\)、平衡系数 \(\alpha\)、专家总数和配比等超参数需针对不同任务调整，可能增加调参成本。
- **任务局限**：仅验证了生存预测任务，尚未在分类、分级等其他下游任务上测试。
- **算力限制未完全探索**：未进行大规模模型实验，限制了 MoE 在大参数场景下的潜力挖掘。
- **类别不平衡路由风险**：若某些病理组织类别样本极端稀少（如坏死），相应专家可能难以充分训练，文中未深入讨论。

（完）
