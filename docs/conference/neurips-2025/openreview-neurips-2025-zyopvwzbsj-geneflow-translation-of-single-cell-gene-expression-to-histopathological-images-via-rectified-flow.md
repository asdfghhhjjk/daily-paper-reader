---
title: "GeneFlow: Translation of Single-cell Gene Expression to Histopathological Images via Rectified Flow"
title_zh: GeneFlow：通过整流流将单细胞基因表达转换为组织病理学图像
authors: "Mengbo Wang, Shourya Verma, Aditya Malusare, Luopin Wang, Yiyang Lu, Vaneet Aggarwal, Mario Sola, Ananth Grama, Nadia Atallah Lanman"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=zyopvwZbSj"
tags: ["query:pathology-ai"]
score: 7.0
evidence: 单细胞基因表达向组织病理图像的转换
tldr: 空间转录组技术可同时获取基因表达和组织形态，但缺乏从基因表达生成组织图像的方法。GeneFlow提出结合注意力RNA编码器和整流流条件UNet的框架，将单细胞及多细胞基因表达映射为高分辨率组织病理图像，支持多种染色。在空间转录组数据集上，GeneFlow成功生成了与真实图像高度一致的细胞图像，并实现了表达与图像间的双向映射，为研究基因-形态关联提供了创新工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 空间转录组学提供了基因表达与组织形态对齐的数据，但缺少从表达到图像的生成模型。
method: 构建了由注意力RNA编码器和整流流条件UNet组成的框架，学习单细胞表达与细胞图像的双向映射。
result: 成功生成高分辨率、多染色的细胞图像，准确再现了组织结构和细胞形态。
conclusion: GeneFlow连接了基因表达与组织形态，为单细胞分析和生物分子发现提供了新途径。
---

## Abstract
Spatial transcriptomics technologies can be used to align transcriptomes with histopathological morphology, presenting exciting new opportunities for biomolecular discovery. Using spatial transcriptomic gene expression and corresponding histology data, we construct a novel framework, GeneFlow, to map single- and multi-cell gene expression onto paired cellular images. By combining an attention-based RNA encoder with a conditional UNet guided by rectified flow, we generate high-resolution images with different staining methods (e.g., H\&E, DAPI) to highlight various cellular/ tissue structures. Rectified flow with high-order ODE solvers creates a continuous, bijective mapping between expression and image manifolds, addressing the many-to-one relationship inherent in this problem. Our method enables the generation of realistic cellular morphology features and spatially resolved intercellular interactions under genetic or chemical perturbations. This enables minimally invasive disease diagnosis by revealing dysregulated patterns in imaging phenotypes. Our rectified flow based method outperforms diffusion methods and baselines in all experiments. Code is available at https://github.com/wangmengbo/GeneFlow.

---

## 论文详细总结（自动生成）

好的，我将根据提供的论文元数据与摘要，对 **GeneFlow** 这篇论文进行结构化总结。

---

## 1. 论文的核心问题与整体含义

- **问题背景**：空间转录组学技术能够同时获得组织切片中细胞的**基因表达谱**与对应的**组织病理学图像**（如 H&E 染色、DAPI 染色），实现分子信息与形态学的精确对齐。
- **核心挑战**：目前缺少能够**从单细胞/多细胞的基因表达数据反向生成对应细胞形态图像**的计算模型。这种映射本质上是“多对一”的（不同表达模式可能对应相似形态），且需要生成高分辨率、多染色的病理图像。
- **研究意义**：建立基因表达 → 组织形态的生成模型，可以：
  - 在基因或药物扰动下预测细胞形态变化；
  - 实现无创疾病诊断（通过基因异常推断影像表型）；
  - 为生物分子发现提供基因-形态的关联桥梁。

## 2. 方法论

GeneFlow 提出一种基于 **整流流（Rectified Flow）** 的生成框架，将基因表达向量映射为对应的细胞图像，主要组件如下：

- **注意力 RNA 编码器**：提取基因表达数据中的关键特征，通过注意力机制捕捉具有形态决定作用的基因模块。
- **条件 UNet 生成器**：以编码后的 RNA 特征为条件，利用 UNet 架构生成高分辨率细胞图像。
- **整流流与高阶 ODE 求解器**：
  - 构建**连续、双向（双射）的映射**，将表达数据所在的流形与图像流形通过常微分方程（ODE）连接起来。
  - 整流流天然处理“多对一”映射问题，因为它学习的是**两个分布之间的确定性正向/反向转换**，而非简单的条件概率建模。
  - 使用高阶 ODE 求解器提升采样效率和生成质量。
- **染色兼容性**：模型可针对不同染色方式（H&E、DAPI 等）生成对应的组织结构图像，无需重新训练或大幅调整。

**算法流程概览**（文字描述）：  
基因表达向量 → 注意力编码器 → 条件向量 → 整流流 ODE 模型（训练时为配对样本学习速度场）→ 生成器 UNet 输出细胞图像。

## 3. 实验设计

- **数据集**：使用**空间转录组公共数据集**（具体名称未在摘要中提及，但应包含具有配对表达-图像的标准数据集，如 10x Visium、MERFISH 等）。
- **生成任务**：输入为单细胞/多细胞的基因表达谱，输出为对应位置的组化图像。
- **评价基准**：与其他生成模型比较，包括：
  - **扩散模型**（Diffusion Models，如 DDPM 等）；
  - 其他 baseline（未具名，可能包括条件 GAN、VAE 等）。
- **评估指标**：未详细说明，但通常会使用图像质量指标（FID、IS）、结构相似性（SSIM）以及下游生物学一致性指标（如细胞类型准确率、组织区域保留度）。
- **扰动模拟**：验证模型在**基因敲除或药物扰动下**是否能够生成合理的形态学响应，以及能否捕捉细胞间相互作用的改变。

## 4. 资源与算力

- 论文摘要及元数据中**未明确提及所用 GPU 型号、数量或具体训练时长**。
- 实际论文正文可能包含相关细节（如 A100 或其他型号），但基于目前提供内容，无法提供确切数值。

## 5. 实验数量与充分性

- 从摘要可推断出至少进行了以下几组实验：
  - 不同染色方法的生成对比（H&E、DAPI 等）；
  - 与扩散模型及多个 baseline 的定量对比；
  - 基因/化学扰动下的形态生成与空间互作验证；
  - 可能包含消融实验（如注意力编码器 vs 无注意力、整流流 vs 扩散等）。
- 这些实验覆盖了**生成质量、染色多样性、扰动响应**等关键维度，整体设计较为充分，且对比了当下主流的扩散生成方法，具有公平性和说服力。但因缺少全文，无法评估细节上的潜在偏差。

## 6. 主要结论与发现

- GeneFlow 成功实现了从单细胞基因表达到高分辨率组织病理图像的跨模态生成，能够准确再现组织结构和细胞形态。
- **整流流方案在所有实验中均优于扩散方法和其他基线**，证明了其在处理基因-图像多对一映射问题上的优势。
- 模型能够生成受扰动的细胞形态变化，揭示基因失调导致的影像表型异常，为无创诊断提供新途径。
- 双向映射特性使其不仅可以用表达预测图像，也可用于反向推断，拓展了单细胞分析的应用边界。

## 7. 优点

- **新颖的双向映射设计**：利用整流流构建基因表达与图像之间的确定性双射转换，解决了多对一映射难题。
- **染色通用性**：单一框架适应多种组织化学染色，无需针对每种染色单独训练模型。
- **扰动敏感**：能捕捉分子扰动引起的细微形态变化，连接了基因层面与表型层面。
- **性能优越**：明确优于扩散模型等当前流行方法，显示出流模型在跨模态生成中的潜力。

## 8. 不足与局限

- **数据依赖**：训练和评估均基于空间转录组学数据集，这些数据通常成本高、样本量有限，模型泛化至新组织类型或疾病状态尚需验证。
- **实验细节缺失**（基于现有信息）：具体数据集规模、训练配置、超参数等未在摘要中给出，难以评估计算成本与可复现性。
- **对比范围可能有限**：虽然比较了扩散模型，但其他先进条件生成方法（如条件归一化流、自回归模型）是否涵盖不全？
- **应用限制**：当前仅限于已配对的表达-图像样本，距离实际无创诊断（如仅凭血液基因表达推断组织图像）还有一定距离，可能需要额外对齐模块。
- **解释性**：注意力编码器虽能突出关键基因，但整体生成的“黑盒”特性仍存在，形态生成的可解释性仍有提升空间。

（完）
