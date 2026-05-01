---
title: Normalized Raman Imaging for Studies of Tissue Physiology of the Kidney
title_zh: 用于研究肾脏组织生理的归一化拉曼成像
authors: "Trim, W. V., Oh, S., Diakova, M., Petrova, K., Ichimura, T., Takakura, A., Karmakar, R., Norrelykke, S. F. F., Peshkin, L., Bonventre, J. V., Kirschner, M. W."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.1101/2025.10.12.681746v3.full.pdf"
tags: ["query:pathseg"]
score: 8.0
evidence: 准确分类肾脏组织中的小管类型和解剖区域
tldr: 本研究提出Normalized Stimulated Raman Imaging (NoRI) 技术，实现了无需染色的蛋白质和脂质定量成像。通过信号校正，NoRI保持组织结构完整并支持AI分析，在肾组织中精准分类结构与性别差异，还量化了急性损伤后的蛋白脂质重塑，为定量病理分析提供了新工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统组织学方法会损伤细胞结构并引入变异，因此需要一种无损、可重复和定量的成像手段来研究组织生理。
method: 研究采用计算归一化的Stimulated Raman成像系统，对蛋白、脂质和水的信号进行校正并实现定量测量。
result: NoRI在小鼠肾组织研究中实现了高精度的细胞分类与性别判别，并揭示蛋白质和脂质含量的性别差异及急性肾损伤中的动态变化。
conclusion: NoRI是一种可重复、定量且无损的组织成像方法，为诊断和病理特征发现提供新的途径。
---

## 摘要
传统的组织学依赖固定、包埋、切片和染色方法，这些过程会扭曲细胞结构、提取脂质并引入变异性，从而限制了可重复性。我们提出了归一化受激拉曼成像（Normalized Stimulated Raman Imaging，NoRI），这是一种能够在高空间分辨率下进行定量、无标记的蛋白质和脂质测量的技术。NoRI通过计算校正蛋白质、脂质和水的拉曼信号，从而实现定量生物质测量，同时保持组织结构完整，并便于卷积神经网络分析。应用于小鼠肾脏时，NoRI能够准确分类肾小管类型（F1—与人工标注的调和平均精确率和召回率=0.93）、解剖区域（F1=0.91）以及生物性别（F1=0.97），揭示出雌性肾小管具有更高的细胞质脂质（+6.9 mg/mL；p=0.028）和核蛋白（+26.3 mg/mL；p<0.001）。在急性肾损伤模型中，NoRI捕捉到动态的脂质和蛋白质组织变化，并在25天内定量分析了刷状缘重塑和脂滴变化。空间脂质定量是急性肾损伤特征分类的关键（F1=1.0）。这些结果确立了NoRI作为一种可重复、定量的诊断、组织病理学和特征发现方法。

## Abstract
Conventional histological relies on fixation, embedding, sectioning, and staining methods that distort cellular architecture, extract lipids, and introduces variability, limiting reproducibility. We present Normalized Stimulated Raman Imaging (NoRI) that enables quantitative, label-free protein and lipid measurements at high-spatial resolution. NoRI computationally corrects protein, lipid, and water Raman signals, allowing quantitative biomass measurements while preserving tissue architecture, facilitating analysis by convolutional neural networks. Applied to mouse kidney, NoRI accurately classified tubule types (F1-[harmonic mean of precision and recall against manual annotation]=0.93), anatomical regions (F1=0.91), and biological sex (F1=0.97), revealing greater cytoplasmic lipid (+6.9mg/mL; p=0.028) and nuclear protein (+26.3mg/mL; p<0.001) in female tubules. In acute kidney injury, NoRI captured dynamic lipid and protein organization and quantified brush border remodelling and lipid droplet changes over 25 days. Spatial lipid quantification was central for feature classification in AKI (F1=1.0). These results establish NoRI as a reproducible, quantitative method for diagnostics, histopathology, and feature discovery.