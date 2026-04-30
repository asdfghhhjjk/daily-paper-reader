---
title: "H2O: A Foundation Model Bridging Histopathology to Spatial Multi-Omics Profiling"
title_zh: H2O：连接组织病理学与空间多组学分析的基础模型
authors: "Gu, Y., Wu, Z., Yan, R., Wang, Z., Li, Y., Lin, S., Cui, Y., Lai, H., Luo, X., Zhou, S. K., Yuan, Z., Yao, J."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.717342v1.full.pdf"
tags: ["query:pathseg"]
score: 10.0
evidence: "连接H&E组织病理学与空间多组学的病理基础模型"
tldr: "论文提出H2O框架，利用AI桥接病理H&E图像与空间多组学信息。结合ViT与LLM进行跨模态对比学习，能从病理图像预测空间转录组与蛋白组表达，在多癌种数据上表现优异，重现关键信号通路，拓展组织分子分析的可扩展性。"
source: biorxiv
selection_source: fresh_fetch
motivation: "空间组学虽能提供分子图谱，但成本高，无法广泛应用，而病理H&E图像则普遍易得。"
method: 模型结合视觉Transformer与大型语言模型，通过对比学习对齐组织形态与分子知识。
result: H2O在25种器官和癌症类型的130万对图像上训练，预测空间转录组和蛋白组精度高，优于现有模型。
conclusion: H2O展示了将常规组织病理图像转化为空间多组学信息的潜力，实现了更高效的组织分子分析与整合。
---

## 摘要
空间组学技术已经彻底改变了组织的分子分析方式，但仍受限于高成本和扩展性不足。尽管苏木精-伊红（H&E）染色在临床中广泛应用，但其缺乏分子特异性。本文提出了 H2O（Histopathology to Omics），一种通用人工智能框架，用于连接组织病理学与空间多组学之间的模态差距，使得能够从常规 H&E 图像直接推断空间转录组学（ST）和蛋白质组学（SP）景观。H2O 通过对比学习将视觉 Transformer（ViT）与大型语言模型（LLM）整合，以对齐组织形态学与语义分子知识。这种跨模态方法使模型能够将空间表达谱信息融入组织学模式识别中，从而有效解码组织形态背后的分子异质性。H2O 在一个涵盖 25 种器官和癌症类型的跨组织数据集中进行训练，包含 130 万对配对的 H&E 与空间图像块，能够从组织学预测空间组学表达，与测序结果高度一致，并在三个癌症基准测试中持续优于最先进的模型。值得注意的是，H2O 可直接从 H&E 图像中恢复 MIF-CD74/CD44 信号通路，展示其无需分子测定即可推断具有生物意义的细胞间通信的能力。在三个额外的公共队列中（包括胎儿和儿童胸腺组织、人类转移性淋巴结和乳腺癌）应用 H2O，涵盖人类发育、三维空间框架及综合多组学分析，模型获得生物一致性见解，展现出卓越的准确性、稳健性和广泛的通用性。H2O 通过计算生成转录组和蛋白质组景观，将常规组织病理学转化为空间分辨多组学分析的入口，从而增强组织表型分析，并推动可扩展的、综合的组织图谱构建。

## Abstract
Spatial omics technologies have revolutionized the molecular profiling of tissues but remain constrained by high costs and limited scalability. While hematoxylin and eosin (H&E) staining is ubiquitous, it lacks molecular specificity. Here, we present H2O (Histopathology to Omics), a generalist AI framework that bridges the modality gap between histopathology and spatial multi-omics, enabling the direct inference of spatial transcriptomics (ST) and proteomics (SP) landscapes from routine H&E images. H2O integrates Vision Transformers (ViT) with Large Language Models (LLM) via contrastive learning to align histological morphology with semantic molecular knowledge. This cross-modal approach allows the model to incorporate spatial expression profiles into histological pattern recognition, effectively decoding the molecular heterogeneity underlying tissue morphology. Trained on a pan-tissue dataset of 1.3 million paired H&E-spatial patches across 25 organs and cancer types, H2O predicts spatial omics expression from histology with high concordance to sequenced measurements and consistently outperforms state-of-the-art models across three cancer benchmarks. Notably, H2O recovers the MIF-CD74/CD44 signaling axis directly from H&E images, highlighting its capacity to infer biologically meaningful cell-cell communication without molecular profiling. Applying on three additional public cohorts covering fetal and paediatric thymus tissues, human metastatic lymph node, and breast cancer, encompassing human development, 3D spatial frameworks, and integrative multi-omics, H2O yields biologically concordant insights, demonstrating superior accuracy, robustness, and generalizability across real-world applications in diverse scenarios. H2O converts routine histopathology into a portal for spatially resolved multi-omics profiling by computationally generating transcriptomic and proteomic landscapes, thereby enhancing tissue phenotyping and enabling scalable, integrative tissue-atlas construction.

---

## 论文详细总结（自动生成）

# H2O：连接组织病理学与空间多组学分析的基础模型 — 综合总结

---

## 一、研究背景与核心问题

- **研究动机**  
  空间组学（spatial omics）技术能揭示组织在空间维度上的分子图谱，对于理解疾病机制至关重要。但其**成本高、技术复杂且无法广泛应用于常规临床样本（如FFPE）**，限制了推广。  
  相比之下，**苏木精-伊红（H&E）染色病理图像**在临床中普遍易得、成本低、覆盖面广，但缺乏分子层面的特异性。

- **核心问题**  
  如何将常规病理图像中隐含的形态信息与高维的分子空间表达对应起来，从而**在不进行昂贵组学测序的情况下推断组织的分子特征**？

- **研究目标与意义**  
  作者提出 *H2O（Histopathology to Omics）* 框架，通过跨模态基础模型建立组织病理学与空间多组学之间的桥梁，使得可以从H&E图像生成空间转录组（ST）与空间蛋白组（SP）表达分布。这一方法有望实现：
  - 病理图像的分子解码；
  - 大规模组织分子图谱的自动化构建；
  - 将多组学知识融入病理分析流程。

---

## 二、方法论与技术框架

### 核心思想
H2O 是一个**对比学习驱动的跨模态基础模型**，旨在将组织形态特征与分子表达特征对齐。模型由两个部分组成：
1. **图像基础模型（Image FM）**：基于 Vision Transformer (ViT, DINOv2 变体)，学习组织形态表征；
2. **空间转录组基础模型（ST FM）**：基于 scGPT 大模型，对 ST 数据进行微调，以获得分子语义嵌入。

### 算法流程（文字说明）

1. **图像编码阶段**  
   - 从TCGA和GTEx等数据集中提取5,400多万张H&E病理图像块（224×224像素），训练Image FM。
   - 使用邻域聚合（Neighbourhood aggregation）和 1D 卷积策略，整合局部空间上下文。
   - 引入 **FiLM（Feature-wise Linear Modulation）** 模块，通过“点径条件(diameter-conditioned)”输入，实现不同空间分辨率样本的适应性。

2. **分子特征编码阶段**  
   - 基于scGPT架构，将空间转录组表达矩阵（spot×gene）转化为“基因token + 表达值 + 条件token”三类输入；
   - 微调scGPT在HEST-1k数据集上，使其能捕捉空间组学特征。

3. **跨模态对比学习（Contrastive Alignment）**  
   利用CLIP风格的目标函数最大化H&E与ST匹配样本的相似度，最小化不匹配样本的相似度。  
   联合训练损失：  
   \[
   L_{total} = \alpha L_{contrastive} + \beta L_{reconstruction}
   \]
   即在保证跨模态对齐的同时，回归精确的分子表达值（MSE损失）。

4. **预测与解码**  
   将对齐后的嵌入输入至3层MLP解码器，生成目标基因或蛋白的空间分布预测。  
   支持下游任务：空间聚类、细胞通讯推断、时间轨迹还原及3D重建。

---

## 三、实验设计与评估体系

### 数据集覆盖
模型训练和验证使用了 **四类主要数据集**：
- **HEST-1k**：包含1,229个配对样本（H&E-ST），覆盖25种器官与癌症类型，用于主训练和benchmark。
- **HTSA（Human Thymus Spatial Atlas）**：用于验证人类发育过程中的空间轨迹预测。
- **OpenST**：来自转移性淋巴结的30张连续切片（19张配对ST+H&E），用于3D空间重建实验。
- **HTAPP（Human Tumor Atlas Pilot Project）**：MERFISH (ST) 与 CODEX (SP) 双模态乳腺癌数据，用于多组学扩展实验。

### 对比方法
作者将 H2O 与以下 **四种主流模型**对比：
1. **HisToGene**  
2. **BLEEP**  
3. **DeepPT**  
4. **OmiCLIP**  

在 ccRCC（肾透明细胞癌）与 PRAD（前列腺癌）两个benchmark上统一评估。

### 评估指标
- **相关性指标**：Pearson (PCC)、Spearman (SRCC)、Concordance (CCC)
- **误差指标**：RMSE
- **聚类一致性**：Adjusted Rand Index (ARI)、Adjusted Mutual Information (AMI)
- **功能验证**：基因集富集分析（GSEA）、细胞通讯回路检测（CellNEST）

---

## 四、资源与算力

- 论文未披露具体**GPU型号、数量或训练时长**。  
- 提到训练数据量超过 **5,400万张图像块** 与 **130万对图像-组学匹配样本**，表明该模型需要大规模算力环境（推测为分布式多GPU训练）。  
- 因未公开具体硬件配置，算力指标无法量化。

---

## 五、实验数量与充分性

- **主要实验**：共进行五个维度验证  
  1. 在 ccRCC / PRAD 中的 ST 预测benchmark；  
  2. 在外部 IDCLymphNode 数据集上的跨癌种泛化实验；  
  3. 在 HTSA 上的人类胸腺发育时序预测；  
  4. 在 OpenST 上的 3D 空间重建；  
  5. 在 HTAPP 上的多模态 ST+SP 联合预测。

- **消融实验**：包括 FiLM模块、邻域聚合、对比学习机制的消融，展示各模块的贡献。

- **实验充分性与公平性**：  
  模型与对比方法统一训练和测试集；度量指标标准化；多数据源和跨平台验证（Visium、Xenium、CODEX），具有较高的客观性与外部验证力。

---

## 六、主要结论与发现

- H2O 能够在常规 H&E 图像上**高精度预测空间转录组表达**，在 PCC/SRCC 上显著优于 SOTA 模型。  
- 能重建关键细胞通讯通路，如 **MIF–CD44/CD74** 轴，表明模型理解生物功能层面的关系。  
- 在发育系统中，成功重现 **T细胞发育轨迹** 与 **SPP1/CCL2/IL33** 在胎儿至儿童阶段的空间重组。  
- 在3D分析中，揭示肿瘤侵袭前沿的连续动态结构（CAF与SPP1+巨噬细胞的交互）。  
- 在多组学场景下，能同时预测空间转录组与蛋白组数据，并在WNN聚类中捕捉RNA与蛋白的互补信息。

---

## 七、方法与设计亮点

- **跨模态基础模型创新**：首个将 ViT 与 scGPT 通过对比学习直接对齐的架构。  
- **生物语义融合**：模型不仅学习形态，还学习转录组的语义依赖（gene–gene关系）。  
- **多尺度适应**：通过 FiLM 模块处理不同技术平台的分辨率差异，增强泛化。  
- **空间上下文聚合**：邻域卷积模块模仿人类病理诊断的“局部+邻域”认知逻辑。  
- **医学实用潜力**：能在 FFPE 样本上推断分子特征，降低实验成本并支持临床扩展。

---

## 八、不足与局限

- **算力与资源透明度不足**：论文未披露训练硬件与时长，不利于复现。  
- **数据覆盖有限**：虽覆盖多组织，但对罕见组织或特殊病理状态的表现未知。  
- **细胞级精度有限**：预测基于224×224像素块+邻域上下文，难以达到单细胞级分辨率。  
- **模型扩展性**：SP预测采用轻量MLP，无专门蛋白前体模型，精度仍有提升空间。  
- **未覆盖代谢组/表观组层面**：未来可拓展至更多组学维度。  
- **生成能力局限**：当前为预测模型，尚不具备生成全片组学图谱的能力。

---

**综合评价**

H2O 建立了一个强大的跨模态基础框架，使病理图像成为空间多组学分析的低成本入口。其在多癌种、发育、3D与多组学任务中的表现均验证了模型的**准确性、稳健性与可推广性**。  
尽管仍存在细胞尺度与算力透明度的限制，H2O 为下一代“图像即组学”的医学AI奠定了重要基础。

---

（完）
