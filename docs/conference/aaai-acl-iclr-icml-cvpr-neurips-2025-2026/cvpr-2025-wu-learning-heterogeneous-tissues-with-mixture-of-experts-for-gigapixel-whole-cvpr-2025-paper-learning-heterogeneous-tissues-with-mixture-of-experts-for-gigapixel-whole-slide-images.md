---
title: Learning Heterogeneous Tissues with Mixture of Experts for Gigapixel Whole Slide Images
title_zh: 用专家混合模型学习千兆像素全切片图像中的异质组织
authors: "Wu, Junxian, Chen, Minheng, Ke, Xinyi, Xun, Tianwang, Jiang, Xiaoming, Zhou, Hongyu, Shao, Lizhi, Kong, Youyong"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wu_Learning_Heterogeneous_Tissues_with_Mixture_of_Experts_for_Gigapixel_Whole_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 8.0
evidence: 利用病理感知的专家混合模型学习千兆像素全切片图像中的异质组织
tldr: 该论文针对全切片图像分析中组织环境复杂且缺乏领域知识注入的问题，提出即插即用的病理感知专家混合模块PAMoE。通过将不同组织区域路由到对应的专家网络，模型自动成为瘤内各组织的专家，从而提取更具判别力的特征。实验表明，PAMoE在多类下游任务上有效提升性能，且无需额外推理步骤，具有良好的扩展性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 759}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 837, \"height\": 833}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1498, \"height\": 820}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1472, \"height\": 996}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 694, \"height\": 554}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1802, \"height\": 659}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1797, \"height\": 373}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1797, \"height\": 246}]"
motivation: 全切片组织环境复杂，需要病理先验知识来引导模型分析。
method: 提出PAMoE模块，基于专家混合思想学习不同组织区域的特征。
result: 在多个下游任务上取得性能提升，且易于集成。
conclusion: 病理感知的专家混合能有效提取全切片图像中的组织知识。
---

## Abstract
Analyzing gigapixel Whole Slide Images (WSIs) is challenging due to the complex pathological tissue environment and the absence of target-driven domain knowledge. Previous methods incorporated pathological priors to mitigate this issue but relied on additional inference steps and specialized workflows, restricting scalability and the model's capacity to identify novel outcome-related factors. To address these challenges, we propose a plug-and-play Pathology-Aware Mixture-of-Experts (PAMoE) module, which based on mixture of experts to learn pathology-related knowledge and extract useful information. We train the experts to become 'specialists' in specific intratumoral tissues by learning to route each tissue to its mapped expert. In addition, to reduce the impact of irrelevant content on the model, we introduce a new routing rule that discards patches in which none of the experts express interest, which helps the model better capture the relationships between relevant patches. Through a comprehensive evaluation of PAMoE on survival task, we demonstrate that 1) Our module enhances the performance of baseline models in most cases, and 2) The sparse expert processing across different tissues enhances the learning of patch representations by addressing tissue heterogeneity.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **核心问题**：千兆像素（Gigapixel）全切片图像（WSI）分析面临两大挑战：
  1. 病理组织环境高度异质，包含多种瘤内组织（如肿瘤上皮、间质、免疫浸润、坏死等），这些组织及其交互对预后等“全景式”任务至关重要。
  2. 现有方法通常依赖额外的病理先验（如聚类原型、预训练分类器），需要专门的工作流和额外推理步骤，限制了可扩展性，且模型可能受限于固定先验，难以发现新的预后相关因素。
- **研究动机**：设计一种无需额外先验推理、可端到端学习组织异质性的即插即用模块，同时保留发现未知因素的能力。
- **含义**：提出一个基于混合专家（Mixture-of-Experts, MoE）的组件，通过可训练的路由机制自主识别并处理不同组织类型的图像块（patch），过滤噪声和无关信息，提升WSI分析性能。

### 2. 论文提出的方法论

- **核心思想**：将MoE引入WSI多实例学习（MIL）框架，使多个“专家”网络各自成为特定瘤内组织的“专业处理单元”，并通过 **Expert Choice Routing** 让专家主动选择感兴趣的图像块，未被选中的块视为噪声丢弃。
- **关键技术细节**：
  - **MoE via Expert Choice Routing**：
    - 不同于传统MoE给每个输入分配专家，此模块让每个专家从输入块中独立选择 top-\( k \) 个块进行处理。
    - 设置容量因子 \( c \)，专家选择数 \( k = \frac{n \times c}{m} \)（\( n \) 为块总数，\( m \) 为专家数）。
    - 路由网络 \( g(\cdot) \) 输出分配概率 \( S \in \mathbb{R}^{m \times n} \)，专家按行取 top-\( k \) 索引，再对列做softmax得到归一化概率 \( \tilde{S} \)。
    - 输出为专家处理后结果的加权求和，未被选中的块输出为零特征并被后处理移除。
  - **病理感知监督（PAMoE核心）**：
    - 专家分为两类：**Prior Supervised Experts**（受病理先验原型监督）和 **Free Experts**（无监督，自由学习未知因素）。
    - **原型预提取**：使用预训练基础模型 CONCH 作为分类器，为数据集中采样子集标记瘤内组织类别（肿瘤、间质、免疫浸润、坏死），计算各类别所有块特征的均值作为原型 \( P \)。
    - **专家选择监督**：对监督类专家，计算输入块特征与原型之间的余弦相似度并做 softmax，得到先验选择概率 \( prob_\omega \)；与专家实际路由归一化概率 \( s_\omega \) 计算交叉熵损失 \( \mathcal{L}_{PAMoE} \)。
    - 总损失 \( \mathcal{L} = \mathcal{L}_{task} + \alpha \mathcal{L}_{PAMoE} \)，引导专家关注特定组织。
  - **即插即用集成**：PAMoE 层可替换 Transformer 或图网络中的全连接层，文中以 TransMIL、LongViT、PatchGCN 为例进行集成。
- **公式/流程**（文字说明）：
  1. 预提取原型：WSI集合 → 切块 → 编码 → 随机采样 → CONCH分类 → 选4类组织 → 计算类别均值原型。
  2. 训练时：输入块特征 → 路由网络得到分配概率 → 专家选 top-\( k \) → 归一化 → 加权输出；同时用原型损失监督监督类专家的选择。
  3. 推理时：端到端，无需额外分类器或聚类步骤。

### 3. 实验设计

- **数据集/场景**：
  - 5个TCGA癌症数据集的生存预测任务：COAD（结直肠癌）、LGG（低级别胶质瘤）、LUAD（肺腺癌）、PAAD（胰腺癌）、BRCA（乳腺癌）。
  - 采用标准的五折交叉验证，评价指标为C指数（Concordance Index）。
- **对比方法**：
  - 经典MIL：ABMIL、AttnMISL。
  - 引入空间/先验的方法：CaMIL（Transformer+邻接矩阵）、PANTHER（原型引导聚合）、HEAT（异构图+组织先验）。
  - 基线集成方法：PatchGCN、TransMIL、LongViT，及其与PAMoE的组合。
  - 本文还对比了用固定余弦相似度分配（CSA层）替代MoE路由的变体。
- **Benchmark配置**：所有方法均使用UNI作为固定特征提取器，PANTHER和AttnMISL设定16个原型，确保公平。

### 4. 资源与算力

- 文中**未明确说明使用的GPU型号、数量及训练时长**。仅提到因硬件限制未探索PAMoE在大规模模型上的表现，未给出计算资源的具体描述。

### 5. 实验数量与充分性

- **主要实验**：
  - 5个数据集 × 9个方法（含集成变体）的生存预测对比实验。
  - 消融实验基于 TransMIL：
    - 专家数量与监督比例（m = 4, 6, 8；先验专家数0~4组合）。
    - 超参数 α 的影响（0, 0.001, 0.01, 0.1, 1）。
    - MoE架构必要性（PAMoE vs. CSA层 vs. 普通TransMIL）。
  - 可解释性可视化：专家选择热图与高分块展示。
  - 补充材料中包含更多消融实验（如路由方式、跳连与class token处理、原型获取方式、容量因子、丢弃比例、自由专家分析等）。
- **充分性与公平性**：
  - 对比了多种SOTA方法，采用相同特征提取器和五折交叉验证，较为公平。
  - 消融实验覆盖关键超参数和设计选择，数量较丰富。
  - 部分消融在正文中只呈现部分组合，但补充材料有延伸，整体较为充分。

### 6. 论文的主要结论与发现

1. PAMoE 模块能够有效提升多数Transformer基线的生存预测性能（C指数提升）。  
2. 基于Expert Choice Routing的MoE可自然过滤噪声块，缓解MIL中无关信息干扰。  
3. 引入病理先验原型监督专家路由，使专家偏好与真实组织一致，增强了可解释性；同时保留自由专家有助于发现新模式。  
4. 性能提升主要归因于不同专家对块进行独特映射，扩展了隐空间，并通过Transformer的全局自注意力捕获更丰富的组织间交互。  
5. 对于PatchGCN等局部交互模型，PAMoE提升有限，原因可能是图网络仅建模近邻块的关系，限制了全局交互带来的增益。

### 7. 优点

- **即插即用**：可无缝集成至多种现有WSI分析模型，无需改动整体框架。
- **端到端且无需推理先验**：训练后推理阶段不依赖额外分类器或聚类，减少流程复杂度。
- **自然去噪**：专家选择机制自动丢弃无关块，适合WSI中大量背景和噪声的特点。
- **可解释性增强**：先验监督使专家显示出与组织类型一致的偏好，可视化结果清晰。
- **设计合理**：将专家分为监督与自由两类，平衡了领域知识注入与未知因素发现。
- **实验验证较全面**：涵盖五种癌种，多种基线，丰富的消融和可视化。

### 8. 不足与局限

- **算力信息缺失**：未报告所用GPU资源、训练时间，难以评估实际部署成本。
- **模型规模限制**：仅在较小模型上验证，未探索在大规模WSI模型或更多专家数量下的表现。
- **对非Transformer架构支持不足**：在PatchGCN上提升微弱，通用性受限。
- **原型依赖CONCH基础模型**：原型提取使用CONCH分类器，若该模型在某些组织类别上表现不佳，可能影响监督质量；虽然有替代方案讨论，但仍需依赖外部工具。
- **先验类别固定**：仅使用肿瘤、间质、免疫浸润、坏死四类，可能忽略其他重要组织成分（如血管、粘液等）。
- **超参数敏感**：容量因子 \( c \)、自由专家数、损失权重 \( \alpha \) 等需调节，文中虽做消融但未提供通用配置原则。
- **仅验证生存预测任务**：未在其他WSI任务（如分级、分型、治疗响应预测）上测试，任务泛化性待考。
- **实验集可能不够多样**：所有数据来自TCGA，外部验证缺乏，存在域偏移风险。
- **机制解释还可深化**：自由专家学到的具体模式未深入分析，其潜在价值未被充分挖掘。

（完）
