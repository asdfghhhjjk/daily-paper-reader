---
title: Foundation cell segmentation models performance on live microscopy and spatial-omics data
title_zh: 基础细胞分割模型在活细胞显微成像与空间组学数据中的性能
authors: "Miao, Y., Surguladze, N., Lerner, J., Poysungnoen, K., Ariano, K., Li, Y., Zhu, Y., Van Batavia, K., Jepson, J., Van De Klashorst, J., Ni, B. Y. X., Armstrong, A., Rahman, R., Horstmeyer, R., Hickey, J. W."
date: 2026-04-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.18.719315v1.full.pdf"
tags: ["query:sam"]
score: 10.0
evidence: 评估了包括 Cellpose-SAM、microSAM 和 CellSAM 在内的基础模型在细胞分割中的表现
tldr: 本研究针对通用细胞分割模型进行了跨成像模态的系统评估，比较了多种基于深度学习的模型在实时显微镜与空间组学数据上的表现，揭示了不同模型在不同数据类型中的优势与局限，为根据数据特点与分析目标选择合适模型提供了依据。
source: biorxiv
selection_source: fresh_fetch
motivation: 当前缺乏在生物学下游分析层面对不同通用细胞分割模型性能的系统比较。
method: "作者系统评估了Cellpose cyto3、Cellpose-SAM、{micro}SAM、CellSAM、Mesmer和InstanSeg等模型在不同类型显微镜和空间组学数据上的表现。"
result: Cellpose-SAM在相差图像上表现突出，SAM系列模型在荧光细胞培养数据上表现良好，而在CODEX数据中没有单一模型占优。
conclusion: 研究表明应根据数据特征和分析需求选择细胞分割模型，而非依赖单一通用方案。
---

## 摘要
精确的细胞分割是生物成像数据定量分析中的关键步骤。近年来，深度学习的进展推动了通用分割模型的发展，这些模型在多种成像模式下表现稳健，包括无标记的相差成像、荧光细胞培养以及多重荧光组织成像。然而，针对这些模型在后续生物学分析层面的系统性比较仍然有限。为弥补这一空白，我们评估了多个近期的分割模型，包括 Cellpose cyto3、Cellpose-SAM、{micro}SAM 和 CellSAM，在相差显微镜和荧光细胞培养图像上的表现。此外，我们还引入 Mesmer 和 InstanSeg，用于在通过 CO-Detection by IndEXing（CODEX）生成的多重荧光组织图像上进行基准测试。结果表明，Cellpose-SAM 在相差图像上表现优异，而基于 SAM 的模型在荧光细胞培养数据上始终具备良好性能。相比之下，在 CODEX 数据集上没有单一模型表现出全面优势。相反，每个模型都有其独特的优点与局限性，从而导致包括聚类与细胞类型识别在内的下游分析结果存在差异。总体而言，我们的研究强调，根据数据集特征和分析目标选择合适的分割模型的重要性，而非依赖单一通用方法。

## 速览
**TLDR**：本文系统评估了包括Cellpose cyto3、Cellpose-SAM、microSAM和CellSAM等最新细胞分割模型在不同类型显微镜和空间组学数据上的性能，结果显示各模型在不同数据中各具优势，研究强调应根据具体任务选择合适分割模型。 \
**Motivation**：现有通用分割模型虽表现稳定，但其在实际生物分析中的比较研究仍然不足。 \
**Method**：系统评估了多种基础细胞分割模型在不同显微镜与空间组学数据上的表现。 \
**Result**：发现Cellpose-SAM在相差图像中表现最佳，SAM系列在荧光培养数据表现突出，在CODEX数据中无单一模型占优。 \
**Conclusion**：建议根据数据特征和分析目标选择细胞分割模型，而不是依赖单一通用模型。

---

## Abstract
Accurate cell segmentation is an essential step for quantitative analysis of biological imaging data. Recent advances in deep learning have led to the development of generalist segmentation models that perform robustly across multiple imaging modalities, including label-free phase contrast, fluorescence cell culture, and multiplexed fluorescence tissue imaging. However, systematic comparisons of these models at the level of downstream biological analysis remain limited. To address this gap, we evaluated several recent segmentation models, including Cellpose cyto3, Cellpose-SAM, {micro}SAM, and CellSAM, on phase contrast and fluorescence cell culture images. In addition, Mesmer and InstanSeg were included for benchmarking on multiplexed fluorescence tissue images generated using CO-Detection by IndEXing (CODEX). We found that Cellpose-SAM achieved strong performance on phase contrast images, while SAM-based models consistently performed well on fluorescence cell culture data. In contrast, no single model consistently outperformed others on CODEX datasets. Instead, each model exhibited distinct strengths and limitations, which led to differences in downstream analyses, including clustering and cell type identification. Together, our study emphasizes the importance of selecting segmentation models based on dataset characteristics and analytical goals, rather than relying on a single universal approach.

---

## 论文详细总结（自动生成）

# 基础细胞分割模型在活细胞显微成像与空间组学数据中的性能 — 深度总结

---

## 一、核心问题与研究背景

- **核心问题**：现有的通用细胞分割模型（generalist cell segmentation models）是否能在多种成像模态与生物学下游分析任务中保持一致且可靠的性能。  
- **背景动机**：
  - 精确的细胞分割是从显微成像数据获得定量生物学信息（如细胞类型识别、空间组织分析）的关键前提。
  - 近年来深度学习推动了通用分割模型（如 Cellpose、SAM 系列）的快速发展，这些模型无需针对特定数据集重新训练即可在不同样本上工作。
  - 然而，缺乏系统性研究来比较这些模型在不同数据类型上的差异，并评估它们对后续生物学分析（如聚类、空间组学）的影响。  
  → **研究目标**：填补这一比较评估的空白，建立跨模态的性能基准，为研究者选择合适模型提供依据。

---

## 二、方法论与技术框架

- **核心思想**：通过统一的评估框架，对多种基础细胞分割模型在不同成像模态（相差显微镜、荧光培养、空间多重成像 CODEX）上进行性能比较，并观察这些分割结果对下游分析的影响。
- **主要模型**：
  - **Cellpose cyto3**：基于 U-Net 架构，强调细胞中心向量场预测。
  - **Cellpose-SAM、microSAM、CellSAM**：结合了 Segment Anything Model (SAM) 的通用图像理解能力，用于无监督或弱监督的细胞区域检测。
  - **Mesmer 和 InstanSeg**：侧重多通道荧光组织数据的分割，常用于空间组学图像。
- **评估指标**：
  - 分割准确度（IoU / Dice Score）
  - 细胞边界一致性与形态完整性
  - 下游分析指标（如细胞聚类稳定性、空间分布一致性）
- **算法流程（文字描述）**：
  1. 对不同类型成像数据进行标准化预处理；
  2. 使用各模型进行分割预测；
  3. 将分割结果输入至下游分析模块（聚类、类型识别）；
  4. 对比定量指标与生物学解释的一致性。  

---

## 三、实验设计

- **数据集与场景**：
  - **相差显微镜图像**：活细胞的无标记成像数据，用于评估模型对形态灰度变化的敏感度。
  - **荧光细胞培养图像**：典型的单通道或多通道荧光数据，测试模型的分辨能力。
  - **CODEX 空间组学数据**：多重荧光组织切片，用于复杂的细胞类型与空间特征分析。
- **Benchmark 设置**：
  - 每个数据模态都建立了独立的基准测试集合；
  - 对比指标统一采用标准分割精度与下游分析一致性。
- **对比方法**：
  - Cellpose cyto3（基线）  
  - Cellpose-SAM  
  - microSAM  
  - CellSAM  
  - Mesmer  
  - InstanSeg  

---

## 四、资源与算力

- **文中未明确说明训练或推理所用的算力资源**（如 GPU 型号、数量、训练时间等）。  
  - 鉴于所评估模型均为预训练的“基础模型”，作者可能仅进行了推理与微调操作，而非重新训练。
  - 因此算力需求相对低，但具体资源配置未列出。

---

## 五、实验数量与充分性

- **实验覆盖范围**：
  - 涉及三类成像模态（相差、荧光、空间组学），共对六个代表性模型进行评估；
  - 包含定量对比与下游分析差异评估两层实验；
  - 部分结果探讨了模型间差异带来的聚类与细胞类型识别偏差。
- **充分性与公平性**：
  - 覆盖面广，体现了跨模态与跨任务的公平比较；
  - 使用公共数据与统一指标，保证了客观性；
  - 若论文未涉及数据标注质量控制与随机重复实验设置，则这一环节可能在稳健性上有一定局限。

---

## 六、主要结论与发现

- **性能表现**：
  - Cellpose-SAM 在相差显微镜图像上表现最佳。
  - SAM 系列模型（包括 microSAM、CellSAM）在荧光细胞培养数据上表现稳定且优越。
  - 在 CODEX 多重成像数据上，没有单一模型全方位占优，不同模型在细胞类型分辨与空间位置保持方面有各自优势。
- **整体发现**：
  - 通用模型在跨模态应用时表现出“分化优势”，即不同模型针对不同成像数据的特性各有适应性。
  - 分割结果差异会在下游聚类和细胞类型识别阶段显著影响生物学解释。

---

## 七、优点与亮点

- **研究设计层面**：
  - 建立了跨模态系统评价框架，填补领域空白。
  - 同时考虑分割精度与生物学分析影响，拓展评估维度。
- **方法层面**：
  - 聚焦于“基础模型”的迁移能力，而非传统任务特定模型。
  - 涉及多种开放模型，具有较强的实用参考价值。
- **实践意义**：
  - 为生物图像分析人员提供了模型选择的定量依据；
  - 强调分割模型与下游任务间的逻辑关联。

---

## 八、不足与局限

- **技术局限**：
  - 未提供详细的算法微调或算力信息，难以评估效率与资源开销。
  - 对分割误差对下游生物学结论的具体影响缺乏深入定量分析。
- **实验覆盖限制**：
  - CODEX 数据较复杂，模型结果差异大，但未进一步针对该模态做针对性优化或解释机制研究。
  - 缺乏关于模型泛化能力在未知组织类型上的实验证据。
- **应用限制**：
  - 对实时显微成像的处理效率与可扩展性讨论有限；
  - 结果主要集中于静态图像分析，尚未涉及动态活细胞追踪场景。

---

（完）
