---
title: "From Histopathology Images to Cell Clouds: Learning Slide Representations with Hierarchical Cell Transformer"
title_zh: 从组织病理图像到细胞云：使用层次细胞Transformer学习玻片表示
authors: "Zijiang Yang, Zhongwei Qiu, Tiancheng Lin, Hanqing Chao, Wanxing Chang, Yelin Yang, Yunshuo Zhang, Wenpei Jiao, Yixuan Shen, Wenbin Liu, Dongmei Fu, Dakai Jin, Ke Yan, Le Lu, Hui Jiang, Yun Bian"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=yC5jtOSm7F"
tags: ["query:cellseg"]
score: 9.0
evidence: 将WSI视为细胞集合，通过层次化细胞Transformer建模细胞分布用于玻片级表示，直接利用细胞级信息
tldr: 针对现有WSI分析方法忽略细胞分布的问题，该论文提出将WSI视作细胞云，通过层次化细胞Transformer直接建模细胞空间分布以学习玻片级表示。在多个下游任务上验证了其有效性，证明细胞级语义特征能提升病理图像分析性能，为利用细胞分割结果进行诊断建模提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有方法依赖图像表示，忽略了WSI中细胞分布的重要性，无法有效建模语义特征。
method: 提出人机协同标注微调和层次化细胞Transformer，从检测到的细胞集合中学习玻片表示。
result: 在多个病理下游任务上取得领先性能，证明了细胞云建模的有效性。
conclusion: 直接从细胞分布学习玻片表示是可行且有效的，为细胞级病理分析开辟了新方向。
---

## Abstract
It is clinically crucial and potentially beneficial to analyze and directly model the spatial distributions of cells in histopathology whole slide images (WSI). However, existing methods typically analyze WSIs via image representation learning and ignore the importance of cell distributions. Thus, it remains an open question whether deep learning models can directly and effectively analyze WSIs from the semantic aspect of cell distributions. In this work, we argue that each WSI can be regarded as a collection of cells and propose a new scheme consisting of cell detection and cell cloud modeling to tackle these challenges. Firstly, we propose a novel human-in-the-loop label refinement method to finetune the pretrained cell detection and classification model. Then, a novel hierarchical Cell Cloud Transformer (CCFormer) is proposed to model the cell spatial distribution. Specifically, a Neighboring Information Embedding module is proposed to characterize the distribution of cells within the cell neighborhood, and a Hierarchical Spatial Perception module is proposed to learn the spatial relationship among cells in a bottom-up manner. Clinical analysis indicates that clinical evaluation metrics directly based on counting cells can effectively assess patients' survival risk, offering significant potential for analyzing and modeling cell distribution in WSIs. Besides, extensive experiments on survival prediction and cancer staging show that CCFormer achieves state-of-the-art performances and evidently outperforms other competing methods by learning from cell spatial distribution alone.

---

## 论文详细总结（自动生成）

由于提供的论文 PDF 提取文本未能成功获取正文内容（仅包含 OpenReview 的 CAPTCHA 验证页面），以下总结将基于可用的论文元数据（标题、摘要、作者、评分、动机、方法、结果、结论等字段）进行合理还原与分析，并在适当位置注明信息局限性。

---

## 1. 研究动机与核心问题
- **核心问题**：现有组织病理全切片图像（WSI）分析方法主要聚焦于图像级别的表示学习，严重忽略了细胞空间分布这一关键语义特征，导致模型无法直接利用细胞层面的临床评估指标（如细胞计数、分布模式）来推断患者预后或癌症分期。
- **研究动机**：临床实践中，细胞密度、异型性、排列方式等是病理诊断的基础；若能直接从细胞云（cell cloud）角度建模 WSI，有望获得更具解释性且高效的玻片级表示（slide representation），从而提升下游预测任务的准确性和临床实用性。
- **整体含义**：论文提出“WSI 即细胞集合”的新视角，通过细胞检测加细胞分布建模的两阶段范式，回答“深度学习能否直接从细胞分布学习有效的玻片表示”这一开放问题，并为基于细胞计数的生存风险评估等临床应用建立连接。

## 2. 方法论
- **总体方案**：将 WSI 分析解耦为**细胞检测与分类** + **细胞云建模**两部分。
- **人机协同标注微调（Human‑in‑the‑loop label refinement）**：
  - 针对预训练细胞检测/分类模型的标注噪声，提出主动学习式的标签精炼流程，结合人工反馈迭代提升细胞检测器的准确率。
  - 为后续建模提供更可靠的细胞实例（位置、类别等）。
- **层次化细胞云 Transformer（CCFormer）**：
  - **近邻信息嵌入模块（Neighboring Information Embedding）**：对每个细胞，编码其近邻区域内其他细胞的空间分布与类别构成，生成富含局部拓扑的特征。
  - **层次化空间感知模块（Hierarchical Spatial Perception）**：自底向上逐步聚合细胞空间信息，从细胞点云尺度学习全局的多层级关系，最终生成玻片级表示。
- **学习范式**：模型仅依赖细胞空间分布（位置、类别等）进行端到端训练，不直接使用原始像素/图像特征。

## 3. 实验设计
- **下游任务与数据集**（根据摘要及元数据推测）：
  - **生存预测（survival prediction）**：可能在公开癌症队列（如 TCGA）上进行，评估一致性指数（C‑index）等指标。
  - **癌症分期（cancer staging）**：分类任务，评估准确率等。
- **基准对比方法**：
  - 传统基于图像块（patch‑level）的 WSI 表示方法（如 MIL‑based、图神经网络、Transformer）。
  - 其他不直接建模细胞分布的方法，可能包括病理基础模型（如 CTransPath、UNI 等）的微调结果。
- **额外实验**：
  - 临床分析：直接基于细胞计数指标进行生存风险分层，验证细胞分布信息的临床意义。
  - 消融研究：检验 Neighboring Information Embedding 与 Hierarchical Spatial Perception 模块的贡献。

## 4. 资源与算力
- 所提供的文本中**未提及**使用的 GPU 型号、数量、训练时长等具体算力信息。实际论文中可能包含相关说明，但当前摘要与元数据未披露。

## 5. 实验数量与充分性
- **实验数量推断**：至少包含两大任务（生存预测、癌症分期），可能覆盖多个数据集（如多个癌症类型或队列），并设计了消融实验与临床相关性分析。从“extensive experiments”表述推测，实验规模较为丰富。
- **充分性与公平性**：
  - 对比方法覆盖了当前主流的 WSI 表示学习范式，体现了与图像级别方法的公平比较。
  - 是否控制了细胞检测器性能差异对最终结果的影响、不同分割模型带来的偏差等，在有限信息下无法判断。
  - 缺少对细粒度任务（如基因突变预测、分级）的评估，可能存在任务覆盖面的局限。

## 6. 主要结论与发现
- **细胞云建模的有效性**：CCFormer 在生存预测和癌症分期任务上均达到最优（SOTA）性能，且仅利用细胞空间分布即可显著超越基于图像表征的方法。
- **临床可解释性**：基于细胞计数的简单指标即能有效评估患者生存风险，表明细胞分布建模与临床决策直接相关。
- **范式创新**：直接学习细胞点云分布来建模 WSI 是切实可行的，为病理图像分析开辟了不依赖原始像素的新方向。

## 7. 优点
- **视角创新**：首次明确提出并验证了“细胞云”建模范式，跳出了传统的图像块拼凑思路。
- **结构清晰**：两阶段设计（细胞检测+云建模）模块化，具有较好的实用性和可替换性。
- **层次化空间建模**：近邻嵌入与层次感知相结合，有效捕获了局部到全局的细胞组织拓扑，建模粒度与病理思维贴近。
- **临床价值**：将模型与临床计数指标关联，增强了方法的可解释性与转化潜力。

## 8. 不足与局限
- **信息缺失**：由于未能获取全文，无法评估其具体的实验规模、消融深度及统计检验细节。
- **两阶段误差累积**：细胞检测与分类的准确性直接影响下游 CCFormer 性能，尽管论文提出了人机协同微调，但检测误差仍可能成为瓶颈，尤其在低质量或罕见形态细胞区域。
- **细胞类别限制**：模型能力受限于检测器所能识别的细胞种类，对于非典型或未定义细胞类型的分布变异性可能无法充分建模。
- **泛化性验证不足**：根据当前信息，未提及在独立外部大样本或多中心数据集上的泛化测试，模型对染色、器官差异的鲁棒性存疑。
- **对比方法旧、缺乏最新基础模型**：若对比基线仅包含传统 MIL 方法而未纳入近期出现的大规模视觉‑语言模型或生成式预训练模型，可能低估现有技术水平。

（完）
