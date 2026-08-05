---
title: Cancer Survival Analysis via Zero-shot Tumor Microenvironment Segmentation on Low-resolution Whole Slide Pathology Images
title_zh: 低分辨率全切片病理图像上基于零样本肿瘤微环境分割的癌症生存分析
authors: "Jiao Tang, WEI SHAO, Daoqiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=BkSRQ1y37l"
tags: ["query:cellseg"]
score: 10.0
evidence: "从H&E全切片图像中分割肿瘤微环境成分，利用空间交互进行癌症生存分析。"
tldr: 针对全切片图像(WSI)生存分析中计算开销大、空间信息丢失和标注依赖问题，本文提出一种零样本肿瘤微环境(TME)分割方法，直接在低分辨率WSI上分割TME成分并建模空间交互，用于癌症预后预测。该方法避免了传统patch切分和人工标注，在多个癌症数据集上取得了优于现有方法的性能，并显著降低了计算复杂度，为WSI生存分析提供了轻量级解决方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有方法需切块识别关键成分，忽略WSI整体空间组织，且依赖大量标注。
method: 提出零样本TME分割，在低分辨率WSI上直接分割并建模空间交互用于生存预测。
result: 在多个癌症数据集上，该方法超越现有生存分析模型，同时降低计算开销。
conclusion: 通过零样本TME分割利用空间信息，提高了WSI生存分析的准确性和效率。
---

## Abstract
The whole-slide pathology images (WSIs) are widely recognized as the golden standard for cancer survival analysis. However, due to the high-resolution of WSIs, the existing studies require dividing WSIs into patches and identify key components before building the survival prediction system, which is time-consuming and cannot reflect the overall spatial organization of WSIs. Inspired by the fact that the spatial interactions among different tumor microenvironment (TME) components in WSIs are associated with the cancer prognosis, some studies attempt to capture the complex interactions among different TME components to improve survival predictions. However, they require extra efforts for building the TME segmentation model, which involves substantial annotation workloads on different TME components and is independent to the construction of the survival prediction model. To address the above issues, we propose ZTSurv, a novel end-to-end cancer survival analysis framework via efficient zero-shot TME segmentation on low-resolution WSIs. Specifically, by leveraging tumor infiltrating lymphocyte (TIL) maps on the 50x down-sampled WSIs, ZTSurv enables zero-shot segmentation on other two important TME components (i.e., tumor and stroma) that can reduce the annotation efforts from the pathologists. Then, based on the visual and semantic information extracted from different TME components, we construct a heterogeneous graph to capture their spatial  intersections for clinical outcome prediction. We validate ZTSurv across four cancer cohorts derived from The Cancer Genome Atlas (TCGA), and the experimental results indicate that our method can not only achieve superior prediction results but also significantly reduce the computational costs in comparison with the state-of-the-art methods.

---

## 论文详细总结（自动生成）

# 论文详细总结：《Cancer Survival Analysis via Zero-shot Tumor Microenvironment Segmentation on Low-resolution Whole Slide Pathology Images》

## 1. 论文的核心问题与整体含义
- **研究背景**：全切片病理图像（WSI）是癌症生存分析的金标准，但其超高分辨率（通常达十亿像素级）给计算和建模带来巨大挑战。
- **现有方法瓶颈**：
  - 传统方法需将WSI切割为数千个小块（patch），再从中识别关键组织成分，这忽略了WSI中细胞与组织成分的宏观空间组织规律。
  - 部分研究已意识到肿瘤微环境（TME）中不同成分（如肿瘤细胞、间质、淋巴细胞）的空间交互对预后至关重要，但其TME分割模型需耗费大量病理学家人工标注，且与生存预测模型割裂构建，无法端到端优化。
- **核心问题**：如何在不依赖密集标注的前提下，高效地分割TME成分并捕捉其空间交互，实现准确且计算友好的WSI生存分析。

## 2. 论文提出的方法论
- **整体框架**：ZTSurv，一个基于低分辨率WSI的端到端零样本TME分割与生存预测框架。
- **核心技术细节**：
  - **零样本TME分割**：在50倍下采样的低分辨率WSI上，利用预先获得的**肿瘤浸润淋巴细胞（TIL）密度图**作为引导，通过无监督或基于先验的推理方式，实现对**肿瘤区域**和**间质区域**的零样本分割，无需额外人工标注。
  - **视觉与语义特征提取**：从分割出的肿瘤、间质、TIL三个TME成分中，分别提取反映其形态和语义信息的特征向量。
  - **异质图构建与交互建模**：
    - 将每种TME成分的不同空间实例（或局部区域）作为不同类型的图节点。
    - 基于节点的空间邻近关系构建异质图边，以捕获成分间的空间共定位与排斥等复杂相互作用。
    - 使用图神经网络（如异质图注意力网络）聚合跨成分的邻域信息，最终生成患者级别的生存风险表征。
  - **生存预测**：将图级表征输入到生存损失函数（如Cox比例风险损失）中进行端到端训练。
- **算法流程**：低分辨率WSI → 预计算TIL图 → 零样本分割肿瘤/间质 → 成分特征提取 → 异质图构建 → 图卷积/注意力 → 生存风险预测输出。

## 3. 实验设计
- **数据集**：来自癌症基因组图谱（TCGA）的4个不同癌种队列（文中未列出具体癌种名称，但常见选择包括肺腺癌、乳腺浸润性癌、胃腺癌等）。
- **基准（Benchmark）**：与当前最先进（state-of-the-art）的WSI生存分析方法进行对比，可能包括：
  - 基于多实例学习（MIL）的patch级方法（如ABMIL、CLAM等）。
  - 基于图神经网络的同类空间建模方法。
  - 需要人工标注TME成分的传统方法。
- **评估指标**：推测主要使用一致性指数（C-index）评估生存预测性能，同时对比计算开销（如训练时长、显存占用）。

## 4. 资源与算力
- **文中未明确说明**具体使用的GPU型号、数量及训练时长。
- 摘要和元数据中仅定性声明该方法“显著降低了计算成本”，但未给出定量对比（如与基线方法的推理时间或参数量对比值）。

## 5. 实验数量与充分性
- **主要实验**：在4个TCGA癌种数据上对比多个主流生存分析方法，验证预测性能的优势。
- **消融实验**：鉴于方法涉及零样本分割、异质图构建等模块，推测进行了消融实验以验证各组件（如TIL引导、图结构、低分辨率策略）的贡献。但提供内容未列出具体消融实验组数。
- **充分性评价**：4个公共数据集的覆盖量尚可，但仅限TCGA内部验证，缺乏外部独立队列验证，使得结果的泛化性证据稍显不足。实验对比若仅与pubic leaderboard上常见方法对比，则公平性可接受。

## 6. 论文的主要结论与发现
- ZTSurv在4个TCGA癌症队列上取得了优于现有SOTA方法的生存预测性能。
- 通过零样本TME分割，该方法成功规避了昂贵的人工标注流程，同时保留了关键的TME空间组织信息。
- 直接在低分辨率WSI上建模，能够在保证或者提升准确度的前提下，大幅降低计算开销，为WSI生存分析提供了轻量级解决方案。

## 7. 优点
- **创新性标注方案**：提出零样本TME分割，利用易获取的TIL图推导其他成分，显著降低病理标注依赖。
- **空间完整性**：绕过patch划分，直接在大尺度下捕获WSI的整体空间组织，符合病理诊断的直觉。
- **端到端设计**：将分割先验与生存预测统一在框架中，避免了多阶段任务脱节和错误累积。
- **计算效率**：在低分辨率上操作，模型轻量，有望推动临床场景下的即时分析报告。

## 8. 不足与局限
- **标注依赖性前移**：零样本分割仍依赖预计算TIL图，而TIL图的生成可能需要另一个训练好的模型（如TIL检测器），其标注成本未被计入。严格意义上是“零额外标注”而非完全零监督。
- **低分辨率信息损失**：50倍下采样可能导致细胞级精细形态（如核异型性）丢失，可能对某些依赖高倍镜特征的癌种不利。
- **数据集局限**：实验仅使用TCGA数据，其样本可能存在人群、中心偏差，缺乏来自不同扫描仪或临床中心的外部验证。
- **可解释性有限**：异质图虽能建模空间交互，但具体的高价值空间模式（如哪种交互模式驱动预后）未深入展示。
- **方法细节未知**：由于无法获取完整论文，零样本分割的具体实现机制（如TIL图如何转化为肿瘤/间质轮廓）及异质图的具体结构尚不明确，影响了对其有效性的完全评判。

（完）
