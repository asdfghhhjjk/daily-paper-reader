---
title: "SMILE: A Scale-aware Multiple Instance Learning Method for Multicenter STAS  Lung Cancer Histopathology Diagnosis"
title_zh: SMILE：一种用于多中心STAS肺癌组织病理诊断的尺度感知多实例学习方法
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/1093.pdf"
tags: ["query:profile"]
score: 7.0
evidence: 用于多中心STAS肺癌组织病理诊断的尺度感知MIL方法
tldr: SMILE通过尺度感知的多实例学习方法，针对多中心STAS肺癌组织病理诊断，解决WSI中肿瘤气腔播散的识别问题。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-1093/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1765, \"height\": 793, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-1093/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 822, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-1093/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1725, \"height\": 697, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-1093/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 889, \"height\": 710, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-1093/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1841, \"height\": 439, \"label\": \"Table\"}]"
motivation: 多中心组织病理WSI诊断需要处理尺度变化和跨中心泛化。
method: 提出SMILE，一种尺度感知的MIL方法，用于肺癌STAS诊断。
result: （无摘要）预期在多中心数据上提升诊断性能。
conclusion: SMILE为肺癌组织病理学中的尺度感知WSI分析提供了新方案。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
*   **研究动机**：肺癌中的气腔播散（STAS）是一种新定义的侵袭模式，与较差的预后、高复发风险以及手术方式选择（肺叶切除 vs. 亚肺叶切除）密切相关。
*   **核心挑战**：
    *   **诊断困难**：STAS 病灶稀疏、形态异质性强（单细胞、微乳头簇、实心巢），传统人工评估主观性高、费时费力，且准确率有限（约74%，AUC 0.67）。
    *   **数据缺失**：缺乏公开、高质量、多中心标注的 STAS 病理数据集，阻碍了计算病理学在该方向的研究。
*   **整体目标**：构建并公开多中心 STAS 组织病理数据集，同时提出一种能自适应捕捉稀疏和异质性病灶的自动化诊断方法，提升 STAS 的识别精度与客观性。

### 2. 论文提出的方法论
*   **整体框架**：提出 SMILE（Scale-aware Multiple Instance Learning），一种用于全切片图像（WSI）分类的尺度感知多实例学习方法。
*   **关键技术细节**：
    *   **特征提取**：采用双阶段策略。离线阶段使用预训练的 CTransPath（CNN+Transformer）提取 patch 级特征；在线阶段通过 BatchNorm、Linear、ReLU 层对特征进行微调。
    *   **尺度自适应注意力机制**：核心创新点。在常规注意力计算后，对注意力分数进行 Max-Min 归一化，设定阈值。超过阈值的实例被视为“高注意力实例”，其原始注意力分数会按一个缩放因子（Factor）进行缩小，从而抑制模型对少数显著区域的过度依赖，促使模型更均匀地关注稀疏的 STAS 病灶特征。
    *   **包级聚合与预测**：利用缩放后的注意力权重对实例特征进行加权求和，得到全局表示，再通过线性层和 Sigmoid 函数进行二分类预测。
*   **损失函数**：采用标准的二元交叉熵损失进行优化。

### 3. 实验设计
*   **数据集**：本工作首次构建并公开了三个多中心 STAS 数据集，总计 2,970 张 WSI：
    *   **STAS-CSU**：来自中南大学湘雅二医院，包含 356 例患者的 1,290 张冰冻和石蜡切片（206 STAS vs. 150 非 STAS）。
    *   **STAS-TCGA**：基于 TCGA 项目，经病理学家重新标注，最终纳入 424 张石蜡切片（155 STAS vs. 269 非 STAS）。
    *   **STAS-CPTAC**：基于 CPTAC 项目，重新标注后纳入 495 张石蜡切片（304 STAS vs. 191 非 STAS）。
*   **基准方法**：与 11 种主流或先进的 MIL 方法进行了全面对比，包括 Maxpooling、Meanpooling、ABMIL、TransMIL、CLAM-SB、CLAM-MB、DTFD-MIL、ACMIL、ILRA、DGRMIL 等。
*   **评估设置**：采用五折交叉验证，以 AUC、准确率（ACC）、Precision、Recall 和 F1-Score 作为评估指标，取平均值报告结果。

### 4. 资源与算力
*   文中明确提及了训练所使用的算力：
    *   **GPU**：2 块 NVIDIA RTX 4090。
    *   **框架与配置**：基于 PyTorch 实现，使用 Ranger 优化器，学习率 2e-4，权重衰减 1e-5，训练 100 个 epoch，批次大小设为 12。

### 5. 实验数量与充分性
*   **实验组数**：
    *   **主实验**：在三个数据集上，对提出的 SMILE 与 11 个基线模型进行了性能比较（合计 36 组模型-数据集组合的核心指标）。
    *   **消融实验**：针对尺度自适应机制中的两个关键超参数（阈值和缩放因子），在 STAS-TCGA 和 STAS-CPTAC 上进行了多组设置下的性能对比（表格展示了 18 种不同组合）。
*   **充分性与公平性**：实验设计相对充分。使用了多中心独立数据集进行外部验证，对比方法具有代表性且覆盖了主流 MIL 范式，消融实验验证了核心模块的有效性，所有评估均遵循统一的交叉验证流程，确保了比较的公平性。

### 6. 论文的主要结论与发现
*   **性能优势**：SMILE 在 STAS-CPTAC 数据集上取得了最佳的准确率（0.645）和 AUC（0.6517），并在其他数据集上展现了有竞争力的结果，证明了方法的有效性。
*   **机制有效性**：尺度自适应注意力机制通过抑制对少数高显著性区域的过度聚焦，能更均衡地捕捉稀疏、异质的 STAS 病灶，从而提升诊断性能。
*   **参数敏感性**：阈值和缩放因子的选择对模型性能有显著影响，不同数据集可能需要不同的参数组合以达到最优，表明该方法具有一定灵活性。

### 7. 优点
*   **数据贡献**：首次构建并承诺公开三个高质量、经病理学家交叉诊断的多中心 STAS 数据集，为该领域研究提供了重要的数据基础。
*   **方法创新**：提出的尺度自适应注意力机制，简洁而有效地解决了传统 MIL 在处理稀疏、小目标病灶时可能出现的“注意力崩塌”问题。
*   **基准全面**：提供了 11 种方法的全面基准测试结果，为后续 STAS 诊断算法的开发提供了清晰的比较参考。
*   **临床应用潜力**：该方法设计针对真实的临床诊断痛点，有望推动计算病理学在 STAS 诊断中的临床整合。

### 8. 不足与局限
*   **跨中心泛化性**：模型在 STAS-CSU 数据集上的性能相对较低，表明在跨不同医院来源和制片流程的数据上，泛化能力仍有提升空间，可能需要引入域适应等技术。
*   **可解释性尚待加强**：虽然注意力热图能提供一定指示，但与病理学家精确的像素级标注之间仍存在鸿沟，在复杂形态的精准定位和解释上仍有不足。
*   **数据模态单一**：当前研究仅基于 H&E 染色图像，未融合可能对 STAS 诊断有益的临床数据（如 TNM 分期）或多组学数据。
*   **样本量限制**：尽管是首个此类规模的数据集，但每个子数据集的样本量（特别是 STAS-CSU）对于训练稳健的深度学习模型仍相对有限，可能影响微小灶性病变的识别能力。

（完）
