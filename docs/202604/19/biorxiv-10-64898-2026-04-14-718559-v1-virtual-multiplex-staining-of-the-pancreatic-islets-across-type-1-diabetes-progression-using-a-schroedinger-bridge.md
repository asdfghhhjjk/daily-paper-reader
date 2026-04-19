---
title: Virtual multiplex staining of the pancreatic islets across type 1 diabetes progression using a Schroedinger bridge
title_zh: 利用薛定谔桥对1型糖尿病进程中的胰岛进行虚拟多重染色
authors: "Shen, Y., Cho, W. J., Joshi, S., Wen, B., Naganathanhalli, S., Beery, M., Grubel, C. R., Sivasubramanian, A., Forjaz, A., Grahn, M. P., Dequiedt, L., Huang, Y., Han, K. S., Wu, F., Pedro, B. A., Wood, L. D., Chen, T., Hruban, R. H., Kusmartseva, I., Atkinson, M. A., Wirtz, D., Kiemen, A. L."
date: 2026-04-17
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.14.718559v1.full.pdf"
tags: ["query:pathseg"]
score: 8.0
evidence: "利用生成式AI将H&E图像进行虚拟染色以进行组织形态学分析。"
tldr: "本文提出Schroedinger-bridge框架SMILE，用于将H&E染色虚拟转换为多重IHC染色图像，相较于传统GAN模型更稳定且保真度更高，可实现胰腺岛和乳腺癌组织的高通量分子标记预测。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718559-v1/fig-001.webp\", \"caption\": \"Figure 6: Visual comparison of ground truth and virtual tiles from public dataset. (a) Mosaic representing ground truth histology (GT H&E, GT IHC) and virtual IHC generated using three models (SMILE, p2p, p-p2p) of four representative testing tiles from two kinds (HER2, Ki67) of IHC stains. (b) radar plots representing quantitative evaluation results using seven methods (SSIM, CW-SSIM, PSNR, FID, CMMD, VMMD, UNI2) for Ki67 (left) and HER2 (right) stains. Larger polygon areas indicate superior model performance. SMILE (blue) consistently outperforms p2p (orange) and p-p2p (green) across multiple metrices for both markers.\", \"page\": 21, \"index\": 1, \"width\": 872, \"height\": 1123}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718559-v1/fig-002.webp\", \"caption\": \"Figure 3: Visual comparison of ground truth and virtual tiles. (a) Mosaic presenting ground truth histology (GT H&E, GT mIHC) and virtual mIHC generated using three models (SMILE, p2p, p-p2p) of five representative testing tiles. Dashed line outlines islet morphology in Tile 1 and Tile 2. Tile 3: yellow arrow pointing to islet labeling, where the SMILE image most closely matches the GT mIHC. Tile 4: plus sign indicating a pancreatic duct adjacent to an islet. Only the SMILE model correctly generates the duct. Tile 5: Asterisk indicates an artery. Only the SMILE mode correctly generates the artery. (b) Representative images of GT H&E, GT mIHC, virtual mIHC, label masks (to segment the mIHC signal), and islet masks (to segment the islet morphology), used to validate the virtually labeled images.\", \"page\": 14, \"index\": 2, \"width\": 647, \"height\": 1114}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718559-v1/fig-003.webp\", \"caption\": \"Figure 4: Virtual labeling and 3D reconstruction of normal and diabetic pancreatic islets. (a) Serial H&E images were converted to mIHC for 3D islet reconstruction using SMILE. (b) Table depicting metrics of the three 3D reconstructed volumes, collected from one nondiabetic (ND) donor (ND), one donor positive for auto-antibodies (Aab+), and one type 1 diabetic (T1D) donor. (c) Sample whole slide mIHC images inferred from serial H&E from each 3D dataset. (d) 3D renderings of the inferred insulin and glucagon in large 3D samples of human pancreas tissue depict the dramatic loss in insulin content with type 1 diabetes onset.\", \"page\": 18, \"index\": 3, \"width\": 881, \"height\": 1174}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718559-v1/fig-004.webp\", \"caption\": \"Figure 5: 3D Quantitative, spatial analysis of pancreatic islets. (a) left: bar graph depicting endocrine cluster (volume <10 4 µm 3 ) and islet (volume >10 4 µm 3 ) density across ND, Aab+, and T1D tissue. Cluster density is relatively consistent across the samples while islet density decreases from ND to AaB+ to T1D. Middle: boxplot displaying islet size across three samples. The size average islet size and islet size variability significantly increases with T1D progression. Right: zoom in view of the middle plot. (b) per-endocrine cluster percent insulin and percent glucagon across ND, Aab+, T1D tissue, highlighting a more heterogenous molecular composition with T1D progression. Percent CD3+ regions within 50 µm of each endocrine cluster depict significantly increasing insulitis with T1D progression. Right: zoom in view of the third plot. (c) The same quantifications as in (b) applied to pancreatic islets. For all graphs, * = p < 10 -5 using the one-way ANOVA test.\", \"page\": 19, \"index\": 4, \"width\": 862, \"height\": 1120}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718559-v1/fig-005.webp\", \"caption\": \"Figure 2: A curated cohort for histology image conversion. (a) Tiles were generated at a size of 256 × 256 pixels with roughly 50% chosen to contain an islet and 50% chosen not to contain an islet. Tiles were manually reviewed to remove poorly aligned pairs. Sample high-quality and low-quality image pairs shown, with the dashed outline highlighting the islets. The table displays total numbers of raw and filtered tiles. (b) Distribution of all tiles before and after filtering. (c - e) Bar and violin plots presenting donor distribution by diabetes status, age, and sex. (f) Summary statistics describing the final training and testing distribution by diabetes status and the number of isletfocused and non-islet-focused tiles.\", \"page\": 12, \"index\": 5, \"width\": 976, \"height\": 1085}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718559-v1/fig-006.webp\", \"caption\": \"Figure 1: Virtual, multiplex labeling of pancreatic islets of Langerhans. (a) Collection of 216 paired H&E and mIHC labeled sections from 72 pancreatic donors from 3 pancreatic locations (pancreas head, body, and tail) with 3 health conditions: donors without diabetes (ND), donors positive for autoantibody (Aab+), and donors with type 1 diabetic (T1D). mIHC image labels for insulin (red), glucagon (blue), and CD3 (brown). (b) A computationa workflow for nonlinear, 20x-resolution image registration and tiling for model training. (c) Virtual labeling models trained on paired image tiles and tested for their ability to generate islets of Langerhans with realistic morphological and molecular features, as tested quantitatively and via blinded pathologist review. (d) Application of virtual labeling workflow to generate three-dimensional maps of pancreatic islets.\", \"page\": 5, \"index\": 6, \"width\": 976, \"height\": 816}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718559-v1/fig-007.webp\", \"caption\": \"Table 3: Quantitative evaluation of virtual labeling models. Arrows indicate whether higher ( ) or lower ( ) values are better. Bold values indicate the best performance for each metric. Texture-based metrics evaluate pixel-level similarity, distribution-based metrics assess feature-level distributional similarity using pretrained neural networks, and label-based metrics quantify morphological and compositional accuracy of the virtual mIHC labels.\", \"page\": 16, \"index\": 7, \"width\": 581, \"height\": 485}]"
motivation: "传统的H&E染色无法提供细胞分子状态信息，而mIHC虽然能实现多蛋白标记，却昂贵并不适合大规模研究。"
method: "研究采用Schroedinger-bridge扩散模型进行H&E到mIHC的图像转换，并建立了大规模胰腺组织配对数据集验证算法性能。"
result: SMILE在图像结构保持与染色转换的准确性方面显著优于GAN，并可跨机构泛化到不同组织类型。
conclusion: "SMILE为从常规H&E图像中高效推断蛋白表达提供了可扩展路径，有望推动数字病理学和胰腺疾病研究。"
---

## 摘要
经典的苏木精-伊红（H&E）染色可用于观察组织形态，但无法提供细胞分子状态的信息。免疫组化（IHC）技术能够标记组织中特定蛋白，从而区分出在H&E染色中可能难以检测的相关结构。然而，IHC过程复杂、昂贵且耗时，尤其是多重免疫组化（mIHC），因此限制了其在大型队列中的应用。利用生成式人工智能模型（如生成对抗网络，GAN）将H&E染色图像转换为IHC图像，为这一问题提供了可能的解决方案。然而，GAN在分布外采样时不稳定，容易出现幻觉或模式崩塌，限制了其在复杂图像转换任务中的准确性。为解决这些问题，研究领域近期转向扩散模型。本研究提出了一种用于多重免疫标记估计的薛定谔桥模型（Schroedinger-bridge for Multiplex ImmunoLabel Estimation，简称SMILE）。与常规的扩散模型需要通过高斯噪声中间步骤从源域映射到目标域不同，薛定谔桥扩散模型跳过了此步骤，已证明能在图像翻译过程中更好地保留结构。为评估SMILE的性能，我们基于胰腺器官捐献者生成了大规模高保真H&E-mIHC图像对数据集，标记目标包括胰岛素、胰高血糖素和CD3。该数据集在1型糖尿病状态、胰腺解剖位置、年龄和性别方面均具有良好的代表性。利用此数据集，我们通过综合评估框架（包括纹理、分布及抗体特异性指标，以及盲法病理学家评审）展示了SMILE优于GAN的性能。我们进一步验证了SMILE可从外部机构生成的H&E图像中准确生成mIHC图像，支持整张切片图像转换，并能够生成非糖尿病、自身抗体阳性及1型糖尿病供体组织中胰岛的逼真三维图谱。最后，我们在乳腺癌样本中将配对的H&E图像转换为HER2和Ki67染色图像，进一步验证了SMILE在不同染色类型转换中的优势。总体而言，该框架为从存档H&E切片中高通量推断蛋白组信息提供了可扩展的流程，对胰腺研究和数字病理学具有变革性潜力。

## Abstract
Classical hematoxylin and eosin (H&E) staining enables review of tissue morphology but lacks information regarding the molecular state of cells. Immunohistochemical (IHC) techniques label specific proteins in tissue, allowing differentiation of relevant structures that may go undetectable in H&E. However, the IHC process is complex, expensive, and time-consuming, especially for multiplex IHC (mIHC) limiting its use in large cohorts. Stain conversion of H&E to IHC using generative artificial intelligence models such as generative adversarial networks (GANs) represent one solution to this problem. However, GANs are unstable during out of distribution sampling and are prone to hallucinations or mode collapse, limiting their accuracy in challenging image conversion tasks. To address this, the field has recently turned to diffusion models. Here, we introduce Schroedinger-bridge for Multiplex ImmunoLabel Estimation (SMILE). Unlike conventional diffusion models that map from source to target through an intermediate Gaussian noise, Schroedinger-bridge diffusion models skip this step and have been shown to better preserve structures during image translation. To test the performance of SMILE, we generated a large cohort of high-fidelity H&E-mIHC image pairs from pancreatic organ donors, targeting insulin, glucagon, and CD3. Our dataset well-sampled across type-1 diabetes status, pancreas anatomical location, age, and sex. Using this cohort, we demonstrate the superiority of SMILE compared to GANs via a comprehensive evaluation framework incorporating texture, distribution, and antibody-specific metrics, as well as blinded pathologist reviews. We further confirmed the ability of SMILE to generate accurate mIHC images from H&Es generated at an external site, to perform whole slide image conversion, and to generate realistic three-dimensional maps of the pancreatic islets in non-diabetic, auto-antibody positive, and type-1 diabetic donor tissue. Finally, we performed stain conversion of paired H&E to HER2 and Ki67 images in breast cancer, confirming the superiority of SMILE in diverse stain conversion applications. Collectively, this framework provides a scalable pipeline for high-throughput proteomic inference from archival H&Es, providing transformative potential for pancreatic research and digital pathology.

---

## 论文详细总结（自动生成）

# 利用薛定谔桥模型实现H&E图像到mIHC图像的虚拟转换：1型糖尿病胰岛研究总结

---

## 一、研究背景与核心问题

- **核心挑战**：传统的苏木精-伊红（H&E）染色是病理学中的标准方法，可呈现组织结构，但无法反映细胞的分子状态。要研究如1型糖尿病（T1D）等疾病中胰岛细胞的功能性变化，需要多重免疫组化（multiplex IHC, mIHC）技术。  
- **现实困境**：mIHC 实验过程复杂、昂贵且耗时，不适用于大规模或三维分析。  
- **技术动机**：近年来，生成式人工智能（Generative AI）被用于“虚拟染色”，即从H&E图像推断IHC标记。然而，主流的生成对抗网络（GAN）模型存在**不稳定、模式坍塌和幻觉（hallucination）**等问题，难以保证病理结构的一致性。  
- **研究目标**：本研究旨在通过一种基于**薛定谔桥（Schrödinger Bridge, SB）**的生成建模方法，建立一种稳定、高保真的H&E→mIHC 虚拟转换框架，以服务于糖尿病病理诊断与空间分子研究。

---

## 二、方法论：SMILE框架与关键技术

### 1. 核心思想
提出 **SMILE (Schrödinger-bridge for Multiplex ImmunoLabel Estimation)**，一种基于薛定谔桥扩散计算的深度学习模型，使H&E图像直接转换为mIHC标记（胰岛素、胰高血糖素、CD3）分布图。

### 2. 理论基础
- **优化传输思想**：  
  薛定谔桥通过最小化相对于参考布朗运动的 Kullback-Leibler 散度，求解从源域分布（H&E）到目标分布（mIHC）的最优路径，具有物理意义上的“最小耗散概率流”。  
- **与标准扩散模型区别**：  
  常规扩散模型从纯高斯噪声逐步“去噪”生成图像，而SB模型可**直接从源图像出发进行漂移演化**，无需噪声起点，从而保留组织结构。
- **核心方程（文字说明）**：  
  模型优化目标是最小化KL散度：  
  *argmin* KL(P‖Q)，其中P是学习到的运输过程分布，Q为布朗运动参考分布，需满足边界约束（源分布=H&E，目标分布=mIHC）。  
- **实现细节**：  
  - 模型基于 NVIDIA 实验室的 **I²SB 框架**（公开代码库）。  
  - 主干网络：Ablated Diffusion Model (ADM) U-Net，带残差模块与注意力层。  
  - 训练过程：1000个时间步、Adam 优化器 (lr=5×10⁻⁵)、EMA平滑。  
  - 推理为多步迭代采样（Function Evaluation, NFE），直接从H&E逐步逼近目标分布。

---

## 三、实验设计与基准设置

### 1. 数据集构建
- **来源**：来自 *Network for Pancreatic Organ Donors with Diabetes (nPOD)* 项目的72名器官捐赠者。
- **数据规模**：
  - 共212对配准的H&E 与 mIHC 全视野扫描图像（WSI）。  
  - 约 **3.9万块高质量256×256像素的图像tile** 用于训练。
  - 数据涵盖**胰头、胰体、胰尾三解剖区**，包含三种健康状态：非糖尿病、抗体阳性、T1D。
- **标注内容**：  
  mIHC 标签包括胰岛素（红）、胰高血糖素（蓝）与 CD3（棕），用于区分β细胞、α细胞和T细胞。

### 2. 对比方法
- **GAN 基线模型**：
  - **pix2pix (p2p)**：基于U-Net生成器与PatchGAN判别器。  
  - **pyramid-pix2pix (p-p2p)**：引入金字塔多尺度对齐损失，提高空间匹配性。  
- **拟合任务**：均执行 H&E → mIHC 虚拟染色。

### 3. 测试与验证
- 内部测试集：1293对tile。  
- 外部验证集：由约翰·霍普金斯大学收集的4个胰腺外科样本。  
- 额外验证：乳腺癌H&E→HER2、Ki67染色转换。  

### 4. 评价指标（共13项）
- **纹理类**：SSIM、CW-SSIM、PSNR  
- **分布类**：FID、CMMD、VMMD、UNI2 embedding  
- **标签类**：IOU、RSD、GID、GGD  
- **人工评审**：两位病理专家进行盲评（PATH Q1、Q2）  
- **3D重建验证**：通过100张序列切片实现胰岛空间重建，对比T1D分期状态。

---

## 四、资源与算力

- 文中未明确说明使用的GPU型号及数量。  
- 模型训练涉及 **I²SB PyTorch 实现**，推理约**3.5秒/Tile**。  
- 提及使用 **fp16 精度优化** 以缩短推理时间（缩短约50%内存占用）。  
- SMILE的WSI推理约需**1小时/张全切片图像**。  

> （官方代码与权重将在同行评审后公开。）

---

## 五、实验数量与充分性

- **主要实验类型**：
  1. 三种模型对比实验（SMILE vs. p2p vs. p-p2p）。  
  2. 不同 NFE 与模型权重下的性能搜索（共30组组合）。  
  3. 内外部数据集泛化测试。  
  4. 乳腺癌单标记泛化测试（HER2、Ki67）。  
  5. 三维重建与空间特征统计验证。  
  6. 病理盲评实验（100张随机Tiles）。  
- **总体评价**：实验覆盖全面，从图像像素到空间生物学均有验证，指标多样且客观，具备充分性与再现性。

---

## 六、主要结论与发现

- **算法性能**：  
  - SMILE在13项指标中有11项得分最高，尤其在**FID（29.06 vs 104.35,p2p）**、**CMMD与VMMD**上表现突出，显示在全局感知质量上显著优于GAN。  
  - 人工盲评中，SMILE生成图像最接近真实mIHC。
- **生物学验证**：  
  - 3D重建揭示了随T1D进展，胰岛内胰岛素减少、CD3+浸润增加、胰岛体积与分布异质性升高的趋势，与既往研究一致。  
  - SMILE 推理出的mIHC呈现与实际实验染色高度一致的蛋白分布。
- **泛化能力**：  
  - 能在不同机构、组织类型（如乳腺癌HER2/Ki67）上准确生成虚拟IHC结果。

---

## 七、方法与设计优点

- **理论创新**：首次在病理图像虚拟染色任务中系统引入薛定谔桥优化传输思想，保证结构保真。  
- **数据科学创新**：构建了高质量、配准精确的胰腺H&E-mIHC对齐数据集，并平衡了稀有的胰岛区域。  
- **指标体系完善**：结合传统图像质量指标与语义感知嵌入（Virchow2、UNI2），更接近人类病理感知。  
- **多维扩展性**：实现了全切片、跨机构、跨病种乃至三维推理，具备高泛用性。  
- **计算优化**：通过fp16推理与NFE调优实现高性能平衡。

---

## 八、不足与局限

- **数据配准局限**：H&E 与 mIHC 来自相邻切片而非同一切片，存在微小位置误差，可能影响像素级一致性。  
- **计算开销高**：单张 WSI 推理耗时较长，难以完全满足临床实时应用。  
- **训练可复现性依赖于高质量数据与硬件资源**，普通实验室可能难以完全复现。  
- **模型未开放**（将在正式发表后发布），目前可验证性受限。  
- **未报告具体GPU配置与耗时**，难以进行算力成本评估。  

---

**（完）**
