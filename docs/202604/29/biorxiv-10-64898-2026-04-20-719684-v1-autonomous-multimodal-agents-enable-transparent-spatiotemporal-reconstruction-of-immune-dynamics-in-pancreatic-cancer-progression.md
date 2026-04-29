---
title: "Autonomous multimodal agents enable transparent, spatiotemporal reconstruction of immune dynamics in pancreatic cancer progression"
title_zh: 自主多模态代理实现胰腺癌进展过程中免疫动态的透明时空重建
authors: "Huang, B., Zhu, B."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719684v1.full.pdf"
tags: ["query:pathseg"]
score: 9.0
evidence: "使用H&E组织学和LLM的计算病理学框架"
tldr: "本研究提出一种名为ROSIE的自主多模态病理计算框架，利用大语言模型和深度学习实现从常规H&E切片中重建胰腺癌的免疫动态，揭示其进展过程由免疫激活、功能衰竭到基质主导的时空序列，为早期治疗靶点识别提供新途径。"
source: biorxiv
selection_source: fresh_fetch
motivation: 胰腺癌的免疫与基质生态系统变化复杂，其时空演化规律尚不清晰。
method: 采用ROSIE框架结合LLM驱动的智能代理与深度学习，从组织切片推断并重建免疫与基质的时空变化。
result: 研究在胰腺癌进展中发现三种时空序列的免疫-基质状态，揭示免疫激活到衰竭及基质接管的过程。
conclusion: 该框架实现了胰腺癌免疫动力学的透明时空重建，为精准病理分析和治疗决策提供可扩展的新基础。
---

## 摘要
胰腺癌的进展受免疫和基质细胞生态系统的动态变化所支配，但控制这些转变的时空规律仍不清楚。在此，我们提出了一种基于代理的计算病理学框架，该框架利用大型语言模型直接从常规的H&E组织学中协调模块化生物标志物推断和时空推理。我们的方法——ROSIE（RObust in Silico Immunofluorescence）——结合了基于深度学习的多重推断与由LLM驱动的代理逻辑，模拟了病理学家级别的推理，从而实现了复杂组织微观结构的透明且可重复的分析。

我们将该工作流程应用于KSC转基因小鼠（n=24，4–12周龄）的胰腺上皮内瘤变（PanIN）进展研究，生成了1044万个单细胞谱图，并识别出一个按时间顺序排列的免疫轨迹，该轨迹包括三种空间上不同的免疫–基质状态：（1）早期免疫监视生态位：适应性免疫激活和抗原呈递富集的锐界窗口；（2）过渡性混合状态：淋巴活性下降、出现衰竭程序，以及早期EMT/血管生成信号；（3）以基质为主的终末状态：成纤维细胞扩增、血管重塑及免疫静默。

这些发现将胰腺癌的进展确立为一个按时间顺序发生的免疫激活—衰竭—基质接管的序列。该基于代理的框架超越了静态AI模型，提供了动态的、工具增强的推理能力，将高维组织数据与临床可解释性相连接，为识别肿瘤早期演化中的治疗转折点提供了可扩展的基础。

## Abstract
Pancreatic cancer progression is orchestrated by dynamic shifts in immune and stromal cellular ecosystems, yet the temporal and spatial principles governing these transitions remain poorly understood. Here, we present an agentic computational pathology framework that leverages large language models to orchestrate modular biomarker inference and spatiotemporal reasoning directly from routine H&E histology. Our approach, ROSIE (RObust in Silico Immunofluorescence), combines deep-learning-based multiplex inference with LLM-driven agent logic that emulates pathologist-level reasoning, enabling transparent and reproducible analysis of complex tissue microarchitectures.

Applying this workflow to pancreatic intraepithelial neoplasia (PanIN) progression in KSC transgenic mice (n=24, ages 4-12 weeks), we generated 10.44 million single-cell profiles and identified a temporally ordered immune trajectory comprising three spatially distinct immune-stromal states: (1) early immune-surveillance niche: sharply bounded window of adaptive immune activation and antigen-presentation enrichment; (2) transitional mixed state: declining lymphoid activity, emerging exhaustion programs, and early EMT/angiogenesis signals; (3) stromal-dominant terminal state: fibroblast expansion, vascular remodeling, and immune silence.

These findings establish pancreatic cancer progression as a temporally ordered sequence of immune activation, exhaustion, and stromal takeover. The agentic framework transcends static AI models by offering dynamic, tool-augmented reasoning that bridges high-dimensional tissue data with clinical interpretability--providing a scalable foundation for identifying therapeutic inflection points in early tumor evolution.

---

## 论文详细总结（自动生成）

# 自主多模态代理在胰腺癌免疫动态时空重建中的应用 —— 论文详细总结

---

## 一、研究问题与整体意义
### 研究背景
- 胰腺癌是恶性程度最高的实体瘤之一，其早期病变（PanIN）阶段往往伴随复杂的**免疫与基质生态系统重塑**。  
- 现有的多组学技术（如单细胞测序、多重免疫荧光成像）虽能揭示细胞异质性及免疫–肿瘤互作，但**成本高、通量低、组织需求大，不利于时序研究和临床转化**。  
- 常规的H&E切片资源丰富，但其分子信息尚未被充分挖掘。如何从H&E图像中解析免疫与基质动态，成为计算病理学的关键挑战。  

### 研究动机
- 现有的AI病理模型大多为**“单任务、静态”系统**，缺乏时空维度建模与可解释性。  
- 作者希望实现一种**透明、可扩展的智能代理架构**，可从H&E图像自动重建免疫动态，弥合计算结果与病理解释之间的鸿沟。  

---

## 二、方法论：框架思想与关键技术
### 总体结构
- 提出自主式计算病理框架 **ROSIE（RObust in Silico Immunofluorescence）**，结合：
  - 深度学习的**多重免疫标志物推断**；
  - **大语言模型（LLM）驱动的模块化任务编排与推理代理（agentic orchestration）**。
- 该系统通过LLM控制多个分析节点，从H&E切片自动生成从细胞分割到空间时序建模的全流程。

### 技术路线（文字化算法描述）
1. **Node 1 - 自适应切片分块 (Adaptive Tiling)**
   - 将整张H&E全扫描图（WSI）切分为512×512标准化图块；去除无效背景区域。
2. **Node 2.1 - 特征提取与生物标志物推断 (ROSIE Inference)**
   - 从H&E图像推断50通道蛋白特征图；
   - 基于训练于多重免疫荧光（CODEX）数据的深度网络预测细胞类型及分子通路活性。
3. **Node 2.2 - 单细胞分割与形态学描述**
   - 用HED滤波+分水岭算法分割细胞核，导出单细胞坐标及形态学特征。
4. **Node 3 - 时序建模 (Temporal Dynamics)**
   - 汇总跨时间点（4–12周）的细胞组成，计算对数倍数变化 (log₂ fold change, LFC)；
   - 构建**Timed Petri Net模型**以捕捉细胞状态间的转换方向与强度。
5. **Node 4 - 空间生态位 (Spatial Niche) 分析**
   - 利用DBSCAN+KMeans聚类，将细胞按邻近关系和通路活性聚类为生态位；
   - 生成免疫激活–衰竭–基质化的时空演化图谱。
6. **LLM 智能代理**
   - 通过LangGraph实现多节点状态机；
   - LLM（Claude 3.5 Sonnet、Llama 2 7B）按模板自动编写与调度Python脚本，实现“可解释执行流”（human-in-the-loop监督、节点可视化、动态决策）。

---

## 三、实验设计
### 数据与实验场景
- **数据来源：**
  - KSC 转基因小鼠模型（Ptf1a-Cre; LSL-Kras^G12D/+; Smad4^fl/fl）；
  - 共 8 张FFPE样本的全组织切片（4–12周龄各阶段）。
- **样本规模与细胞总量：**
  - 共分析单细胞水平数据 **10,446,317个细胞**，跨度覆盖胰腺癌早期进展全过程。
- **验证数据：**
  - 与已发表的多模态实验数据（如免疫组化IHC、Trichrome染色、功能成像）比对以验证推断可靠性。

### Benchmark与对比
- 无直接对比于传统AI算法的benchmark，而是通过**实验验证与文献对照**（Sharma et al., 2025）证明结果一致性；
- 通过**7项生物指标交叉验证表格（Supp. Table 4.6）**核实方向正确性，包括：
  - CD68⁺髓系细胞扩张；
  - TSPO活化；
  - M1/M2极化；
  - 基质扩增及纤维化；
  - 病变阶段对应等。

---

## 四、资源与算力
- 文中提及：
  - 使用 **Texas Advanced Computing Center (TACC)** 计算资源；
  - 未具体给出GPU型号、数量或运行时长。
- 说明所有生成代码均由LLM驱动、Python脚本实现，具备本地轻量化运行（Llama 2 7B 确保低延迟）。
- **推断阶段**未涉及模型再训练，因此整体算力需求中等。

---

## 五、实验数量与充分性
- **实验规模：**  
  - 约10.4百万单细胞，多时间点（4、5、6、7、8、9、11、12周）；
  - 每个阶段均进行生态位聚类与通路活性分析；
  - 共生成8张阶段性热图 + 7项验证指标 + 50通道蛋白推断。
- **实验完整度：**  
  - 从细胞丰度、时间变化、通路活性到空间结构均有独立分析；
  - 与已发表的生物学结果一致；
  - 虽未展示跨模型对比，但在范围内实验**系统且充分**。

---

## 六、主要结论与发现
- 定义了胰腺癌进展中的**三阶段免疫轨迹**：
  1. **早期免疫激活期（4–6周）**：
     - 富含T/B细胞、NK细胞及抗原呈递活性；
     - 存在紧密聚集的“免疫监视生态位”。
  2. **中期过渡期（7–9周）**：
     - 淋巴活性降低、出现T细胞衰竭；
     - 成纤维细胞与上皮细胞的EMT与血管新生信号上升；
     - 形成“免疫–基质混合生态位”。
  3. **晚期基质主导期（11–12周）**：
     - 免疫静默、EMT/纤维化/血管化显著；
     - 空间上形成结构化的成纤维细胞团块。
- 结论：胰腺癌的免疫生态系统沿着**“激活 → 衰竭 → 基质接管”**的时序演化。

---

## 七、方法优点与创新点
- **新颖性：**
  - 首次实现完全基于H&E的**多模态免疫动态重建**；
  - 结合LLM生成式编排（LangGraph + Human-in-Loop）确保可解释性。
- **可扩展性与可复用性：**
  - 模块化“node”框架可用于其他癌种或多时间点组织研究；
  - 支持快速平行化任务执行。
- **透明性：**
  - 每个节点的输出与逻辑可视化；
  - 所有步骤可被人工审查与替换；
  - 代码与数据开放。
- **生物学洞察力：**
  - 发现“免疫监视窗口”可能为早期干预靶点；
  - 揭示免疫衰竭与基质扩展协同驱动癌变。

---

## 八、不足与局限
- **数据维度限制：**
  - 仅采自KSC小鼠模型，尚未跨物种或人类样本验证。
- **时间结构为横截面推断：**
  - 并非同一病灶的纵向追踪，潜在的个体间差异未完全消除。
- **生物验证深度有限：**
  - ROSIE推断依赖于模型训练的多重荧光数据；
  - 稀有细胞型和过渡态仍需实验验证。
- **算力与可复现性：**
  - LLM生成代码高度依赖特定版本设定（如Claude 3.5），外界复现需环境同步。
- **通用性尚待验证：**
  - 虽有跨癌比较讨论（与肺腺癌模型类似轨迹），但实际证明尚属初步。

---

**（完）**
