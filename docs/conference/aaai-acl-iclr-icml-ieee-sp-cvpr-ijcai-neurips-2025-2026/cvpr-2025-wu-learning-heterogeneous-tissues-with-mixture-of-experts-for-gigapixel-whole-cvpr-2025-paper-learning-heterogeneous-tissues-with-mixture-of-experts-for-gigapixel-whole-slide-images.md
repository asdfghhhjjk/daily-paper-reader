---
title: Learning Heterogeneous Tissues with Mixture of Experts for Gigapixel Whole Slide Images
title_zh: 用混合专家学习异质组织以处理千兆像素全切片图像
authors: "Wu, Junxian, Chen, Minheng, Ke, Xinyi, Xun, Tianwang, Jiang, Xiaoming, Zhou, Hongyu, Shao, Lizhi, Kong, Youyong"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wu_Learning_Heterogeneous_Tissues_with_Mixture_of_Experts_for_Gigapixel_Whole_CVPR_2025_paper.pdf"
tags: ["query:profile"]
score: 6.0
evidence: 提出MoE将组织区域路由到专家，实现WSI分析中的跨patch信息整合
tldr: 针对全切片图像中组织异质性和领域知识缺失的挑战，提出即插即用的病理感知混合专家模块PAMoE，通过将不同组织区域路由到多个专家网络，学习特定组织类型相关的病理知识。实验表明该方法能有效捕捉瘤内组织异质性，提升下游任务性能。该模块可灵活集成到现有框架，为利用跨patch信息进行WSI级任务提供了新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 759, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 837, \"height\": 833, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1498, \"height\": 820, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1472, \"height\": 996, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 694, \"height\": 554, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1802, \"height\": 659, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1797, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1797, \"height\": 246, \"label\": \"Table\"}]"
motivation: WSI分析面临复杂组织环境和领域知识缺失。
method: 提出病理感知的混合专家模块，学习将组织区域路由到专家。
result: 模型能有效捕捉组织异质性并提升预测性能。
conclusion: PAMoE为WSI分析提供了一种灵活有效的跨patch信息整合方案。
---

## Abstract
Analyzing gigapixel Whole Slide Images (WSIs) is challenging due to the complex pathological tissue environment and the absence of target-driven domain knowledge. Previous methods incorporated pathological priors to mitigate this issue but relied on additional inference steps and specialized workflows, restricting scalability and the model's capacity to identify novel outcome-related factors. To address these challenges, we propose a plug-and-play Pathology-Aware Mixture-of-Experts (PAMoE) module, which based on mixture of experts to learn pathology-related knowledge and extract useful information. We train the experts to become 'specialists' in specific intratumoral tissues by learning to route each tissue to its mapped expert. In addition, to reduce the impact of irrelevant content on the model, we introduce a new routing rule that discards patches in which none of the experts express interest, which helps the model better capture the relationships between relevant patches. Through a comprehensive evaluation of PAMoE on survival task, we demonstrate that 1) Our module enhances the performance of baseline models in most cases, and 2) The sparse expert processing across different tissues enhances the learning of patch representations by addressing tissue heterogeneity.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：在处理千兆像素的全切片图像（WSI）时，面临两大挑战：一是肿瘤内部存在高度异质性（即组织类型的多样性及其相互作用）；二是传统方法在利用病理先验知识时，需要额外且复杂的推理步骤和特定工作流程（如预分类、构建异构图），这限制了模型的可扩展性和发现未知预后特征的能力。
*   **整体含义**：该研究旨在设计一种端到端的、无需在推理阶段依赖额外先验知识的模块，能够自适应地学习、识别并处理WSI中的异质性组织区域，从而提升基于弱监督多实例学习（MIL）框架的病理图像分析性能。

### 2. 论文提出的方法论
*   **核心思想**：提出一个即插即用的“病理感知混合专家模块”（PAMoE），其核心是让不同“专家”网络专门负责处理特定类型的肿瘤内组织，并滤除与任务无关的背景区域。
*   **关键技术细节**：
    *   **基于专家选择的路由规则**：区别于传统为每个输入分配专家的方法，PAMoE让每个专家网络主动选择其“感兴趣”的patch。未被任何专家选中的patch将被直接丢弃，从而天然地滤除了噪声和无关组织。
    *   **专家路由的病理先验监督**：
        1.  **原型预提取**：利用预训练基础模型（CONCH）对数据集中的patch进行分类，提取出与预后高度相关的四种组织类别（肿瘤、基质、免疫浸润、坏死）的原型特征向量。
        2.  **专家分组与监督**：将专家分为“有监督先验专家”和“自由专家”。通过计算patch特征与组织原型之间的余弦相似度，获得每个patch属于各组织类别的概率，并以此监督“有监督先验专家”的patch选择偏好。保留“自由专家”是为了让模型能发现未知的、但与预后相关的模式。
        3.  **损失函数**：最终损失函数为任务相关损失（如Cox回归损失）与专家路由偏好监督损失（交叉熵损失）的加权和。
*   **公式与算法流程（文字说明）**：
    *   流程从使用基础模型提取所有WSI patch的特征开始。
    *   路由器网络计算每个patch对于所有专家的“被选择概率”得分。
    *   每个专家根据得分选择固定数量（由容量因子决定）的前K个patch。
    *   选定patch的最终输入特征是其原始特征经对应专家网络处理后，再根据归一化的被选择概率加权求和的结果。未被选中的patch特征被置零（后被移除）。

### 3. 实验设计
*   **数据集与场景**：实验基于癌症生存期预测任务，使用了来自癌症基因组图谱（TCGA）的五个不同癌种数据集：结肠腺癌（COAD）、低级别胶质瘤（LGG）、肺腺癌（LUAD）、胰腺腺癌（PAAD）、乳腺浸润癌（BRCA）。
*   **Benchmark方法**：
    *   **经典MIL方法**： ABMIL, AttnMISL。
    *   **利用组织先验的方法**：PANTHER (基于原型), HEAT (基于异构图)。
    *   **其他对比方法**：CaMIL (基于Transformer并具有空间感知能力)。
    *   **基线集成模型**：将PAMoE集成到TransMIL, LongViT (基于Transformer) 和 PatchGCN (基于图神经网络) 中进行对比。
*   **评估指标**：采用生存分析常用的一致性指数（C-index），并报告了5折交叉验证的均值和标准差。所有方法统一使用UNI作为patch特征编码器以保证公平。

### 4. 资源与算力
*   论文中**未明确说明**所使用的GPU型号、数量或具体的训练时长。

### 5. 实验数量与充分性
*   **实验数量**：论文进行了多组实验来评估PAMoE的有效性。
    *   **主实验**：在5个数据集上，将PAMoE集成到3种基线模型中的性能对比。
    *   **消融实验**：
        1.  专家数量与配比（4/6/8个专家，有监督专家从0到4个不等）。
        2.  Mixture-of-Experts（MoE）架构的必要性（对比了基于直接余弦相似度分配的CSA方法）。
        3.  先验损失函数权重 \(\alpha\) 的影响。
        4.  文中提及在补充材料中还有对路由方式、残差连接、原型获取方式等的进一步消融。
*   **充分性评估**：实验设计**较为充分和客观**。通过与多种先进方法对比、集成到不同架构的基线模型中、并在多个数据集上验证，有力地证明了方法的有效性。消融实验细致探讨了关键设计选择的影响，增强了结论的可靠性。

### 6. 论文的主要结论与发现
*   PAMoE作为一个即插即用模块，能在多种癌种的生存预测任务中，一致地提升基于Transformer的MIL基线模型的性能。
*   性能提升归因于PAMoE模型通过不同的专家以不同方式映射和组织patch，扩展了模型的潜在表示空间，并通过Transformer的全局自注意力机制更有效地捕捉全局组织间的交互。
*   可解释性分析证实，“有监督先验专家”成功学习到了与预定义组织类别高度一致的patch选择偏好，而“自由专家”则展现出更分散的偏好，倾向于探索新模式。

### 7. 优点
*   **即插即用性**：模块可无缝集成到现有的主流WSI分析框架中，无需改变其整体架构。
*   **端到端学习**：在推理阶段无需像以往方法那样依赖额外的分类器或聚类等先验工作流。
*   **显式处理异质性与噪声**：通过专家选择路由机制，直接识别并处理不同组织，同时有效丢弃无关背景，这是针对WSI分析痛点的创新设计。
*   **可解释性**：专家对特定组织类型的偏好提供了良好的可解释性，有助于理解模型的决策依据。

### 8. 不足与局限
*   **架构普适性有限**：实验证明PAMoE对Transformer架构提升显著，但对PatchGCN这类基于图神经网络、仅建模局部上下文交互的模型提升有限且不稳定。其优势的发挥依赖于长距离全局交互机制。
*   **依赖于额外分类器**：原型提取步骤需要依赖一个预训练的组织分类器（CONCH），这引入了额外的计算开销和对第三方模型的依赖（尽管文中在补充材料中讨论了替代方案）。
*   **实验场景单一**：所有实验仅基于生存预测这一个“全景”任务进行验证，未探讨在癌症分型（typing）、分级（grading）等其他关键预后任务上的表现。
*   **算力规模限制**：作者承认受限于硬件，未能在更大规模的模型上探索PAMoE的效果，其在大规模参数下的性能表现尚不明确。

（完）
