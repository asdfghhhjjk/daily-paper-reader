---
title: "D-VST: Diffusion Transformer for Pathology-Correct Tone-Controllable Cross-Dye Virtual Staining of Whole Slide Images"
title_zh: D-VST：用于全切片图像病理校正色调可控交叉染料虚拟染色的扩散变换器
authors: "Shurong Yang, Dong Wei, Yihuang Hu, Qiong Peng, Hong Liu, Yawen Huang, Xian Wu, Yefeng Zheng, Liansheng Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=jl0O0MYLyh"
tags: ["query:pathology-ai"]
score: 4.0
evidence: 使用扩散变换器对全切片图像进行虚拟染色以避免病理泄漏
tldr: 全切片图像交叉染料虚拟染色面临病理泄漏问题：非病理区域被错误染色。D-VST提出可解耦病理与色调条件的扩散变换器框架，实现病理正确的虚拟染色，在多个染色任务中保持病理区域真实性，为WSI预处理和计算病理学提供高质量图像。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 解决全切片图像虚拟染色中的病理泄漏问题，确保染色后病理区域仍保持正确。
method: 提出D-VST框架，解耦病理和色调条件，使用扩散变换器进行交叉染料虚拟染色。
result: 在虚拟染色任务中有效避免病理泄漏，保持病理区域真实性。
conclusion: D-VST为WSI虚拟染色提供了病理正确的可控方案，有助下游分析。
---

## Abstract
Diffusion-based virtual staining methods of histopathology images have demonstrated outstanding potential for stain normalization and cross-dye staining (e.g., hematoxylin-eosin to immunohistochemistry). However, achieving pathology-correct cross-dye virtual staining with versatile tone controls poses significant challenges due to the difficulty of decoupling the given pathology and tone conditions. This issue would cause non-pathologic regions to be mistakenly stained like pathologic ones, and vice versa, which we term “pathology leakage.” To address this issue, we propose diffusion virtual staining Transformer (D-VST), a new framework with versatile tone control for cross-dye virtual staining. Specifically, we introduce a pathology encoder in conjunction with a tone encoder, combined with a two-stage curriculum learning scheme that decouples pathology and tone conditions, to enable tone control while eliminating pathology leakage. Further, to extend our method for billion-pixel whole slide image (WSI) staining, we introduce a novel frequency-aware adaptive patch sampling strategy for high-quality yet efficient inference of ultra-high resolution images in a zero-shot manner. Integrating these two innovative components facilitates a pathology-correct, tone-controllable, cross-dye WSI virtual staining process. Extensive experiments on three virtual staining tasks that involve translating between four different dyes demonstrate the superiority of our approach in generating high-quality and pathologically accurate images compared to existing methods based on generative adversarial networks and diffusion models. Our code and trained models will be released.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：在数字病理学中，组织病理图像常需进行多种化学染色以辅助诊断。利用深度学习进行虚拟染色，尤其是从一种染料图像生成另一种染料图像（交叉染料染色，如苏木精-伊红染色向免疫组化染色转换），能够节省时间、降低成本并实现染色归一化。
- **核心问题**：现有基于扩散模型的虚拟染色方法虽具有潜力，但在实现“色调可控”的交叉染料染色时，面临一个关键挑战：**病理泄漏**。即在染色风格迁移过程中，模型难以解耦输入的病理信息与色调条件，导致非病理区域被错误地染成类似病理区域的模样，或者病理区域未能正确染色，严重损害图像的真实性和下游分析可靠性。
- **整体含义**：论文旨在提出一个能够实现“病理正确、色调可控”的交叉染料虚拟染色框架，特别针对全切片图像的高分辨率特性，解决病理泄漏问题，为计算病理学提供高质量预处理。

## 2. 方法论：核心思想、关键技术细节与算法流程

- **核心思想**：通过明确解耦病理信息与色调条件，并设计适用于超高分率万像素图像的高效推理策略，构建一个病理正确且色调可控的扩散虚拟染色变换器。
- **关键技术细节**：
    - **病理编码器与色调编码器**：分别提取组织病理结构信息和目标染色色调信息，并将两者作为扩散模型的条件输入，从架构上实现条件解耦。
    - **两阶段课程学习方案**：设计两阶段的训练策略，阶段性地向模型注入病理与色调条件，进一步强制模型解耦这两种控制信号，从而消除病理泄漏。
    - **扩散变换器骨干网络**：采用扩散变换器作为生成骨干，利用其捕捉长程依赖的能力，更好地保持全局组织结构和染色一致性。
    - **频率感知自适应块采样策略**：针对全切片图像高达数十亿像素、无法直接输入模型的难题，提出一种零样本的推理策略。该策略根据图像块的频率信息自适应选择采样区域，在保证生成质量的同时实现高效推理，无需额外微调。
- **算法流程说明**：训练时，输入源染色图像和对应的目标染色图像，通过病理编码器将源图的病理结构编码，色调编码器将目标染色类型与风格编码；噪声预测网络结合这两种条件学习逆向扩散过程。推理时，给定源全切片图像和目标色调，利用频率感知策略采样方块，分批通过模型生成目标染色图像，再拼接回完整全切片图像。

## 3. 实验设计：数据集、场景、基准与对比方法

- **任务场景**：交叉染料虚拟染色，涉及四种不同染料之间的三种相互转换任务（摘要中未列出具体染料名称，如H&E、IHC等，但明确为四种染料间的转换）。
- **数据集**：摘要未明确说明数据集来源与规模，仅提及“广泛的实验”。
- **基准与评价指标**：未在摘要中给出具体指标名称，但强调“生成高质量且病理准确的图像”。
- **对比方法**：与基于生成对抗网络的方法和基于扩散模型的方法进行对比，说明方法优越性。

## 4. 资源与算力

- 摘要及所提供的元数据中**未明确提及**所使用的GPU型号、数量、训练时长或运算量等算力资源细节。

## 5. 实验数量与充分性

- **实验组数**：摘要提到执行了三组虚拟染色任务（四种染料间的相互转换），每组任务均与多个现有方法比较，并可能包含消融实验（虽未明确说明，但通常此类工作会包括，文中提到“整合两个创新组件”）。
- **充分性与公平性**：基于摘要，实验覆盖了多组染色转换任务，与代表先进水平的GAN和扩散模型方法对比，具备一定广度。但具体数据集、指标和消融实验的细节未知，无法从摘要判断实验是否足够全面和公平。据称代码和模型将开源，有助于复现和验证。

## 6. 主要结论与发现

- D‑VST框架成功实现了病理正确、色调可控的交叉染料虚拟染色，有效消除了病理泄漏问题。
- 所提出的解耦编码器和两阶段课程学习方案对保持病理区域真实性至关重要。
- 频率感知自适应块采样策略使得对万像素全切片图像的零样本高效染色成为可能。
- 在与现有GAN和扩散模型方法的对比中，D‑VST能生成质量更高且病理更准确的图像。

## 7. 优点：方法或实验设计亮点

- **问题新颖性**：明确指出了虚拟染色中的“病理泄漏”现象，并针对性设计了解耦方案。
- **技术整合**：将扩散变换器、双编码器、两阶段课程学习和频率感知采样策略有机结合，同时解决了病理正确性、色调控制和高分辨率推理三个难点。
- **应用价值高**：可直接应用于全切片图像预处理，改善下游计算病理学分析，且推理效率高（零样本处理高分辨率图像）。

## 8. 不足与局限

- **信息缺失**：摘要中未提供数据集、评价指标、算力消耗等关键细节，无法评估方法的实际开销和泛化边界。
- **染料类别有限**：实验仅涉及四种染料，尚不清楚方法能否直接扩展至更多种或更稀有的染色类型。
- **临床验证缺失**：未提及是否进行下游病理诊断任务的评估，虚拟染色图像对真实诊断的影响有待验证。
- **潜在偏差风险**：如果训练数据来自单一机构或特定扫描仪，模型可能对数据分布偏移敏感，摘要未说明数据多样性。

（完）
