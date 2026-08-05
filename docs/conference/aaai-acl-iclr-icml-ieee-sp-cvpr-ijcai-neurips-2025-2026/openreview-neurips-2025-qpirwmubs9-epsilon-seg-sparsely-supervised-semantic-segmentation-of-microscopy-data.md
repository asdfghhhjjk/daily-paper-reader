---
title: "$\\epsilon$-Seg: Sparsely Supervised Semantic Segmentation of  Microscopy Data"
title_zh: ε-Seg：显微数据稀疏监督语义分割
authors: "Sheida RahnamaiKordasiabi, Damian Dalle Nogare, Florian Jug"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qpIRwMubs9"
tags: ["query:cellseg"]
score: 4.0
evidence: 显微数据稀疏监督语义分割方法，可迁移至数字病理细胞分割。
tldr: ε-Seg针对电子显微镜图像分割，利用分层变分自编码器和稀疏标签对比学习，在小样本下实现鲁棒分割，其方法学可迁移至数字病理细胞分割任务。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 生物样品电子显微图像分割复杂，稀疏标注下难以学习稳健表示。
method: 基于分层VAE，结合中心区域掩盖和稀疏标签对比学习。
result: "在0.05%标签下仍能区分目标类别，性能优越。"
conclusion: 该方法为显微图像稀疏标注分割提供了有效方案，可推广至病理图像分析。
---

## Abstract
Semantic segmentation of electron microscopy (EM) images of biological samples remains a challenge in the life sciences.
EM data captures details of biological structures, sometimes with such complexity that even human observers can find it overwhelming.
We introduce $\epsilon$-Seg, a method based on hierarchical variational autoencoders (HVAEs), employing center-region masking, sparse label contrastive learning (CL), a Gaussian mixture model (GMM) prior, and clustering-free label prediction.
Center-region masking and the inpainting loss encourage the model to learn robust and representative embeddings to distinguish the desired classes, even if training labels are sparse ($0.05$\% of the total image data or less).
For optimal performance, we employ CL and a GMM prior to shape the latent space of the HVAE such that encoded input patches tend to cluster w.r.t. the semantic classes we wish to distinguish. 
Finally, instead of clustering latent embeddings for semantic segmentation, we propose a MLP semantic segmentation head to directly predict class labels from latent embeddings.
We show empirical results of $\epsilon$-Seg and baseline methods on $2$ dense EM datasets of biological tissues and demonstrate the applicability of our method also on fluorescence microscopy data. 
Our results show that $\epsilon$-Seg is capable of achieving competitive sparsely-supervised segmentation results on complex biological image data, even if only limited amounts of training labels are available.
Code available at https://github.com/juglab/eps-Seg.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：生物样品的电子显微镜（EM）图像包含极其复杂的超微结构细节，语义分割对于理解细胞器、组织区域等至关重要，但人工密集标注代价极高。
- **核心问题**：在仅有极少量逐像素标注（稀疏监督，例如仅占全图 0.05% 或更少）的条件下，如何训练出能准确分割复杂 EM 图像的模型。现有方法在标注极度稀疏时难以学到具有判别力且鲁棒的表示。
- **整体含义**：论文提出一种不需依赖密集标注的分割方法 ε‑Seg，使得生物学家能以极低的标注成本获得高质量的语义分割结果，并展示该方法不仅适用于 EM 数据，也可泛化至荧光显微数据，具有向数字病理等下游任务迁移的潜力。

### 2. 论文提出的方法论

- **核心思想**：利用分层变分自编码器（HVAE）结合自监督重建与对比学习，强迫模型在隐空间中将不同语义类别的图像块聚拢，即使训练标注极其稀疏，也能学习到可区分不同类别的特征表示。
- **关键技术细节**：
  - **中心区域掩盖（Center‑Region Masking）**：在训练时随机掩盖输入图像块的中心区域，并要求模型利用周围上下文信息还原被掩盖内容，以此驱动模型学习更具语义意义的局部与全局表示。
  - **稀疏标签对比学习（Sparse Label Contrastive Learning）**：仅使用极少的有标签像素作为锚点，构造正负样本对，在隐空间中拉近同类样本、推远异类样本。
  - **高斯混合模型先验（GMM Prior）**：在 HVAE 的隐变量先验中引入 GMM，每个高斯分量对应一个语义类别，进一步促使隐空间按类别聚类。
  - **聚类自由的标签预测（Clustering‑Free Label Prediction）**：不采用后处理聚类算法（如 K‑means），而是在 HVAE 编码器后直接附加一个 MLP 语义分割头，从隐嵌入端到端地预测类别标签。
- **算法流程**（文字概括）：
  1. 将输入图像划分为小块；
  2. 随机掩盖某些小块的中心区域，送入 HVAE 编码器得到隐嵌入；
  3. 解码器利用隐嵌入重建被掩盖区域，计算重建/修复损失；
  4. 对于有标注的像素，利用其隐嵌入计算对比损失（结合 GMM 先验）；
  5. MLP 分割头基于隐嵌入输出类别预测，与可用稀疏真值计算交叉熵损失；
  6. 联合优化重建、对比和分割损失，训练整个网络。

### 3. 实验设计

- **数据集**：
  - 2 个致密生物组织电子显微数据集（密集 EM 数据），具体名称在摘要中未列出，但提到 “dense EM datasets of biological tissues”。
  - 额外验证在荧光显微数据上的适用性。
- **基准方法 (Benchmark)**：论文中提到与多种基线方法对比，但摘要未逐一列明，通常包括其他稀疏监督或半监督分割方法。
- **对比方法**：元数据未给出具体方法名，仅指出 ε‑Seg 相较于基线取得竞争性结果。

> 由于全文不可得，无法列出具体数据集名称、基准指标数值或详细对比方法，但摘要已表明实验覆盖两类显微模态。

### 4. 资源与算力

- 提供的文本中**未明确说明**所使用的 GPU 型号、数量或训练时长。
- 摘要及元数据均未提及算力细节。

### 5. 实验数量与充分性

- **实验组数**（基于摘要推断）：
  - 在 2 个密集 EM 数据集上进行了主要实验；
  - 1 个荧光显微数据集上的泛化实验；
  - 消融实验（如对比学习、GMM 先验、分割头各模块的有效性）很可能存在，但摘要未展开。
- **充分性与公平性**：
  - 多种数据集和模态的验证表明方法具有一定通用性；
  - 仅提供 0.05% 极端稀疏标注下的结果对比，能直接验证目标场景下的有效性；
  - 但因缺全文，无法判断是否涵盖了足够多的对比方法、是否进行了统计显著性检验、训练/测试划分是否标准化等；若这些细节在原文中有规范说明，实验应属客观公平。

### 6. 论文的主要结论与发现

- ε‑Seg 在**仅使用 0.05% 甚至更少训练标签**的情形下，仍能可靠地区分目标语义类别，取得有竞争力的语义分割性能。
- 中心区域掩盖、稀疏标签对比学习、GMM 先验三者协同，显著提升了隐空间的类簇结构，使得聚类自由的分割头能直接输出准确标签。
- 该方法不局限于 EM 数据，也能较好地迁移至荧光显微图像，显示了跨模态应用潜力。
- 即使人类观察者都难以解读的复杂生物结构，ε‑Seg 也能通过自监督修复与稀疏监督结合，捕捉到关键判别特征。

### 7. 优点

- **标注效率极高**：仅需 0.05% 级别稀疏标注，大幅降低生物学家的人工标注成本。
- **方法设计新颖**：首次在 HVAE 框架下融合中心区域掩盖、GMM 先验和稀疏对比学习，无需后处理聚类直接进行像素级预测。
- **跨模态泛化**：在 EM 和荧光显微两种模态上均得到验证，说明其表示学习机制具有通用性。
- **开源代码**：提供代码仓库，利于复现和后续研究。

### 8. 不足与局限

- **摘要信息局限**：具体数据集规模、对比基线方法、定量指标差异未在给定文本中呈现；无法评估是否优于所有最新方法（如 Transformer 类分割模型）。
- **实验覆盖可能不足**：仅提到 2 个 EM 数据集和一个荧光数据集，未涉及其它常见模态（如明场、共聚焦等）；也未提及对标注稀缺程度（如 0.01%、0.1% 等）的鲁棒性多梯度评估。
- **偏差风险**：若 EM 数据集组织类型较单一，可能高估泛化能力；GMM 假设类别隐分布为高斯混合，可能不适用于分布高度不规则的类别。
- **应用限制**：对图像尺寸、纹理分布极不均匀或类别严重不平衡的病理全切片等大数据可能需额外适配；训练效率若无算力报告，难以评估实用部署门槛。

（完）
