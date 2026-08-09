---
title: Histopathology-Genomics Multi-modal Structural Representation Learning for Data-Efficient Precision Oncology
title_zh: 组织病理学-基因组学多模态结构表示学习用于数据高效精准肿瘤学
authors: "Kun Wu, Zhiguo Jiang, Xinyu Zhu, Jun Shi, Yushan Zheng"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=24QX6XpvSL"
tags: ["query:cellseg"]
score: 7.0
evidence: 通过结构表示学习融合组织病理学与基因组学，间接利用细胞级信息进行癌症诊断。
tldr: 针对精准肿瘤学中基因组数据常缺失的问题，MSRL框架利用诊断相关病例的真实基因组数据，通过多模态结构表示学习建立病例间关系，仅凭组织病理学图像即可实现数据高效推理。该方法在不降低预测精度的前提下减少了对基因组数据的依赖，推动了计算病理学在临床场景中的应用。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 基因组数据获取困难，现有方法忽视病例间结构关系，无法利用已知基因组。
method: 提出多模态结构表示学习框架MSRL，建模病例间关系以增强推理。
result: 在基因组缺失情况下，仅使用组织病理图像即可实现高效预测。
conclusion: 多模态结构学习为数据受限的精准肿瘤学提供了有效方案。
---

## Abstract
Fusing histopathology images and genomics data with deep learning has significantly advanced precision oncology. However, genomics data is often missing due to its high acquisition cost and complexity in real-world clinical scenarios. Existing solutions aim to reconstruct genomics data from histopathology images. Nevertheless, these methods typically relied only on individual case and overlooked the potential relationships among cases. Additionally, they failed to take advantage of the authentic genomics data of diagnostically related cases that are accessible from training for inference. In this work, we propose a novel Multi-modal Structural Representation Learning (MSRL) framework for data-efficient precision oncology. We pre-train a histopathology-genomics multi-modal representation graph adopting Graph Structure Learning (GSL) to construct inter-case relevance based on the data inherently. During the fine-tuning stage, we dynamically capture structural relevance between the training cases and the acquired authentic cases for precise prediction. MSRL leverages prior inter-case associations and authentic genomics data from diagnosed cases based on the graph, which contributes to effective inference based on the single histopathology image modality. We evaluated MSRL on public TCGA datasets with 7,263 cases across various tasks, including survival prediction, cancer grading, and gene mutation prediction. The results demonstrate that MSRL significantly outperforms existing missing-genomics generation approaches with improvements of 1.44% to 3.12% in C-Index on survival prediction tasks and achieves comparable performance to multi-modal fusion methods. The code and data are available at https://github.com/WkEEn/MSRL.

---

## 论文详细总结（自动生成）

# 论文详细总结：组织病理学-基因组学多模态结构表示学习用于数据高效精准肿瘤学

## 1. 论文的核心问题与整体含义
*   **核心问题**：在精准肿瘤学中，深度学习需要同时利用组织病理学图像和基因组学数据进行多模态建模，以提升诊断与预测性能。然而，在真实临床场景中，基因组测序成本高、流程复杂，数据经常缺失。
*   **现有方法的局限**：
    *   目前的主流方法是试图从组织病理图像直接“重建”或“生成”缺失的基因组特征。
    *   这些方法仅关注单个病例，忽视了不同病例之间潜在的关联（例如，同一癌症亚型或相似形态模式的病例可能存在相关基因突变）。
    *   它们未能有效利用训练集中那些已知基因组数据的“诊断相关病例”，这些病例的真实基因组信息其实是可以获取并用于辅助缺失病例推理的。
*   **整体含义**：本文提出了一种从“病例间结构关系”切入的新思路，旨在即使用户只有单张组织病理图像也能实现高效、精准的推断，从而在基因组数据普遍缺失的临床场景中，将多模态融合的优势落地应用。

## 2. 论文提出的方法论
*   **整体框架**：名为 **MSRL**（Multi-modal Structural Representation Learning，多模态结构表示学习）。
*   **核心思想**：不是去重建基因组，而是构建一个包含组织病理与基因组两个模态的“病例表示图”，显式建模病例与病例之间的关联结构，并在推理时利用图中已知基因组病例的真实信息来增强对未知（仅图像）病例的预测。
*   **关键流程与算法细节**：
    *   **预训练阶段（图结构学习）**：
        *   采用 **图结构学习** 技术，基于数据本身固有的病例相似性（如图像形态、临床特征等）动态构建**多模态表示图**。
        *   在该图上同时学习每个病例的组织病理表示和基因组表示，并让两种表示在结构空间中对齐，形成可迁移的病例间关联模式。
    *   **微调/推理阶段（动态结构捕捉）**：
        *   对于缺失基因组的测试病例，算法会动态捕捉该病例与训练集中“已知真实基因组”的病例之间的**结构相关性**。
        *   利用这些真实基因组病例在图中传递的信息，结合测试病例自身的组织病理图像表示，进行**基于单一图像模态的精准预测**（如生存分析、基因突变判定）。
    *   **公式与算法文字说明**：论文未在给出的摘要中提供具体公式，但整体流程可概括为：先用图学习建立“病例-病例”关联图 → 在图网络上融合并传播真实基因组信息 → 解码时仅依赖单模态图像+图中传播的邻域基因组隐性信息，得到最终预测结果。

## 3. 实验设计
*   **数据集**：使用公开数据集 **TCGA**（The Cancer Genome Atlas），包含 **7,263** 例样本，覆盖多种癌症类型。
*   **评估场景/任务**：
    *   生存预测（Survival Prediction）
    *   癌症分级（Cancer Grading）
    *   基因突变预测（Gene Mutation Prediction）
*   **Benchmark 与对比方法**：
    *   **主要对比**：现有的“缺失基因组生成/重建”类方法（即那些试图从图像直接合成基因组特征的方法）。
    *   **上界对比**：标准的“多模态融合”方法（同时使用图像和完整基因组，代表理想状态下的性能上限）。

## 4. 资源与算力
*   **明确说明**：论文提取文本（仅包含摘要与元数据）中**未明确提及其他算力细节**，例如 GPU 型号、单卡/多卡数量、具体训练时长、显存消耗等信息均未涵盖。需要查阅完整论文才能获取。

## 5. 实验数量与充分性
*   **实验规模**：在 7,263 例的大规模 TCGA 数据集上进行了验证，样本量较大。
*   **任务多样性**：至少覆盖了 3 种典型的肿瘤学下游任务（生存、分级、突变），评估维度比较全面。
*   **对比公平性**：不仅与同类“缺失处理”方法对比，还与“全模态”方法进行了对比，展示了模型在仅用单模态图像时接近多模态融合的性能，验证思路较为客观。
*   **可能不足（基于当前摘要）**：摘要中未提及消融实验（如去除图结构学习、去除预先真实基因组利用等模块的影响），也未表现跨数据集的外部验证。因此，无法从当前文本判断其内部模块的贡献度以及泛化能力的充分验证情况。

## 6. 论文的主要结论与发现
*   在基因组缺失的条件下，MSRL 仅使用组织病理图像就可实现高效推理。
*   **性能提升**：在生存预测任务上，MSRL 的 C-Index 指标比现有的缺失基因组生成方法**提升了 1.44% 至 3.12%**。
*   **与上界的距离**：即使在极端缺失场景下，MSRL 的性能可以达到与同时使用完整图像和真实基因组的多模态融合方法**相当**的水平。
*   **最终结论**：利用诊断相关病例的真实基因组数据构建病例间结构关系，是一种有效且数据高效的精肿瘤学多模态学习方案，能显著降低临床对基因组测试的硬性依赖。

## 7. 优点：方法或实验设计上的亮点
*   **视角新颖**：跳出“生成缺失模态”的传统框架，转而利用“病例间结构关系”传递已知信息，构思巧妙。
*   **信息利用率高**：没有放弃训练集中可用的真实基因组数据，通过图结构让它们在推理阶段为其他病例提供“知识背景”，最大化现有诊断数据的价值。
*   **临床实用性强**：最终可以在纯单模态（仅病理切片）条件下工作，并保持接近全模态的性能，极大利于在基因组数据稀缺的一线临床环境中落地。
*   **开源可复现**：论文提供了代码与数据链接，便于后续研究的验证与扩展。

## 8. 不足与局限
*   **算力信息缺失**：当前摘要未提及训练所需的资源开销，对于评估方法的部署复杂度构成障碍。
*   **对已知病例库的依赖**：推理需要依赖训练库中诊断明确、基因组已知的病例构建的图结构，若遇到训练库中未覆盖的新发罕见癌症或变异类型，性能可能会受限。
*   **图构建的泛化风险**：图结构是在现有数据集上学习的，当迁移到不同来源的、扫描协议不同的病理图像时，病例间关联的准确性可能下降，摘要未展示跨中心验证结果。
*   **消融与敏感性未知**：目前信息无法判断图结构学习各组件的重要性，也不清楚对已知基因组病例数量的敏感性（例如，已知病例较少时性能下降多少）。

（完）
