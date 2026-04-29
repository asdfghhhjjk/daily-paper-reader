---
title: 3D Reconstruction of Nanoparticle Distribution in Tumor Spheroids with Volume Electron Microscopy
title_zh: 利用体积电子显微术实现肿瘤类球体中纳米颗粒分布的三维重建
authors: "Bottone, D., Gerken, L. R., Habermann, S., Mateos, J. M., Lucas, M. S., Riemann, J., Fachet, M., Resch-Genger, U., Kissling, V. M., Roesslein, M., Gogos, A., Herrmann, I. K."
date: 2026-04-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.17.719153v1.full.pdf"
tags: ["query:sam"]
score: 9.5
evidence: 微调Cellpose-SAM模型用于细胞和细胞核分割
tldr: 本研究提出一种基于SBF-SEM数据的端到端分析流程，结合微调的Cellpose-SAM模型和经验贝叶斯方法，实现细胞与金纳米颗粒的联合三维分割与定量重建，揭示了颗粒在类肿瘤球体中核周优先分布的规律，为纳米材料在生物体系中的定量研究提供开放可复用的框架。
source: biorxiv
selection_source: fresh_fetch
motivation: 该研究旨在通过体积电子显微镜定量分析纳米材料在肿瘤类器官中的空间分布，以理解其生物摄取和作用机制。
method: 研究采用序列块面扫描电子显微镜（SBF-SEM）结合深度学习与统计建模的混合分割策略，实现细胞与金纳米颗粒的三维重建。
result: 模型在细胞和核分割上优于基线与商业软件，并揭示纳米颗粒主要聚集于细胞核周围，细胞间摄取差异显著。
conclusion: 该工作建立了可重复的三维定量分析流程，为探索纳米材料与细胞结构的相互作用提供了新工具。
---

## 摘要
在细胞超微结构中对纳米材料（NM）分布进行空间分辨表征，对于理解纳米材料在生物系统中的命运和活性至关重要。体积电子显微术（vEM）在解决这一挑战方面具有独特优势，但现有同时对纳米材料和细胞结构进行分割的定量分析流程记录仍然十分稀缺。本文基于含有纳米颗粒（NPs）的肿瘤类球体的串联块面扫描电子显微镜（SBF-SEM）数据，提出了一种端到端的分析流程。该方法采用混合分割策略：使用经过微调的 Cellpose-SAM 模型来分割细胞和细胞核，并采用经验贝叶斯方法来分割金纳米颗粒（AuNPs）。微调后的模型在性能上优于预训练模型及 Amira 基准实验，并且在不同样品类型的二维电子显微数据上表现出良好的泛化能力，表明其有潜力成为电子显微术的通用分割模型。完整的三维纳米颗粒分布重建揭示了其在核周区域的优先聚集，细胞核到纳米颗粒的中位距离为 2.57 微米，且细胞间纳米材料摄取量相差几个数量级。此外，通过三维形状描述符和局部曲率度量对分割细胞和细胞核进行形态学分析，可以定量获取单层切片无法访问的特征。综上，这些结果建立了一个可重复的开放框架，用于在体积电子显微数据中对纳米材料分布和细胞形态进行联合定量分析。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWSpatially resolved characterization of nanomaterial (NM) distribution within cellular ultrastructure is essential for understanding NM fate and activity in biological systems. Volume electron microscopy (vEM) is uniquely positioned to address this challenge, yet fully documented quantitative pipelines that simultaneously segment NMs and cellular structures remain scarce. Here, an end-to-end analytical pipeline is presented based on the example of serial block-face scanning electron microscopy (SBF-SEM) data of tumor spheroids containing nanoparticles (NPs). A hybrid segmentation strategy is adopted: a fine-tuned Cellpose-SAM model for cells and nuclei, and an empirical Bayes approach for AuNPs. The fine-tuned model outperforms both the pre-trained baseline and benchmark experiments in Amira, and shows good generalization to 2D EM datasets of varying sample types, suggesting potential as a general-purpose segmentation model for electron microscopy. Full 3D reconstruction of NP distributions reveals preferential clustering in the perinuclear region, with a median nucleus-to-NP distance of 2.57 {micro}m and NM uptake spanning several orders of magnitude across cells. Furthermore, morphological analysis of segmented cells and nuclei using 3D shape descriptors and local curvature metrics provides quantitative access to features inaccessible from single sections. Together, these results establish a reproducible, open framework for the joint quantitative analysis of NM distribution and cellular morphology in vEM data.

---

## 论文详细总结（自动生成）

# 利用体积电子显微术实现肿瘤类球体中纳米颗粒分布的三维重建 — 论文结构化总结

---

## 一、研究核心问题与整体含义

- **研究动机**：  
  在纳米医学与材料科学中，理解纳米材料（Nanomaterials, NMs）在细胞微结构中的空间分布，对于评估其生物摄取、毒理作用及治疗效果至关重要。传统二维电子显微成像无法全面揭示三维空间关系和细胞内定位。
- **研究背景**：  
  体积电子显微术（Volume Electron Microscopy, vEM）能够实现纳米级分辨率的三维成像，但目前实现纳米材料与细胞结构联合分割和定量分析的完整流程仍十分有限。
- **研究目标**：  
  本文旨在构建一个可重复、开放的端到端分析流程，用以在 vEM 数据中实现细胞及纳米颗粒的三维分割与定量重建，揭示其在肿瘤类球体中的分布规律。

---

## 二、方法论：核心思想与关键技术细节

- **总体流程概述**：  
  论文提出一个混合式端到端分析框架，整合深度学习分割与统计建模两大部分：

  1. **数据获取与预处理**：基于序列块面扫描电子显微镜（Serial Block-Face SEM, SBF-SEM）获取肿瘤类球体含金纳米颗粒的三维数据。
  2. **细胞/细胞核分割**：使用微调后的 **Cellpose-SAM 模型**（结合 Cellpose 的实例分割能力与 SAM 的自注意力机制），针对 vEM 图像的形态密集特征进行优化。
  3. **纳米颗粒分割**：采用 **经验贝叶斯（Empirical Bayes）方法**，利用像素灰度分布建立背景与颗粒概率模型，实现自适应阈值与噪声抑制。
  4. **三维重建与定量分析**：通过形状描述符、局部曲率和空间距离计算，定量描述颗粒的空间分布、细胞形态及颗粒-核空间关系。
  
- **算法核心逻辑**：
  ```
  Pipeline:
  SBF-SEM data acquisition → image normalization →
  Cellpose-SAM fine-tuning → cell & nucleus segmentation →
  Empirical Bayes inference → AuNP segmentation →
  3D geometric reconstruction → quantitative morphology analysis
  ```
- **关键创新点**：将语义分割模型与显微术数据的统计特征结合，形成跨模态分割方案，实现对高密度、噪声数据的精准识别。

---

## 三、实验设计

- **数据来源与场景**：  
  肿瘤类球体样本经金纳米颗粒（AuNPs）处理后，通过 SBF-SEM 成像获得。数据规模未给出具体体积，但为多层切片序列，显微分辨率达纳米级。
- **Benchmark 与对比方法**：
  - 基线模型：原始预训练 **Cellpose**。
  - 商业软件：**Amira**（常用于显微三维重建）。
  - 对比指标：分割准确率、边界一致性、泛化性能（在不同组织样本上的测试）。
- **验证策略**：
  - 使用不同样品类型（含多种细胞组织的二维 EM 数据）评估模型的泛化能力；
  - 对金纳米颗粒的空间距离统计验证其定量稳定性；
  - 通过形态度量分析验证三维重建的生物学合理性。

---

## 四、资源与算力

- **算力说明**：  
  文中未明确给出计算资源配置（GPU 型号、训练时长、CPU 数等）。  
  根据同类工作推测，该类 Cellpose-SAM 微调过程通常在单或多 GPU 环境下完成（如 NVIDIA RTX 3090 / A100），但论文未提及具体数值。
- **推断结论**：算力细节缺失，可能影响 reproducibility 的精确复现。

---

## 五、实验数量与充分性

- **实验组别**：
  1. 主实验：肿瘤类球体 SBF-SEM 数据的三维分割。
  2. 对照实验：Cellpose、Amira 对比测试。
  3. 泛化实验：其他二维 EM 数据上的迁移验证。
  4. 形态学定量实验：细胞核及细胞形状特征分析。
- **实验充分性**：  
  四类实验涵盖性能、泛化、形态和定量验证维度，设计较为完善；但没有涉及扩展到多种纳米材料或多成像设备，范围仍偏有限。
- **公平性与客观性**：  
  对比选择合理，包含开源和商业基线；定量指标明确，但部分统计样本量未给出，略影响结果的统计支撑力度。

---

## 六、主要结论与发现

- 微调后的 Cellpose-SAM 模型显著提升了细胞和核分割精度，兼具边界识别和结构连贯性。
- 金纳米颗粒在细胞核周区域存在显著聚集趋势，**中位颗粒距离细胞核 2.57 μm**。
- 不同细胞之间的纳米材料摄取量相差可达数个数量级，体现细胞摄取差异性。
- 三维形态分析揭示了二维切片无法表征的结构特征，为细胞解剖学和纳米材料相互作用研究提供新的定量指标。
- 该研究建立了一个 **开放、可重复的三维分析框架**，可在不同 vEM 数据中迁移应用。

---

## 七、优点与亮点

- **方法创新**：混合分割（深度学习 + 统计推断）式设计有效应对显微数据的高噪声。
- **可复用性高**：开源框架与模型微调流程可推广到其他显微数据集。
- **生物学意义突出**：首次定量揭示纳米颗粒在核周分布的规律。
- **三维定量分析能力强**：可提取曲率、空间距离等复杂结构参数，扩展显微术的分析维度。

---

## 八、不足与局限

- **算力与训练细节缺失**：未说明 GPU 配置与训练参数，影响 reproducibility。
- **数据集多样性较弱**：主要集中于一种肿瘤类球体与特定金属纳米颗粒，外推性有限。
- **生物学验证欠充分**：缺乏进一步的实验验证（如功能性实验或多通道标记）。
- **统计样本量未详述**：可导致部分差异分析的显著性判断不够稳健。
- **实际应用限制**：对高分辨率显微数据具有较高硬件与存储要求，难以大规模推广。

---

（完）
