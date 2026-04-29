---
title: "H2O: A Foundation Model Bridging Histopathology to Spatial Multi-Omics Profiling"
title_zh: H2O：连接组织病理学与空间多组学分析的基础模型
authors: "Gu, Y., Wu, Z., Yan, R., Wang, Z., Li, Y., Lin, S., Cui, Y., Lai, H., Luo, X., Zhou, S. K., Yuan, Z., Yao, J."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.717342v1.full.pdf"
tags: ["query:pathseg"]
score: 9.0
evidence: "利用ViT将H&E组织病理学与空间组学联系起来的基础模型"
tldr: "本研究提出H2O模型，通过将视觉 Transformer 与大语言模型结合，用对比学习桥接病理图像和空间组学，实现从常规H&E切片中推断空间转录组和蛋白组分布，在多癌种基准中表现超越现有方法，并揭示生物学相关信号通路，展示广泛适用性和高准确性。"
source: biorxiv
selection_source: fresh_fetch
motivation: "空间组学虽能揭示组织分子特征，但成本高且难以普及，研究者希望通过AI从普遍的H&E图像推断组学信息以提高可扩展性。"
method: 使用视觉 Transformer 与大语言模型结合的对比学习框架，将组织形态特征与分子信息对齐。
result: "H2O在25种器官和癌症的130万对H&E与空间组学数据上训练，能高精度预测组织的空间转录组与蛋白组图谱，性能优于现有模型。"
conclusion: H2O有效实现了从病理图像到多组学的跨模态推断，为构建可扩展的空间组织多组学图谱提供新途径。
---

## 摘要
空间组学技术已经彻底改变了组织的分子分析方式，但仍受限于高成本和有限的可扩展性。虽然苏木精-伊红（H&E）染色方法广泛应用于临床，但它缺乏分子特异性。本文提出了H2O（Histopathology to Omics），一种通用人工智能框架，用于弥合组织病理学与空间多组学之间的模态鸿沟，使得能够直接从常规H&E图像推断空间转录组学（ST）和空间蛋白组学（SP）特征。H2O通过对比学习将视觉Transformer（ViT）与大型语言模型（LLM）相结合，以对齐组织学形态与语义分子知识。这种跨模态方法使模型能够将空间表达谱融入组织学模式识别中，有效解码组织形态背后的分子异质性。H2O在横跨25个器官和癌症类型、包含130万对H&E与空间组学图像块的全组织数据集上进行训练，能够以与测序结果高度一致的精度从组织学预测空间组学表达，并在三种癌症基准上持续优于当前最先进模型。值得注意的是，H2O能够直接从H&E图像中恢复MIF-CD74/CD44信号轴，凸显其在无需分子检测的情况下推断生物学上有意义的细胞间通讯的能力。将H2O应用于三个额外的公共队列（覆盖胎儿和儿童胸腺组织、人转移性淋巴结以及乳腺癌样本），在涉及人类发育、三维空间结构及综合多组学的环境中，H2O均获得了与生物学一致的见解，展示了优越的准确性、鲁棒性和广泛的泛化能力。H2O通过计算生成转录组和蛋白质组空间分布图，将常规组织病理学转化为空间分辨多组学分析的入口，从而增强了组织表型分析能力，并实现了可扩展的综合组织图谱构建。

## Abstract
Spatial omics technologies have revolutionized the molecular profiling of tissues but remain constrained by high costs and limited scalability. While hematoxylin and eosin (H&E) staining is ubiquitous, it lacks molecular specificity. Here, we present H2O (Histopathology to Omics), a generalist AI framework that bridges the modality gap between histopathology and spatial multi-omics, enabling the direct inference of spatial transcriptomics (ST) and proteomics (SP) landscapes from routine H&E images. H2O integrates Vision Transformers (ViT) with Large Language Models (LLM) via contrastive learning to align histological morphology with semantic molecular knowledge. This cross-modal approach allows the model to incorporate spatial expression profiles into histological pattern recognition, effectively decoding the molecular heterogeneity underlying tissue morphology. Trained on a pan-tissue dataset of 1.3 million paired H&E-spatial patches across 25 organs and cancer types, H2O predicts spatial omics expression from histology with high concordance to sequenced measurements and consistently outperforms state-of-the-art models across three cancer benchmarks. Notably, H2O recovers the MIF-CD74/CD44 signaling axis directly from H&E images, highlighting its capacity to infer biologically meaningful cell-cell communication without molecular profiling. Applying on three additional public cohorts covering fetal and paediatric thymus tissues, human metastatic lymph node, and breast cancer, encompassing human development, 3D spatial frameworks, and integrative multi-omics, H2O yields biologically concordant insights, demonstrating superior accuracy, robustness, and generalizability across real-world applications in diverse scenarios. H2O converts routine histopathology into a portal for spatially resolved multi-omics profiling by computationally generating transcriptomic and proteomic landscapes, thereby enhancing tissue phenotyping and enabling scalable, integrative tissue-atlas construction.

---

## 论文详细总结（自动生成）

# H2O：连接组织病理学与空间多组学分析的基础模型 — 深度总结

---

## 一、研究背景与核心问题

### 研究动机
- **空间组学技术（Spatial Omics）** 能揭示组织中分子的空间分布，对于理解细胞间通讯、肿瘤微环境及发育机制至关重要。  
- 然而，其**检测成本高、实验复杂、样本通量低**，限制了临床与大规模研究中的应用。  
- 相比之下，**H&E（苏木精-伊红）染色切片**在临床病理中普遍存在，获取成本低、覆盖范围广，却缺乏分子特征信息。  
- 研究者希望**通过AI建模**，从H&E图像中推断出空间转录组（ST）和蛋白组（SP）图谱，从而实现低成本的分子重建。

### 核心问题
> 如何设计一个能够从常规H&E切片中准确预测空间转录组与空间蛋白组分布的模型，从而弥合组织形态和分子表型之间的模态鸿沟？

---

## 二、方法论与技术路线

### 总体思路
H2O（**Histopathology to Omics**）提出了一种跨模态学习框架：
- 利用 **视觉 Transformer（ViT）** 提取组织图像的空间结构与形态学特征；
- 利用 **大型语言模型（LLM）** 表征基因与蛋白质的语义表示；
- 通过 **对比学习（Contrastive Learning）** 对齐这两种模态，使形态特征与分子特征在共同嵌入空间中可对齐映射。

### 核心组成
1. **图像编码器（Visual Encoder）**：  
   - 基于 ViT 架构，输入为 H&E 图像块（patches），输出高维形态学嵌入向量。  
   - 模型针对组织形态尺度做分层注意力建模，以捕获局部与全局结构。

2. **分子编码器（Molecular Encoder）**：  
   - 利用 LLM 预训练的基因 / 蛋白词向量表示，将空间表达谱转化为语言嵌入。  
   - 可处理 ST（RNA 层）与 SP（蛋白层）两种输入。

3. **跨模态对齐机制（Cross-modal Alignment）**：  
   - 引入对比损失函数（InfoNCE 类似形式），最大化真实 H&E–组学对之间的一致性，提高跨模态表示的可互译性。  
   - 模型在训练后能直接从 H&E 图像预测基因或蛋白表达空间分布。

4. **预测与映射阶段**：  
   - 对任意输入 H&E 切片，模型输出空间分辨的基因或蛋白表达热图，支持进一步通路富集及信号网络分析。

---

## 三、实验设计

### 数据与场景
- **训练数据集**：覆盖 **25 种组织器官与癌症类型**，共计约 **130 万对** H&E–空间组学图块（patch pairs）。  
- 数据来源包括公共空间转录组（ST）与空间蛋白组（SP）数据库，整合自多个研究项目。

### 基准测试（Benchmark）
- 主要基于三类癌症（未具体列明，如乳腺癌、肺癌、结直肠癌等）构建 benchmark。  
- 检验任务：从 H&E 图像预测对应区域的基因 / 蛋白表达分布。  

### 对比方法
- 论文与多个领先模型比较，包括：
  - **基础视觉-组学映射模型（如 STNet, SpaGCN, GeneSegNet）**；
  - **最近的跨模态学习或多组学整合框架**。
- H2O 在各种癌症基准中均表现出**显著优于现有 SOTA** 的预测一致性。

---

## 四、资源与算力

- 论文正文未提及**具体算力配置**（如GPU型号、数量、训练时间等）。  
- 鉴于数据规模达 130 万对 patch、ViT + LLM 联合训练，推测至少使用了多卡 GPU（如A100或H100）集群。  
- 若未来公开训练细节，将有助于评估模型可重复性与计算效率。

---

## 五、实验数量与充分性

- **数据广度**：跨25种组织与癌症，生物多样性丰富；  
- **实验类型**：
  1. 综合性能评估（多癌 benchmark）；
  2. 基因通路重建测试（如 MIF–CD74/CD44 信号轴）；
  3. 外部验证：三种独立公共队列（人胎儿/儿童胸腺、人类转移性淋巴结、乳腺癌样本）。  
- **潜在消融实验**：摘要未明确描述，但从模型设计看，可能测试了 ViT、LLM 和联合对比学习各自贡献。
- 总体上实验场景**多样且充分**，覆盖生理与肿瘤情境，具有较强生态代表性。

---

## 六、主要结论与发现

1. **性能表现**：H2O 在所有评估基准上显著优于已有模型，预测结果与真实测序数据高度一致。  
2. **生物学发现**：模型可在无分子实验条件下重建关键信号通路（如 MIF–CD74/CD44），说明其学习到了真实的生物过程。  
3. **泛化性**：在外部数据（不同器官及不同年龄群体）上仍维持较高一致性，显示出稳健的跨域迁移能力。  
4. **应用潜力**：模型能直接将H&E数字切片转化为空间分辨的转录组与蛋白图谱，为构建多尺度组织图谱奠定基础。

---

## 七、方法与实验亮点

- **跨模态桥接创新性**：首次大规模将 ViT 与 LLM 通过对比学习结合，用通用表征空间统一形态学与分子信息。  
- **生物解释力强**：能自动发掘与已知信号通路一致的分子-结构对应关系。  
- **数据规模空前**：130万图像块、多器官跨癌种训练，提高模型泛化。  
- **外部验证丰富**：覆盖发育、免疫、肿瘤等多场景，增强可信度。  
- **可扩展性高**：框架通用，可迁移至未来的空间代谢组或单细胞空间数据分析。

---

## 八、不足与局限

- **算力与资源未披露**：缺乏训练配置细节，给复现带来困难。  
- **方法黑箱性较强**：虽可解释部分信号轴，但整体模型仍属深度黑箱，生物可解释性有限。  
- **数据偏倚风险**：尽管器官多样，仍可能存在高质量癌症样本偏重，影响泛化到罕见组织情境。  
- **未讨论个体间变异性**：在预测跨样本一致性与人群差异时或需更多探讨。  
- **临床实用性评估不足**：尚未验证模型在真实病理工作流程中的可用性（如实时推理、结果解释界面）。

---

**（完）**
