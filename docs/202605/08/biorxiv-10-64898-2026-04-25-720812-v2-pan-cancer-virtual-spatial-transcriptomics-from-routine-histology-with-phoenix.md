---
title: Pan-cancer virtual spatial transcriptomics from routine histology with Phoenix
title_zh: 利用常规组织学实现跨癌种虚拟空间转录组学的 Phoenix 系统
authors: "Tran, M., Gindra, R. H., Putze, P., Senbai, K., Palla, G., Kos, T., Falcomata, C., Wang, C., Guo, R., Boxberg, M., Berclaz, L. M., Lindner, L. H., Bergmayr, L., Knoesel, T., Jurmeister, P., Klauschen, F., Homicsko, K., Gottardo, R., Eckstein, M., Matek, C., Mock, A., Theis, F. J., Saur, D., Peng, T."
date: 2026-05-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.25.720812v2.full.pdf"
tags: ["query:cellrep"]
score: 9.0
evidence: 从常规组织学中推断泛癌空间分辨率的单细胞基因表达
tldr: 本研究针对空间转录组学成本高、样本有限的问题，提出生成模型Phoenix，可从常规组织学图像精确推断不同癌种及跨物种的空间单细胞基因表达，验证了其在识别新生物标志物和模拟治疗反应方面的广泛适用性。
source: biorxiv
selection_source: fresh_fetch
motivation: 实验性空间转录组学成本高、数据量有限，难以进行大规模疾病研究，需要准确的计算推断方法。
method: 研究提出名为Phoenix的潜在流匹配生成模型，从组织学图像推断单细胞空间基因表达。
result: Phoenix在多癌种和跨物种研究中实现高精度表达预测，发现新的空间生物标志物并揭示治疗相关免疫重塑。
conclusion: Phoenix建立了从常规组织学数据生成虚拟空间转录组的可扩展框架，为研究组织结构和治疗反应提供了新途径。
---

## 摘要
空间转录组学将基因表达与组织结构联系起来，提供了细胞组织的机制性视角。然而，现有数据集覆盖的供体数量有限，无法捕捉人类疾病的复杂性。实验成本仍然高昂，而针对人群水平的大规模分析在实践上极为缓慢。因此，迫切需要准确的计算方法。然而，从标准组织学图像预测基因表达仍是一个开放问题，因为当前的方法在新的队列和疾病上泛化能力较差。本文提出了 Phoenix，这是一种潜在流匹配生成模型，能够以高准确度推断跨癌种、空间分辨的单细胞基因表达。Phoenix 可以在体外分析治疗反应：应用于 763 例头颈癌患者的数据中，它识别出三个新的空间生物标志物，并在两个癌种（乳腺癌，n = 84；卵巢癌，n = 157）及两种治疗方案（铂类药物、曲妥珠单抗）中获得验证。Phoenix 的泛化能力超越了癌瘤类型：在一个大型肉瘤队列（802 个组织芯片核心）中，它在留出的样本中准确预测了细胞类型特异性特征，并捕捉到化疗诱导的免疫重塑。此外，Phoenix 还可跨物种扩展：在小鼠模型中，它准确预测了胰腺癌谱系标志物及突变的 mKrasG12D 基因的表达。综合来看，Phoenix 通过常规组织学建立了虚拟空间转录组学，为研究组织结构、治疗反应及疾病机制提供了可扩展的框架。

## Abstract
Spatial transcriptomics links gene expression to tissue architecture, providing a mechanistic view of cellular organization. Yet existing datasets cover few donors and miss the complexity of human disease. Experimental costs remain prohibitive, and large-scale profiling is impractically slow for population-level studies. Accurate computational methods are urgently needed. Predicting gene expression from standard histology, however, remains an open problem, as current approaches transfer poorly to unseen cohorts and diseases. Here, we present Phoenix, a latent flow matching generative model that infers pan-cancer spatially resolved single-cell gene expression with high accuracy. Phoenix analyzes treatment response in silico: Applied to 763 head and neck cancer patients, it identified three new spatial biomarkers that we validated across two cancers (breast cancer, n = 84; ovarian cancer, n = 157) and treatment regimens (platinum, trastuzumab). Phoenix generalizes beyond carcinomas: In a large sarcoma cohort (802 tissue microarray cores), it accurately predicted cell-type-specific signatures in held-out samples and captured chemotherapy-induced immune remodeling. Phoenix also extends across species: In a mouse model, it accurately predicted the expression of pancreatic cancer lineage markers and the mutant mKrasG12D allele in silico. Together, Phoenix establishes virtual spatial transcriptomics from routine histology as a scalable framework for studying tissue organization, therapeutic response, and disease mechanisms.

---

## 论文详细总结（自动生成）

# 《利用常规组织学实现跨癌种虚拟空间转录组学的 Phoenix 系统》论文总结

---

## 一、研究核心问题与整体含义
### 研究动机
- 空间转录组学（Spatial Transcriptomics, ST）能够将基因表达与组织结构结合，揭示细胞空间组织与疾病机制。  
- 当前 ST 技术（如 Visium、Xenium）虽精确，但实验成本高昂（每样本需数千美元）、周期长（数日到数周），且通常仅覆盖少量供体。  
- 因此无法进行 **人群规模** 的疾病研究，如泛癌分析或大规模治疗反应评估。  
- 需要一种能 **从常规 H&E 组织学图像推断单细胞空间基因表达** 的准确计算模型，实现虚拟 ST。

### 研究目标
- 提出一个能跨癌种、跨机构、跨物种泛化的 **生成式 AI 模型（Phoenix）**，从常规组织切片预测空间分辨的单细胞基因表达。
- 实现“虚拟空间转录组学”（Virtual ST），以低成本、快速度在大规模队列中开展精准组织与治疗研究。

---

## 二、方法论：Phoenix 模型设计与核心思想
### 核心概念
- **Phoenix** 为一种基于 **潜在流匹配（latent flow matching, LFM）** 的生成模型，属于条件生成式框架。  
- 目标：学习从组织图像特征到基因表达的映射关系，模拟真实细胞的空间转录组分布。

### 模型结构三部分
1. **编码器（Encoder）**  
   - 将高维基因表达向量压缩至低维潜在空间。  
   - 使用改进的 **MLP-Mixer 自编码器（AE）** 实现“通道混合”和“序列混合”，学习高效特征表达。
2. **流模型（Flow Model）**  
   - 基于条件流匹配（Conditional Flow Matching, CFM）算法，通过神经网络近似时间连续的向量场。  
   - 采用带有 **Transformer + Cross-Attention** 的架构，生成潜在特征。
   - 模型通过求解常微分方程 (ODE) $\dot{x} = u_\theta(t, x)$ 进行样本生成。
3. **解码器（Decoder）**  
   - 将生成的潜在向量映射回基因表达空间，实现单细胞或区域级表达预测。

### 关键技术细节
- **图像编码**：利用病理基础模型（PFM）如 HO-Mini、H-Optimus-1、UNI2-h、Virchow2 生成紧凑图像特征。  
- **训练策略**：完全数据驱动，无需手工特征或标签。  
- **推理方式**：可在标准硬件上处理千兆像素整张组织切片，约 1 小时即可完成，而实验 ST 需 3–6 天。  
- **空间尺度**：支持单细胞、55 μm、100 μm三种分辨率，通过六边形 tiling 模拟 Visium 采样点。

---

## 三、实验设计
### 数据集与场景
- 构建了大型训练数据集 **The Nest**：
  - 包含 **79 张 Xenium 全片图像** 和 **924 个 Xenium 组织芯片核心**。
  - 涵盖 **16 个器官系统、7 个基因面板**，共 **22.2 百万对细胞图像-基因表达样本**。
- 数据来源多机构（欧洲、北美、亚洲）：
  - CHUV（瑞士）、LMU（德国）、NCBI（美）、SNUH（韩国）、UKER（德国）、TUM（德国）等。
- 额外数据：  
  - **人类肉瘤（sarcoma）** 队列：802 个 TMA 核心。  
  - **小鼠胰腺癌模型（mPDAC）**：15 个样本。

### Benchmark 设置
- **训练集**：TENX 公共队列（8.2 百万细胞）。  
- **测试集**：多个独立外部队列（CHUV、LMU、NCBI、SNUH、UKER）。  
- **对比方法**：BLEEP、DeepSpot、GHIST、Linear、SpatialEx。  
- **评估指标**：Spearman/Pearson 相关系数、MSE、Geary’s C、Moran’s I、Spatial R² 等。

---

## 四、资源与算力
- 训练于 **JURECA 前超算系统**（德国于利希研究中心）。  
- 使用 **多节点分布式 GPU 计算，总计超 10,000 GPU 小时**。  
- GPU 配置：每节点 **4× NVIDIA H100 NVL (96 GB HBM3)**。  
- 总耗电：约 6,000 kWh，对应碳排放约 2.0 吨 CO₂e。  
- 旗舰模型（人类癌瘤版）参数量：约 **1.2 亿至 12 亿** 级别。

---

## 五、实验数量与充分性
- **泛化评估**：跨机构、跨器官、跨疾病验证（共涉及 6 大队列 + 独立 hold-out 样本）。  
- **生物学验证**：乳腺癌亚型、结直肠癌进化结构、胰腺癌前驱病变。  
- **临床验证**：头颈癌（763 例）、乳腺癌（84 例）、卵巢癌（157 例）治疗反应。  
- **跨物种验证**：鼠 PDAC（15 样本）。  
- **共计验证样本超 10,000 名患者与样本**。  
👉 设计充分，实验分层全面（从生成性能 → 泛化性能 → 生物学机制 → 治疗预测 → 跨物种）。  
👉 所有评估均使用未见样本（严格训练-测试分离），保证客观。

---

## 六、主要结论与发现
1. **模型性能**：Phoenix 在 Spearman 相关度上比基线提升 35%–173%，可零样本泛化至未见器官组织。  
2. **泛化能力**：在胃癌、头颈癌、肺癌等未参与训练的数据中可稳定预测。  
3. **生物学发现**：
   - 在乳腺癌中正确重建分子亚型（AUROC = 0.826），揭示 Claudin-low 亚型免疫微环境差异。
   - 在结直肠癌中解析形态级别与 CNV 负担递增关系，发现新 TME 程序（反应型与稳态型）。
   - 描述胰腺癌 PanIN-LG 向 PanIN-HG 的分子转变及纤维母细胞空间分层。
4. **泛癌空间图谱**：在 TCGA 9544 名患者上构建三类 **肿瘤生态类型（ecotypes）**：EC1（免疫失调）、EC2（免疫协同）、EC3（基质重塑），并揭示其与生存相关。  
5. **治疗建模与生物标志物发现**：
   - 识别三种跨癌种的免疫-基质共现空间标志物（如 CD8T × Fibro(S02)），验证于多癌多疗法中。  
   - 可预测放化疗或抗血管生成治疗中的免疫重塑机制。  
6. **跨物种与成体系拓展**：
   - 在肉瘤和小鼠模型中验证 Phoenix 能推断突变及治疗驱动的空间变化。

---

## 七、优点与亮点
- **规模优势**：全球最大 FFPE 单细胞空间数据集（>22M 样本）。  
- **零样本泛化能力**：能直接对未见器官和机构工作，无需微调。  
- **模型创新性**：将流匹配生成模型引入空间转录组学领域，提高可解释性与连续生成能力。  
- **计算效率高**：用常规硬件数小时即可完成整片推理。  
- **跨癌种、多尺度、跨物种的一致性能**。  
- **可实际用于临床归档材料分析**，弥合数字病理与分子病理间的鸿沟。

---

## 八、不足与局限
- **数据平台限制**：训练主要依赖 Xenium In Situ 面板，基因覆盖较窄（280–480 个基因）。  
- **跨平台能力未验证**：尚未在 MERFISH、CosMx、seqFISH+ 等技术上测试。  
- **低质量数据敏感性**：在 Xenium 5K Prime 低敏版本上泛化性能显著下降。  
- **生物学注释受限**：受面板基因与标记特异性影响，对罕见细胞亚型的识别有限。  
- **计算成本高**：训练需万级 GPU 小时，不适合中小型实验室独立复现。  
- **生态验证**：虽跨癌种，但仍需更广泛的人群数据与临床结局验证以确认普适性。

---

**（完）**
