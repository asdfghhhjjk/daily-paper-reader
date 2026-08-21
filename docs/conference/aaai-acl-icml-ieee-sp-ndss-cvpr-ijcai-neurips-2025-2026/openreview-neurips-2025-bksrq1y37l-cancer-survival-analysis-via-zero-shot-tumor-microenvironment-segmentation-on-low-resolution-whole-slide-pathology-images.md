---
title: Cancer Survival Analysis via Zero-shot Tumor Microenvironment Segmentation on Low-resolution Whole Slide Pathology Images
title_zh: 基于低分辨率全切片病理图像零样本肿瘤微环境分割的癌症生存分析
authors: "Jiao Tang, WEI SHAO, Daoqiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=BkSRQ1y37l"
tags: ["query:cell-path"]
score: 9.0
evidence: 全切片图像零样本肿瘤微环境分割与空间交互用于癌症生存预测
tldr: 针对传统全切片病理图像生存分析方法需要分块且无法反映全局空间组织的问题，该研究提出在低分辨率全切片图像上进行零样本肿瘤微环境分割，并利用不同TME成分间的空间交互来改进生存预测。方法避免了耗时的分块步骤，直接在整图层面建模空间关系。实验表明该方法能有效提升癌症生存预测性能，证明了TME空间组织在预后分析中的价值。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有WSI生存分析常需分块处理，无法反映整体空间组织，且TME交互建模成本高。
method: 提出在低分辨率WSI上进行零样本TME分割，利用不同TME成分的空间交互构建生存预测系统。
result: 在整图层面实现TME空间关系建模，有效提升癌症生存预测精度。
conclusion: 零样本TME分割和空间交互分析为全切片病理生存预测提供了高效方案。
---

## Abstract
The whole-slide pathology images (WSIs) are widely recognized as the golden standard for cancer survival analysis. However, due to the high-resolution of WSIs, the existing studies require dividing WSIs into patches and identify key components before building the survival prediction system, which is time-consuming and cannot reflect the overall spatial organization of WSIs. Inspired by the fact that the spatial interactions among different tumor microenvironment (TME) components in WSIs are associated with the cancer prognosis, some studies attempt to capture the complex interactions among different TME components to improve survival predictions. However, they require extra efforts for building the TME segmentation model, which involves substantial annotation workloads on different TME components and is independent to the construction of the survival prediction model. To address the above issues, we propose ZTSurv, a novel end-to-end cancer survival analysis framework via efficient zero-shot TME segmentation on low-resolution WSIs. Specifically, by leveraging tumor infiltrating lymphocyte (TIL) maps on the 50x down-sampled WSIs, ZTSurv enables zero-shot segmentation on other two important TME components (i.e., tumor and stroma) that can reduce the annotation efforts from the pathologists. Then, based on the visual and semantic information extracted from different TME components, we construct a heterogeneous graph to capture their spatial  intersections for clinical outcome prediction. We validate ZTSurv across four cancer cohorts derived from The Cancer Genome Atlas (TCGA), and the experimental results indicate that our method can not only achieve superior prediction results but also significantly reduce the computational costs in comparison with the state-of-the-art methods.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景与动机**  
  全切片病理图像（WSI）是癌症生存分析的“金标准”，但其分辨率极高，现有方法通常需要先将 WSI 切分成大量小块（patch），再识别关键成分并构建生存预测系统。  
  这种做法存在两个主要问题：
  - 分块处理耗时较长；
  - 分块后的局部特征难以反映整张切片的全局空间组织关系。

- **科学问题**  
  肿瘤微环境（TME）中不同成分（如肿瘤、基质、淋巴细胞等）的空间交互与癌症预后密切相关。已有研究尝试建模这些交互关系，但往往需要额外训练 TME 分割模型，带来大量病理医生标注工作，且分割模型与生存预测模型相互独立，增加了成本和复杂度。

- **整体含义**  
  该论文希望在不依赖大量人工标注、不进行耗时分块的前提下，直接在低分辨率 WSI 上实现 TME 成分分割，并利用各成分之间的空间关系提升癌症生存预测效果，同时降低计算成本。

## 2. 论文提出的方法论

- **核心思想**  
  提出 **ZTSurv**，一个端到端的癌症生存分析框架，核心是在低分辨率 WSI 上实现**零样本 TME 分割**，并基于分割结果构建**异构图**建模不同 TME 成分的空间交互。

- **关键技术细节**
  - **低分辨率输入**：使用 50 倍下采样的 WSI，避免传统高分辨率分块步骤，直接从全局图像层面分析。
  - **零样本 TME 分割**：
    - 利用已有的肿瘤浸润淋巴细胞（TIL）图作为先验信息；
    - 在 TIL 图的基础上，实现对另外两种重要 TME 成分（**肿瘤区域**和**基质区域**）的零样本分割；
    - 该方法减少了对病理医生手工标注的依赖。
  - **特征提取与异构图构建**：
    - 从不同 TME 成分中提取**视觉信息**和**语义信息**；
    - 构建**异构图**（heterogeneous graph）来捕获不同 TME 成分之间的空间交叉/交互关系；
    - 基于该图进行临床结局（生存）预测。
  - **端到端框架**：将 TME 分割与生存预测整合到同一个框架中，而不是分割模型与预测模型相互独立。

- **算法流程概述**
  1. 输入低分辨率 WSI；
  2. 利用 TIL 图进行零样本分割，得到肿瘤、基质等 TME 成分；
  3. 提取各成分的视觉与语义特征；
  4. 构建异构图，建模空间交互；
  5. 输出生存预测结果。

## 3. 实验设计

- **数据集**  
  使用来自 **The Cancer Genome Atlas（TCGA）** 的 **4 个癌症队列** 进行验证，具体癌症类型在提供的摘要中未列出。

- **评价基准与对比方法**
  - 与当前最先进（state-of-the-art）方法进行比较；
  - 评估指标包括**预测性能**和**计算成本**；
  - 具体对比方法名称、数据划分方式、评价指标细节未在摘要中说明。

- **实验场景**  
  在四个不同癌症队列上验证模型的泛化能力与效率，覆盖了多癌种生存分析任务。

## 4. 资源与算力

- 提供的论文摘要和元数据中**未明确说明**使用的 GPU 型号、数量、训练时长、显存消耗或推理时间等算力信息。
- 摘要仅提到该方法“显著降低计算成本”，并与现有方法进行了对比，但具体数值或硬件配置未在可见文本中给出。

## 5. 实验数量与充分性

- **可见的实验规模**
  - 覆盖 **4 个 TCGA 癌症队列**；
  - 与 **state-of-the-art 方法** 进行预测性能和计算成本对比；
  - 表明实验具备一定的多队列验证基础。

- **充分性与客观性评估**
  - 从摘要看，多队列验证有利于说明方法的普适性；
  - 但未提供消融实验、超参数敏感性分析、统计显著性检验、外部独立验证等细节，因此无法全面判断实验是否充分、是否完全公平；
  - 由于对比方法名称和具体实验设置未说明，客观性和公平性尚难以从现有文本中评估。

## 6. 论文的主要结论与发现

- ZTSurv 在四个 TCGA 癌症队列上取得了**优于现有方法**的生存预测结果；
- 该方法在低分辨率 WSI 上通过零样本 TME 分割，**显著降低了计算成本**；
- 联合使用不同 TME 成分的空间交互信息，能够有效提升癌症生存预测精度；
- 零样本 TME 分割与空间交互分析为全切片病理生存预测提供了一种**高效、端到端**的解决方案。

## 7. 优点

- **减少标注负担**：通过零样本分割避免了对肿瘤、基质等 TME 成分的大量人工标注。
- **全局空间建模**：直接在低分辨率 WSI 上工作，避免分块导致的空间信息丢失。
- **端到端设计**：将 TME 分割与生存预测整合，避免两个独立模型带来的额外复杂度和误差传播。
- **计算效率高**：低分辨率输入和零样本策略显著降低计算成本。
- **多队列验证**：在多个 TCGA 癌症队列上验证，增强了结果的可信度。

## 8. 不足与局限

- **技术细节披露不足**：摘要未给出零样本分割的具体实现方式、异构图构建细节、损失函数、训练策略等，难以复现。
- **数据集来源单一**：仅使用 TCGA 数据，且具体癌种未说明，可能限制在其他来源或罕见癌症上的泛化能力。
- **缺乏对比细节**：未列出具体对比方法、评价指标和统计检验，难以客观评估“优于现有方法”的程度。
- **实验充分性存疑**：未提及消融实验、敏感性分析或外部验证，无法确认各模块的实际贡献。
- **零样本分割的依赖风险**：依赖 TIL 图作为先验，若某些癌症类型中 TIL 图质量不稳定，可能影响后续肿瘤和基质分割效果。
- **计算成本对比不透明**：虽然声称降低计算成本，但未给出具体硬件、时间和资源对比数据。

（完）
