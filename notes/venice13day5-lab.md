---
timezone: UTC+8
---

# venice13day5-lab

**GitHub ID:** venice13day5-lab

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
### [**Transformer**](https://aiweb3.school/zh/handbook/ai/llm/#transformer)

Transformer 是现代 LLM 的核心架构之一。它的关键能力来自 attention：模型可以在生成时关注输入中的不同位置，学习词、代码、事实和上下文之间的关系。

你不需要一开始就推公式，但要理解一个工程事实：Transformer 擅长在上下文里找模式，不等于它拥有稳定数据库。它能把文档、代码和用户目标组合起来生成解释，也可能因为上下文缺失或相似模式误导而给出错误归纳。

**Transformer 给了模型强大的模式组合能力，但没有给它事实最终裁决权。**
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

### [**Embedding**](https://aiweb3.school/zh/handbook/ai/llm/#embedding)

Embedding 是把文本、代码或其他对象映射成向量，用来衡量“语义上是否接近”。它常用于搜索、聚类、推荐、异常检测和 RAG。

Embedding 适合帮你从文档、知识库、代码仓库、讨论记录和产品日志中找相关材料。但它不适合单独判断“这个结论是否正确”。向量相似度只能说明内容接近，不能替代来源校验、规则检查和人工判断。

RAG 的全名是 **Retrieval-Augmented Generation**，中文通常译为“检索增强生成”或“检索增强式生成”。

它的意思是：先从外部知识库检索相关资料，再让模型基于这些资料生成回答。
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->


Token

Def：Token 是模型处理文本的基本单位。它不一定等于一个汉字、一个英文单词或一个符号，而是 tokenizer 切分后的片段。

Notice：需要决定哪些信息原样放入，哪些先压缩，哪些交给检索系统按需取回。代码、JSON、长标识符、表格和混合语言文本经常比普通段落更吃 token。
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
