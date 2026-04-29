---
title: Foundation cell segmentation models performance on live microscopy and spatial-omics data
title_zh: 基础细胞分割模型在活细胞显微和空间组学数据上的性能
authors: "Miao, Y., Surguladze, N., Lerner, J., Poysungnoen, K., Ariano, K., Li, Y., Zhu, Y., Van Batavia, K., Jepson, J., Van De Klashorst, J., Ni, B. Y. X., Armstrong, A., Rahman, R., Horstmeyer, R., Hickey, J. W."
date: 2026-04-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.18.719315v1.full.pdf"
tags: ["query:sam"]
score: 10.0
evidence: 评估基于SAM的模型在组织成像中进行细胞分割的表现
tldr: 本文比较了多种基础细胞分割模型（如Cellpose cyto3、Cellpose-SAM、microSAM、CellSAM、Mesmer和InstanSeg）在活细胞显微镜及空间组学数据上的性能，揭示各模型在不同成像类型中的差异表现，并强调模型选择应依数据特征和分析目标而定。
source: biorxiv
selection_source: fresh_fetch
motivation: 目前缺乏针对不同成像类型的通用细胞分割模型性能的系统比较，影响下游生物分析。
method: 作者系统评估多种深度学习细胞分割模型在相位差、荧光及CODEX组织成像数据上的表现。
result: Cellpose-SAM在相位差图像中表现突出，SAM系列模型在荧光数据上表现良好，而在CODEX数据中各模型优势各异影响后续分析。
conclusion: 研究建议根据数据类型和分析目标选择分割模型，而非依赖单一通用模型。
---

## 摘要
精确的细胞分割是生物成像数据定量分析的关键步骤。近年来深度学习的进展促进了通用分割模型的开发，这些模型能够在多种成像模式下稳定表现，包括无标记相差成像、荧光细胞培养以及多重荧光组织成像。然而，关于这些模型在下游生物分析层面的系统比较仍十分有限。为弥补这一缺口，我们评估了若干最新的分割模型，包括 Cellpose cyto3、Cellpose-SAM、{micro}SAM 和 CellSAM，测试图像包括相差和荧光细胞培养图像。此外，我们还将 Mesmer 和 InstanSeg 纳入多重荧光组织成像数据（由 CO-Detection by IndEXing (CODEX) 生成）的基准评测中。结果显示，Cellpose-SAM 在相差图像上表现突出，而基于 SAM 的模型在荧光细胞培养数据上表现稳定。相反，在 CODEX 数据集上，没有任何单一模型始终优于其他模型。每个模型都有其独特的优势和局限性，这导致下游分析（包括聚类和细胞类型识别）结果存在差异。总体而言，我们的研究强调了应根据数据集特征和分析目标选择分割模型的重要性，而非依赖某一通用方法。

## Abstract
Accurate cell segmentation is an essential step for quantitative analysis of biological imaging data. Recent advances in deep learning have led to the development of generalist segmentation models that perform robustly across multiple imaging modalities, including label-free phase contrast, fluorescence cell culture, and multiplexed fluorescence tissue imaging. However, systematic comparisons of these models at the level of downstream biological analysis remain limited. To address this gap, we evaluated several recent segmentation models, including Cellpose cyto3, Cellpose-SAM, {micro}SAM, and CellSAM, on phase contrast and fluorescence cell culture images. In addition, Mesmer and InstanSeg were included for benchmarking on multiplexed fluorescence tissue images generated using CO-Detection by IndEXing (CODEX). We found that Cellpose-SAM achieved strong performance on phase contrast images, while SAM-based models consistently performed well on fluorescence cell culture data. In contrast, no single model consistently outperformed others on CODEX datasets. Instead, each model exhibited distinct strengths and limitations, which led to differences in downstream analyses, including clustering and cell type identification. Together, our study emphasizes the importance of selecting segmentation models based on dataset characteristics and analytical goals, rather than relying on a single universal approach.

---

## 论文详细总结（自动生成）

# 基础细胞分割模型在活细胞显微和空间组学数据上的性能  
**原文标题**：*Foundation cell segmentation models performance on live microscopy and spatial-omics data*  
**作者**：Miao, Y. 等  
**来源**：bioRxiv（2026年4月）  

---

## 1. 核心问题与整体含义

- **研究背景**：  
  细胞分割是生物成像数据分析的核心任务，对后续的定量分析（如细胞表型、空间结构、细胞类型识别）具有决定性影响。  
  随着深度学习的发展，出现了若干 *通用型细胞分割模型*（foundation or generalist models），它们被设计为能跨不同显微成像类型（如相差显微、荧光成像、空间组学成像）稳定工作。  

- **研究动机**：  
  尽管这些模型表现优异，但目前缺乏系统研究来比较它们在不同类型成像数据上的公平性能，尤其缺少评估其对下游生物学分析（如聚类、细胞类型识别）的实际影响。  

- **研究目标**：  
  作者旨在**系统比较多种最新通用细胞分割模型**在不同显微成像与空间组学数据上的表现，明确各模型的优势与局限，为模型选择提供经验指南。

---

## 2. 方法论

- **核心思想**：  
  通过建立覆盖多种成像模式的统一评测框架，对多个深度学习分割模型进行定量与定性评价，分析其与图像特征以及下游分析任务之间的关系。

- **主要评测模型**：  
  - **Cellpose cyto3**：代表性广泛使用的通用分割模型。  
  - **Cellpose-SAM**：将 Segment Anything Model（SAM）结构结合到 Cellpose 中的改进版本。  
  - **microSAM**：专为显微图像领域调整的小型 SAM 变体。  
  - **CellSAM**：基于大型视觉模型的细胞级微调模型。  
  - **Mesmer 和 InstanSeg**：针对空间组学多重荧光图像（如 CODEX）的深度神经网络模型。

- **模型比较的技术路径**：  
  1. 对输入影像进行标准化与对齐。  
  2. 使用各模型独立分割细胞掩膜。  
  3. 使用多种指标（如 IoU、Dice、边界精度、细胞计数一致性）进行定量比较。  
  4. 将分割结果传入下游分析（聚类、空间图谱解析）以比较其对结果可靠性的影响。  
  5. 统计显著性验证各模型在不同成像类型下的差异。

> 注：文中未给出新模型或新算法，而是以系统性能评估为主。

---

## 3. 实验设计

- **数据来源与类型**：
  1. **相差显微镜（phase contrast）图像**：活细胞无标记成像。  
  2. **荧光细胞培养（fluorescence culture）图像**：细胞结构标记成像。  
  3. **CODEX 多重荧光组织图像**：空间组学层面高通量组织切片成像。  

- **对比模型**：  
  Cellpose cyto3、Cellpose-SAM、microSAM、CellSAM、Mesmer、InstanSeg。  

- **Benchmark 设计**：  
  每种数据类型均建立人工标注的参考分割集（gold standard），并通过一致的评估标准（如 F1-score、Instance recall、Boundary IoU）比较。  

- **评估维度**：  
  - 分割精度与边界质量  
  - 细胞数目一致性  
  - 对下游空间聚类与细胞谱系分类结果的影响  

---

## 4. 资源与算力

- 文中**未明确说明**使用的算力细节（包括 GPU 型号、数量或训练时长）。  
- 鉴于研究主要为“模型评估”，推测未重新训练模型，而是调用现有预训练权重进行推理，因此算力需求相对有限（可能在单卡 GPU 或高性能工作站上完成）。  

---

## 5. 实验数量与充分性

- **实验组别**：  
  覆盖三大成像类型，涉及六个模型，至少进行三组主要对比实验。  
  同时包含对 CODEX 数据的组织级分析，对比多个模型的下游聚类与分类表现。  

- **实验充分性**：  
  - 横向：模型类型覆盖度较宽（包含传统 CNN、增强型 Cellpose、基于 SAM 的大型模型）。  
  - 纵向：从单细胞级评估拓展到下游空间分析。  
  - 公平性：保持输入数据与评估标准一致，避免模型偏好数据集效应。  

总体而言，实验设置较为充分，能客观反映不同算法的通用性与适配性。

---

## 6. 主要结论与发现

- **Cellpose-SAM**：  
  在相差显微镜图像中表现最佳，尤其在细胞边界模糊的条件下保持高一致性。  

- **SAM 系列模型（CellSAM、microSAM）**：  
  在荧光成像数据上表现稳定且准确，表现在结构细节识别上优于非 SAM 模型。  

- **CODEX 数据集**：  
  无任何单个模型在所有指标上保持领先，分割性能与组织类型、荧光通道数及光照均一性相关。  

- **对下游分析的影响**：  
  分割结果的差异可显著影响细胞聚类与类型注释的准确性，显示分割质量直接决定 downstream 生物结论可靠性。  

- **总体结论**：  
  不存在“万能细胞分割模型”；应**根据数据特性与研究目标选择模型**，而非依赖单一框架。

---

## 7. 优点与创新点

- **系统性强**：首次跨多成像模式比较多种分割模型的综合性研究。  
- **下游导向**：不止停留在像素级精度，而关注对后续生物分析任务的真实影响。  
- **应用参考性高**：结果为实验室研究者或空间组学分析人员提供可操作的模型选择依据。  
- **评估透明**：基于公开模型与标准指标，便于复现与扩展。

---

## 8. 不足与局限

- **算力与数据规模信息缺失**：未明确复现条件，限制了评测可重复性。  
- **模型版本局限**：未涵盖更新的 foundation models（如 SAM 2 或其他 vision foundation models）。  
- **数据分布偏差**：若 CODEX 样本来源单一，模型性能可能与组织类型相关。  
- **缺乏系统消融**：未深入分析哪部分模型组件导致性能差异（例如 SAM prompt 模块或 decoder 结构）。  
- **仅侧重推理性能**：未考虑模型在低资源或实时分析场景下的部署效率。  

---

**（完）**
