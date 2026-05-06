---
title: "Autonomous multimodal agents enable transparent, spatiotemporal reconstruction of immune dynamics in pancreatic cancer progression"
title_zh: 自主多模态智能体实现胰腺癌进展过程中免疫动态的透明时空重建
authors: "Huang, B., Zhu, B."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719684v1.full.pdf"
tags: ["query:pathseg"]
score: 9.0
evidence: "基于常规H&E组织学的智能体计算病理学框架"
tldr: 本研究针对胰腺癌进展过程中免疫与间质生态系统的动态变化，提出ROSIE框架，通过LLM驱动的多模态病理推理从常规切片中重建免疫时空过程，揭示了癌变从免疫监视、功能衰退到间质控制的演化序列。
source: biorxiv
selection_source: fresh_fetch
motivation: 当前对胰腺癌发展中免疫与间质细胞变化的时空规律缺乏深入理解。
method: "提出一个结合大语言模型与深度学习的多模态病理计算框架ROSIE，用于从常规H&E组织切片中进行免疫动态的时空重建。"
result: 在小鼠胰腺上皮内瘤变模型中揭示了三阶段免疫-间质演化轨迹，涵盖免疫激活、衰竭到间质主导转变。
conclusion: 该框架为早期肿瘤演化的关键干预点识别和可解释病理分析提供了新途径。
---

## 摘要
胰腺癌的进展由免疫和基质细胞生态系统的动态变化所主导，但调控这些转变的时空规律仍然知之甚少。本文提出了一种智能计算病理学框架，该框架利用大型语言模型，从常规H&E组织切片中直接执行模块化生物标志物推断和时空推理。我们的方法ROSIE（RObust in Silico Immunofluorescence，鲁棒的硅基免疫荧光）将基于深度学习的多重推断与由LLM驱动的智能体逻辑相结合，模拟病理学家级别的推理，从而实现对复杂组织微结构的透明且可重复的分析。

我们将该流程应用于KSC转基因小鼠（n=24，年龄4–12周）胰腺上皮内瘤变（PanIN）的进展研究，生成了1044万个单细胞特征，并识别出由三个空间上不同的免疫–基质状态组成的按时间顺序排列的免疫轨迹：（1）早期免疫监视生态位：适应性免疫激活和抗原呈递富集的明确边界窗口；（2）过渡混合状态：淋巴活性下降、衰竭程序出现、早期EMT/血管生成信号；（3）基质占优势的终末状态：成纤维细胞扩增、血管重塑以及免疫沉默。

这些发现表明，胰腺癌进展是一个从免疫激活、免疫衰竭到基质接管的时间有序过程。该智能体框架超越了静态AI模型，提供了一种动态的、工具增强的推理方式，将高维组织数据与临床可解释性相连接，为识别肿瘤早期演化的治疗拐点提供了可扩展的基础。

## Abstract
Pancreatic cancer progression is orchestrated by dynamic shifts in immune and stromal cellular ecosystems, yet the temporal and spatial principles governing these transitions remain poorly understood. Here, we present an agentic computational pathology framework that leverages large language models to orchestrate modular biomarker inference and spatiotemporal reasoning directly from routine H&E histology. Our approach, ROSIE (RObust in Silico Immunofluorescence), combines deep-learning-based multiplex inference with LLM-driven agent logic that emulates pathologist-level reasoning, enabling transparent and reproducible analysis of complex tissue microarchitectures.

Applying this workflow to pancreatic intraepithelial neoplasia (PanIN) progression in KSC transgenic mice (n=24, ages 4-12 weeks), we generated 10.44 million single-cell profiles and identified a temporally ordered immune trajectory comprising three spatially distinct immune-stromal states: (1) early immune-surveillance niche: sharply bounded window of adaptive immune activation and antigen-presentation enrichment; (2) transitional mixed state: declining lymphoid activity, emerging exhaustion programs, and early EMT/angiogenesis signals; (3) stromal-dominant terminal state: fibroblast expansion, vascular remodeling, and immune silence.

These findings establish pancreatic cancer progression as a temporally ordered sequence of immune activation, exhaustion, and stromal takeover. The agentic framework transcends static AI models by offering dynamic, tool-augmented reasoning that bridges high-dimensional tissue data with clinical interpretability--providing a scalable foundation for identifying therapeutic inflection points in early tumor evolution.

---

## 论文详细总结（自动生成）

# 论文总结：自主多模态智能体在胰腺癌免疫动态时空重建中的应用

---

## 一、研究核心问题与背景

- **问题核心**：胰腺癌是一种高度致死性肿瘤，其早期演化过程包含复杂的免疫与间质生态系统重塑。然而，目前缺乏对这一过程的**时空动态规律**的系统理解。  
- **研究动机**：  
  - 高通量分子成像和单细胞测序虽能揭示肿瘤–免疫互作，但成本高、难以应用于队列级和纵向研究。  
  - 常规 H&E（苏木精–伊红）切片在临床中普遍存在，却未充分开发其潜在分子信息。  
  - 现有计算病理模型多为单任务静态系统，无法统一解析时间、空间和生物标志物层次。  
- **目标意义**：本研究试图从常规 H&E 切片中重建胰腺癌进展的免疫时空轨迹，为早期肿瘤拐点识别与临床干预提供计算基础。

---

## 二、方法论：核心思想与技术框架

- **总体思路**：  
  提出一个由大型语言模型（LLM）驱动的智能体型计算病理学框架——**ROSIE (RObust in Silico Immunofluorescence)**，实现从 H&E 图像到免疫动态的透明时空重建。

- **核心组件**：  
  1. **ROSIE 模块**：  
     - 深度学习模型，训练于配对的 H&E 与多重免疫荧光数据，可预测 50 通道蛋白表达谱。  
     - 从每个细胞生成虚拟分子特征，实现“免疫组学”在常规切片上的推断。  
  2. **LLM 代理（Agentic Framework）**：  
     - 基于 LangGraph 框架的多节点自动化流程。  
     - LLM 生成任务级 Python 执行模板，实现节点间的模组化与可解释推理。  
     - 四个核心节点：
       - Node 1：WSI 自适应分块（512×512 patch）。  
       - Node 2.1：特征提取（空间坐标、核分割）。  
       - Node 2.2：ROSIE 免疫标志物推断与细胞分类。  
       - Node 3：时间建模（计算 Log₂ Fold Change、构建 Timed Petri Net）。  
       - Node 4：空间生态位（niche）分析（DBSCAN + KMeans 聚类 + 通路评分）。
  3. **人类在环监督 (HITL)**：研究者实时监控 LLM 生成的代码并优化模型执行，确保实验透明与可重复。

- **关键算法和推理流程（文字说明）**：  
  ① 从全景 H&E 图像分块 → ② 细胞级分割与坐标提取 → ③ 通过 ROSIE 预测每个细胞的 50 个蛋白通道表达 → ④ 聚合成单细胞特征矩阵 → ⑤ 计算各时间点细胞组成与变化率 → ⑥ 构建 **Timed Petri Net** 描述免疫状态转移 → ⑦ 空间聚类形成免疫–间质生态位映射。

---

## 三、实验设计

- **数据来源与对象**：  
  - 使用 **KSC 转基因小鼠模型**（Ptf1a-Cre; LSL-Kras^G12D/+; Smad4^fl/fl），涵盖 4–12 周龄阶段，共 8 张 H&E 全切片（SVS 格式）。  
  - 共处理 **约 1044 万个单细胞**，每张图像独立执行全流程分析。  
- **实验场景**：模拟胰腺上皮内瘤变（PanIN）到腺癌（PDAC）的自然进展。  
- **验证与对比**：  
  - 与 **湿实验室测定数据（IHC、免疫荧光、三色染色）**进行方向性一致性验证。  
  - 对比指标包括：CD68⁺巨噬细胞扩展、TSPO 表达（巨噬活化标志物）、纤维化水平、上皮扩增。  
  - 未与其他计算病理模型直接“benchmark”比较，但与前人 ROSIE 应用于肺癌的结果进行机制性对照。  

---

## 四、资源与算力

- **LLM 后端**：Claude 3.5 Sonnet（用于代码生成），Llama 2 (7B) 本地运行以快速迭代。  
- **部署方式**：使用 Texas Advanced Computing Center (TACC) 的高性能资源。  
- **算力细节**：  
  - 文中未明确报告 GPU 型号、数量或训练时长。  
  - 推断阶段基于预训练的 ROSIE 模型，无再训练过程。  
  - 明确说明模型在温度参数设置为 0以实现确定性输出。  
  → **结论**：论文未提供精确算力信息，仅描述计算环境（TACC）。

---

## 五、实验数量与充分性

- **主要实验类型**：  
  1. 时间序列分析（8 个时间点：4–12 周）。  
  2. 细胞组成与变化率分析（24 只样本 × 百万单细胞量级）。  
  3. 通路动态分析（8 生物程序：免疫标志、抗原呈递、T细胞激活/衰竭、EMT、血管生成、纤维化等）。  
  4. 空间生态位分析（8 阶段各自的 niche 热图，附 S7.1–S7.8）。  
  5. 与实验室测定的 7 个生物指标进行定向验证（见补充表4.6）。  
- **充分性与公平性**：  
  - 时间跨度覆盖完整肿瘤早期至晚期过程。  
  - 验证指标多维度（免疫、结构、分子），方向一致性强。  
  - 局限：未包含正常或不同癌型对照，属于单模型验证。

---

## 六、主要结论与发现

- 胰腺癌进展可归纳为三个空间上可分的免疫–间质阶段：
  1. **早期免疫监视阶段**（4–6周）：富含CD4⁺/CD8⁺T细胞、NK、B细胞与树突细胞，抗原呈递和免疫活化显著。  
  2. **过渡混合阶段**（7–9周）：淋巴功能衰退、免疫耗竭与早期 EMT / 血管生成标志出现。  
  3. **间质主导终末阶段**（11–12周）：成纤维细胞扩张、血管重塑，免疫沉默。  
- 构建的 **Timed Petri Net** 明确展示免疫活化→衰退→间质接管的时间有序调节。  
- 首次仅基于 H&E 图像实现对胰腺癌免疫时空动力学的单细胞级重建。  
- 指明**早期免疫活化窗口**可能为临床干预最具价值阶段。

---

## 七、优点与创新亮点

- **方法创新**：首次将大型语言模型（LLM）作为病理计算流程的“智能调度器”，实现模块化、透明化的多任务推理。  
- **可解释性强**：每个计算节点可视化中间输出，便于路径追踪和实验审核。  
- **数据来源普遍**：完全基于常规 H&E 切片 —— 有利于临床推广与数据复用。  
- **时空整合能力**：同时融合单细胞分辨率、空间结构与真实时间点，实现多维动态重构。  
- **验证充分**：跨模态验证与实验结果高度一致，增强了生物学可信度。  

---

## 八、不足与局限

- **数据局限**：仅使用 KSC 小鼠模型，未纳入人类样本或正常对照，无法验证跨物种泛化。  
- **时间设计**：为横截面分析而非纵向同体跟踪，无法捕捉单体演化或克隆层次变化。  
- **模型偏差风险**：ROSIE 的预训练数据偏向免疫荧光背景，罕见细胞类型可能识别不足。  
- **机制验证缺失**：缺乏直接实验证据来区分免疫衰竭与间质接管的因果关系。  
- **算力透明度不足**：未说明训练/推理资源规模与耗时，影响复现性评估。  

---

**（完）**
