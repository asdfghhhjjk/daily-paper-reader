---
title: "Interpreting and Validating a Deep Learning Model Predictive of Spatial Morphologic-Molecular Patterns in Lung Adenocarcinoma, Using Ground Truth Immunohistochemistry"
title_zh: 利用免疫组织化学真实对照解释并验证一种可预测肺腺癌空间形态–分子模式的深度学习模型
authors: "Rao, V. R., Workman, A. A., Palisoul, S. M., Limoge, C. J., Vaickus, L. J., Zanazzi, G. J., Lu, L., Liu, X., Sukhadia, S. S."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719723v1.full.pdf"
tags: ["query:pathseg"]
score: 9.0
evidence: "针对肺腺癌H&E全切片图像的深度学习模型"
tldr: 该研究提出了XpressO-Lung深度学习模型，通过学习组织形态与转录组数据的关联，在肺腺癌诊断切片上预测基因空间表达异质性，并利用免疫组化实验验证模型预测的空间模式，从而实现病理图像与分子特征的可解释性连接。
source: biorxiv
selection_source: fresh_fetch
motivation: 由于肺腺癌分子和形态异质性强，而基因组与空间转录组分析昂贵且复杂，研究旨在用可解释AI模型实现病理图像与分子信息的融合。
method: 研究开发了XpressO-Lung模型，将HE染色切片形态与总体转录组数据关联，实现基因空间表达预测。
result: 模型在200例LUAD样本上预测多个基因的空间表达模式，AUC介于0.64到0.92，并在外部免疫组化验证中表现出高度一致性。
conclusion: 该模型有效连接组织形态与基因表达空间信息，为肺腺癌的生物标志物发现与精准治疗提供新工具。
---

## 摘要
肺腺癌（LUAD）是非小细胞肺癌中最常见的亚型，表现出显著的组织学和分子异质性。尽管基因组分析已经识别出关键的致癌驱动因子和免疫特征，但其应用受制于成本、技术要求及样本可获得性。此外，空间转录组学虽然能够提供分子层面的空间性洞察，但仍然具有挑战性且耗时。为了解决这一问题，我们开发了 XpressO-Lung，这是一种可解释的深度学习模型，能够通过学习组织形态与对应的整体转录组数据之间的关联，在基于苏木精–伊红（H&E）染色的诊断全切片图像（Dx WSIs）上预测肿瘤及其微环境中的基因表达异质性的空间分布。利用来自癌症基因组图谱（The Cancer Genome Atlas, TCGA）的 200 例 LUAD 样本，XpressO-Lung 在 Dx-WSIs 上预测了 NAPSA、TP53I3、CD8A、TTF1、KRT7、CDKN2A、FOXO1、KEAP1、RB1 和 TP53 的空间表达模式，AUC 范围为 0.64 至 0.92。模型预测的空间基因表达模式与已知的肿瘤及其微环境形态学相互作用高度一致，能够在 Dx-WSIs 上直接捕捉生物学事件。这些空间–形态–分子关联进一步通过达特茅斯健康中心的临床样本免疫组织化学验证，显示出模型预测的空间模式与实际组织形态学特征的一致性。通过将预测性能与 Dx-WSIs 上基因表达的空间可解释性相结合，XpressO-Lung 模型在组织病理学与整体转录组学之间架起了桥梁，为 LUAD 的生物标志物发现、治疗分层及精准肿瘤学研究提供了一种可解释的空间–形态–基因组分析途径。

## Abstract
Lung adenocarcinoma (LUAD), the most common subtype of non-small cell lung cancer, exhibits profound histological and molecular heterogeneity. While genomic profiling has identified key oncogenic drivers and immune signatures, its use is limited by cost, technical demands and tissue availability. In addition, spatial transcriptomics provides spatially resolved molecular insights but remains challenging and time-consuming. To address this gap, we developed XpressO-Lung, an explanatory deep learning model that predicts gene expression heterogeneity spatially in tumor and its microenvironment on hematoxylin and eosin based diagnostic (Dx) whole-slide images (WSIs) by learning associations between tissue morphology and the corresponding bulk-transcriptomic data. Utilizing 200 LUAD cases from The Cancer Genome Atlas, XpressO-Lung predicted spatial expression patterns of NAPSA, TP53I3, CD8A, TTF1, KRT7, CDKN2A, FOXO1, KEAP1, RB1 and TP53 on Dx-WSIs with AUCs ranging from 0.64 to 0.92. The predicted spatial gene expression patterns aligned with the known morphologic interactions of the tumor and its microenvironment, capturing biological events directly on Dx-WSIs. These spatio-morpho-molecular associations were further validated using immunohistochemistry on an external set of clinical samples at Dartmouth Health, demonstrating concordance between model-predicted spatial patterns and observed histomorphologic features. By coupling predictive performance with spatial interpretability of gene expression on Dx-WSIs, the XpressO-Lung model bridges histopathology and bulk-transcriptomics, enabling explainable spatio-morpho-genomic analyses to advance biomarker discovery, therapeutic stratification and precision oncology in LUAD.

---

## 论文详细总结（自动生成）

# 论文总结：利用免疫组织化学验证的可解释深度学习模型预测肺腺癌空间形态–分子模式

---

## 一、核心问题与研究背景

- **研究动机**  
  肺腺癌（LUAD）是非小细胞肺癌中最常见的类型，具有显著的组织学和分子异质性。传统的基因组测序与空间转录组学方法虽然能够揭示肿瘤内部的分子机制，但其应用受限于：
  - 高昂的成本与复杂的实验条件；
  - 对组织形态空间信息的利用效率低；
  - 临床常规病理切片数据未被充分挖掘。

- **研究目标**  
  研究旨在开发一种可解释的人工智能模型，通过普通的 H&E 染色病理图像（Dx whole-slide images, WSIs），预测肿瘤及其微环境中的 **空间基因表达模式与异质性**，为精准诊断和分子标志物研究提供更具实用性的工具。

---

## 二、方法论：XpressO-Lung 模型框架与技术路线

- **核心思想**
  - 利用深度学习模型学习组织形态与转录组数据之间的关联；
  - 在病理全切片级别上预测特定基因的空间表达分布，并以可解释的「热图」形式展示结果；
  - 结合免疫组织化学（IHC）结果验证模型的准确性和生物学合理性。

- **技术架构**
  1. **数据预处理**：  
     - 使用 XpressO 管线的分割模块，将 20× 放大下的 H&E 图像划分为 256×256 像素的非重叠图块；
     - 采用 CLAM 框架的弱监督多实例学习（MIL）方法分配注意力权重，选取最具信息性的图像 patch。
  2. **特征提取**：  
     - 使用基于 Vision Transformer 的预训练模型（ViT-L/16，经 DINOv2 训练），生成高维特征嵌入。
  3. **建模与训练**：  
     - 模型基于 CLAM-SB 架构；
     - 使用二元交叉熵损失函数和 Adam 优化器（学习率 2×10⁻⁴），迭代 200 epochs；
     - 每个基因单独训练一个分类器，弱监督地学习 slide-level 的高 / 低表达类别。
  4. **输出与解释**：  
     模型生成空间热图（attention heatmap），以红—黄—蓝渐变反映基因表达高低区域，实现可视化解释。

---

## 三、实验设计

- **数据来源**
  - 主数据集：**The Cancer Genome Atlas (TCGA-LUAD)** 共 200 个肺腺癌病例；
  - 外部验证集：来自 **Dartmouth Health** 的 8 例临床组织样本，用于免疫组织化学验证。
  - RNA-seq 数据形式为 FPKM，经过中位数分割二值化为“高/低”表达。

- **实验场景与任务**
  - 使用模型预测 10 个关键基因的表达空间分布：
    NAPSA、TP53I3、CD8A、TTF1、KRT7、CDKN2A、FOXO1、KEAP1、RB1、TP53。
  - 评估指标：
    - AUC-ROC（0.64–0.92）
    - 准确率、精确率、召回率、F1 值及其置信区间。

- **参考与对比方法**
  - 未与其他模型直接定量比较，但参考了 CLAM 以及作者此前的 XpressO-Breast 和 XpressO-Melanoma 模型；
  - 主要与免疫组织化学（IHC）实验结果进行**空间一致性验证**。

---

## 四、算力与资源

- **计算资源**  
  文中未明确说明训练所用 GPU 型号、数量或训练时间，仅说明使用 Python 环境与预训练的 Vision Transformer (ViT-L/16, DINOv2)。  
  因此，算力信息 **未公开**。

---

## 五、实验数量与充分性

- **主实验**  
  - 10 个基因单独训练并测试，共得到 10 套性能指标；
  - 200 例 TCGA 病例用于训练与内部测试（包括验证集与独立测试集划分）；
  - 8 例达特茅斯样本用于外部空间验证。
- **补充实验**
  - 每个基因生成空间热图，进行了病理学专家人工比对；
  - 附加 STRING 网络分析，验证所选基因对 LUAD 及相关疾病的通路相关性。
- **充分性判断**  
  虽未包含严格的消融实验或多模型对比，但在研究目标（空间匹配与可解释性验证）范围内实验较为完整，生物学验证丰富。

---

## 六、主要结论与发现

1. **模型性能优异**：  
   各基因预测 AUC 介于 0.64–0.92，充分展示区分高/低表达的能力。
2. **空间表达模式符合生物学知识**：  
   模型生成的空间热图与已知肿瘤组织形态和免疫微环境结构吻合。
3. **IHC 验证结果一致**：  
   模型预测的空间高表达区域与免疫染色信号显著重合，证明模型辨识能力可靠。
4. **模型建立了病理图像与转录组之间的桥梁**：  
   可作为廉价、高效的空间分子分析手段，辅助精准病理诊断。

---

## 七、方法与实验亮点

- **创新点**
  - 在常规 H&E 切片上直接实现空间转录组预测；
  - 弱监督学习结合注意力机制，实现可解释性；
  - 外部真实组织样本的免疫组化比对确保生物学可信度；
  - 可视化模块（热图）直观呈现肿瘤与微环境中基因的空间异质性。
- **跨模态融合**
  - 整合病理影像、RNA-seq 和免疫组化三种数据；
  - 以解释性深度学习实现形态–分子对应分析。

---

## 八、不足与局限

- **数据量与验证规模**  
  外部验证集仅 8 例样本，统计充足性有限。
- **缺乏基准对比**  
  未与现有空间转录组学或图像预测模型做定量对照。
- **算力与参数透明性不足**  
  论文未说明硬件配置与训练耗时。
- **预测层次局限**  
  基于组织级别的弱监督，无法解析亚细胞层面的表达差异。
- **潜在偏差与泛化风险**  
  TCGA 单中心数据可能带有样本采集偏差；需要多机构扩展验证。

---

（完）
