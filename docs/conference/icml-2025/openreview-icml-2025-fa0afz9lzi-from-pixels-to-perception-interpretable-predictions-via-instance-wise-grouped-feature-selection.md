---
title: "From Pixels to Perception: Interpretable Predictions via Instance-wise Grouped Feature Selection"
title_zh: 从像素到感知：通过实例级分组特征选择实现可解释预测
authors: "Moritz Vandenhirtz, Julia E Vogt"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Fa0aFZ9LZi"
tags: ["query:pathology-ai"]
score: 5.0
evidence: 通过实例级分组特征选择实现可解释预测
tldr: 该论文提出一种通过实例级稀疏化输入图像到语义区域的方法，实现内在可解释的分类预测。方法动态决定每个实例的稀疏度，生成人类可理解的解释，可应用于病理图像特征提取的可解释性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 721, \"height\": 242, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1587, \"height\": 650, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 828, \"height\": 116, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1705, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 836, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1635, \"height\": 933, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1703, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1709, \"height\": 1023, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1607, \"height\": 284, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1756, \"height\": 1678, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1747, \"height\": 1670, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1748, \"height\": 1617, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1744, \"height\": 1617, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1748, \"height\": 1498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fa0afz9lzi/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1744, \"height\": 2041, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-fa0afz9lzi/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 1718, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fa0afz9lzi/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 850, \"height\": 810, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fa0afz9lzi/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1177, \"height\": 895, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fa0afz9lzi/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1057, \"height\": 1223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fa0afz9lzi/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1086, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fa0afz9lzi/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 981, \"height\": 291, \"label\": \"Table\"}]"
motivation: 理解模型决策过程对任务和数据洞察至关重要，需要可解释的预测方法。
method: 在语义区域空间学习图像掩码，实现实例级稀疏化，并动态确定稀疏度。
result: 在半合成和自然图像上生成了更有意义、人类可理解的解释。
conclusion: 该方法为可解释分类提供了新途径，可应用于医学图像分析。
---

## Abstract
Understanding the decision-making process of machine learning models provides valuable insights into the task, the data, and the reasons behind a model's failures. In this work, we propose a method that performs inherently interpretable predictions through the instance-wise sparsification of input images. To align the sparsification with human perception, we learn the masking in the space of semantically meaningful pixel regions rather than on pixel-level. Additionally, we introduce an explicit way to dynamically determine the required level of sparsity for each instance. We show empirically on semi-synthetic and natural image datasets that our inherently interpretable classifier produces more meaningful, human-understandable predictions than state-of-the-art benchmarks.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义
- **研究动机**：深度学习的决策过程缺乏透明性，理解模型如何做出预测对于识别偏见、确保安全、建立信任至关重要。传统可解释性方法分为内在可解释性和事后解释，但事后解释可能存在不忠实于模型的问题。
- **整体含义**：本文提出一种**内在可解释**的实例级特征选择方法，通过将输入图像稀疏化为人类可感知的语义区域，使模型预测基于选择性的、有意义的像素组，从而提供忠实于模型计算的可解释性。

### 2. 方法论
- **核心思想**：在超像素（superpixels，如SLIC算法生成的语义区域）空间进行二进制掩码，而不是在像素级。每个区域被视为一个可选择的特征。通过实例级预测区域选择概率，并利用Gumbel-Softmax进行可微采样。
- **关键技术细节**：
  - 区域提议：使用SLIC（或FastSLIC）快速生成感知上有意义的原子区域。
  - 掩码生成：像素级重要性预测器输出每个像素的logit，然后聚合到区域内得到区域选择概率。
  - 二元掩码：使用Gumbel-Softmax实现可微分采样，确保掩码为二进制。
  - 部分关系建模：引入对数正态分布（LogitNormal），通过可学习的区域嵌入（3维）计算协方差矩阵，捕捉区域间关系，并确保正定性。
  - 动态阈值：训练时随机采样阈值τ ~ U[0.05,1]，并作为输入提供给模型。推理时逐步增加τ直到分类器置信度达到设定阈值δ，实现自适应稀疏度。
- **损失函数**：`-log p(y|x_m) - λ1 * 1[¯p > τ] * log(1-¯p) + λ2 * ||Σ||_1`。第一项为分类损失；第二项为稀疏正则化，仅在平均激活像素比例超过τ时生效；第三项为协方差L1正则化防止过拟合。

### 3. 实验设计
- **数据集**：自然图像数据集CIFAR-10（10类）、ImageNet（1000类）、ImageNet-9（9类，有对象分割）、COCO-10（从MS COCO选取10类，每个类1000训练100测试，有对象分割），以及半合成数据集BAM Object和BAM Scene。
- **基准方法**：黑盒模型（Blackbox）、Blackbox Pixel（均匀像素掩码）、COMET（连续值掩码）、DiET、RB-AEM、REAL-X、B-cos（内在可解释模型）。此外还对比了COMET的反转版本COMET⁻¹以及InfoMask。
- **评估指标**：
  - **性能**：测试准确率（因为数据集类平衡）。
  - **定位**：掩码与真实对象分割的重叠率（|m∩m⋆|/|m|）。
  - **忠实度**：插入和删除忠实度（以原预测为基准），评估掩码重要像素与模型预测的一致性。

### 4. 资源与算力
- 论文未明确说明使用的GPU型号、数量和具体训练时长。仅提及使用预训练的LR-ASPP MobileNetV3作为选择器，预训练ViT-Tiny作为分类器，训练20个epoch（ImageNet）或100个epoch（其他数据集），batch size 64，使用Adam优化器。未提及硬件资源。

### 5. 实验数量与充分性
- **实验数量**：在5个主流数据集（CIFAR-10、ImageNet、ImageNet-9、COCO-10、BAM）上进行全面评估；每个实验重复10个随机种子，报告均值和标准差；进行了消融研究（固定阈值、不同超像素算法、不同置信度阈值δ、与InfoMask对比等）。提供了丰富的可视化结果（随机选取的掩码图像、嵌入可视化）。
- **充分性**：实验设计较充分，涵盖了性能、定位、忠实度三个维度的评估，并与多个先进方法对比。消融实验探究了动态阈值、超像素算法选择、置信度参数的影响。但缺少在高维医学影像或复杂场景（如病理WSI）上的实验，且未详细报告训练时间成本。

### 6. 主要结论与发现
- P2P在保持与黑盒模型相近预测性能的同时，能够生成高度稀疏且语义有意义的掩码，定位对象准确率显著优于基线（例如在COCO-10上定位47% vs COMET 36%）。
- 动态阈值机制使模型根据实例难度自适应调整稀疏度，在准确率和可解释性间取得更好平衡。
- 忠实度实验（插入/删除曲线）表明P2P的预测确实依赖于所选区域，而COMET等连续掩码方法在反转掩码后性能不变，说明其掩码不忠实。
- 像素级均匀掩码（Blackbox Pixel）仍能保持高准确率，证明像素级特征选择问题设置本身存在缺陷，而区域级稀疏化更有效。

### 7. 优点
- **创新性**：首次将特征选择引入超像素（语义区域）空间，并建模区域间关系，更符合人类感知。
- **动态稀疏度**：实例自适应的稀疏度选择，比固定超参数更灵活实用。
- **忠实性**：通过插入/删除实验证明解释忠实于模型决策，优于现有方法。
- **可视化清晰**：生成的掩码直接显示模型关注的语义区域，易于人类理解。
- **实验严谨**：多数据集、多指标、重复种子、消融实验齐全。

### 8. 不足与局限
- **计算开销**：需额外运行超像素算法和预测协方差矩阵，可能增加推理时间；未报告具体时间开销。
- **区域质量依赖**：掩码效果高度依赖初始超像素分割的质量，算法选择（SLIC vs Watershed）影响结果（尽管消融显示差异不大）。
- **应用限制**：在图像中对象区域边界不清晰或存在大量噪声时，超像素可能无法正确分离语义单元，影响可解释性。
- **缺少医学或病理应用验证**：论文未在医学图像（如病理切片）上实验，而这类场景通常需高可解释性。
- **动态阈值推理过程**：逐步增加阈值直到满足置信度，可能引入额外计算，且需设定δ（默认0.8~0.99），敏感度消融显示准确率随δ变化。
- **协方差解释性有限**：3维嵌入虽可直接可视化，但颜色含义不固定，难以定量评估区域关系的正确性。

（完）
