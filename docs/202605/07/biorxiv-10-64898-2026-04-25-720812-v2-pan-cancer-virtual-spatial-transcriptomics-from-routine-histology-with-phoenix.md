---
title: Pan-cancer virtual spatial transcriptomics from routine histology with Phoenix
title_zh: 利用 Phoenix 从常规组织学实现跨癌种虚拟空间转录组学
authors: "Tran, M., Gindra, R. H., Putze, P., Senbai, K., Palla, G., Kos, T., Falcomata, C., Wang, C., Guo, R., Boxberg, M., Berclaz, L. M., Lindner, L. H., Bergmayr, L., Knoesel, T., Jurmeister, P., Klauschen, F., Homicsko, K., Gottardo, R., Eckstein, M., Matek, C., Mock, A., Theis, F. J., Saur, D., Peng, T."
date: 2026-05-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.25.720812v2.full.pdf"
tags: ["query:cellrep"]
score: 9.0
evidence: 从常规组织学推断泛癌空间分辨率的单细胞基因表达
tldr: 本研究针对空间转录组数据稀缺与成本高的问题，提出生成模型Phoenix，从常规组织学图像高精度推测单细胞层面的空间基因表达。Phoenix在多种癌症和物种中均表现出优异的泛化能力，揭示了新的空间生物标志物，并为大规模疾病机制和治疗响应研究提供了可扩展方案。
source: biorxiv
selection_source: fresh_fetch
motivation: 空间转录组学昂贵且数据有限，限制了疾病机制和治疗响应的研究。
method: 提出基于潜变量流匹配的生成模型Phoenix，从组织切片图像预测单细胞空间基因表达。
result: Phoenix准确重建癌症组织的空间基因表达，发现新的空间生物标志物并验证跨癌种通用性。
conclusion: Phoenix确立了从常规组织学实现虚拟空间转录组学的可行路径，推动组织结构与基因表达研究的普及。
---

## 摘要
空间转录组学将基因表达与组织结构联系起来，提供了细胞组织的机制性视角。然而，现有的数据集覆盖的供体数量有限，未能体现人类疾病的复杂性。实验成本仍然高昂，大规模分析对于群体层面的研究来说难以实现。因此，亟需准确的计算方法。但是，从标准组织病理学中预测基因表达仍是一个未解决的问题，因为当前的方法在新的队列和疾病中迁移性能较差。在此，我们提出了 Phoenix，一种潜在流匹配生成模型，能够高精度推断跨癌种的空间分辨单细胞基因表达。Phoenix 可以在体外分析治疗反应：应用于763例头颈癌患者时，识别出了三种新的空间生物标志物，并在两个癌种（乳腺癌，n=84；卵巢癌，n=157）及不同治疗方案（铂类、曲妥珠单抗）中得到了验证。Phoenix 的泛化能力不仅限于癌瘤：在一个大型肉瘤队列（802个组织芯片核心）中，它在留出样本中准确预测了细胞类型特异性特征，并捕捉到化疗诱导的免疫重塑。Phoenix 还可跨物种扩展：在小鼠模型中，它准确预测了胰腺癌谱系标记基因及突变型 mKrasG12D 等位基因的表达。总体而言，Phoenix 建立了从常规组织学出发的虚拟空间转录组学框架，为研究组织结构、治疗反应以及疾病机制提供了可扩展的方案。

## Abstract
Spatial transcriptomics links gene expression to tissue architecture, providing a mechanistic view of cellular organization. Yet existing datasets cover few donors and miss the complexity of human disease. Experimental costs remain prohibitive, and large-scale profiling is impractically slow for population-level studies. Accurate computational methods are urgently needed. Predicting gene expression from standard histology, however, remains an open problem, as current approaches transfer poorly to unseen cohorts and diseases. Here, we present Phoenix, a latent flow matching generative model that infers pan-cancer spatially resolved single-cell gene expression with high accuracy. Phoenix analyzes treatment response in silico: Applied to 763 head and neck cancer patients, it identified three new spatial biomarkers that we validated across two cancers (breast cancer, n = 84; ovarian cancer, n = 157) and treatment regimens (platinum, trastuzumab). Phoenix generalizes beyond carcinomas: In a large sarcoma cohort (802 tissue microarray cores), it accurately predicted cell-type-specific signatures in held-out samples and captured chemotherapy-induced immune remodeling. Phoenix also extends across species: In a mouse model, it accurately predicted the expression of pancreatic cancer lineage markers and the mutant mKrasG12D allele in silico. Together, Phoenix establishes virtual spatial transcriptomics from routine histology as a scalable framework for studying tissue organization, therapeutic response, and disease mechanisms.

---

## 论文详细总结（自动生成）

# 《Pan-cancer virtual spatial transcriptomics from routine histology with Phoenix》论文总结

---

## 一、研究背景与核心问题

- **研究动机**  
  空间转录组学（Spatial Transcriptomics, ST）能将基因表达精确定位到组织结构中，为理解细胞组织和疾病机制提供关键视角。  
  然而现实中存在三大挑战：  
  1. **实验成本高昂**：每份样本代价通常在数千美元级别，实验周期长达数天。  
  2. **数据稀缺与批次效应严重**：现有公开数据量有限，不同平台（如 Visium、Xenium）之间差异显著。  
  3. **现有算法泛化性差**：从常规 H&E 组织切片预测空间基因表达的深度学习模型很难在新机构或新癌种上零样本迁移。  

- **研究目标**  
  构建一种可从常规组织学图像直接推断单细胞层级空间基因表达的生成式模型，实现：  
  - 高精度预测  
  - 对未见样本和新癌种具备“零样本”泛化能力  
  - 可在群体尺度上开展虚拟空间转录组学分析。

---

## 二、方法论：Phoenix 模型原理与技术框架

- **核心思想**  
  提出 **Phoenix**：一种基于“**潜在流匹配（latent flow matching）**”的生成模型，可从组织图像生成单细胞空间转录组数据。

- **模型结构**  
  - **输入**：H&E 组织学图像  
  - **输出**：单细胞或伪空间点的基因表达向量  
  - **主要模块**：
    1. **病理图像编码器（PFM）**：使用预训练的“病理学基础模型”提取图像特征。  
    2. **自编码器（AE / MLP-Mixer-AE）**：将高维基因表达压缩到潜变量空间；可选模块。  
    3. **流匹配生成器（Conditional Flow Matching Transformer）**：学习潜变量在时间维度上的演化，生成表达向量。  
    4. **解码器**：将潜变量重构为目标基因表达值。  
  - **训练过程**：最小化生成流场与真实样本流场之间的回归误差，通过 ODE（常微分方程）积分得到最终生成表达。  
  - **推理阶段**：通过积分器（Dormand–Prince, DOPRI5）在 [0,1] 区间求解，结合图像特征生成单细胞表达。

- **技术特点**  
  - 无需手工特征设计，全端到端学习形态—转录组映射。  
  - 在 1.2 亿到 12 亿参数规模下实现多层 Transformer 架构。  
  - 支持单细胞、55 μm、100 μm 三种空间分辨率。

---

## 三、实验设计

- **主要数据集：The Nest**
  - 来源：79 张 Xenium 全切片图与 924 组织芯片核心（来自欧洲、亚洲、北美多个机构）。  
  - 总量：约 22.2 百万张图像—表达配对样本。  
  - 涵盖：16 个器官系统、7 个基因 panel（乳腺、结肠、肺、皮肤、免疫、多组织等）。  

- **训练与评估策略**
  - 训练集：公开 10x Genomics（TENX）数据，8.2 百万细胞。  
  - 测试集：外部独立队列（CHUV、LMU、NCBI、SNUH、UKER）。  
  - 确保机构级、供体级严格隔离，实现真正零样本测试。

- **比较方法（Baseline）**
  - BLEEP（contrastive learning）
  - DeepSpot（contextual CNN）
  - GHIST（deep generative histology）
  - Linear（线性回归基线）
  - SpatialEx（图卷积整合模型）

- **评估指标**
  - Spearman/Pearson 相关系数
  - 空间自相关（Geary’s C、Moran’s I）
  - 空间 R² / MSE / Frobenius distance 等。

---

## 四、算力与资源

- **硬件资源**  
  - 使用德国 JURECA 预百级模块化超算系统。  
  - 每节点配置：4 × NVIDIA H100 NVL GPU（每卡 96 GB HBM3）。  
  - 总训练时间：> 10,000 GPU 小时。  
  - 推测能耗约 6,000 kWh，CO₂ 排放约 2 吨。  

- **软件生态**  
  - 使用 PyTorch / Squidpy / Scanpy / scikit-survival 等主流生物计算框架。  
  - 模型、权重、数据管线均已开源。  

---

## 五、实验数量与充分性

- **总体实验规模**
  - 超过 10,000 名患者、多癌种（乳腺癌、卵巢癌、头颈癌、结直肠癌、胰腺癌、肉瘤等）实验证明。
  - 主要实验包括：
    - 基准泛化测试（五个独立外部队列）  
    - 生物学回溯实验（乳腺癌亚型、CRC 进化、胰腺前癌进展）  
    - 群体级空间图谱分析（TCGA 9544 例患者）  
    - 治疗反应建模（抗血管生成药、放疗、化疗、免疫治疗）。  
    - 不同物种迁移（人类 → 小鼠模型）  
  - **消融与复现性**：报告中包含多层空间分辨率与不同 AE 模式的对照，实验覆盖充分、指标多样。

- **客观性与公平性**
  - 测试严格隔离训练数据，未使用任何重叠样本。  
  - 与 SOTA 方法的比较采用统一指标和公共数据。  

---

## 六、主要结论与发现

1. **性能提升显著**：Phoenix 在 Spearman 相关上较最优现有方法提升 35%–173%。  
2. **零样本泛化能力**：无需微调即可适应新机构、新癌种，能正确再现空间梯度与细胞类群分布。  
3. **生物学发现**：  
   - 恢复并验证乳腺癌分型与免疫图谱特征；  
   - 揭示结直肠癌侵袭演化的基因组不稳定性梯度；  
   - 解析胰腺癌前病变从低级 PanIN 至 PDAC 的分子轨迹。  
4. **群体级空间图谱**：基于 TCGA 数据建立 9,544 名患者的**泛癌空间图谱**，发现三种保守的肿瘤微环境生态系统（EC1–EC3），对应不同免疫功能状态与生存结局。  
5. **治疗预测与机制解析**：  
   - 发现 CD8⁺ T 细胞与成纤维细胞空间共现是化疗反应预测因子；  
   - 验证在乳腺癌和卵巢癌不同治疗下的可迁移性。  
6. **跨物种可迁移性**：在肉瘤及小鼠 PDAC 模型中复现空间结构、突变等位基因表达和免疫重塑。  

---

## 七、方法与实验亮点

- **方法学创新**
  - 首次在空间生物领域应用 **latent flow matching** 生成框架。  
  - 模型规模与数据规模均超越现有同类研究。  
  - 单细胞级预测支持多层空间分辨率选择。  

- **数据体系创新**  
  - 构建 The Nest 数据集（2200 万 image–gene 对），成为最大 Xenium 单细胞 ST 集合之一。  

- **应用亮点**
  - 具备跨癌种、跨机构、跨物种通用性。  
  - 推理时间显著缩短（全切片 < 1 小时，对比实验 3–6 天）。  
  - 模型与管线完全开源、可复现。  

---

## 八、不足与局限

- **基因面板限制**：训练数据依赖 Xenium In Situ 固定基因集合（280–480 基因），缺乏全转录组覆盖。  
- **跨平台迁移风险**：对 MERFISH、CosMx、Visium HD 等平台泛化尚未验证。  
- **数据质量依赖强**：模型性能受图像清晰度与探针敏感度主导（Xenium 5K Prime 表现不佳）。  
- **注释与标签依赖**：空间细胞类型仍受 panel 基因特异性与标准不一致影响。  
- **能耗与计算门槛高**：需集群级 GPU 资源，不易在普通实验室复现。  

---

**（完）**
