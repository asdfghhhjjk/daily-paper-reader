---
title: "Autonomous multimodal agents enable transparent, spatiotemporal reconstruction of immune dynamics in pancreatic cancer progression"
title_zh: 自主多模态代理实现胰腺癌进展中免疫动态的透明时空重建
authors: "Huang, B., Zhu, B."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719684v1.full.pdf"
tags: ["query:pathseg"]
score: 9.5
evidence: "用于从 H&E 组织学中进行免疫动力学时空重建的计算病理学框架"
tldr: 研究团队开发了ROSIE智能病理系统，结合大语言模型与深度学习从常规组织切片中推断免疫标志和时空演化规律，在小鼠胰腺癌模型中揭示了免疫活化到基质主导的序列化进程，为理解肿瘤免疫动力学和早期干预提供新思路。
source: biorxiv
selection_source: fresh_fetch
motivation: 胰腺癌的免疫和基质细胞生态动态变化机制尚不清楚，需要揭示其时空演变规律。
method: 提出了基于大语言模型的ROSIE计算病理框架，结合深度学习多重生物标志推断和空间时间推理。
result: ROSIE在小鼠模型中生成千万级单细胞图谱，解析出三个空间上不同的免疫-间质状态及其时间顺序。
conclusion: 研究表明胰腺癌的发展遵循免疫激活、免疫衰竭和基质主导三个阶段，为早期干预提供关键窗口。
---

## 摘要
胰腺癌的进展是由免疫和基质细胞生态系统的动态变化所驱动的，然而支配这些转变的时间和空间规律仍然知之甚少。在此，我们提出了一种基于“代理”概念的计算病理学框架，该框架利用大型语言模型来协调模块化生物标志物推断及时空推理，能够直接从常规的H&E组织病理切片中进行分析。我们的方法ROSIE（RObust in Silico Immunofluorescence）结合了基于深度学习的多重推断能力和由大型语言模型驱动的代理逻辑，可模拟病理学专家级的推理水平，从而实现对复杂组织微结构的透明且可重复分析。

将该工作流程应用于KSC转基因小鼠（n=24，年龄为4-12周）胰腺上皮内瘤变（PanIN）进展的研究中，我们生成了1044万个单细胞谱，并识别出一个按照时间顺序排列的免疫轨迹，其中包括三个空间上截然不同的免疫-基质状态：（1）早期免疫监视生态位：具有明显边界的适应性免疫活化和抗原呈现富集窗口；（2）过渡性混合状态：淋巴活性下降、衰竭程序出现，以及早期EMT/血管生成信号；（3）基质占优的终末状态：成纤维细胞扩增、血管重塑和免疫沉默。

这些发现揭示了胰腺癌进展是一个在时间上有序的免疫激活、衰竭与基质接管的序列。该代理框架超越了静态AI模型，通过提供动态、工具增强的推理，将高维组织数据与临床可解释性相连接——为在早期肿瘤演化中识别治疗拐点提供了可扩展的基础。

## Abstract
Pancreatic cancer progression is orchestrated by dynamic shifts in immune and stromal cellular ecosystems, yet the temporal and spatial principles governing these transitions remain poorly understood. Here, we present an agentic computational pathology framework that leverages large language models to orchestrate modular biomarker inference and spatiotemporal reasoning directly from routine H&E histology. Our approach, ROSIE (RObust in Silico Immunofluorescence), combines deep-learning-based multiplex inference with LLM-driven agent logic that emulates pathologist-level reasoning, enabling transparent and reproducible analysis of complex tissue microarchitectures.

Applying this workflow to pancreatic intraepithelial neoplasia (PanIN) progression in KSC transgenic mice (n=24, ages 4-12 weeks), we generated 10.44 million single-cell profiles and identified a temporally ordered immune trajectory comprising three spatially distinct immune-stromal states: (1) early immune-surveillance niche: sharply bounded window of adaptive immune activation and antigen-presentation enrichment; (2) transitional mixed state: declining lymphoid activity, emerging exhaustion programs, and early EMT/angiogenesis signals; (3) stromal-dominant terminal state: fibroblast expansion, vascular remodeling, and immune silence.

These findings establish pancreatic cancer progression as a temporally ordered sequence of immune activation, exhaustion, and stromal takeover. The agentic framework transcends static AI models by offering dynamic, tool-augmented reasoning that bridges high-dimensional tissue data with clinical interpretability--providing a scalable foundation for identifying therapeutic inflection points in early tumor evolution.

---

## 论文详细总结（自动生成）

# 自主多模态代理实现胰腺癌进展中免疫动态的透明时空重建  
——论文结构化总结

---

## 一、核心问题与研究背景

- **研究动机**：胰腺癌是一种高度致死的恶性肿瘤，其早期演化涉及复杂的免疫与基质重塑过程。现有研究虽揭示了部分炎症和纤维化变化，但缺乏能够系统刻画其**时空动态演进**的工具。尤其是在仅凭常规 H&E 染色切片的条件下，尚无法实现高维度的免疫状态重建。  
- **研究目标**：作者希望构建一种**可解释、可扩展、具代理能力（agentic）的计算病理学框架**，能够直接从常规组织切片中重建胰腺癌进展的免疫动力学与空间生态演化规律。

---

## 二、方法论与技术体系

### 1. 总体框架
论文提出了基于大型语言模型（LLM）驱动的**“代理式计算病理框架”ROSIE（RObust in Silico Immunofluorescence）**。核心思想是将：
- 深度学习模型用于**生物标志推断（multiplex biomarker inference）**；
- LLM 用于**跨模块任务协调与推理逻辑生成**；
- 从而实现一个**能模仿病理专家多步骤推断过程**的自主多模态分析系统。

### 2. 模块与流程设计
该框架采用**多节点（multi-node）的模块化管线**，由 LLM 通过 LangGraph 状态图体系进行调度：

| 节点编号 | 功能模块 | 主要任务说明 |
|-----------|-----------|--------------|
| Node 1 | **Adaptive Tiling** | 切分全切片 (WSI) 为 512×512 像素小块，执行组织检测与背景去除 |
| Node 2.1 | **Spatial Feature Extraction** | 基于颜色去卷积和分水岭算法计算每个细胞核坐标及形态特征 |
| Node 2.2 | **Biomarker Inference** | 利用 ROSIE 模型从 H&E 图像预测 50 种蛋白通道的表达分布 |
| Node 3 | **Temporal Dynamics** | 构建时间序列模型（采用Timed Petri Net）描述细胞群体转变 |
| Node 4 | **Spatial Niche Construction** | 基于 DBSCAN + K-means 聚类生成空间生态位，并计算通路活性 |

### 3. 算法与推理逻辑
- **时序分析**：利用多时间点（4–12周）的鼠胰腺切片数据，通过计算相邻时间点的 Log₂ Fold Change（LFC）获得细胞组成变化速率。  
- **状态模型**：构建 Timed Petri Net，以节点代表不同病程阶段的主导细胞群，边表示细胞状态转变速率。  
- **空间分析**：通过 ROSIE 推断的蛋白表达矩阵，计算各细胞通路 Z-score；再根据空间聚类结果形成免疫活跃、免疫-基质混合、或基质占优的生态位。  
- **LLM 编排逻辑**：LLM 自动生成 Python 执行脚本，实现跨模块数据传递，并通过人类监督（Human-in-the-loop）确保解释性与可靠性。

---

## 三、实验设计

- **数据来源**：来自 KSC 转基因小鼠（Ptf1a-Cre; LSL-Kras^G12D/+; Smad4^fl/fl），共 8 张 H&E 全切片（SVS 格式），年龄跨度 4–12 周。  
- **分析对象**：约 10,446,317 个单细胞。数据涵盖胰腺上皮内瘤变到晚期纤维化阶段。  
- **验证方式**：
  - 计算预测与 **免疫组化（IHC）、三色染色（Trichrome）、免疫荧光（IF）** 等实验数据对比；
  - 与前期公开的 **Sharma et al. (2025)** 胰腺癌模型及 **Zhu et al. (2025)** 肺腺癌模型结果进行交叉验证。  
- **Benchmark**：与多模态空间组学（CODEX）结果比对，验证 ROSIE 的推断准确性。  
- **对比方法**：无直接算法竞争对比（如弱监督或 foundation model），重点在于跨模态验证（计算 vs 实验）。

---

## 四、算力与资源消耗

- 论文未明确说明具体 GPU 型号或训练时长。  
- 提及计算资源来源于 **Texas Advanced Computing Center (TACC)**；推理阶段通过 **Claude 3.5 Sonnet (Anthropic)** 或 **Llama 2 (7B, Ollama 部署)** 执行。  
- 推理过程为确定温度 (temperature=0)，确保代码生成一致性。  
→ **结论**：文中未提供确切算力参数，仅说明使用云端高性能计算环境并行处理千万级细胞数据。

---

## 五、实验数量与充分性评估

- **主要实验组**：8 个时间点（4–12周）× 多个空间分析模块；
- **验证实验**：7 项湿实验指标（CD68⁺、TSPO、M1/M2 极化、纤维化、腺泡丢失、导管负荷、病理分期）；
- **补充实验**：8 张空间生态位热图（S7.1–S7.8）展示病程中免疫生态变化。

总体来看，**实验覆盖充分**，在时间维度（长达8阶段）和空间维度（细胞层级）均具完备性，且与独立湿实验相符；但缺乏跨物种或临床人类队列对照，属前临床规模验证。

---

## 六、主要结论与发现

1. 胰腺癌的进展遵循**三相免疫轨迹**：
   - **早期免疫监视阶段（4–6周）**：富含 T/B/NK/DC 细胞，抗原呈现及适应性免疫高活性。  
   - **过渡混合状态（7–9周）**：淋巴耗竭、髓系抑制上升，并出现 EMT 与血管生成信号。  
   - **终末基质占优阶段（11–12周）**：成纤维细胞与内皮重塑明显，免疫沉默。  
2. 免疫衰竭与基质重塑是同步发生的过程，而非独立事件。  
3. LLM 驱动的代理框架可在无需分子实验情况下重建细胞级时空动力学。  
4. 该分析揭示潜在的“**早期免疫易感窗口**”——为干预胰腺癌提供时间依据。

---

## 七、研究亮点（优势）

- **创新性强**：首次将 LLM 代理逻辑引入计算病理学，实现多节点自动推理与代码生成。  
- **数据规模巨大**：超过千万级单细胞分析，展现卓越的分辨率与统计稳健性。  
- **多模态整合**：将 H&E 图像转化为虚拟多重免疫荧光（virtual multiplex IF），显著拓宽常规组织学的分子解释能力。  
- **跨维度推理**：同时整合空间聚类、时间序列与免疫通路层面分析。  
- **可解释与可重构**：模块化设计使各节点可独立更新或替换，适应未来病理任务。  
- **临床可转化性**：依赖常规 FFPE 切片，可用于大规模患者样本和早筛项目。

---

## 八、不足与局限

- **数据来源单一**：仅采用小鼠模型，缺乏人体样本验证。  
- **时间序列为横断面采样**：未跟踪同一病灶的连续演化。  
- **ROSIE 模型依赖预训练数据**：部分稀有或过渡状态细胞预测需进一步实验验证。  
- **算力与超参未透明公布**：难以复现具体训练性能。  
- **因使用 LLM 自动生成代码**，存在潜在输出不确定性或逻辑偏向风险。  
- **机制层面尚需实验验证**：免疫与成纤维互作的因果关系仍待探究。

---

**（完）**
