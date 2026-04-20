---
title: Deep-learning deconvolution and segmentation of fluorescent membranes for high-precision bacterial cell-size profiling
title_zh: 基于深度学习的荧光膜反卷积与分割用于高精度细菌细胞尺寸分析
authors: "Reyes-Matte, O., Fortmann-Grote, C., Gericke, B., Hüttmann, N., Ojkic, N., Lopez-Garrido, J."
date: 2026-04-15
pdf: "https://www.biorxiv.org/content/10.1101/2025.10.26.684635v2.full.pdf"
tags: ["query:sam"]
score: 7.0
evidence: 基于深度学习的荧光膜图像细胞自动分割
tldr: 这项研究针对细菌细胞尺寸研究不足的问题，开发了基于深度学习的MEDUSSA方法，通过对荧光膜图像的自动去卷积与分割，实现高通量、精确的细胞尺寸分析，从多菌株比较中揭示细胞体积差异及遗传机制。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-10-26-684635-v2/fig-001.webp\", \"caption\": \"\", \"page\": 6, \"index\": 1, \"width\": 1378, \"height\": 1639}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-10-26-684635-v2/fig-002.webp\", \"caption\": \"\", \"page\": 9, \"index\": 2, \"width\": 1207, \"height\": 1395}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-10-26-684635-v2/fig-003.webp\", \"caption\": \"\", \"page\": 10, \"index\": 3, \"width\": 1226, \"height\": 1067}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-10-26-684635-v2/fig-004.webp\", \"caption\": \"\", \"page\": 12, \"index\": 4, \"width\": 1004, \"height\": 1467}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-10-26-684635-v2/fig-005.webp\", \"caption\": \"\", \"page\": 15, \"index\": 5, \"width\": 1156, \"height\": 1689}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-10-26-684635-v2/fig-006.webp\", \"caption\": \"\", \"page\": 17, \"index\": 6, \"width\": 1170, \"height\": 1241}]"
motivation: 细菌进化研究常关注遗传和代谢多样性，但对细胞尺寸变化的研究较少。
method: 研究提出了名为MEDUSSA的基于深度学习的荧光膜图像去卷积与自动分割方法，用于高精度细菌细胞尺寸测定。
result: 该方法在六株巨芽孢杆菌中发现细胞体积差异超过两倍，主要由宽度变化导致，并鉴定出影响宽度的部分功能性PBP1等位基因。
conclusion: MEDUSSA扩展了细菌细胞生物学的研究工具，促进了细胞尺寸进化的机制解析。
---

## 摘要
细菌进化研究历来侧重于遗传和代谢多样性，而对细胞尺寸变异的关注相对不足。本文介绍了 MEDUSSA，这是一种基于荧光膜图像自动分割的高通量精确细菌细胞尺寸分析方法，非常适合用于研究细胞尺寸多样性。该方法采用基于深度学习的膜反卷积、针对荧光膜图像微调的分割模型，以及经过误差校正的细胞测量，从而能够准确提取不同形状、尺寸、链状或簇状细菌的单细胞尺寸。我们的方案克服了相差显微分割的局限性，能够可靠地获得单细胞尺寸。我们将 MEDUSSA 应用于六株 Priestia megaterium 并发现其细胞体积在菌株间相差超过两倍，主要由细胞宽度差异所致。我们识别出一株菌中导致细胞宽度减小的部分功能性 PBP1 等位基因。这些结果共同展示了比较分析在细菌细胞生物学中的强大作用，并扩展了研究细菌细胞尺寸演化的工具库。

## Abstract
Evolutionary studies in bacteria have emphasized genetic and metabolic diversity, while cell-size variation has received less attention. Here we introduce MEDUSSA, a high-throughput method for precise bacterial cell-size profiling based on automatic segmentation of fluorescent membrane images, well suited to studying cell-size diversity. The approach uses deep-learning-based membrane deconvolution, segmentation models fine-tuned for fluorescent-membrane images, and error-corrected cell measurement to extract accurate sizes from individual bacterial cells regardless of shape, size, chaining, or clustering. Our method overcomes limitations of phase-contrast segmentation, yielding reliable single-cell dimensions. We applied MEDUSSA to six strains of Priestia megaterium and found over twofold differences in cell volume across strains, largely driven by differences in cell width. We identified a partially-functional PBP1 allele that underlies the reduced width of one strain. Together, these results demonstrate the power of comparative analyses in bacterial cell biology and expand the toolkit to investigate the evolution of bacterial cell size.