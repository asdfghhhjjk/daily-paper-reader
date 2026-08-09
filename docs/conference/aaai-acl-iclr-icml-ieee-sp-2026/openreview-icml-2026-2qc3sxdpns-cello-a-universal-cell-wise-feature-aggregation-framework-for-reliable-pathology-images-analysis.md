---
title: "Cello: A Universal Cell-wise Feature Aggregation framework for  Reliable  Pathology Images Analysis"
title_zh: "Cello: 一种用于可靠病理图像分析的通用细胞级特征聚合框架"
authors: "Hengrui Lou, Weihan Li, Jiazhen Yang, Lingxiang Jia, Shengxuming Zhang, Linyun Zhou, Xiuming Zhang, Zhenyang Wang, Mingli Song, Zunlei Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0fac7f88f69a8fee60081cbee4e3d07d13b48f75.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 通用细胞级特征聚合用于可靠病理分析
tldr: 现有计算病理学依赖斑块级特征，与病理学家以细胞为中心的推理存在差距。Cello提出通用细胞级特征聚合框架，通过蛋白质信号监督的细胞学习整合细胞表征，在千兆像素限制下保留细微线索，为局部与全局任务提供可信证据，增强对微小病变的敏感性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 当前WSI分析依赖斑块级特征，偏离病理学家的细胞推理，对微病变不敏感。
method: 提出Cello框架，通过蛋白质信号监督的细胞学习实现细胞级特征聚合。
result: （摘要截断）预期提升WSI分析的可靠性与敏感性。
conclusion: 该方法为计算病理学提供了更贴近临床推理的解决方案。
---

## Abstract
Computational pathology has made progress in diagnosis and prognosis prediction from whole slide images (WSIs), yet pipelines still rely on patch-level feature extraction and aggregation, departing from the cell-centric reasoning used by pathologists.
This gap limits sensitivity to micro-lesions and subtle changes, and current methods rarely provide a unified solution that supports both local and global tasks with trustworthy evidence. We propose Cello, a universal cell-wise feature aggregation framework for reliable pathology image analysis. Cello integrates cell-level representations into WSI modeling via protein-signal–supervised cell-wise learning, preserving fine-grained cellular cues under gigapixel constraints. For local tasks, Cello introduces a flexible prototype-based contrastive module for scalable, task-adaptive representation learning. For global tasks, Cello adopts a weakly supervised gated aggregation that can widely leverage WSI labels. Finally, a cell–local–global decision-route consistency objective dynamically aggregates cellular evidence and aligns local predictions with global outcomes, improving reliability and faithfulness. 
Trained with only hundreds to thousands of samples, Cello achieves performance gains of 3.0%~7.6% and outperforms SOTA pathology foundation models pretrained on tens of thousands of samples. Code is available at https://github.com/HengruiLou/Cello.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：当前计算病理学（Computational Pathology）主要依赖从全切片图像（WSIs）中提取**斑块级（patch‑level）特征**并进行聚合，这严重偏离了病理学家以**细胞为中心（cell‑centric）**的推理方式。这种 gap 导致模型对微小病灶和细微组织变化不够敏感。
- **缺口**：现有方法很少提供能够同时支持**局部任务**（如细胞识别、微小区域分析）和**全局任务**（如整图诊断、预后预测）的统一方案，且缺乏可信任的决策证据。
- **整体含义**：Cello 旨在通过构建一个**通用细胞级特征聚合框架**，将病理分析拉回到更贴近人类专家的细胞推理范式，从而在千兆像素规模的 WSI 上保留细粒度线索，并增强诊断的可靠性与忠实度。

## 2. 方法论：核心思想与关键技术细节
Cello 的整体设计围绕 **“细胞级特征聚合 + 多尺度决策一致性”** 展开，主要包含三个模块：
- **细胞级表征学习（Cell‑wise Learning）**  
  利用**蛋白质信号监督**训练细胞级表征，将单个细胞的信息融入 WSI 建模，在千兆像素约束下依然能保留精细的细胞线索。
- **局部任务模块（Local Tasks）**  
  引入一种**灵活的基于原型的对比学习模块**。该模块可拓展、任务自适应，能够为不同类型的局部任务提供可伸缩的表征。
- **全局任务模块（Global Tasks）**  
  采用**弱监督门控聚合（weakly supervised gated aggregation）**，可广泛利用 WSI 级别标签进行学习，不依赖密集标注。
- **决策一致性目标（Cell–Local–Global Decision‑Route Consistency）**  
  动态聚合细胞证据，并强制**局部预测与全局输出对齐**。这一“细胞‑局部‑全局”路由一致性损失使模型在推理时更可靠，证据更忠实于数据。

## 3. 实验设计：数据集、基准与对比方法
- **训练规模**：据摘要说明，Cello 仅使用 **数百到数千个样本**进行训练。
- **性能提升**：相比基线，Cello 取得了 **3.0%~7.6% 的性能增益**。
- **对比对象**：与在**上万样本**上预训练的最先进病理基础模型（SOTA pathology foundation models）对比，Cello 仍具有优势。
- **局限性说明**：论文摘要及提供的元数据中**未列出具体数据集名称、具体 benchmark 任务、对比方法的具体名称**（如 CTransPath、CONCH、HIPT 等），因此此处无法给出详细清单。

## 4. 资源与算力
- 文中的摘要与元数据**未提及任何 GPU 型号、数量、训练时长或显存消耗**等信息。关于计算资源的需求，目前无法从提供的内容中获取。

## 5. 实验数量与充分性
- 从现有片段看，摘要仅高度概括了“数百到数千样本”和“3.0%~7.6% 增益”，**未能展示实验的具体组数、消融研究、多数据集跨任务验证等细节**。因此，无法从当前信息判断实验设计是否充分、客观或公平。

## 6. 主要结论与发现
- Cello 成功构建了一个**通用、可扩展的细胞级特征聚合框架**，在少量训练样本的条件下即可获得显著提升。
- 该方法能够为局部与全局任务提供**可信的统一解决方案**，其性能甚至超过那些在更大规模数据上预训练的病理基础模型。
- 通过强制细胞‑局部‑全局决策一致性，模型不仅提高了准确率，还增强了预测的**可解释性和事实一致性**。

## 7. 优点（方法或实验设计的亮点）
- **以细胞为中心**：从特征提取到决策链路均模仿病理学家的推理过程，更贴近临床认知。
- **多任务统一**：同一框架同时支持局部和全局任务，无需为不同场景单独设计流程。
- **监督信号创新**：用蛋白质信号监督细胞学习，比单纯依赖形态学更富含生物学先验。
- **数据效率高**：只需数百至数千样本即可超越大规模预训练模型，有效降低了对稀有病理数据的依赖。
- **可靠性增强**：“决策路由一致性”机制使局部和全局预测相互印证，提供可信证据。

## 8. 不足与局限
- **细节缺失严重**：由于原论文内容在此处仅以摘要和元数据形式出现，无法评估其具体实验设置、数据分布、对比公平性、敏感度分析等。
- **未知的技术限制**：细胞级学习很可能依赖**细胞分割或检测的精度**，如果前序步骤在复杂组织上存在误差，可能影响框架稳定性；但摘要未讨论该风险。
- **应用范围待验证**：文中未提及该框架在罕见肿瘤、细胞密集区或跨染色平台上的泛化能力。
- **算力需求不透明**：缺乏计算资源信息，使用者难以预估部署成本。

（完）
