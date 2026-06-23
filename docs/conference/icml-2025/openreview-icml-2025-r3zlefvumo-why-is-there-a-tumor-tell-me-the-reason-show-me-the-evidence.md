---
title: "\"Why Is There a Tumor?\": Tell Me the Reason, Show Me the Evidence"
title_zh: “为什么会有肿瘤？”：告诉我原因，展示证据
authors: "Mengmeng Ma, Tang Li, Yunxiang Peng, Lu Lin, Volkan Beylergil, Binsheng Zhao, Oguz Akin, Xi Peng"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=r3ZLefVUMO"
tags: ["query:pathology-ai"]
score: 4.0
evidence: 用于肿瘤分割的可解释AI，生成文本理由并定位证据
tldr: 针对医学AI模型只能定位肿瘤却不能解释原因的问题，该论文提出同时输出分割掩码和文本理由的模型。通过构建包含180K条人工标注理由的数据集，训练模型能够用临床术语解释分割结果并指出图像中的证据位置。该方法增强了模型的可信度和可解释性，适用于病理图像分析中的可解释特征提取需求。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-r3zlefvumo/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1774, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r3zlefvumo/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1751, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r3zlefvumo/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r3zlefvumo/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1661, \"height\": 724, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r3zlefvumo/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1761, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r3zlefvumo/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 863, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r3zlefvumo/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1765, \"height\": 885, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r3zlefvumo/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1761, \"height\": 498, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-r3zlefvumo/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 858, \"height\": 491, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r3zlefvumo/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1770, \"height\": 462, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r3zlefvumo/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1702, \"height\": 615, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r3zlefvumo/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 866, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r3zlefvumo/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r3zlefvumo/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 863, \"height\": 635, \"label\": \"Table\"}]"
motivation: 现有肿瘤检测模型只能输出分割结果，缺乏临床语义解释，难以获得医生信任。
method: 构建包含图像、分割注释和文本理由的数据集，训练能同时输出分割和临床术语解释的模型。
result: 模型能在肿瘤区域生成对应的文本理由，并定位到视觉证据，提升了解释的完整性。
conclusion: 结合分割与文本解释的方法有助于推动可信AI在病理学中的实际应用。
---

## Abstract
Medical AI models excel at tumor detection and segmentation. However, their latent representations often lack explicit ties to clinical semantics, producing outputs less trusted in clinical practice. Most of the existing models generate either segmentation masks/labels (localizing where without why) or textual justifications (explaining why without where), failing to ground clinical concepts in spatially localized evidence. To bridge this gap, we propose to develop models that can justify the segmentation or detection using clinically relevant terms and point to visual evidence. We address two core challenges: First, we curate a rationale dataset to tackle the lack of paired images, annotations, and textual rationales for training. The dataset includes 180K image-mask-rationale triples with quality evaluated by expert radiologists. Second, we design rationale-informed optimization that disentangles and localizes fine-grained clinical concepts in a self-supervised manner without requiring pixel-level concept annotations. Experiments across medical benchmarks show our model demonstrates superior performance in segmentation, detection, and beyond. The anonymous link to our code.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有的医学AI模型在肿瘤检测和分割上表现出色，但其内部表示缺乏与临床语义的显式关联，导致输出难以获得临床信任。大多数模型要么只输出分割掩码/标签（定位“哪里”但不说“为什么”），要么只生成文本解释（解释“为什么”但不定位“哪里”），无法将临床概念锚定到空间局部化证据上。
- **整体目标**：开发一种能够同时用临床术语解释其预测结果，并指出证据在图像中具体位置的模型，弥合语义-视觉鸿沟，提升临床可信任度。

## 2. 方法论
### 核心思想
- 构建“图像-掩码-理由”三元组数据集，并通过自监督优化框架，在不依赖像素级概念标注的情况下，解耦并定位细粒度临床概念，实现分割、检测与可解释理由的联合输出。

### 关键技术细节
- **理由数据集构建**：
  - 从PI-CAI挑战的1500个前列腺MRI扫描中，由放射科专家标注PI-RADS报告。
  - 设计PI-RADS决策树（PDT），将领域知识结构化。
  - 利用GPT-4o和PDT通过上下文学习从临床报告中自动提取详细理由，最终生成180K个2D三元组（图像、掩码、理由）。
  - 经两位专家放射科医生的四维度（连贯性、一致性、全面性、事实准确性）人工验证，质量较高。

- **理由知情优化**：
  - **主目标**：联合优化分割损失（Dice损失）和图像-文本对齐损失（InfoNCE），学习共享视觉-语言嵌入空间。
  - **解耦约束**：不同临床概念的热图应在图像上突出不同区域（相似度距离≥ϵ1），避免退化解。
  - **定位约束**：描述同一解剖结构的不同概念的热图应重合，且与真实掩码对齐（距离≤ϵ2）。
  - 通过KKT条件和拉格朗日乘子转化为无约束优化问题。
  - **推理**：在测试时，模型通过遍历PI-RADS决策树，在共享嵌入空间中检索与图像最相似的理由，并生成对应热图。

## 3. 实验设计
### 数据集
- **理由数据集**：来自PI-CAI（1500个3D MRI扫描，180K 2D三元组），80/20划分训练/测试。
- **Prostate158**：158个mp-MRI，德国医院采集，存在分布偏移。
- **MSD-Prostate**：48个mp-MRI，荷兰医院采集。

### Benchmark与对比方法
- **分割/检测**：U-Net、ITUNet、Swin UNETR、CSwin U-Net、SSL CSwin U-Net、MA-SAM、SAMed、BiomedParse。
- **可解释性对比**：与OpenAI o1模型比较理由生成和定位。
- **评估指标**：DSC（分割），AP、AUROC（检测），RMA（视觉证据定位准确率），以及分类的精确率/召回率/F1。

## 4. 资源与算力
- **未明确说明**：论文中未提及使用的GPU型号、数量、训练时长等硬件资源。仅在附录D提到使用Adam优化器、学习率调度等，但未提供具体计算资源信息。

## 5. 实验数量与充分性
- **实验组数**：
  - 表1：理由数据集上的分割与检测（5种对比方法 + 本文模型）。
  - 表2：两个零样本数据集上的分割与检测（6-8种对比方法）。
  - 表3：理由分类准确性（与logits、掩码基线对比）。
  - 表4：视觉证据定位准确性（与无约束变体对比）。
  - 表5：消融实验（无约束、仅解耦、两者结合）。
  - 图4：人类评估理由质量（两位专家，100个样本）。
  - 图6：与OpenAI o1定性定量比较（20例）。
  - 图7：可视化热图消融效果。
- **充分性评估**：实验覆盖了分割、检测、可解释性、泛化性、消融分析、人类评估、与SOTA及LLM对比，较为全面。所有结果均基于多次独立运行，并报告均值与标准差。对比方法均使用相同训练/测试配置，公平性良好。

## 6. 主要结论与发现
- 结合文本理由的训练可以提升模型的分割和检测性能（在理由数据集上，Lesion DSC +8.8%，AP +5.3%）。
- 模型在零样本泛化上显著优于现有方法（Prostate158上Zone DSC +2.0%，Lesion DSC +4.3%）。
- 模型能够生成准确的临床理由（分类F1 0.583），并有效定位视觉证据（RMA 0.403 vs 基线0.010）。
- 自监督优化框架无需像素级概念标注即可实现概念定位，且解耦和定位约束缺一不可。

## 7. 优点
- **数据贡献**：首次构建了包含图像、分割掩码和详细文本理由的大规模高质量数据集，且数据构建流程可迁移至其他癌症类型。
- **方法创新**：提出自监督约束（解耦+定位）来学习概念级视觉证据，无需昂贵人工标注。
- **性能突破**：在分割、检测和可解释性三个指标上同时超越现有方法，且零样本泛化能力强。
- **临床价值**：输出的理由和视觉证据符合放射科医生工作流程，有望提升临床信任与辅助诊断效率。

## 8. 不足与局限
- **数据局限**：理由数据集仅针对前列腺癌（PI-RADS），未覆盖乳腺癌、肺癌等其他癌种。
- **失败案例**：在肿瘤出现的过渡切片上，存在分割掩码与理由不一致的情况（有理由无掩码，或有掩码无理由），可能影响临床信任。
- **对比范围有限**：与OpenAI o1的对比仅20例，样本量小；且未与其他视觉语言模型（如LLaVA-Med）进行定量比较。
- **计算成本未报告**：未说明训练所需的硬件资源和时间，难以评估方法的实际部署成本。
- **临床验证缺失**：仅在公开数据集上验证，未在真实临床场景中评估人机协作效果或医生满意度。
- **应用限制**：当前方法依赖结构化临床报告和决策树，对于缺乏标准化报告的领域可能难以直接迁移。

（完）
