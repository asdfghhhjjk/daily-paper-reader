---
title: A Hierarchical Spatial Graph Neural Network Resolves Immunogenic and Tolerogenic Tertiary Lymphoid Structures in Renal Cell Carcinoma
title_zh: 分层空间图神经网络解析肾细胞癌中免疫原性与耐受性三级淋巴结构
authors: "Peng, G."
date: 2026-04-22
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.07.717084v3.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 用于空间转录组集群分类的分层图神经网络
tldr: 本研究针对肾细胞癌中的三级淋巴结构（TLS）提出一种分层空间图神经网络，用于区分免疫性与耐受性TLS状态。模型通过在10x Visium空间转录组数据上构建三层结构融合GAT与DiffPool机制，实现从局部到区域的信号聚合与功能预测，显著提高了TLS功能识别的准确性并具备跨癌种泛化能力。
source: biorxiv
selection_source: fresh_fetch
motivation: 肾癌的肿瘤微环境中存在免疫促进或免疫抑制的三级淋巴结构（TLS），区分它们对预测免疫治疗反应至关重要。
method: 作者设计了结合图注意力和可微池化的三级层次空间GNN，在空间转录组数据上训练用于TLS功能分类。
result: 模型在RCC样本上验证AUC为0.718，在临床验证样本上为0.908，并能跨癌种准确识别肝癌中较强的耐受性TLS。
conclusion: 分层空间GNN能可靠识别TLS功能状态，为理解肿瘤免疫微环境及临床预测提供新工具。
---

## 摘要
肿瘤微环境中的三级淋巴结构（TLS）具有从免疫原性——驱动生发中心反应和抗肿瘤免疫——到耐受性、富含调节性T细胞和抑制性髓系细胞群的功能谱。区分这些状态具有临床关键意义：免疫原性TLS能够预测免疫检查点抑制剂（ICI）的应答，而耐受性TLS可能促进免疫逃逸。常规的群体转录组分析将活跃的TLS与耗竭的免疫浸润混为一谈，从而掩盖了这种差异。我们提出了一种分层图神经网络（GNN），直接作用于10x Visium空间转录组图上，以在聚类层面分类TLS的功能状态。该模型采用三层级架构结合图注意力机制（GAT）与可微分池化（DiffPool），在预测免疫原性或耐受性状态之前，分层聚合点位级信号形成生态位与区域级表征。模型在24例肾细胞癌（RCC）Visium样本（GSE175540）中的915个TLS聚类上训练，验证集AUC-ROC达到0.718，在BIONIKK队列IgG验证样本上的临床AUC为0.908。在独立多癌种Visium队列（GSE203612；包括乳腺、肝脏、卵巢、胰腺、子宫）上的零样本迁移测试中，模型准确识别肝细胞癌中最具耐受性TLS，这与肝癌微环境的免疫抑制特征一致。对TLS与非TLS区域的CXCL13空间分解显示，85%的组织CXCL13信号来源于非TLS实质区，在该区域中CXCL13主要与耗竭标志物共表达（平均Spearman相关系数ρ = 0.233），而与Tfh标志物（CXCR5相关系数ρ = 0.039）共表达较弱——这一模式与在TCGA-KIRC队列中群体CXCL13与总体生存率下降的悖论性关联一致（HR = 1.38，p < 0.001）。代码与处理后的数据已存储于GitHub和Zenodo。

## Abstract
Tertiary lymphoid structures (TLS) in the tumour microenvironment span a functional spectrum from immunogenic -- driving germinal centre reactions and anti-tumour immunity -- to tolerogenic, harbouring regulatory T cells and suppressive myeloid populations. Distinguishing these states is clinically critical: immunogenic TLS predict ICI response whereas tolerogenic TLS may promote immune evasion. Bulk transcriptomics conflates productive TLS with exhausted immune infiltrates, masking this distinction. We present a hierarchical graph neural network (GNN) that operates directly on 10x Visium spatial transcriptomics graphs to classify TLS functional state at the cluster level. Using a three-scale architecture combining graph attention (GAT) and differentiable pooling (DiffPool), the model hierarchically aggregates spot-level signals into niche- and region-level representations before predicting immunogenic versus tolerogenic state. Trained on 915 TLS clusters from 24 renal cell carcinoma (RCC) Visium samples (GSE175540), the model achieves a validation AUC-ROC of 0.718 and a clinical AUC of 0.908 on IgG-validated samples from the BIONIKK cohort. Zero-shot transfer to an independent multi-cancer Visium cohort (GSE203612; breast, liver, ovarian, pancreatic, uterine) correctly identifies hepatocellular carcinoma as harbouring the most tolerogenic TLS, consistent with the known immunosuppressive liver tumour microenvironment. Spatial decomposition of CXCL13 across TLS and non-TLS compartments reveals that 85% of tissue CXCL13 signal originates from non-TLS parenchyma, where it co-expresses primarily with exhaustion markers (mean Spearman rho = 0.233) rather than Tfh markers (CXCR5 rho = 0.039) -- a pattern consistent with the paradoxical association of bulk CXCL13 with worse overall survival in TCGA-KIRC (HR = 1.38, p < 0.001). Code and processed data are deposited at GitHub and Zenodo.