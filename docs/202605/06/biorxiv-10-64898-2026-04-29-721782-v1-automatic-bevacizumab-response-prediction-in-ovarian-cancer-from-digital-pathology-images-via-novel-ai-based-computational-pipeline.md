---
title: Automatic Bevacizumab Response Prediction in Ovarian Cancer from Digital Pathology Images via Novel AI-based Computational Pipeline
title_zh: 基于新型人工智能计算管线的数字病理图像卵巢癌贝伐珠单抗反应自动预测
authors: "Alsaiari, A., Turki, T., Taguchi, Y.-h."
date: 2026-05-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.29.721782v1.full.pdf"
tags: ["query:cellrep"]
score: 7.5
evidence: 从数字病理图像预测药物反应的计算流水线
tldr: 该研究针对卵巢癌药物贝伐单抗的反应预测问题，提出了一种基于数字病理图像和AI计算管道的新方法，通过特征提取与回归分析显著提升预测准确率，与现有深度学习模型相比性能优越。
source: biorxiv
selection_source: fresh_fetch
motivation: 当前卵巢癌药物反应预测依赖人工诊断，过程复杂且耗时，现有工具准确性有限。
method: 作者构建了从数字病理图像提取特征、降维到基于支持向量回归的药物反应预测的AI计算流程。
result: "所提出的SVRD+R模型相比最佳Transformer模型和深度学习模型的AUC性能分别提升17%和14.9%。"
conclusion: 该研究表明AI计算管道在预测卵巢癌贝伐单抗药物反应方面具有较高准确性和可行性。
---

## 摘要
卵巢癌是妇科癌症类型之一，如果发生转移且未能早期检测，会导致女性死亡。因此，需要准确预测卵巢癌的药物反应。妇科病理学家会检查组织中的异常情况，并撰写患者报告；然而，这样的诊断过程（1）困难；（2）需要经验；（3）耗时。此外，现有工具距离完美还很远。因此，我们提出一个用于改善卵巢癌药物反应预测的计算管线，其构建如下。首先，我们从癌症影像档案库中下载与卵巢癌贝伐珠单抗疗效相关的数字病理图像。接着，我们对这些图像应用梯度方向直方图（histogram of oriented gradients），构建特征向量，并将其输入 Fisher 线性判别分析以进行降维转换。然后，将降维后的数据用于支持向量回归（support vector regression）分析，结合不同的核函数，并计算 ROC 曲线下面积（AUC）。与基于 Transformer 的模型（ViT 和 Swin）以及其他深度学习（DL）模型（VGG16、ResNet50、InceptionV3、MobileNetV2 和 EfficientNetB6）的实验结果表明，我们基于径向核的方案（命名为 SVRD+R）在 AUC 性能上比表现最佳的 Transformer 模型（ViT）提高了 17%，比表现最佳的深度学习模型（MobileNetV2）提高了 14.9%。这些结果表明，我们的基于 AI 的计算管线在应对与妇科癌症研究相关的预测问题时具有优越性和可行性。

## Abstract
Ovarian cancer is one of the gynecological cancer types, which, if metastasized and not detected early, can cause deaths among women. Therefore, there is a need to accurately predict drug responses to ovarian cancer. A gynecological pathologist inspects abnormality in tissues, followed by providing a report about patients; however, such a diagnostic process is (1) hard; (2) requires experience; and (3) time consuming. Moreover, existing tools are far from perfect. Hence, we present a computational pipeline to improve predicting drug response pertaining to ovarian cancer, derived as follows. First, we download digital pathology images pertaining to ovarian bevacizumab response from the cancer imaging archive repository. We employed histogram of oriented gradients to images, constructing feature vectors, provided to Fisher linear discriminant analysis to change the representation through dimensionality reduction. Then, we provide reduced-dimensionality data for regression analysis through support vector regression coupled with various kernels and calculating the area under the ROC curve (AUC). Experimental results against transformer-based models (ViT and Swin) and other deep learning (DL) models (VGG16, ResNet50, InceptionV3, MobileNetV2, and EfficientNetB6) demonstrate that our approach with radial kernel (named SVRD+R) yielded an AUC performance improvements of 17% against the best-performing transformer-based model (ViT) while obtaining an AUC performance improvements of 14.9% when compared against the best DL-based model (MobileNetV2). These results demonstrate the superiority and feasibility of our AIbased pipeline when tackling prediction problems pertaining to gynecologic cancer studies.