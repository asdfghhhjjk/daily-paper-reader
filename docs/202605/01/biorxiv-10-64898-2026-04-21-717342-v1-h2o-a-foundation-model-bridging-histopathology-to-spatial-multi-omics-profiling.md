---
title: "H2O: A Foundation Model Bridging Histopathology to Spatial Multi-Omics Profiling"
title_zh: H2O：连接组织病理学与空间多组学分析的基础模型
authors: "Gu, Y., Wu, Z., Yan, R., Wang, Z., Li, Y., Lin, S., Cui, Y., Lai, H., Luo, X., Zhou, S. K., Yuan, Z., Yao, J."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.717342v1.full.pdf"
tags: ["query:pathseg"]
score: 10.0
evidence: "利用ViT将H&E图像与空间多组学联系起来的基础模型"
tldr: "H2O是一种融合视觉Transformer和大型语言模型的AI框架，通过对比学习将病理图像与空间组学信息对齐，可从常规H&E图像直接推测空间转录组和蛋白组表达，在多种组织和癌症中表现优异，显著提升组织分子表型分析的可扩展性和精度。"
source: biorxiv
selection_source: fresh_fetch
motivation: "空间组学成本高且难以规模化，而普通H&E染色广泛使用却缺乏分子信息，因此需要一种桥接病理图像与分子组学的AI方法。"
method: "H2O利用视觉Transformer与大型语言模型的对比学习结合，将病理图像与分子表达数据对齐，实现从H&E图像直接推测空间转录组和蛋白组信息。"
result: "H2O在25种组织和癌症类型上训练，预测空间多组学表达的精度高并优于现有模型，能从H&E图像中恢复生物学意义明确的信号通路。"
conclusion: H2O实现了从常规病理图像到空间多组学的跨模态推理，为低成本、高通量的组织分子分析和全人体组织图谱构建提供了新途径。
---

## 摘要
空间组学技术已彻底改变了组织的分子分析方式，但其高成本和有限的可扩展性仍然限制了应用。虽然苏木精-伊红（H&E）染色在病理学中极为普遍，但其缺乏分子特异性。本研究提出了 H2O（Histopathology to Omics），一个跨模态的通用人工智能框架，用于弥合组织病理学与空间多组学之间的界限，实现从常规 H&E 图像直接推断空间转录组（ST）与蛋白质组（SP）图谱。H2O 通过对比学习将视觉 Transformer（ViT）与大型语言模型（LLM）结合，从而对齐组织形态学与语义分子知识。该跨模态方法使模型能够将空间表达谱融入组织学模式识别中，从而有效解析组织形态背后的分子异质性。H2O 在包含 25 种器官与癌症类型、共 130 万对 H&E–空间配对样本的泛组织数据集上训练，可从组织病理图像高一致性地预测空间组学表达，并在三个癌症基准测试中稳定优于现有最先进模型。值得注意的是，H2O 能直接从 H&E 图像中恢复 MIF–CD74/CD44 信号通路，体现出其无需分子检测即可推断生物学相关的细胞间通讯能力。进一步地，在三个额外的公共队列上应用——涵盖胎儿与儿童胸腺组织、人类转移性淋巴结及乳腺癌——涉及人类发育、三维空间框架与整合多组学分析，H2O 均能产生与生物学一致的洞见，展现出优异的准确性、稳健性与广泛的通用性。H2O 通过计算生成转录组与蛋白质组空间图谱，将常规组织病理学转化为空间分辨多组学分析的入口，从而增强组织表型分析并助力构建可扩展、整合的组织图谱。

## Abstract
Spatial omics technologies have revolutionized the molecular profiling of tissues but remain constrained by high costs and limited scalability. While hematoxylin and eosin (H&E) staining is ubiquitous, it lacks molecular specificity. Here, we present H2O (Histopathology to Omics), a generalist AI framework that bridges the modality gap between histopathology and spatial multi-omics, enabling the direct inference of spatial transcriptomics (ST) and proteomics (SP) landscapes from routine H&E images. H2O integrates Vision Transformers (ViT) with Large Language Models (LLM) via contrastive learning to align histological morphology with semantic molecular knowledge. This cross-modal approach allows the model to incorporate spatial expression profiles into histological pattern recognition, effectively decoding the molecular heterogeneity underlying tissue morphology. Trained on a pan-tissue dataset of 1.3 million paired H&E-spatial patches across 25 organs and cancer types, H2O predicts spatial omics expression from histology with high concordance to sequenced measurements and consistently outperforms state-of-the-art models across three cancer benchmarks. Notably, H2O recovers the MIF-CD74/CD44 signaling axis directly from H&E images, highlighting its capacity to infer biologically meaningful cell-cell communication without molecular profiling. Applying on three additional public cohorts covering fetal and paediatric thymus tissues, human metastatic lymph node, and breast cancer, encompassing human development, 3D spatial frameworks, and integrative multi-omics, H2O yields biologically concordant insights, demonstrating superior accuracy, robustness, and generalizability across real-world applications in diverse scenarios. H2O converts routine histopathology into a portal for spatially resolved multi-omics profiling by computationally generating transcriptomic and proteomic landscapes, thereby enhancing tissue phenotyping and enabling scalable, integrative tissue-atlas construction.

---

## 论文详细总结（自动生成）

# H2O：连接组织病理学与空间多组学分析的基础模型 —— 深度总结

---

## 一、研究背景与核心问题

### 研究动机
- 空间组学（Spatial Omics）——包括空间转录组（ST）和空间蛋白组（SP）——能在组织尺度上揭示分子表达的空间分布，为理解疾病机制和细胞通讯提供关键线索。  
- 然而，该技术存在**高成本、实验复杂、样本类型受限（多为新鲜冻存样品）**等问题，难以在临床和常规病理工作中推广。  
- 相比之下，苏木精-伊红（H&E）染色的组织切片几乎在所有病理实验室中普遍存在，但缺乏分子层面信息。  
- 因此，本文试图**建立一种通用人工智能框架，使常规病理图像能推断空间分子表达分布，实现从形态到多组学信息的映射。**

### 整体目标
- 提出 **H2O（Histopathology to Omics）**：一个“基础模型（Foundation Model）”，通过跨模态对齐学习，将组织病理学影像与多组学表达空间连接起来。  
- 最终目标是：**将普通H&E图像转化为低成本、可扩展的空间分子地图**，用于生物学研究和临床诊断。

---

## 二、方法论与关键技术

### 核心思想
- H2O通过**对比学习（Contrastive Learning）**将视觉Transformer（ViT）特征与基因表达嵌入对齐，实现跨模态表征。  
- 架构由两个主要部分组成：
  1. **视觉基础模型（Image FM）**：基于DINO-V2和ViT架构，从H&E组织图像提取形态学特征；
  2. **空间转录组学模型（ST FM）**：基于fine-tuned的scGPT模型，以单细胞预训练模型为基础，增补空间表达知识。

### 关键模块
- **对比学习模块**：最大化配对的图像–表达嵌入的相似性，最小化非配对样本的相似性；使图像特征空间嵌入分子信息。
- **邻域聚合（Neighborhood Aggregation）**：通过1D卷积整合邻近的图像patch上下文，模拟组织连续空间。
- **直径条件化模块（Diameter-conditioned FiLM）**：根据不同平台的spot大小（2–150μm）自适应地调节特征，以适应多种分辨率。
- **联合损失函数**：  
  \( L_{total} = \alpha L_{con} + \beta L_{rec} \)  
  其中 \(L_{con}\) 为对比损失，\(L_{rec}\) 为重构损失（预测表达与实验测定的MSE）。

### 模型推理流程（简述）
1. 输入H&E图像；
2. ViT提取图像特征，融合邻域与尺度信息；
3. 图像嵌入向量经与scGPT-FT生成的表达嵌入进行对比学习对齐；
4. 编码后的特征解码为特定空间位置的基因或蛋白表达谱。

---

## 三、实验设计与验证体系

### 数据来源与规模
- **HEST-1k**：主要训练数据集，含1,300,000个H&E–ST配对spot，覆盖25种器官和癌症类型；
- **TCGA、GTEx**：用于视觉FM预训练；
- **IDCLymphNode**：独立外部验证集，肺转移性乳腺癌淋巴结；
- **HTSA**：人类胸腺空间发育图谱，用于发育阶段检验；
- **OpenST**：三维空间重构测试集；
- **HTAPP**：MERFISH（RNA）与CODEX（Protein）配对乳腺癌多组学集合，用于多模态扩展。

### 对比模型与基准测试
- 与以下主流方法比较：
  - HisToGene、BLEEP、DeepPT、OmiCLIP。
- 评估指标：
  - **PCC**（Pearson相关系数）
  - **SRCC**（Spearman秩相关）
  - **CCC**（一致性相关）
  - **RMSE**（均方根误差）
- Benchmark组织：ccRCC（肾透明细胞癌）、PRAD（前列腺癌）、IDC-LymphNode（乳腺癌转移性淋巴结）。

---

## 四、资源与算力情况

- 论文未明确列出GPU型号、GPU数量或训练时长。  
- 仅表明图像训练共涉及 **≈5400万图像patch、约4.5万样本**，推断需大规模计算资源。  
- 由于源代码已在 **GitHub（TencentAILabHealthcare/H2O）** 开放，未来用户可验证所需算力。

---

## 五、实验数量与充分性评估

- 主要实验包括：
  - **跨模型对比（4组）**；
  - **不同组织与癌症类型验证（≥3组场景）**；
  - **多模态延伸（ST→SP）**；
  - **发育系统验证（HTSA）**；
  - **三维重建实验（OpenST）**；
  - **消融研究**：如去除FiLM、邻域聚合模块等（Extended Data Fig.3）。
- 该实验体系覆盖**不同样本类型、时间、空间和模态维度**，数量全面、验证充分。
- 对比方法均复现自公开论文或开源实现，具有一定公平性。

---

## 六、主要结论与发现

- H2O能以高精度从H&E图像预测空间组学表达（ST与SP），在ccRCC、PRAD和IDCLymphNode中均显著优于现有方法。  
- 能直接从图像恢复经典生物信号通路，如 **MIF–CD74/CD44轴**，揭示细胞间通讯。  
- 在发育系统中成功重现**胸腺T细胞分化轨迹**，显示跨时间维度鲁棒性。  
- 3D重构中揭示**CAF与SPP1+巨噬细胞追踪肿瘤侵袭边界**等结构。  
- 扩展到蛋白质组预测，H2O能同时生成 RNA 与 Protein 空间分布，WNN整合后增强对肿瘤微环境识别能力。  
- 总体展示出**高准确性、强泛化与跨物种、跨平台的通用性。**

---

## 七、方法与设计亮点

- **跨模态对齐策略**：通过scGPT引入分子知识，使视觉模型获得生物语义能力。  
- **多尺度条件化与邻域融合**：有效提升空间分辨率兼容性。  
- **广覆盖数据训练**：25种器官+多肿瘤类型构成真正泛组织模型。  
- **3D重构与多模态扩展**：从H&E实现三维分子成像与RNA–Protein联合预测。  
- **可公开复现**：数据与代码全面开放，研究透明度高。

---

## 八、不足与局限

- **训练算力未说明**：无法评估计算开销与重现成本。  
- **细胞级分辨率缺失**：目前仅基于224×224 patch及邻居融合，仍非真正单细胞尺度。  
- **蛋白组预测能力有限**：SP部分仅用轻量MLP解码器，缺乏大规模蛋白预训练。  
- **少数组织与稀有病理类型仍未覆盖**：泛化仍依赖现有ST数据集。  
- **生成性质受限**：目前为预测模型，暂不支持全图生成或补全（generative能力）。  

---

（完）
