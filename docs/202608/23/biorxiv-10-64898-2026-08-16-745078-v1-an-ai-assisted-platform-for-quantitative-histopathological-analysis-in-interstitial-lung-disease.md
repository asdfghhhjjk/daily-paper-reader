---
title: An AI-assisted platform for quantitative histopathological analysis in interstitial lung disease
title_zh: 用于间质性肺疾病定量组织病理学分析的AI辅助平台
authors: "Mizrahi, I., Guo, Y., He, J., Livneh, I., Stein, P., Shimron, R. B., Raz, A., Abu Saleh, M., Napso Shogan, T., Matalon, N., Hershfinkel, M., Cohen, H. A., Shemesh, A., Palty, R., Dotan, Y., Wolfenson, H., Hasson, P., Odeh, A."
date: 2026-08-19
pdf: "https://www.biorxiv.org/content/10.64898/2026.08.16.745078v1.full.pdf"
tags: ["query:cell-graph"]
score: 7.0
evidence: 间质性肺病定量组织病理学分析的AI辅助平台
tldr: 间质性肺病（ILD）的纤维化评估依赖半定量评分，存在主观性和采样局限。FibroSight平台整合深度学习结构分割与颜色特征提取，实现天狼星红染色切片的全自动全叶分析。该平台在博来霉素模型中与Ashcroft评分高度相关，且优于半自动ImageJ流程，并能区分炎症与纤维化。FibroSight为ILD临床前和转化研究提供了可扩展、可重复的多腔室定量框架。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有ILD组织病理评分半定量、耗时、观察者间变异大，且采样有限，亟需客观自动化方法。
method: 开发FibroSight平台，结合深度学习结构分割和颜色特征提取，对天狼星红染色切片进行全自动全叶多参数定量。
result: 在博来霉素模型中，FibroSight指标与Ashcroft评分强相关，优于ImageJ半自动流程，并能在流感模型和人类ILD活检中区分纤维化与炎症。
conclusion: FibroSight扩展了传统纤维化评估，整合纤维化、炎症、气道和血管重塑指标，支持更精准的ILD研究和治疗反应分析。
---

## 摘要
间质性肺疾病（ILDs）是一类以慢性炎症和/或纤维化为特征的异质性肺部疾病。30%–40%的ILD患者会发展为纤维化性疾病，这与进行性呼吸功能下降和不良预后相关，尤其是在特发性肺纤维化中。目前的抗纤维化治疗可减缓疾病进展，但无法逆转纤维化，这凸显了改进治疗策略的必要性。临床前模型中可靠的组织病理学评估对于药物开发至关重要；然而，传统评分系统是半定量的、劳动密集型的、易受观察者间变异影响，且依赖于有限的视野采样。在此，我们介绍FibroSight，一个用于在天狼星红染色切片中进行肺重塑分区解析定量的独立平台。通过整合基于深度学习的结构分割与基于颜色的特征提取，FibroSight能够实现高度自动化的全叶分析，无需复杂的计算设置。该平台可量化互补的重塑参数，包括实质胶原分数、实质组织密度、核面积分数、实质气腔分数以及气道和血管相关重塑。在博来霉素诱导的纤维化模型中验证后，FibroSight衍生的指标与专家Ashcroft评分强相关，并且与组织学严重程度的关联性比基于ImageJ的半自动工作流程的相应输出更强。该平台进一步区分了流感诱导的肺损伤中的炎症性与纤维化重塑，并在人类ILD活检标本中展示了转化概念验证的适用性。通过实现可扩展、可重复且多分区的组织学定量，FibroSight为肺重塑的客观评估提供了一个实用框架。该方法通过整合纤维化、炎症、气道和血管相关读数扩展了传统的纤维化评估，支持在临床前和转化ILD研究中对疾病机制和治疗反应进行更精确的分析。

## Abstract
Interstitial lung diseases (ILDs) are heterogeneous pulmonary disorders characterized by chronic inflammation and/or fibrosis. 30--40% of ILD patients develop fibrotic disease that is associated with progressive respiratory decline and poor prognosis, particularly in idiopathic pulmonary fibrosis. Current antifibrotic therapies slow disease progression but do not reverse fibrosis, highlighting the need for improved therapeutic strategies. Robust histopathological evaluation in preclinical models is essential for drug development; however, conventional scoring systems are semi-quantitative, labor-intensive, subject to inter-observer variability, and rely on limited field sampling. Here, we introduce FibroSight, a standalone platform for compartment-resolved quantification of lung remodeling in Sirius Red--stained sections. By integrating deep learning--based structural segmentation with color-based feature extraction, FibroSight enables highly automated whole-lobe analysis without requiring complex computational setup. The platform quantifies complementary remodeling parameters, including parenchymal collagen fraction, parenchymal tissue density, nuclear area fraction, parenchymal airspace fraction, and airway- and vascular-associated remodeling. Validated in the bleomycin-induced fibrosis model, FibroSight-derived metrics strongly correlated with expert Ashcroft scoring and showed stronger associations with histological severity than corresponding outputs from a semi-automated ImageJ-based workflow. The platform further distinguished inflammatory from fibrotic remodeling in influenza-induced lung injury and demonstrated translational proof-of-concept applicability in human ILD biopsy specimens. By enabling scalable, reproducible, and multi-compartment histological quantification, FibroSight provides a practical framework for objective assessment of lung remodeling. This approach expands conventional fibrosis evaluation by integrating fibrotic, inflammatory, airway, and vascular-associated readouts, supporting more precise analysis of disease mechanisms and therapeutic responses in preclinical and translational ILD research.