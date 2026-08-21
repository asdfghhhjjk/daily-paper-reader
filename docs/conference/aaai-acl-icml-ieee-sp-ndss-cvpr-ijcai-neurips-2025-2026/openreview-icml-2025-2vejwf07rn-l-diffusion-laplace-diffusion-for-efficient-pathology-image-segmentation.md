---
title: "L-Diffusion: Laplace Diffusion for Efficient Pathology Image Segmentation"
title_zh: L-Diffusion：用于高效病理图像分割的拉普拉斯扩散模型
authors: "Weihan Li, Linyun Zhou, YangJian, Shengxuming Zhang, Xiangtong Du, Xiuming Zhang, Jing Zhang, ChaoqingXu, Mingli Song, Zunlei Feng"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=2veJwf07RN"
tags: ["query:cell-graph"]
score: 6.0
evidence: "高效的扩散模型病理图像分割，可适用于H&E全切片细胞/细胞核分割"
tldr: "L-Diffusion针对病理图像分割中标注成本高和长尾类别识别困难的问题，提出基于拉普拉斯分布的扩散模型。该方法利用多个拉普拉斯分布替代高斯分布建模特征成分，增强特征空间分解。实验表明其能高效分割病理图像。该工作可作为H&E全切片图像中细胞或组织区域分割的基础工具。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 630}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1745, \"height\": 1026}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1764, \"height\": 452}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1693, \"height\": 1119}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1770, \"height\": 508}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1157, \"height\": 617}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1731, \"height\": 1695}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1591, \"height\": 2180}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1547, \"height\": 2154}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1653, \"height\": 2070}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1569, \"height\": 1651}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1777, \"height\": 718}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1777, \"height\": 718}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 850, \"height\": 252}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 836, \"height\": 261}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 850, \"height\": 227}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 851, \"height\": 178}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1205, \"height\": 264}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1544, \"height\": 689}]"
motivation: 病理图像分割受限于标注成本高和长尾分布导致的尾部类别识别不足。
method: 提出拉普拉斯扩散模型，用多个拉普拉斯分布建模不同特征成分。
result: 在病理图像分割上提高效率并改善尾部类别识别。
conclusion: 为病理图像分割提供高效新方法，可服务于细胞/组织区域提取。
---

## Abstract
Pathology image segmentation plays a pivotal role in artificial digital pathology diagnosis and treatment. Existing approaches to pathology image segmentation are hindered by labor-intensive annotation processes and limited accuracy in tail-class identification, primarily due to the long-tail distribution inherent in gigapixel pathology images. In this work, we introduce the Laplace Diffusion Model, referred to as L-Diffusion, an innovative framework tailored for efficient pathology image segmentation. L-Diffusion utilizes multiple Laplace distributions, as opposed to Gaussian distributions, to model distinct components—a methodology supported by theoretical analysis that significantly enhances the decomposition of features within the feature space. A sequence of feature maps is initially generated through a series of diffusion steps. Following this, contrastive learning is employed to refine the pixel-wise vectors derived from the feature map sequence.  By utilizing these highly discriminative pixel-wise vectors, the segmentation module achieves a harmonious balance of precision and robustness with remarkable efficiency. Extensive experimental evaluations demonstrate that L-Diffusion attains improvements of up to  7.16\%,  26.74\%,  16.52\%, and  3.55\% on tissue segmentation datasets, and  20.09\%,  10.67\%,  14.42\%, and  10.41\% on cell segmentation datasets, as quantified by DICE, MPA, mIoU, and FwIoU metrics. The source are available at https://github.com/Lweihan/LDiffusion.

---

## 论文详细总结（自动生成）

# L-Diffusion：用于高效病理图像分割的拉普拉斯扩散模型

## 1. 论文的核心问题与整体含义

- **研究背景**：病理图像分割在人工智能辅助的数字病理诊断与治疗中具有核心作用。然而，病理全切片图像（WSI）具有极高的分辨率，人工标注成本昂贵，且目标类别呈现显著的长尾分布。
- **核心问题**：
  - 现有分割方法受限于标注成本高，难以高效利用有限标注。
  - 长尾分布导致尾部类别（如稀有细胞或组织类型）识别精度不足。
- **整体含义**：论文提出一种新的扩散模型框架 L-Diffusion，旨在以高效方式提升病理图像分割精度，尤其是改善尾部类别的识别能力。该方法可作为 H&E 全切片图像中细胞或组织区域分割的基础工具。

## 2. 论文提出的方法论

- **核心思想**：
  - 传统扩散模型通常使用高斯分布建模特征，L-Diffusion 改用**多个拉普拉斯分布**来建模不同特征成分。
  - 理论分析表明，这种设计能显著增强特征空间中的特征分解能力。

- **关键技术流程**：
  1. **扩散特征生成**：通过一系列扩散步骤逐步生成特征图序列。
  2. **对比学习细化**：利用对比学习对从特征图序列中得到的逐像素向量进行细化，增强其判别性。
  3. **高效分割**：基于这些高判别性的逐像素向量，分割模块在精度和鲁棒性之间取得平衡，同时保持较高效率。

- **方法特色**：
  - 用拉普拉斯分布替代高斯分布，适配病理图像中特征成分的非高斯、重尾特性。
  - 扩散模型与对比学习结合，提升像素级特征表达能力。
- **局限说明**：提供的材料仅包含摘要，未给出具体公式、网络结构、损失函数等细节，因此无法进一步展开算法实现细节。

## 3. 实验设计

- **数据集 / 场景**：
  - 摘要提到在**组织分割数据集**和**细胞分割数据集**上进行评估。
  - 但未列出具体数据集名称（如 MoNuSeg、PanNuke、BCSS 等），无法确认数据来源和规模。

- **评价指标（Benchmark）**：
  - DICE（Dice 系数）
  - MPA（平均像素准确率）
  - mIoU（平均交并比）
  - FwIoU（频率加权交并比）

- **对比方法**：
  - 摘要未列出具体对比方法名称，因此无法确认与哪些 baseline 进行了比较。

- **实验提升结果**：
  - 组织分割数据集：DICE 提升最高 7.16%，MPA 提升 26.74%，mIoU 提升 16.52%，FwIoU 提升 3.55%。
  - 细胞分割数据集：DICE 提升 20.09%，MPA 提升 10.67%，mIoU 提升 14.42%，FwIoU 提升 10.41%。
  - 这些结果表明 L-Diffusion 在多项指标上相较基线有显著改进，尤其是尾部类别的改善可能反映在 MPA 等指标的大幅提升中。

- **代码开源**：https://github.com/Lweihan/LDiffusion

## 4. 资源与算力

- 提供的论文材料中**未提及** GPU 型号、数量、训练时长、显存消耗等算力信息。
- 因此无法总结该工作的实际算力需求；如需评估，需要查阅论文正文、附录或代码仓库的说明。

## 5. 实验数量与充分性

- **已报告实验**：
  - 至少包含**组织分割**和**细胞分割**两大类实验，每类均报告 4 个指标上的性能提升。
  - 提供的元数据显示论文包含 **11 张图** 和 **8 张表**，说明可能包含方法示意图、分割结果可视化、消融实验、对比实验等，但具体内容在提供的材料中不可见。

- **充分性与客观性评估**：
  - 从摘要看，实验覆盖了两个主要病理图像分割方向，指标使用较为全面。
  - 但无法确认：是否在多个数据集上重复验证、是否进行统计显著性检验、是否有消融实验验证各模块贡献、对比方法是否公平调参等。
  - 因此，仅凭现有信息难以对实验的充分性和客观性作出完全判断，需要阅读全文进一步核实。

## 6. 论文的主要结论与发现

- L-Diffusion 通过引入多个拉普拉斯分布替代高斯分布，有效增强了特征空间分解能力。
- 结合扩散过程生成的特征图序列和对比学习细化，能够得到高判别性的逐像素向量，使分割模块在精度和鲁棒性上达到平衡。
- 在组织和细胞分割任务上，L-Diffusion 相较现有方法取得了显著提升，尤其在改善长尾类别识别方面表现突出。
- 该方法为病理图像分割提供了一种高效且具有理论支撑的新途径。

## 7. 优点

- **方法创新性强**：首次提出用拉普拉斯分布替代扩散模型中的高斯分布，并有理论分析支撑。
- **针对实际痛点**：直接面向病理图像标注成本高和长尾分布问题，实用价值高。
- **技术组合合理**：扩散模型 + 对比学习，特征判别性强，有利于像素级分类。
- **指标覆盖全面**：同时使用 DICE、MPA、mIoU、FwIoU 四种指标，从不同角度衡量分割性能。
- **结果显著**：多个指标上提升幅度明显，尤其是 MPA 提升高达 26.74%，说明尾部类别识别改善明显。
- **代码开源**：提供源码链接，便于复现和后续研究。

## 8. 不足与局限

- **信息不完整**：提供的摘要未披露具体数据集名称、对比方法、算力消耗，难以全面评估实验设置和公平性。
- **实验细节缺失**：缺少统计显著性检验、交叉验证、参数敏感性分析等信息，结论的稳健性有待验证。
- **应用范围有限**：主要针对病理图像分割，是否适用于其他医学图像或自然图像分割仍需进一步研究。
- **效率指标未说明**：虽然强调“高效”，但未给出推理时间、模型参数量、FLOPs 等具体效率数据。
- **潜在偏差风险**：若实验数据集选择或对比方法调参不充分，可能影响性能提升结论的普适性。
- **尾部类别改善未单独量化**：摘要只给出整体指标提升，未单独展示尾部类别的精度变化，无法准确评估长尾问题的解决程度。

（完）
