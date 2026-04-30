---
title: A novel attention mechanism for noise-adaptive and robust segmentation of microtubules in microscopy images
title_zh: 一种用于显微镜图像中微管噪声自适应与鲁棒分割的新型注意力机制
authors: "Ait Laydi, A., Cueff, L., Crespo, M., El Mourabit, Y., Bouvrais, H."
date: 2026-04-22
pdf: "https://www.biorxiv.org/content/10.1101/2025.10.23.684152v3.full.pdf"
tags: ["query:sam"]
score: 6.5
evidence: 使用新型注意力机制对显微镜图像中的生物结构进行分割
tldr: 本文针对噪声和标注困难问题，提出一种噪声自适应注意机制并集成到U-Net中形成轻量化的ASE_Res_UNet模型，通过合成数据集与真实数据验证，其在微管分割和其他曲线状结构任务中表现优异，并发布标准化数据集以促进后续研究。
source: biorxiv
selection_source: fresh_fetch
motivation: 在噪声、多重交织和标注困难的显微图像中，微管分割任务表现不稳定，亟需鲁棒性强的模型。
method: 提出基于自适应注意机制的ASE_Res_UNet结构，并结合合成数据生成与损失函数优化进行训练。
result: ASE_Res_UNet在合成与真实显微数据上均优于其他模型，具备高效性与迁移能力。
conclusion: 该研究为微管分割提供了新的基准数据集和轻量化、噪声自适应模型，并验证其跨多种影像结构的泛化性。
---

## 摘要
背景 在显微镜图像中分割细胞骨架丝状结构对于研究它们在细胞分裂和细胞内运输等细胞过程中的作用至关重要。然而，由于这些结构纤细、密集且相互交织的特性，这一任务极具挑战性。成像中的噪声、低对比度和荧光不均进一步增加了分析难度。尽管深度学习推动了大型且结构清晰的生物结构分割的发展，但在这些不利条件下，其性能往往会下降。其他挑战还包括获取曲线状结构的精确标注以及应对训练过程中的严重类别不平衡。

结果 我们提出了一种新型的噪声自适应注意力机制，它扩展了 Squeeze-and-Excitation（SE）模块，以动态适应不同噪声水平。将其整合入带有残差编码器块的 U-Net 解码器中，形成 ASE_Res_UNet，这是一种轻量但高性能的模型。为解决标注难题，我们开发了一种合成数据集生成策略，能够在噪声图像中提供精确的细丝标注，生成包含两个难度等级的合成数据集用于分割基准测试。我们系统评估了多种损失函数和评估指标，以缓解类别不平衡并确保稳健的性能评估。ASE_Res_UNet 能够有效地分割噪声合成图像中的微管结构，并优于其消融变体。相比采用其他注意力机制或不同架构的模型，ASE_Res_UNet 在保持较少参数的同时表现出更优的分割性能，使其适用于资源受限的环境。在新整理的真实显微镜数据集及近期重新标注的数据集上的评估进一步表明，ASE_Res_UNet 在真实图像中的微管分割上同样具有出色表现。在这些数据集中，ASE_Res_UNet 的性能可与一种利用两种细胞骨架预训练模型的最新合成数据驱动方法相竞争。值得注意的是，ASE_Res_UNet 对其他曲线状结构（如血管和神经）在不同成像条件下也表现出良好的可迁移性。

结论 本研究通过三项关键贡献推动了微管分割的发展：（1）提供了两个基准数据集（合成与真实），以填补该任务在标准化评估资源方面的关键空缺；（2）提出了 ASE_Res_UNet，这一结合噪声自适应注意力与残差学习的轻量但鲁棒模型；（3）在合成与真实显微镜数据上验证了其具有竞争力的性能。此外，我们展示了所提架构在多种曲线状分割任务中的稳健性与通用性，展现了其在生物研究与医学诊断中的广泛应用潜力。

## Abstract
BackgroundSegmenting cytoskeletal filaments in microscopy images is essential for studying their roles in cellular processes such as cell division and intracellular transport. However, this task is highly challenging due to the fine, densely packed, and intertwined nature of these structures. Imaging limitations--noise, low contrast, and uneven fluorescence--further complicate analysis. While deep learning has advanced segmentation of large, well-defined biological structures, its performance often degrades under such adverse conditions. Additional challenges include obtaining precise annotations for curvilinear structures and managing severe class imbalance during training.

ResultsWe introduce a novel noise-adaptive attention mechanism that extends the Squeeze-and-Excitation (SE) module to dynamically adjust to varying noise levels. Integrated into a U-Net decoder with residual encoder blocks, this yields ASE_Res_UNet, a lightweight yet high-performance model. To address annotation challenges, we developed a synthetic dataset generation strategy that ensures accurate annotations of fine filaments in noisy images, producing a synthetic dataset with two difficulty levels for segmentation benchmarking. We systematically evaluated loss functions and metrics to mitigate class imbalance, ensuring robust performance assessment. ASE_Res_UNet effectively segmented microtubules in noisy synthetic images, outperforming its ablated variants. It also demonstrated superior segmentation compared to models with alternative attention mechanisms or distinct architectures, while requiring fewer parameters, making it efficient for resource-constrained environments. Evaluation on a newly curated real microscopy dataset and a recently reannotated dataset highlighted ASE_Res_UNets effectiveness in segmenting microtubules beyond synthetic images. For these datasets, ASE_Res_UNet was competitive with a recent synthetic data-driven approach that shares two cytoskeleton pretrained models. Importantly, ASE_Res_UNet showed strong transferability to other curvilinear structures (blood vessels and nerves) across diverse imaging conditions.

ConclusionsThis work advances microtubule segmentation through three key contributions: (1) Providing two benchmark datasets (synthetic and real), addressing a critical gap in standardised evaluation resources for this task; (2) Introducing ASE_Res_UNet, a lightweight yet robust model combining noise-adaptive attention with residual learning; (3) Validating competitive performance across synthetic and real microscopy data. Additionally, we demonstrated the robustness and versatility of the proposed architecture across diverse curvilinear segmentation tasks, showcasing potential for broader applications in biological research and medical diagnosis.