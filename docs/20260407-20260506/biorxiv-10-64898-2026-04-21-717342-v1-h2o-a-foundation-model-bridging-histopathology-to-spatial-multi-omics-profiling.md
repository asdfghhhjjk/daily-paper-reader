---
title: "H2O: A Foundation Model Bridging Histopathology to Spatial Multi-Omics Profiling"
title_zh: H2O：连接组织病理学与空间多组学分析的基础模型
authors: "Gu, Y., Wu, Z., Yan, R., Wang, Z., Li, Y., Lin, S., Cui, Y., Lai, H., Luo, X., Zhou, S. K., Yuan, Z., Yao, J."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.717342v1.full.pdf"
tags: ["query:pathseg"]
score: 9.0
evidence: 连接组织病理学与空间多组学的基础模型
tldr: "本研究提出H2O，一种融合视觉Transformer与大语言模型的通用AI框架，可从常规H&E病理图像直接推断组织的空间转录组和蛋白质组分布。该模型在多器官癌症数据上表现优异，实现对分子异质性的解码，并为大规模组织组学研究提供新途径。"
source: biorxiv
selection_source: fresh_fetch
motivation: "为克服空间组学高成本和低扩展性的限制，利用普遍存在的H&E染色图像推断分子层面信息。"
method: H2O通过对比学习将视觉Transformer与大语言模型结合，建立病理影像与空间组学间的跨模态映射。
result: 模型在25种组织和癌症类型数据上获得高一致性预测，并在多项癌症基准中超越现有模型。
conclusion: H2O展现出卓越的跨模态推理能力，为病理学与多组学数据融合提供可扩展的基础模型框架。
---

## 摘要
空间组学技术革新了组织的分子分析，但仍受限于高成本和有限的可扩展性。虽然苏木精-伊红（H&E）染色广泛应用，但缺乏分子特异性。本文提出了 H2O（Histopathology to Omics），一种通用人工智能框架，用于弥合组织病理学与空间多组学之间的模态差距，使得可以直接从常规的 H&E 图像推断空间转录组（ST）和空间蛋白组（SP）分布。H2O 通过对比学习，将视觉 Transformer（ViT）与大型语言模型（LLM）融合，以对齐组织形态学与分子语义知识。该跨模态方法使模型能够将空间表达谱融入组织学模式识别中，有效解码组织形态背后的分子异质性。H2O 在一个跨组织的训练数据集上进行训练，该数据集包含130万个配对的 H&E-空间图像块，涵盖25种器官和癌症类型。实验结果显示，H2O 能够以与测序结果高度一致的方式从组织学预测空间组学表达，并在三个癌症基准上持续优于现有的先进模型。值得注意的是，H2O 能够仅通过 H&E 图像恢复 MIF-CD74/CD44 信号通路，充分展示其无需分子检测即可推断出具有生物学意义的细胞间通信能力。进一步在三个公共队列中进行测试，这些队列涵盖胎儿及儿童胸腺组织、人类转移性淋巴结和乳腺癌，涉及人类发育、三维空间框架以及整合多组学，H2O 产生了与生物学一致的洞见，展现出其在真实场景中卓越的准确性、稳健性和泛化能力。H2O 将常规的组织病理学转化为可空间分辨的多组学分析门户，通过计算生成转录组和蛋白质组图谱，从而增强组织表型分析，并推动可扩展的综合组织图谱构建。

## Abstract
Spatial omics technologies have revolutionized the molecular profiling of tissues but remain constrained by high costs and limited scalability. While hematoxylin and eosin (H&E) staining is ubiquitous, it lacks molecular specificity. Here, we present H2O (Histopathology to Omics), a generalist AI framework that bridges the modality gap between histopathology and spatial multi-omics, enabling the direct inference of spatial transcriptomics (ST) and proteomics (SP) landscapes from routine H&E images. H2O integrates Vision Transformers (ViT) with Large Language Models (LLM) via contrastive learning to align histological morphology with semantic molecular knowledge. This cross-modal approach allows the model to incorporate spatial expression profiles into histological pattern recognition, effectively decoding the molecular heterogeneity underlying tissue morphology. Trained on a pan-tissue dataset of 1.3 million paired H&E-spatial patches across 25 organs and cancer types, H2O predicts spatial omics expression from histology with high concordance to sequenced measurements and consistently outperforms state-of-the-art models across three cancer benchmarks. Notably, H2O recovers the MIF-CD74/CD44 signaling axis directly from H&E images, highlighting its capacity to infer biologically meaningful cell-cell communication without molecular profiling. Applying on three additional public cohorts covering fetal and paediatric thymus tissues, human metastatic lymph node, and breast cancer, encompassing human development, 3D spatial frameworks, and integrative multi-omics, H2O yields biologically concordant insights, demonstrating superior accuracy, robustness, and generalizability across real-world applications in diverse scenarios. H2O converts routine histopathology into a portal for spatially resolved multi-omics profiling by computationally generating transcriptomic and proteomic landscapes, thereby enhancing tissue phenotyping and enabling scalable, integrative tissue-atlas construction.

---

## 论文详细总结（自动生成）

# H2O：连接组织病理学与空间多组学分析的基础模型 — 深度总结

---

## 一、研究核心问题与整体背景

- **核心问题**：  
  空间组学（spatial omics）技术能够在微观尺度解析组织中的转录与蛋白表达图谱，但实际应用受限于实验成本高、技术复杂以及样本兼容性差（尤其是 FFPE 样本）。  
  同时，H&E 染色病理图像虽然在临床中普遍存在，但仅提供形态学信息，缺乏分子层面解读能力。

- **研究动机**：  
  作者希望探索一种利用已有的病理影像数据、低成本且可扩展的方式，推断组织的 **空间分子特征**，即通过人工智能将 **组织形态映射至转录组和蛋白组表达空间**。  

- **总体目标**：  
  构建一个“图像到组学”的基础模型 —— **H2O（Histopathology to Omics）**，以跨模态对齐的方式将 H&E 图像与空间多组学数据统一建模，从而实现由常规病理图像直接预测空间转录组（ST）与空间蛋白组（SP）特征。

---

## 二、方法论与核心技术

### 1. 核心思想  
H2O 是一个以 **对比学习（contrastive learning）** 为核心的跨模态基础模型框架：
- 将 **视觉 Transformer（ViT）** 作为图像基础模型；
- 将 **单细胞大模型 scGPT（Large Language Model for Cells）** 作为组学语义模型；
- 通过对比学习对齐图像编码与组学编码，使模型在潜在空间中学习“形态—分子”的对应关系。

### 2. 模型结构与流程
- **输入数据**：  
  成千上万的配对 H&E 切片与空间转录组（ST）spots。
- **主要模块**：
  1. **图像编码（Image FM）**：基于 DINOv2 预训练的 Vision Transformer（ViT），输入 224×224 图像块，输出 384 维特征；
  2. **组学编码（ST FM）**：采用 scGPT 模型作为教师网络（teacher），通过在 ST 数据上微调（fine-tune），获得**空间特征感知**的基因表示；
  3. **跨模态对齐**：使用对比学习（CLIP 形式）最大化匹配 H&E–ST 配对样本间的相似度；
  4. **FiLM 模块**：基于 spot 直径（不同平台对应不同空间分辨率）进行特征线性调制，实现尺度自适应；
  5. **邻域上下文聚合**：通过卷积聚合相邻 patch 的上下文信息，增强空间连续性；
  6. **解码层**：多层感知机（MLP）将融合后的跨模态特征映射回基因表达或蛋白表达值。

- **训练目标函数**：  
  联合对比损失与重构损失：  
  \[
  L_{total} = \alpha \cdot L_{contrastive} + \beta \cdot L_{reconstruction}
  \]
  前者强调跨模态对齐，后者保证表达值重建精度。

---

## 三、实验设计与评测设置

### 1. 数据集与场景  
- **主训练集**：  
  - **HEST-1k** 数据集（MahmoodLab 发布），包含 1,229 份 H&E-ST 配对样本，1.3M 配对 patch，覆盖 **25 个器官**与癌种。  
- **补充数据与测试集**：
  - **TCGA / GTEx / 自建乳腺癌样本**：用于 Image FM 预训练；
  - **HTSA（Human Thymus Spatial Atlas）**：验证在时间尺度上的发育泛化能力；
  - **OpenST**：用于 3D 空间重建；
  - **HTAPP（来自 HTAN 项目）**：包含 MERFISH（RNA）与 CODEX（蛋白）配对，用于多组学融合测试。

### 2. Benchmark 设置与对比方法  
对比的主流方法包括：
- HisToGene (2021)  
- BLEEP (2023)  
- DeepPT (2024, Nature Cancer)  
- OmiCLIP (2025, Nature Methods)

评估指标：
- Pearson 相关系数（PCC）  
- Spearman 秩相关（SRCC）  
- Concordance correlation coefficient (CCC)  
- RMSE（均方根误差）

### 3. 实验任务覆盖
- 空间转录组预测（两个癌症基准：ccRCC + PRAD）  
- 跨癌种泛化验证（IDCLymphNode）  
- 空间域聚类与细胞-细胞通信分析  
- 发育系统验证（胸腺多阶段）  
- 3D 空间重构（OpenST）  
- 蛋白组预测与多模态整合（HTAPP）

---

## 四、资源与算力

- 论文中未明确提供 GPU 型号、显存大小、训练时长等算力信息。  
- 从数据规模（>5400 万 patch，训练样本约4.4万张切片）与使用基础模型（DINOv2 + scGPT）来看，推测训练需多 GPU 并行（≥8×A100 或同级别）及较长训练周期（多周级别）。  
- 未提供显存占用或 batch size 细节。

---

## 五、实验数量与充分性

- **实验维度丰富**：  
  包括跨癌种泛化、空间聚类、信号通路分析、发育时序验证、三维构建、蛋白组预测、多模态整合。
- **消融研究**：  
  对 FiLM 模块与邻域聚合进行了消融，验证其在多尺度一致性和空间连续性中的贡献。
- **公平性**：  
  所有对比模型均使用相同的训练/测试划分与评估基因集（5,033 genes）。  
  但论文未明确说明随机种子或超参调优策略，可能存在轻微偏差风险。  
- **充分性**：  
  涵盖多种器官、疾病、时间与空间维度，实验整体充分可靠。

---

## 六、主要结论与发现

1. **性能优势显著**：  
   H2O 在 ccRCC 与 PRAD 两个基准上均超越所有 SOTA 方法，预测相关度显著提升（提升幅度见 PCC/SRCC 图表）。  
2. **跨数据集泛化**：  
   在独立乳腺癌淋巴结数据上亦表现稳健，显示强跨癌种迁移能力。  
3. **生物学一致性**：  
   成功仅基于 H&E 图像重构出关键信号通路（MIF–CD74/CD44），揭示细胞间通讯网络。  
4. **发育与空间连续性复现**：  
   能够重建胸腺发育中 T 细胞分化轨迹及细胞亚型迁移。  
5. **3D 重构能力**：  
   在 OpenST 数据上实现肿瘤–免疫–基质空间的立体化预测。  
6. **多模态融合突破**：  
   能同时预测 RNA 与蛋白分布，实现跨模态互补聚类。

---

## 七、方法与实验的亮点

- **跨模态融合创新**：首次在病理图像与空间多组学间使用对比学习进行“图像—组学”语义对齐。  
- **利用已存在的病理资产**：使常规 H&E 切片在无需实验测序的情况下获得分子层面信息。  
- **多尺度适配（FiLM）机制**：解决不同 ST 平台之间的分辨率差异。  
- **广泛泛化性**：跨器官、跨组织、跨模态（ST→SP）均成功迁移。  
- **高层次生物验证**：不仅预测单基因表达，更能复现信号网络与发育轨迹。  
- **多组学整合潜力**：支持三维重构与多模态加权聚类（WNN），具备快速全景图谱生成前景。

---

## 八、不足与局限性

- **显式算力与设置缺失**：未披露 GPU 类型、训练时间，复现成本不透明。  
- **细胞级分辨率受限**：目前基于 patch（224×224），尚未实现真正的单细胞预测。  
- **蛋白组预测阶段功能仍有限**：缺乏专门的蛋白组预训练模型，仅采用轻量 MLP 解码。  
- **罕见组织代表性不足**：训练集中稀有组织及病理状态覆盖有限，对零样本迁移仍需验证。  
- **未探讨模型可解释性**：尚未对模型内部特征与生物意义的对应进行系统分析。  

---

**（完）**
