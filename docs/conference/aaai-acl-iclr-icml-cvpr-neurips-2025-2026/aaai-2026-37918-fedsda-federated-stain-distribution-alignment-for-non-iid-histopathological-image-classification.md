---
title: "FedSDA: Federated Stain Distribution Alignment for Non-IID Histopathological Image Classification"
title_zh: FedSDA：面向非独立同分布组织病理图像分类的联邦染色分布对齐
authors: "Cheng-Chang Tsai, Kai-Wen Cheng, Chun-Shien Lu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37918/41880"
tags: ["query:immuno-topo"]
score: 7.0
evidence: 用于非独立同分布组织病理图像分类的联邦学习，贡献于数字病理图像分析
tldr: 针对联邦学习在组织病理图像分类中遇到的特征分布偏移问题，提出基于扩散模型和染色分离的联邦染色分布对齐方法FedSDA，通过仅调整各客户端数据分布来缓解非IID影响，提升了协作训练效果。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 576, \"height\": 727}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 859, \"height\": 298}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1812, \"height\": 489}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 358}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 871, \"height\": 418}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 858, \"height\": 341}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 867, \"height\": 381}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 168}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 787, \"height\": 599}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1149, \"height\": 303}]"
motivation: 联邦学习中组织病理图像的非IID问题导致模型性能下降。
method: 提出FedSDA，通过扩散模型对齐各客户端的染色分布。
result: 在多个组织病理图像分类基准上，FedSDA有效解决了非IID问题，性能优于现有联邦学习方法。
conclusion: FedSDA为隐私保护的分布式病理图像分析提供了实用方案。
---

## Abstract
Federated learning (FL) has shown success in collaboratively training a model among decentralized data resources without directly sharing privacy-sensitive training data. Despite recent advances, non-IID (non-independent and identically distributed) data poses an inevitable challenge that hinders the use of FL. In this work, we address the issue of non-IID histopathological images with feature distribution shifts from an intuitive perspective that has only received limited attention. Specifically, we address this issue from the perspective of data distribution by solely adjusting the data distributions of all clients. Building on the success of diffusion models in fitting data distributions and leveraging stain separation to extract the pivotal features that are closely related to the non-IID properties of histopathological images, we propose a Federated Stain Distribution Alignment (FedSDA) method. FedSDA aligns the stain distribution of each client with a target distribution in an FL framework to mitigate distribution shifts among clients. Furthermore, considering that training diffusion models on raw data in FL has been shown to be susceptible to privacy leakage risks, we circumvent this problem while still effectively achieving alignment. Extensive experimental results show that FedSDA is not only effective in improving baselines that focus on mitigating disparities across clients’ model updates but also outperforms baselines that address the non-IID data issues from the perspective of data distribution. We show that FedSDA provides valuable and practical insights for the computational pathology community.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
用于非独立同分布组织病理图像分类的联邦学习，贡献于数字病理图像分析。

### 2. 核心内容
针对联邦学习在组织病理图像分类中遇到的特征分布偏移问题，提出基于扩散模型和染色分离的联邦染色分布对齐方法FedSDA，通过仅调整各客户端数据分布来缓解非IID影响，提升了协作训练效果。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/37918](https://ojs.aaai.org/index.php/AAAI/article/view/37918)
