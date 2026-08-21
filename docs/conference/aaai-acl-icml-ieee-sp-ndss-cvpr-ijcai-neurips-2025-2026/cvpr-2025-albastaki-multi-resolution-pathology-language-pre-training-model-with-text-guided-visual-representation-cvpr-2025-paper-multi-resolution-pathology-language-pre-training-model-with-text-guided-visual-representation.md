---
title: Multi-Resolution Pathology-Language Pre-training Model with Text-Guided Visual Representation
title_zh: 多分辨率病理-语言预训练模型与文本引导视觉表征
authors: "Albastaki, Shahad, Sohail, Anabia, Ganapathi, Iyyakutti Iyappan, Alawode, Basit, Khan, Asim, Javed, Sajid, Werghi, Naoufel, Bennamoun, Mohammed, Mahmood, Arif"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Albastaki_Multi-Resolution_Pathology-Language_Pre-training_Model_with_Text-Guided_Visual_Representation_CVPR_2025_paper.pdf"
tags: ["query:cell-path"]
score: 4.0
evidence: 多分辨率病理-语言预训练模型用于全切片图像
tldr: 现有病理视觉语言模型通常仅在单一放大倍率下对齐图像-文本对，限制了细节信息的利用。本文提出多分辨率病理-语言预训练模型，从全切片图像中提取多分辨率斑块并生成文本描述，实现多分辨率及跨分辨率对齐。实验表明该方法在癌症亚型分类、组织表型和生存分析等任务上优于单分辨率模型，为计算病理学提供了更强大的基础表示。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-albastaki-multi-resolution-pathology-language-pre-training-model-with-text-guided-visual-representation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 784, \"height\": 669, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-albastaki-multi-resolution-pathology-language-pre-training-model-with-text-guided-visual-representation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-albastaki-multi-resolution-pathology-language-pre-training-model-with-text-guided-visual-representation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 685, \"height\": 722, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-albastaki-multi-resolution-pathology-language-pre-training-model-with-text-guided-visual-representation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1633, \"height\": 1080, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-albastaki-multi-resolution-pathology-language-pre-training-model-with-text-guided-visual-representation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1507, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-albastaki-multi-resolution-pathology-language-pre-training-model-with-text-guided-visual-representation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1593, \"height\": 534, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-albastaki-multi-resolution-pathology-language-pre-training-model-with-text-guided-visual-representation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 154, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-albastaki-multi-resolution-pathology-language-pre-training-model-with-text-guided-visual-representation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 874, \"height\": 108, \"label\": \"Table\"}]"
motivation: 现有病理视觉语言模型局限于单一分辨率，限制了癌症亚型分类等任务的性能。
method: 提出多分辨率范式，从全切片图像提取多分辨率斑块并生成文本描述，进行多分辨率视觉文本对齐和跨分辨率对齐。
result: 在癌症亚型分类、组织表型和生存分析等任务上验证了改进效果。
conclusion: 多分辨率病理-语言预训练可提升计算病理学多种下游任务的表现。
---

## Abstract
In Computational Pathology (CPath), the introduction of Vision-Language Models (VLMs) has opened new avenues for research, focusing primarily on aligning image-text pairs at a single magnification level. However, this approach might not be sufficient for tasks like cancer subtype classification, tissue phenotyping, and survival analysis due to the limited level of detail that a single-resolution image can provide. Addressing this, we propose a novel multi-resolution paradigm leveraging Whole Slide Images (WSIs) to extract histology patches at multiple resolutions and generate corresponding textual descriptions through advanced CPath VLM. We introduce visual-textual alignment at multiple resolutions as well as cross-resolution alignment to establish more effective text-guided visual representations. Cross-resolution alignment using a multi-modal encoder enhances the model's ability to capture context from multiple resolutions in histology images. Our model aims to capture a broader range of information, supported by novel loss functions, enriches feature representation, improves discriminative ability, and enhances generalization across different resolutions. Pre-trained on a comprehensive TCGA dataset with 34 million image-language pairs at various resolutions, our fine-tuned model outperforms State-Of-The-Art (SOTA) counterparts across multiple datasets and tasks, demonstrating its effectiveness in CPath. The code is available on GitHub at: https://github.com/BasitAlawode/MR-PLIP.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：计算病理学（CPath）中，视觉语言模型（VLM）通常仅在单一放大倍率下对齐图像-文本对，限制了癌症亚型分类、组织表型分析和生存预测等任务的性能。
- **核心问题**：病理学家在实际诊断中会综合观察全切片图像（WSI）的多个分辨率（如 5×、10×、20×、40×），以同时获取组织整体结构（低倍）和细胞细节（高倍）。但现有 CPath VLM（如 PLIP、CONCH、QuiltNet、CPLIP）只利用单一分辨率，无法充分捕捉多尺度上下文信息，导致泛化能力不足。
- **本文动机**：提出多分辨率病理-语言预训练模型（MR-PLIP），利用多分辨率组织斑块及其对应的文本描述，实现多分辨率视觉-文本对齐和跨分辨率对齐，从而学习更强的文本引导视觉表征。

## 2. 论文提出的方法论

### 2.1 多分辨率组织袋构建
- 从 TCGA 数据集的 20,000 张 WSI 中提取多分辨率斑块，分辨率包括 5×、10×、20×、40×。
- 以 5× 斑块为“父”斑块，每个父斑块对应 4 个 10× 子斑块、16 个 20× 子斑块、64 个 40× 子斑块，形成父子层级结构。
- 总共生成约 3,400 万图像-文本对。
- 使用 Quilt-LLaVA 为每个斑块生成文本描述，使用 QuiltNet 文本编码器提取文本特征，使用 UNI 视觉编码器（ViT-L/16）提取视觉特征。

### 2.2 跨分辨率视觉-文本对齐（CVTA）
- 对于每个视觉特征 \(v_a\)，从对应文本袋 \(T_{i,j}\) 中选取 top-\(k_o\) 个正关键词（基于余弦相似度最大化）。
- 使用对比损失 \(L_{CVTA}\) 对齐视觉特征与正关键词，同时推开负关键词：

\[
L_{CVTA} = -\frac{1}{v_o v_0} \sum_{a=1}^{v_o} \frac{1}{k_o} \sum_{b=1}^{k_o} \log \frac{\exp(v_a^\top w_b^+/\tau)}{\sum_{b=1}^{k} \exp(v_a^\top w_b/\tau)}
\]

### 2.3 文本引导视觉表征与多模态编码器
- 将视觉特征 \(v_r^{i,j}\) 与选出的 \(k_o\) 个正关键词特征拼接，输入多模态编码器 \(E_{mm}\)，得到文本引导的视觉表征 \(z_r^{i,j}\)。
- 该表征融合了视觉和文本信息，能够更好地表达多分辨率上下文。

### 2.4 跨分辨率对齐损失（MRTVA）
- 基于 SimSiam 框架，对父-子分辨率对之间的文本引导视觉特征进行对齐：

\[
L_{MRTVA}(h_p^{i,j}, g_c^{i,j}) = -\sum_{p,c \in R, p \neq c} \left( \frac{h_p^{i,j}}{\|h_p^{i,j}\|_2} \cdot \frac{g_c^{i,j}}{\|g_c^{i,j}\|_2} \right)
\]

- 使用对称损失和 stop-gradient 操作防止模型坍塌。
- 最终总损失：\(L_t = L_{bl} + L_{CVTA} + L_{MRTVA}\)，其中 \(L_{bl}\) 包含 ITC、ITM、MLM、PLM 四个预训练任务损失。

## 3. 实验设计

### 3.1 数据集与任务
- **Tile 级分类**：15 个数据集，包括 Databiox、BACH、PatchCamelyon、Osteo、SkinCancer、MHIST、RenalCell、NCT-CRC、LC25000Lung、LC25000Colon、DigestPath、SICAP、WSSS4LUAD、UniToPatho、WILDS-CAM17。
- **WSI 级分类**：8 个数据集，包括 CAMELYON16、CAMELYON17、NSCLC-CPTAC、RCC-DHMC、BRCA-BRACS、HunCRC、PANDA、EBRAINS。
- 此外还涉及 WSI 级分割、核分割、跨模态检索等任务，总计 26 个独立数据集。

### 3.2 对比方法
- **视觉语言模型**：CLIP、PLIP、MI-Zero、BioCLIP、CONCH、QuiltNet、CPLIP。
- **纯视觉基础模型**：CTransPath、DinoSSLPath、UNI、CHIEF、GigaPath、Virchow、REMEDIS。

### 3.3 评估协议
- 零样本分类（含提示词集成 PE 与无提示词集成 nPE）
- 线性探测（冻结主干，训练线性分类器）
- 弱监督 WSI 分类（使用 ABMIL 聚合）
- 所有对比方法使用官方代码，保持一致的测试划分和推理提示。

## 4. 资源与算力

- **GPU**：使用 6 块 NVIDIA A100 GPU 进行模型实现和训练。
- **训练设置**：batch size = 64，共训练 50 个 epoch，优化器为 AdamW。
- **推理时间**：在 CAM16 数据集上，WSI 级分类平均每张 WSI 耗时 4.51 分钟，对比 MI-Zero（3.00 分钟）、BioCLIP（2.70 分钟）、PLIP（2.90 分钟），MR-PLIP 推理速度稍慢但仍可接受。
- 文中未明确给出总训练时长（如小时数或天数）。

## 5. 实验数量与充分性

- **实验规模**：在 26 个数据集上进行了多种任务的评估，包括零样本、线性探测、弱监督等，并进行了消融实验（表 3、4）。
- **消融实验**：
  - 损失项组合：\(L_{bl}\)、\(L_{bl}+L_{CVTA}\)、\(L_{bl}+L_{MRTVA}\)、\(L_{bl}+L_{CVTA}+L_{MRTVA}\) 的对比。
  - 父子层级结构：有/无父子层级约束的对比。
- **公平性**：使用官方代码和统一设置，且对比了 VLM 和纯视觉基础模型两大类方法，较为全面客观。
- **充分性**：实验覆盖多分辨率、多任务、多数据集，且包含消融研究，整体实验设计充分。

## 6. 论文的主要结论与发现

- MR-PLIP 在零样本 tile 级和 WSI 级分类上全面超越现有 VLM（如 CPLIP、CONCH、QuiltNet）和纯视觉基础模型（如 UNI、Virchow、GigaPath）。
- 多分辨率对齐（CVTA）和跨分辨率对齐（MRTVA）均能显著提升性能，两者结合效果最佳。
- 父子层级结构对于跨分辨率对齐至关重要，去除层级会降低性能。
- 多分辨率预训练能够有效增强模型的泛化能力，尤其在需要同时观察组织结构和细胞细节的任务中。

## 7. 优点

- **创新性强**：首次在 CPath VLM 中系统引入多分辨率图像-文本对齐和跨分辨率对齐，模拟病理学家的多尺度观察方式。
- **大规模预训练**：利用 3,400 万图像-文本对，数据规模大，覆盖多种分辨率。
- **技术合理**：CVTA 模块从文本袋中筛选相关关键词，MRTVA 损失基于 SimSiam 实现跨分辨率特征对齐，设计有理论支撑。
- **实验全面**：在 26 个数据集、多种任务和多种评估协议下验证，对比方法广泛，且包含消融实验。
- **开源代码**：提供 GitHub 代码，便于复现和进一步研究。

## 8. 不足与局限

- **计算成本高**：使用 6 块 A100 GPU，预训练数据规模大，训练和推理开销较高。
- **推理速度较慢**：每张 WSI 平均 4.51 分钟，比部分 VLM 慢约 30-50%，可能限制临床实时应用。
- **文本描述依赖外部模型**：使用 Quilt-LLaVA 生成描述，可能引入噪声或偏差，影响对齐质量。
- **预训练数据单一**：仅在 TCGA 数据集上预训练，未覆盖更多样化的组织来源和染色协议，可能存在分布偏移风险。
- **任务覆盖有限**：虽然涵盖分类、分割等，但未在生存分析等更复杂的临床预测任务上充分验证，尽管摘要中提及。
- **多模态编码器细节较少**：对多模态编码器的具体架构和训练策略描述不够详细，可能影响复现性。
- **未来工作**：作者计划扩展到 X 光、CT、MRI 等其他医学影像模态，但当前模型仅针对病理 H&E 图像。

（完）
