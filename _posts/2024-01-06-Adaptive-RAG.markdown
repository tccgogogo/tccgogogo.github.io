---
layout:     post
title:      Adaptive-RAG：让查询处理更智能，检索更精准！
subtitle:   Adaptive-RAG: Making Query Processing Smarter and Retrieval More Precise!
date:       2024-01-06
author:     tiancc
# header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - RAG
    - LLM
---


## 论文来源
今天分享的是韩国科学技术院发布的一篇工作。

论文题目：Adaptive-RAG: Learning to Adapt Retrieval-Augmented
 Large Language Models through Question Complexity

Adaptive-RAG：智能检索策略，提升问答模型效率
 

论文链接：https://arxiv.org/pdf/2403.14403
![](https://files.mdnice.com/user/80675/464ebac9-3dae-446d-9309-b8680bd880d3.png)

## 论文概述
RAG（Retrieval-Augmented Generation）通过将外部知识库的非参数化知识整合到大型语言模型中，来提升模型的回答准确性，尤其是在一些任务（如问答）中。现有的检索增强方法对于简单查询往往会产生不必要的计算开销，而对于多步骤复杂查询可能无法有效地处理，导致模型的回答不准确或者效率低下。为了应对用户查询的复杂性和多样性，论文的核心思想是提出了一种高度灵活的方法，通过实施自适应的RAG策略，根据问题的复杂度动态调整选择机制，能够在不同情况下评估并决定是否启动检索过程，以及决定检索的深度和范围。


## 核心内容
提出了 **Adaptive-RAG** 框架，能够根据查询的复杂度动态选择最适合的策略。通过使用一个较小的语言模型作为分类器，自动判断查询的复杂度，并根据判断结果选择已有的最适合的检索策略进行下游任务。

![](https://files.mdnice.com/user/80675/53ec3b83-bf78-44b8-990f-35eb133e64a3.png)

### 查询复杂度分类器
- **作用**：输入是用户查询，输出是对查询复杂度的分类，类别包括：
  - **A**：简单查询
  - **B**：中等复杂度查询
  - **C**：复杂查询
  
- **训练**：训练数据是通过模型预测结果和数据集中的归纳偏差自动标注的，使用这些数据训练一个小规模的语言模型作为分类器。

### 检索策略选择
- **No Retrieval**：这是最简单的策略，直接使用大型语言模型（LLM）本身的知识库来生成答案。这种方法适用于那些模型已经知道答案的简单问题，不需要额外的外部信息。
- **Single-step Approach**：当问题需要额外的信息时，这种方法会先从外部知识源检索相关信息，然后将检索到的文档作为上下文信息输入到LLM中，帮助模型生成更准确的答案。这种方法适用于需要一次额外信息检索的中等复杂度问题。
- **Multi-step Approach**：对于最复杂的问题，需要从多个文档中综合信息并进行多步推理。这种方法通过迭代地访问检索器和LLM，逐步构建起解决问题所需的信息链。这种方法适用于需要多步逻辑推理的复杂问题。

根据查询的复杂度，Adaptive-RAG可以在不进行检索、单步检索和多步检索之间切换。

## 论文总结

- **提出了适应性检索增强的语言模型**：成功地解决了现有检索增强型LLMs在处理不同复杂度查询时面临的效率和准确性平衡问题。实验结果表明，该方法在多个开放域问答数据集上都取得了显著的性能提升。
![](https://files.mdnice.com/user/80675/99f3f4db-8e13-4fed-8402-5b743ff759e9.png)
- **效率提升**：实验结果显示，Adaptive-RAG在处理简单查询时，能够有效减少检索步骤和响应时间；而在处理复杂查询时，虽然检索步骤增加，但通过精确的多步检索，提高了答案的准确性。





![](https://files.mdnice.com/user/80675/d355632b-428f-4ec3-9750-79123f062dde.png)

