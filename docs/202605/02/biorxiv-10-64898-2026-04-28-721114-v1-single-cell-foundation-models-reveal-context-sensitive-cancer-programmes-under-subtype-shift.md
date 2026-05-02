---
title: Single-cell foundation models reveal context-sensitive cancer programmes under subtype shift
authors: "Wallace, J., Youssef, G., Han, N."
date: 2026-05-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721114v1.full.pdf"
tags: ["query:cellrep"]
score: 7.0
evidence: 用于癌症亚型识别的单细胞基础模型
tldr: 评估了单细胞基础模型在癌症亚型分类和域外泛化中的表现。
source: biorxiv
selection_source: fresh_fetch
motivation: 用于癌症亚型识别的单细胞基础模型。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Single-cell foundation models (scFMs) have shown promise as transferable representations of cellular state, but recent zero-shot evaluations suggest that they do not consistently outperform simpler baselines. We asked whether this apparent limitation reflects an intrinsic weakness of scFMs or instead the difficulty of using them without task-specific adaptation. To test this, we fine-tuned two widely used scFMs, Geneformer and scGPT, on common tumour subtypes from renal, lung, and breast cancer, and compared them with a LightGBM baseline on within-domain validation cohorts and on out-of-domain rarer, unseen cancer subtypes. Across all three organs, the models achieved near-perfect within-domain discrimination (AUROC 0.98-1.00), but differences emerged under subtype shift. On chromophobe RCC, scGPT and Geneformer achieved AUROC 0.88 and 0.92 respectively versus 0.64 for LightGBM; on SCLC, Geneformer reached 1.00 versus 0.82 for LightGBM; and on TNBC, scGPT achieved 0.80 versus 0.49 for LightGBM. To determine whether this generalisation reflected meaningful adaptation rather than arbitrary feature drift, we applied Integrated Gradients, an interpretability technique, to the fine-tuned scFMs and SHAP to LightGBM. LightGBM showed highly stable gene-importance rankings across datasets, whereas the foundation models were substantially more context-sensitive. However, this flexibility was not random: all models converged on a shared within-domain core, while scFMs acquired larger rare-subtype-specific gene sets and pathway programmes during transfer. Pathway enrichment further supported the biological relevance of these attributed genes. Together, these results suggest that fine-tuned scFMs can bridge clinically relevant domain shifts in cancer single-cell analysis and that interpretability provides a practical route to distinguishing biologically grounded adaptation from rigid reuse of training-era rules.