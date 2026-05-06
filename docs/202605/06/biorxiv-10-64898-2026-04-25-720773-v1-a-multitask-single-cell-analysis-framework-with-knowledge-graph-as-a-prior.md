---
title: A multitask single-cell analysis framework with knowledge graph as a prior
title_zh: 一种以知识图谱为先验的多任务单细胞分析框架
authors: "Mathew, B., Ganguly, R., Maity, A., Halder, A., Sabu, J. T., Gupta, N., Peela, S. C. M., Samanta, S., Kumari, S., Bhattacharjee, N., Joshi, S., Gupta, S., Ahuja, G., Farooq, M., Majumdar, A., Hasan, S., Sengupta, D."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.25.720773v1.full.pdf"
tags: ["query:cellrep"]
score: 6.5
evidence: 用于细胞状态程序的单细胞多任务分析框架
tldr: 本文提出scKNIFE框架，通过将多源生物知识图谱嵌入非负矩阵分解，实现单细胞数据的聚类、注释、代谢与信号推断一体化分析，在癌症数据集中展现出高效性与生物一致性，为单细胞多任务研究提供统一方案。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有单细胞分析流程将聚类、注释及生物功能推断分开进行，缺乏信息整合与统一解释能力。
method: 提出了知识图谱正则化的非负矩阵分解框架scKNIFE，将生物学知识图谱嵌入分解目标实现多任务联合推断。
result: scKNIFE在多种癌症单细胞数据中表现出与领先方法相当的聚类与注释性能，并准确恢复代谢程序及治疗相关状态。
conclusion: scKNIFE为单细胞癌症转录组学提供了可扩展的统一分析框架，促进从表达数据到功能实体的系统解释。
---

## 摘要
单细胞RNA测序通过揭示肿瘤微环境的细胞和分子多样性，重塑了癌症生物学。然而，大多数分析流程仍将聚类、注释、通路评分、代谢推断以及细胞间通讯等视为独立任务。在此，我们提出了scKNIFE（基于知识图谱的非负矩阵分解框架，用于功能实体推断），这是一个统一的、图正则化的非负矩阵分解框架，能够联合重建单细胞表达谱并推断多种生物实体的活性，包括通路、细胞类型标记、代谢反应与任务、配体-受体互作以及细胞状态程序。通过将异质知识图谱直接嵌入分解目标中，scKNIFE通过Laplacian正则化在生物相关实体间传播信息，同时稀疏性约束保持了解释性。整合的先验图涵盖47,274个节点和506,620条边，来源于包括Gene Ontology、Reactome、Hallmark基因集、Human-GEM、CellChat、PanglaoDB、Cytopus以及Tabula Muris衍生注释等多种互补资源。在多个以癌症为中心的单细胞数据集中，scKNIFE在聚类和细胞类型注释方面表现出与领先方法相当的性能，同时能够恢复生物学上一致的代谢程序，这些程序与专注代谢的独立方法结果一致，并捕获与治疗反应相关的状态。此外，该框架支持从单一潜在表示中进行细胞类型特异性生物活性下游推断。总体而言，这些结果确立了scKNIFE作为一个模块化且可扩展的框架，用于单细胞癌症转录组学的端到端生物学解释。

## Abstract
Single-cell RNA sequencing has reshaped cancer biology by revealing the cellular and molecular diversity of the tumor microenvironment, yet most analysis pipelines still treat clustering, annotation, pathway scoring, metabolic inference, and cell-cell communication as separate tasks. Here, we present scKNIFE (Knowledge graph-based NMF for Inference of Functional Entities), a unified graph-regularized non-negative matrix factorization framework that jointly reconstructs single-cell expression profiles and infers activities of diverse biological entities, including pathways, cell-type markers, metabolic reactions and tasks, ligand-receptor interactions, and cell-state programs. By embedding a heterogeneous knowledge graph directly into the factorization objective, scKNIFE propagates information between biologically related entities through Laplacian regularization while sparsity constraints preserve interpretability. The integrated prior graph spans 47,274 nodes and 506,620 edges, assembled from complementary resources including Gene Ontology, Reactome, Hallmark gene sets, Human-GEM, CellChat, PanglaoDB, Cytopus, and Tabula Muris-derived annotations. Across multiple cancer-focused single-cell datasets, scKNIFE yields competitive to leading performance for clustering and cell-type annotation, while also recovering biologically coherent metabolic programs that agree with dedicated metabolism-focused methods and capture therapy-response-associated states. In addition, the framework supports downstream inference of cell-type-specific biological activities from a single latent representation. Together, these results establish scKNIFE as a modular and extensible framework for end-to-end biological interpretation of single-cell cancer transcriptomics