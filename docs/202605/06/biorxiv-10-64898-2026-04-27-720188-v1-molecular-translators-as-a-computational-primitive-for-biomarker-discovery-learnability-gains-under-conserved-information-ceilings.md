---
title: "Molecular Translators as a Computational Primitive for Biomarker Discovery: Learnability Gains Under Conserved Information Ceilings"
title_zh: 用于生物标志物发现的计算原语——分子翻译器：在保守信息上限下的可学习性提升
authors: "Saisan, P. A., Patel, S. P."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.720188v1.full.pdf"
tags: ["query:cellrep"]
score: 7.0
evidence: "将H&E全切片图像转换为生物结构化的分子表征"
tldr: 本研究探讨病理图像向分子表征的翻译系统及其性能瓶颈，建立理论框架区分可提升的学习限制与形态信息天花板，并通过分析实验验证，提出实用工具诊断学习阶段与提高分子生物标志物发现效率。
source: biorxiv
selection_source: fresh_fetch
motivation: 论文旨在探究病理图像中生物标志物预测的性能瓶颈究竟源自方法限制还是形态信息的固有天花板。
method: 作者构建了形式化框架分析确定性分子翻译的能力与限制，并通过受控实验验证理论推论。
result: 研究发现分子翻译保持形态信息上限，但可提高有限样本下的可学习性，并给出了区分这两种学习状态的可检验特征。
conclusion: 研究最终建立了一个理论与工具体系，用于区分和诊断可移除方法瓶颈与不可突破信息上限，从而指导病理分子翻译系统优化。
---

## 摘要
虚拟分子映射系统（如 MISO 和 GigaTIME）在计算病理学中引入了一种潜在具有变革性的基本单元：基于配对队列学习，将 H&E 全切片图像翻译为具有生物学结构的分子表示，并在推理阶段作为映射使用。尽管机器学习取得了持续进展，H&E 到分子生物标志物（例如基因突变）的预测仍呈现领域层面的性能瓶颈，其成因尚未得到很好解释。尚不清楚持续优化所针对的问题是可移除的算法局限，还是由形态学所施加的固有上限。我们建立了一个形式化框架，用于刻画确定性译码器可以和不能改变的内容。基于组织学的生物标志物建模受到两类约束的支配：方法受限的差距（有限标签、弱监督、结构化干扰）和模态受限的上限（形态学中与切片特定信息相关的固有上限）。由于确定性翻译在推理过程中不会引入新的切片层级测量，H&E 信息上限被保留；然而，翻译仍可改善有限样本的可学习性，由此产生一个表面上的信息—性能悖论，我们将其形式化为在保守信息上限下的可学习性提升。我们推导出可验证的特征以区分这些机制，并在与代表性系统（包括 MISO 和 GigaTIME）相关的受控分析实验中刻画它们。我们还引入了一个开源工具包，包含学习机制诊断、信息上限估计、阶段分析、保真度扰动测试和快捷混淆压力测试，作为一种操作框架，用于在翻译器辅助的分子生物标志物发现和计算病理学中识别并克服可移除的性能瓶颈。

## Abstract
Virtual molecular mapping systems such as MISO and GigaTIME introduce a potentially transformative primitive in computational pathology: translation of H&E whole-slide images into biologically structured molecular representations, learned on paired cohorts and deployed as an inference-time map. Despite sustained progress in machine learning, H&E-to-molecular-biomarker (e.g., gene mutation) prediction continues to exhibit recurrent field-level performance plateaus whose drivers remain poorly resolved. It remains unclear whether continued optimization targets a removable methodological limitation or instead presses against an intrinsic ceiling imposed by morphology. We develop a formal framework characterizing what deterministic translators can and cannot change. Histology-based biomarker modeling is governed by two constraints: method-limited gaps (finite labels, weak supervision, structured nuisance) and modality-limited ceilings (intrinsic slide-specific information in morphology). Because deterministic translation introduces no new slide-level measurements at inference, H&E information ceilings are conserved; however, translation can still improve finite-sample learnability, yielding an apparent information-performance paradox that we formalize as learnability gains under conserved information ceilings. We derive falsifiable signatures distinguishing these regimes and characterize them in controlled analytical experiments anchored to representative systems, including MISO and GigaTIME. We introduce an open-source toolkit comprising learning regime diagnosis, information-ceiling estimations, phase analyses, fidelity perturbation tests, and shortcut-confounding stress tests as an operational rubric for identifying and overcoming removable performance plateaus in translator-assisted molecular biomarker discovery and computational pathology.