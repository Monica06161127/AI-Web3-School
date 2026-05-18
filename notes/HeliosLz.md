---
timezone: UTC+8
---

# Helios

**GitHub ID:** HeliosLz

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->
**Hermes 从 0 到 1 教程**  
  
它最大的特点是**内置学习循环**：**每次完成任务后，它会自动从经验中提炼出可复用的 Skill，存入持久记忆，下次遇到类似任务时会自动改进和调用。**

这个记忆是持久的，能逐步构建对你的“用户模型”。它是一个能自主成长的代理，常用于长期项目辅助、自动化任务、研究等。  
  
最简单的解释  
  
想象你有一个**超级聪明的助手**。普通助手是这样的：你说"帮我订披萨"，他订了，然后就忘了这件事。下次你还得重新说一遍。

**Hermes Agent 更像一个会成长的学徒：**

> 你第一次教他怎么订披萨，他不仅做了——他还**把这个技能写进了笔记本**。下次你不用教了，他自己就知道怎么做。而且每次做，他都在想"我上次怎么做的？有没有更好的方法？"

三个关键点：

-   🧠 **记忆** — 他记得你们之前聊过什么
    
-   📚 **技能本** — 他把学到的方法存起来，以后复用
    

🔄 **自我改进** — 他越用越聪明，不是每次从零开始

```
普通Agent vs Hermes Agent：

普通Agent：
大模型 → 决定用哪个工具 → 调用工具 → 返回结果
（每次都一样，没有成长）

Hermes Agent：
大模型 → 决定用哪个工具 → 调用工具 → 返回结果
              ↓
        "这个流程有用！写进技能本"
              ↓
        下次直接调用技能，更快更准
              ↓
        还会问自己：这个技能能改进吗？
```

### 它怎么"记住"东西？

Hermes有**三层记忆**，就像人类一样：  

| 层级 | 类比 | 技术实现 |
| --- | --- | --- |
| 短期记忆 | 当前对话内容 | Context Window |
| 长期记忆 | 你的日记本 | 跨Session持久化存储 |
| 用户模型 | 对你这个人的理解 | Honcho dialectic modeling |

关键工程思维：**记忆不是简单存储，而是带索引的检索**——用FTS5全文搜索+LLM摘要，让Agent能从大量历史中快速找到相关片段。

类比：不是把所有日记都读一遍，而是有个聪明的图书管理员帮你找关键页。

### 技能（Skills）到底是什么？

这是Hermes最有意思的设计！

> 技能 = **Agent自己写给自己看的操作手册**

具体来说，一个技能就是一个`SKILL.md`文件，里面写着：

-   这件事是什么
    
-   怎么一步步做
    
-   踩过哪些坑
    
-   什么时候该用它
    

```
工程思维关键点：

第一次做某件事 → 摸索完成
      ↓
Agent判断："这个值得记录吗？"
      ↓
自动生成SKILL.md
      ↓
第二次遇到类似任务 → 直接读技能文件
      ↓
做完后："这次有没有更好的做法？" → 更新技能文件
```

  
Hermes的设计哲学可以用一句话概括：

> **"不要每次从零开始，要把经验变成资产。"**

留给自己的作业：  
  
如果Hermes Agent帮你完成了一个"自动整理邮件"的任务，它在背后经历了哪几个步骤？它下次再做类似任务时，会有什么不同？

官方资源：

-   主站与文档：
    
    [https://hermes-agent.nousresearch.com/docs/](https://hermes-agent.nousresearch.com/docs/)
    
-   Quickstart：
    
    [https://hermes-agent.nousresearch.com/docs/getting-started/quickstart/](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart/)
    
-   GitHub：
    
    [https://github.com/NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
