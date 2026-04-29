---
title: "H2O: A Foundation Model Bridging Histopathology to Spatial Multi-Omics Profiling"
title_zh: H2O：连接组织病理学与空间多组学分析的基础模型
authors: "Gu, Y., Wu, Z., Yan, R., Wang, Z., Li, Y., Lin, S., Cui, Y., Lai, H., Luo, X., Zhou, S. K., Yuan, Z., Yao, J."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.717342v1.full.pdf"
tags: ["query:pathseg"]
score: 9.0
evidence: "H&E图像的基础模型，连接空间组学"
tldr: "本研究提出跨模态基础模型H2O，通过整合视觉Transformer和大语言模型，从常规H&E病理图像推断空间转录组与蛋白组特征，实现组织分子景观的计算预测，在多器官和癌症数据集上表现卓越，显著提升了组织分子表征的精准性与可扩展性。"
source: biorxiv
selection_source: fresh_fetch
motivation: "空间组学虽能揭示组织分子特征，但成本高且难以大规模应用，而常规H&E染色缺乏分子特异性。"
method: 提出了H2O框架，将视觉Transformer与大语言模型结合，通过对比学习实现组织形态与分子信息的跨模态对齐。
result: "H2O能从H&E图像准确预测空间转录组和蛋白组表达，在多个癌症基准上优于现有方法，并揭示具有生物意义的信号通路。"
conclusion: H2O实现了从常规病理图像到空间多组学的高精度映射，为组织表型分析和可扩展的组织图谱构建提供了新途径。
---

## 摘要
空间组学技术革新了组织的分子谱分析，但仍受限于高成本和有限的可扩展性。尽管苏木精-伊红（H&E）染色广泛应用，但其缺乏分子特异性。本文提出了 H2O（Histopathology to Omics），一个通用的人工智能框架，用于弥合组织病理学与空间多组学之间的模态差距，从常规 H&E 图像直接推断空间转录组学（ST）和蛋白质组学（SP）景观。H2O 通过对比学习将视觉 Transformer（ViT）与大语言模型（LLM）集成，使组织形态特征与语义分子知识对齐。该跨模态方法使模型能够将空间表达谱融入组织模式识别，从而有效解码组织形态背后的分子异质性。模型在涵盖 25 种器官和癌症类型的 130 万对 H&E–空间组块的全组织数据集上训练，在从组织病理学预测空间组学表达上，与测序结果高度一致，并在三个癌症基准测试中稳定优于现有最先进模型。值得注意的是，H2O 能从 H&E 图像直接恢复 MIF–CD74/CD44 信号通路，彰显其在无分子检测情况下推断具有生物学意义的细胞–细胞通讯的能力。进一步应用于三个公共队列——包括胎儿与儿童胸腺组织、人类转移性淋巴结及乳腺癌——涵盖人类发育、三维空间框架及综合多组学分析，H2O 生成的结果与生物学一致，展示了在多样化真实场景中卓越的准确性、稳健性与泛化能力。H2O 通过计算生成转录组和蛋白质组景观，将常规组织病理学转化为空间分辨的多组学分析门户，从而提升组织表型分析并促进可扩展、综合的组织图谱构建。

## Abstract
Spatial omics technologies have revolutionized the molecular profiling of tissues but remain constrained by high costs and limited scalability. While hematoxylin and eosin (H&E) staining is ubiquitous, it lacks molecular specificity. Here, we present H2O (Histopathology to Omics), a generalist AI framework that bridges the modality gap between histopathology and spatial multi-omics, enabling the direct inference of spatial transcriptomics (ST) and proteomics (SP) landscapes from routine H&E images. H2O integrates Vision Transformers (ViT) with Large Language Models (LLM) via contrastive learning to align histological morphology with semantic molecular knowledge. This cross-modal approach allows the model to incorporate spatial expression profiles into histological pattern recognition, effectively decoding the molecular heterogeneity underlying tissue morphology. Trained on a pan-tissue dataset of 1.3 million paired H&E-spatial patches across 25 organs and cancer types, H2O predicts spatial omics expression from histology with high concordance to sequenced measurements and consistently outperforms state-of-the-art models across three cancer benchmarks. Notably, H2O recovers the MIF-CD74/CD44 signaling axis directly from H&E images, highlighting its capacity to infer biologically meaningful cell-cell communication without molecular profiling. Applying on three additional public cohorts covering fetal and paediatric thymus tissues, human metastatic lymph node, and breast cancer, encompassing human development, 3D spatial frameworks, and integrative multi-omics, H2O yields biologically concordant insights, demonstrating superior accuracy, robustness, and generalizability across real-world applications in diverse scenarios. H2O converts routine histopathology into a portal for spatially resolved multi-omics profiling by computationally generating transcriptomic and proteomic landscapes, thereby enhancing tissue phenotyping and enabling scalable, integrative tissue-atlas construction.

---

## 论文详细总结（自动生成）

# H2O：连接组织病理学与空间多组学分析的基础模型 — 深度总结

---

## 一、研究动机与核心问题

- **研究背景**：  
  空间组学（Spatial Omics）技术能以高空间分辨率示踪组织中的转录组和蛋白质分布，为理解组织分子异质性提供关键工具。但其成本高、操作复杂，不适用于大规模临床分析。  
  相反，传统的苏木精—伊红（H&E）病理图像广泛存在且成本低，但缺乏分子水平的表达信息。

- **研究问题**：  
  如何在不依赖昂贵的空间组学实验下，从常规 H&E 病理切片中**推断出空间转录组和空间蛋白质组图谱**，从而用计算手段实现“分子级病理重建”。

- **研究目标**：  
  构建一个跨模态的人工智能基础模型，能够将组织形态（图像模态）嵌入到分子空间（转录组/蛋白组模态）中，实现“从形态到分子”的直接映射。

---

## 二、方法论：H2O 框架设计

### 核心思想
- 构建一个跨模态基础模型 **H2O (Histopathology to Omics)**，通过对比学习（contrastive learning）将视觉模型与分子模型对齐。
- 将 **视觉Transformer (Vision Transformer, ViT)** 与 **分子语言模型（如 scGPT）**结合，使模型既能理解形态特征，又能融入分子语义。

### 模型结构
1. **两阶段训练架构**：
   - 阶段一：通过对比学习对齐图像 FM（foundation model）与转录组 FM。
   - 阶段二：基于对齐后的嵌入空间，训练解码器预测空间转录组表达。
2. **主要组成模块**：
   - **图像编码器**：基于 DINOv2 ViT，输入 H&E 图像块（224×224 像素），输出 384–512 维向量。
   - **基因编码器**：基于 fine-tuned scGPT，从单细胞转录组扩展至空间转录组数据。
   - **邻域聚合 (Neighborhood Aggregation)**：使用 1D 卷积方式整合中心块与 8 个邻域块的信息，捕获局部空间结构。
   - **FiLM 模块（Feature-wise Linear Modulation）**：引入“直径条件”嵌入，区分不同空间组学平台的 spot 尺度，增强跨平台泛化能力。
3. **损失函数**：
   - 对比损失：最大化正样本（图像–转录组对）的相似性，最小化负样本相似。
   - 重构损失：预测表达谱与真实表达谱之间的 MSE。
   - 总损失：  
     \[
     L_{total} = \alpha L_{con} + \beta L_{rec}
     \]
4. **训练输出**：
   - 可预测转录组（ST）与蛋白组（SP）表达空间分布。
   - 支撑下游任务：细胞聚类、通信网络分析、时空发育分析、3D 组织重建、跨模态整合等。

---

## 三、实验设计与验证体系

### 数据集
- **主要训练集**：
  - **HEST‑1k**：来自 25 种器官与癌症类型，共 1229 个 ST–WSI 配对样本，130 万个 spot。
  - 对应 54,435,706 个图像块（约 4.5 万张病理切片）。  
- **外部验证与应用数据**：
  1. **ccRCC, PRAD**（肾癌与前列腺癌）→ 基准任务。
  2. **IDC LymphNode** → 外部癌症泛化验证。
  3. **HTSA** → 胎儿–儿童胸腺发育系统。
  4. **OpenST** → 转移性淋巴结三维空间组学。
  5. **HTAPP** → MERFISH+CODEX 多组学融合（乳腺癌）。

### 对比模型
- HisToGene
- BLEEP
- DeepPT
- OmiCLIP

### Benchmark 指标
- Pearson 相关系数 (PCC)  
- Spearman 秩相关 (SRCC)  
- Concordance correlation coefficient (CCC)  
- 均方根误差 (RMSE)

---

## 四、算力资源说明

- 论文未明确给出 GPU 型号、规模或训练时长。  
- 仅指出预训练数据量极大（>5400 万图像块）与模型规模接近主流基础模型（ViT + GPT 架构），可推测使用多 GPU 集群（>8 GPU，推测 A100 或 H100）。  
- 由于缺乏硬件细节，本研究的计算成本无法定量复现。

---

## 五、实验数量与充分性

- **实验覆盖广泛**：
  1. 三个癌症基准（ccRCC, PRAD, IDC-LN）→ 定量对比。
  2. 三个独立场景：发育 (HTSA)、三维重建 (OpenST)、多组学融合 (HTAPP)。  
  3. 多层消融：FiLM、邻域聚合、对比学习模块。  
  4. 多模态任务：SP、ST 双模预测。  
- **验证维度**：
  - 预测精度、可解释性、可泛化性、生物一致性。
- **结论**：
  实验数量大且层次多，覆盖癌症、发育、生理及多组学，具备良好的完整性与公平性。

---

## 六、主要结论与发现

- H2O 实现从 H&E 图像直接预测空间信息，在多数据集上显著优于现有方法（平均 PCC 提升约 0.1–0.2）。
- 成功重现关键生物信号轴 **MIF–CD74/CD44**，可无分子检测推断细胞通信网络。
- 在胸腺发育数据集上再现 T 细胞成熟轨迹与细胞亚群时空迁移。
- 在 OpenST 数据中实现三维（3D）分子重构，揭示 CAFs、SPP1⁺ 巨噬细胞的侵袭边界分布。
- 与 HTAPP 蛋白组数据融合后，显示 RNA–蛋白互补特征，提升多模态聚类的解析度。
- 结论：**H2O 是首个从常规病理图像生成多组学预测的统一基础模型**。

---

## 七、方法与实验亮点

- **创新的跨模态对齐框架**：首次实现 ViT–LLM 在病理与组学间的联合对比训练。
- **FiLM 直径调制**：解决空间组学平台间分辨率差异导致的尺度偏差。
- **大规模跨癌种数据预训练**：学习到广义组织形态–分子映射关系，支持零样本泛化。
- **多层验证体系**：横跨癌症、发育、3D重建、多组学整合，展示生物推断能力。
- **下游生物发现能力突出**：能推断细胞–细胞通信、发育时间轨迹和组织层级结构。

---

## 八、不足与局限

- **算力与资源缺乏透明度**：未说明训练时长与硬件配置，复现成本难以评估。  
- **细胞级分辨率受限**：基于 224×224 图像块及邻域信息，尚不足以精确到单细胞尺度。  
- **蛋白组预测能力有限**：缺乏大规模 SP 预训练，仅使用轻量 MLP 解码器。  
- **数据分布偏倚风险**：训练集主要为肿瘤组织，极少数稀有或非病理组织未覆盖。  
- **生成式能力缺失**：目前仅为预测框架，尚不支持生成整张组织多组学图谱。

---

**总体评价**：  
H2O 将病理图像分析推进至“分子层级”的新阶段，是跨模态基础模型在生物医学中的重要探索。其广泛验证显示出强大泛化潜力和生物解释力，尽管目前仍存在计算和分辨率限制，但其研究范式对未来“图像—多组学融合计算病理”具有里程碑意义。

---

（完）
