---
title: Pheno-MYCN maps the morphological footprint of MYCN amplification in paediatric neuroblastoma
title_zh: Pheno-MYCN 绘制儿童神经母细胞瘤中 MYCN 扩增的形态学足迹
authors: "Chai, B., Fourkioti, O., Naidoo, R., De Vries, M., George, S., Chesler, L., Hutchinson, J. C., Bakal, C."
date: 2026-08-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.08.20.745848v1.full.pdf"
tags: ["query:cell-path"]
score: 7.0
evidence: "弱监督框架将MYCN扩增映射到H&E全切片图像上可解释的形态亚群。"
tldr: "MYCN扩增是儿童神经母细胞瘤的重要预后标志，但现有检测与组织形态脱节，难以定位其生物学影响。Pheno-MYCN利用弱监督学习将切片级MYCN预测与可解释形态学子群关联，在189张常规H&E切片上识别出MYCN扩增特征（AUC 0.93-1.00）。该方法揭示MYCN扩增在不同形态区域通过不同特征留下足迹，并可作为连续梯度追踪。这为分子检测受限场景提供了低成本、可解释的MYCN定位手段。"
source: biorxiv
selection_source: fresh_fetch
motivation: MYCN扩增是预后标志，但现有检测与形态脱节，无法定位其生物学影响。
method: 开发Pheno-MYCN，弱监督地将切片级预测与可解释形态学子群关联。
result: "在189张H&E切片上，识别出MYCN扩增特征（AUC 0.93-1.00），且可追踪为连续梯度。"
conclusion: "MYCN扩增在常规H&E上留下可解释足迹，提供低成本定位手段，尤其适合分子检测受限场景。"
---

## 摘要
MYCN 扩增长期以来一直是儿童神经母细胞瘤的预后标志物，但通常在整体水平上进行检测，且与病理医生所评估的异质性组织结构并列而非在其内。这留下了一个空白：仅凭 MYCN 状态无法定位 MYCN 相关生物学，而仅凭形态学也无法确定分子风险。基于我们发现两者结合可识别任一单独指标均会漏掉的高危病例，我们开发了 Pheno-MYCN，一个弱监督框架，将切片级 MYCN 预测与常规 H&E 全切片图像上可解释的形态学亚群联系起来。其目标不是更强的分类器：预测探究的是 MYCN 扩增对组织产生的影响，其证据可供病理学审查。在 189 张切片中，Pheno-MYCN 将每张切片解析为表型簇，专家评审将这些簇与神经母细胞瘤形态相对应。细胞水平分析显示，MYCN 扩增在每一个亚群中都留下了“标记”，但在每个亚群中通过不同特征体现：细胞密集但结构紊乱的肿瘤，伴有更稀疏、多样性更低的网络；在坏死和出血区域主要以丰度体现。仅凭这些特征即可在每张切片上识别出 MYCN 扩增样组织（AUC 0.93–1.00，留一片交叉验证），并在肿瘤内追踪为连续梯度。因此，MYCN 扩增留下了具体、可解释的足迹，可在常规 H&E 上读取和定位，为分子检测受限地区提供一种低成本标记和绘图手段。

## Abstract
MYCN amplification has long been a prognostic marker in paediatric neuroblastoma, yet is typically assayed in bulk, alongside rather than within the heterogeneous tissue architecture pathologists assess. This leaves a gap: MYCN status alone cannot localise MYCN-associated biology, while morphology alone cannot assign molecular risk. Motivated by our finding that the two together identify high-risk cases missed by either, we developed Pheno-MYCN, a weakly supervised framework linking slide-level MYCN prediction to interpretable morphological sub-populations on routine H&E whole-slide images. The aim is not a stronger classifier: prediction probes what MYCN amplification does to the tissue, its evidence open to pathological scrutiny. Across 189 slides, Pheno-MYCN resolved each into phenotypic clusters that expert review mapped to neuroblastoma morphologies. Cell-level profiling revealed MYCN amplification "marked" every sub-population, through a different feature in each: densely cellular yet disorganised tumour with sparser, less diverse networks; chiefly abundance in necrotic and haemorrhagic regions. MYCN-amplified-like tissue was identifiable per slide from these features alone (AUC 0.93-1.00, leave-one-slide-out) and traced as a continuous gradient within tumours. Thus MYCN amplification leaves a concrete, interpretable footprint that can be read and localised on routine H&E, offering a low-cost means to flag and map it where molecular testing is limited.