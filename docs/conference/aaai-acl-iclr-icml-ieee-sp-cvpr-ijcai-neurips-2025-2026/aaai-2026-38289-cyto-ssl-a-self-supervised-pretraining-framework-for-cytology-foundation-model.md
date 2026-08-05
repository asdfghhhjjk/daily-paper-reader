---
title: "Cyto-SSL: A Self-Supervised Pretraining Framework for Cytology Foundation Model"
title_zh: Cyto-SSL：面向细胞学基础模型的自监督预训练框架
authors: "Yiming Zhang, Rui Yan, Xiaohua Wan, Yifan Zhao, Shuang Feng, Zhetao Xu, Ying Wang, Fa Zhang, Bin Hu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38289/42251"
tags: ["query:cellseg"]
score: 4.0
evidence: 面向细胞学图像的自监督预训练，以细胞核为中心的扰动，赋能下游细胞分析
tldr: 细胞学WSI稀疏且细胞关系非结构化，限制了基础模型发展；提出首个细胞学自监督预训练框架Cyto-SSL，引入以核为中心的扰动策略；在下游任务中有效提升模型能力，为细胞学图像分析提供通用预训练模型。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38289/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 870, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38289/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1833, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38289/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 709, \"height\": 1637, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38289/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 884, \"height\": 825, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38289/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 1219, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38289/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 856, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38289/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 751, \"height\": 418, \"label\": \"Table\"}]"
motivation: 细胞学图像空间稀疏、无组织结构，现有组织学模型难以迁移。
method: 提出以细胞核为中心的扰动自监督预训练框架Cyto-SSL。
result: 在细胞学图像下游任务中取得更好性能。
conclusion: 为细胞学图像分析提供了首个专用自监督基础模型。
---

## Abstract
Cytological images originate from exfoliated cells, collected via liquid-based slides and digitized into whole slide images (WSIs). Unlike histological WSIs that exhibit continuous and well-structured tissue, cytological WSIs are sparse in spatial distribution and unstructured in cellular relationships. Typically, the nucleus serves as the primary diagnostic feature, while surrounding cytoplasmic information plays a supportive role. These unique characteristics limit the development of effective foundation models and hinder the transferability of histology-based models for cytopathology. To address this, we propose **Cyto-SSL**, the first self-supervised pretraining framework for cytological images. It introduces **Nuclei-Centered Perturbation**, which highlights individual nuclei by perturbing non-nuclear regions. We also design an SR-Transformer module, which complements this by using sparse attention to concentrate on diagnostically relevant scattered cells, while iRPE helps model to capture local spatial relationships and avoids unnecessary attention to irrelevant global structures. Experimental results show that **Cyto-SSL** enhances performance across diverse cytological datasets and Multiple Instance Learning (MIL) methods. On a WSI-level dataset, it achieved 95.67% accuracy and outperformed ImageNet-pretrained ResNet-50 by 11.33%, demonstrating superior feature representation for cytological analysis. Additionally, **Cyto-SSL** modules are plug-and-play, easily integrated into other pretraining frameworks, yielding a 2.6% accuracy gain across different SSL methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：细胞学图像来源于脱落细胞，经液基薄层制片和全切片扫描得到，是宫颈癌、乳腺癌等早期筛查的重要无创工具。
- **核心问题**：与组织病理学图像（连续、结构化）不同，细胞学图像具有两大特点：
  - **空间稀疏性**：细胞分布稀疏，背景和空白区域占比高。
  - **语义非结构化**：细胞间缺乏紧密的组织连续性，诊断往往以单个细胞核为核心特征，细胞质起辅助作用。
- **研究动机**：现有自监督预训练方法多针对组织学图像设计，直接迁移至细胞学效果不佳；而基于ImageNet预训练的CNN或VPU学习等方法，也受限于CNN架构和自然图像差异，难以应对稀疏、非结构化的细胞学数据。
- **整体含义**：论文提出首个专为细胞学图像设计的自监督预训练框架**Cyto-SSL**，旨在从零开始训练一个细胞学基础模型，为下游多实例学习（MIL）提供更优质的细胞学特征表示。

### 2. 方法论
- **整体架构**：
  - 采用教师-学生自蒸馏框架（类似DINO），学生网络学习教师网络的概率分布，教师通过指数移动平均（EMA）更新。
  - 损失为交叉熵：\( \mathcal{L}_{\text{Cyto-SSL}} = -\sum_{i=1}^{K} p_t^{(i)} \log p_s^{(i)} \)，其中 \(p_t\)、\(p_s\) 分别为教师、学生的softmax输出，\(K\) 为原型维度。
- **Nuclei-Centered Perturbation（以细胞核为中心的扰动）**：
  - **目的**：强制模型聚焦于诊断关键细胞核区，抑制背景和非细胞区域的干扰。
  - **步骤**：
    1. **细胞核检测**：使用冻结的CellViT（Transformer分割模型）定位细胞核中心 \(P\)。
    2. **扰动**：保留细胞核周围半径 \(r=50\) 像素的区域（维持核质比等关键形态信息），对半径外的像素进行随机打乱，破坏背景与无关细胞的结构。
    3. **视图生成**：以核为中心裁剪多尺度视图，并施加旋转、颜色抖动等增强，适应不同SSL框架（如SimCLR、DINO）的尺度策略。
- **SR-Transformer模块**：
  - **稀疏自注意力**：对注意力矩阵 \(P = QK^T/\sqrt{d}\) 施加top-\(h\)二值掩码，仅保留每行最大的 \(h\) 个值（\(h=16\)），将非关键token的注意力置为 \(-\infty\)，从而突出稀疏的诊断性细胞核。
  - **图像相对位置编码（iRPE）**：引入可学习相对位置偏置 \(R = Q(r^K)^T + K(r^Q)^T\)，修改注意力分数为 \((QK^T + R)/\sqrt{d}\)，并在值矩阵上添加偏置 \(r^V\)，提升局部空间关系建模能力，避免绝对位置编码引入的不必要长距离依赖。
- **模块融合**：Nuclei-Centered Perturbation与SR-Transformer协同工作，前者通过视图设计引导注意力焦点，后者通过稀疏注意力和相对位置编码强化特征提取，两者均作为即插即用模块可嵌入多种SSL方法。

### 3. 实验设计
- **数据集**：
  - **预训练**：私有宫颈细胞学WSI数据集（760张，40×放大，约80000×80000像素，含阴/阳性标签）。
  - **下游评估**：同上宫颈WSI数据集（70%训练/30%测试）、**FNAC 2019**（212张乳腺细胞学图像，2048×1536，良/恶性）、**NIH-NLM Thin Blood Smears Pf**（965张血涂片图像，5312×2988，阴/阳性）。
- **基准对比**：
  - **特征提取器**：ImageNet预训练ResNet-50、DINO V2（ImageNet初始化，ViT-tiny）、Prov-GigaPath（组织学基础模型，并用LoRA微调），以及CNN+VPU（用于LESS方法）。
  - **MIL方法**：ABMIL、TransMIL、DTFD-MIL、CLAM-SB、DSMIL、LESS。
  - **SSL框架兼容性**：SimCLR、MoCo、DINO基础上增加Cyto-SSL模块。
- **评价指标**：AUC、准确率（ACC）、召回率（Recall）。
- **实现细节**：预训练用Adam优化器，初始学习率5e-4，余弦退火；下游MIL均使用官方配置。

### 4. 资源与算力
- **硬件**：实验在配备**Intel Core i9-14900K CPU**和**NVIDIA RTX 4090 GPU**的工作站上进行，但未明确说明使用的GPU数量、训练时长及显存消耗等具体算力细节。
- **模型规模**：骨干网络为ViT-tiny（参数量较小），预训练数据集包含约250万个40×下512×512的patch。

### 5. 实验数量与充分性
- **下游任务实验**：在3个数据集上，结合6种MIL方法，与3种主流特征提取器（ResNet-50、DINO V2、Prov-GigaPath）及VPU baseline进行了全面对比，结果呈现在大型表格中（大约18组配置）。
- **消融实验**：以DINO为基线，分别单独添加Nuclei-Centered Perturbation、稀疏自注意力、iRPE，以及在ABMIL和LESS两种MIL下评估，验证各组件贡献（共约8组实验）。
- **SSL框架兼容性**：在SimCLR、MoCo、DINO上测试Cyto-SSL即插即用效果（3组对比）。
- **注意力可视化**：对三个数据集进行定性分析。
- **充分性与公平性**：实验覆盖多种数据集、多种MIL方法和多个SSL框架，对比基线具有代表性，所有MIL方法保持同一特征提取器之外的设置不变，比较公平。消融实验系统评估了各模块必要性，整体实验设计较为充分。

### 6. 主要结论与发现
- **性能提升显著**：Cyto-SSL在宫颈WSI上与LESS结合达到95.67%准确率，较ImageNet预训练ResNet-50在ABMIL上提升11.33%准确率；在其他数据集上普遍优于组织学基础模型和DINO V2。
- **特征质量增强**：Nuclei-Centered Perturbation和SR-Transformer协同使模型能聚焦于稀疏的诊断性细胞核，注意力可视化显示其能清晰区分细胞核、细胞质和伪影，而基线方法注意力分散。
- **通用性与兼容性**：Cyto-SSL作为即插即用模块可提升SimCLR、MoCo、DINO等多个自监督框架的性能（准确率提升0.86%～2.6%）。
- **MIL方法适配性**：在细胞学场景中，简单的注意力池化（ABMIL）反而优于复杂的组织学MIL方法（如TransMIL、DTFD-MIL），表明细胞学特有的稀疏结构需要简单聚焦策略。

### 7. 优点
- **领域针对性设计**：首个专为细胞学图像设计的自监督预训练框架，充分考虑了稀疏分布与非结构化特性。
- **创新模块**：Nuclei-Centered Perturbation直观有效地抑制背景干扰；SR-Transformer通过稀疏注意力和相对位置编码重点捕获局部细胞关系，避免虚假全局依赖。
- **即插即用**：模块可无缝集成到主流自监督方法中，提升通用性。
- **实验全面**：覆盖多个数据集、多种MIL方法、消融研究和可视化，论证充分。

### 8. 不足与局限
- **预训练数据单一**：仅在单一中心的宫颈细胞学数据上预训练，可能限制模型在不同细胞学亚型（如胸腹水、痰液、尿液等）或不同制片/扫描条件下的泛化能力。
- **模型规模较小**：仅使用ViT-tiny骨干，未探索更大模型（如ViT-S、ViT-B）的扩展规律及性能潜力。
- **细胞核检测依赖外部模型**：Nuclei-Centered Perturbation依赖预训练的CellViT，其性能直接影响伪影去除和焦点生成质量，且需额外计算开销。
- **iRPE模块效用在部分MIL下不显著**：消融实验显示，在与LESS结合时，稀疏注意力和iRPE增益有限，模块效用与下游MIL方法的注意力机制存在耦合，且未深入分析原因。
- **缺乏细粒度诊断任务验证**：实验仅关注WSI级分类，未探讨细胞级分类、计数或分割等任务上的效果。
- **算力细节缺失**：未提供具体GPU使用数量和训练时长，难以评估训练成本。

（完）
