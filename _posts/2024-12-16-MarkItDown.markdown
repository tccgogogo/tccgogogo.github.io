---
layout: post
title: "微软又放大招了！MarkItDown：轻松转换为Markdown的神器"
subtitle:   "Python Markitdown"
date:       2024-12-16 12:00:00
author:     "tiancc"
header-mask: 0.3
catalog:    true
tags:
    - RAG
    - LLM
---


微软最新开源的 Python Markitdown 工具，能将 PDF、Office 文档（Word/PPT/Excel）、图片、音频等多种格式的文件智能转换为 Markdown 格式，支持 OCR 文字识别、语音转文字和元数据提取等功能，特别适合文档分析和内容索引场景。

项目地址：https://github.com/microsoft/markitdown
![](/img/markitdown/main.png)


## 主要功能
- 将各类文档自动转换为 Markdown 格式
- 特别适合做文本分析和内容索引
- 提供了简单易用的 Python API

## 支持的文件格式
- 办公文档：Word、PowerPoint、Excel
- PDF 文件
- 图片（可提取 EXIF 元数据，支持 OCR 文字识别）
- 音频文件（可提取元数据，支持语音转文字）
- 网页内容（对维基百科等网站有特殊优化）
- 其他文本格式（CSV、JSON、XML 等）

## 使用方法
安装首先，通过 pip 安装工具：

```
pip install markitdown
```
用 Python 调用并转换文件内容：
```
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("test.xlsx")
print(result.text_content)
```
要使用大型语言模型进行图像描述，请提供llm_client和llm_model：


```
from markitdown import MarkItDown
from openai import OpenAI

client = OpenAI()
md = MarkItDown(llm_client=client, llm_model="gpt-4o")
result = md.convert("example.jpg")
print(result.text_content)
```


