---
timezone: UTC+8
---

# HanXiangQian

**GitHub ID:** Flygreenbaby

**Telegram:** @anrusi

## Self-introduction

在几年前，我曾经有一个大致的概念，网络中有一颗大树，以ai为土壤培养，其中的树枝树干，可以由世界任何一个地方访问，去做文件上传、备份等等都可以，很笼统的一个概念，我希望这次课程能够实现，也希望认同我这个想法的partner来组队。

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
📝 今日学习笔记预览 (Day 3)

\# Day 3 学习笔记：Prompt Engineering & Context Engineering

**日期**: 2026-05-20

**学习时长**: 约 2 小时

**学习主题**: Prompt 工程与 Context 工程

\---

\## 一、Prompt Engineering 核心要点

\### 1.1 核心理念

\- **Prompt 是软约束**，不是安全边界

\- 真正的安全必须由代码、权限、校验和审计保障

\- 高风险动作不能仅靠 Prompt 拦截

\### 1.2 四段式 Instruction 结构

\[任务目标\]

\[可用输入\]

\[禁止行为\]

\[输出格式 & 失败格式\]

\### 1.3 Few-shot vs Structured Output

| 特性 | Few-shot | Structured Output |

|------|----------|-------------------|

| 用途 | 风格模仿、边界模糊场景 | 固定格式供代码处理 |

| 输出 | 自由文本 | JSON/schema 约束 |

| 适用场景 | 难以一句话说清的任务 | 必须固定字段的任务 |

\### 1.4 Prompt Injection 风险

\- 外部输入可能覆盖原始规则

\- 需代码层校验 + 人工审批

\- 敏感动作通过白名单 + 人工确认

\---

\## 二、Context Engineering 核心要点

\### 2.1 核心理念

\- **Context ≠ 简单拼接**

\- 必须把系统规则、用户目标、历史状态、工具结果和外部文档分清楚

\- 每类信息要标注来源、时效、权限和可信度

\### 2.2 Context 信息来源分级

| 类型 | 可信度 | 处理方式 |

|------|--------|----------|

| 系统状态/配置 | ✅ 高可信 | 直接放入 Context 顶层 |

| 用户输入 | ⚠️ 中可信 | 需要参数校验后再使用 |

| 检索文档 | ⚠️ 中可信 | 标注来源和获取时间 |

| 工具结果 | ⚠️ 需验证 | 检查返回 schema 完整性 |

| 外部网页 | ❌ 低可信 | 隔离层处理，不可直接信任 |

\### 2.3 Memory 风险检查清单

\- ✅ 所有 Memory 条目都有明确的过期时间或撤销方式

\- ✅ 涉及钱包地址的交易记录需每次重新确认

\- ✅ 记住"用户偏好"不等同于记住"用户授权"

\- ✅ 跨会话的记忆不包含敏感凭证

\- ❌ 禁止：根据历史行为自动推断用户风险偏好

\- ❌ 禁止：长期缓存用户资产余额用于决策

\- ❌ 禁止：默认上次任务的上下文延续到下次任务

\---

\## 三、Prompt vs Context 对比

| 维度 | Prompt | Context |

|------|--------|---------|

| 核心作用 | 定义任务目标和输出格式 | 提供可信信息和边界 |

| 设计重点 | 指令清晰、格式可校验 | 来源标注、权限隔离 |

| 安全层级 | 软约束（可被覆盖） | 信息治理（分级管理） |

| 常见风险 | Prompt Injection | 信息过载、权限越界 |

| 最佳实践 | 四段式结构 + Few-shot + Structured Output | 来源分级 + 可撤销记忆 + 刷新机制 |

\---

\## 四、实践练习

\### 4.1 构建"交易风险摘要" Prompt

\- 输入：交易目标地址、函数名、参数、资产变化、模拟结果、用户原始意图

\- 输出：JSON 格式的风险分析报告

\- 测试用例：普通转账、无限授权、地址不匹配

\---

\## 五、学习收获

1\. **理解了 Prompt 的本质**：不是"怎么问"，而是可执行的通信协议

2\. **掌握了 Context 治理**：信息分级、权限隔离、可撤销记忆

3\. **识别了安全风险**：Prompt Injection、信息过载、权限越界

4\. **学会了最佳实践**：四段式结构、结构化输出、来源标注

\---

\## 六、待深入学习的问题

1\. 如何设计一个"防注入"的 Prompt 结构？

2\. 在 Agent 场景中，如何设计"上下文刷新机制"？

3\. 当 Context Window 接近上限时，优先级排序策略是什么？

\---

_学习笔记结束_

\---
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

**目录**

[前言](#%E5%89%8D%E8%A8%80)

[创建AI + Web3 学习仓库](#%E5%88%9B%E5%BB%BAAI%20+%20Web3%20%E5%AD%A6%E4%B9%A0%E4%BB%93%E5%BA%93)

[git两种工作流](#git%E4%B8%A4%E7%A7%8D%E5%B7%A5%E4%BD%9C%E6%B5%81)

[先有本地项目](#%E5%85%88%E6%9C%89%E6%9C%AC%E5%9C%B0%E9%A1%B9%E7%9B%AE)

[先有远程仓库](#%E5%85%88%E6%9C%89%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93)

[LLM 基础概念](#LLM%20%E5%9F%BA%E7%A1%80%E6%A6%82%E5%BF%B5)

[🎯 核心问题](#%F0%9F%8E%AF%20%E6%A0%B8%E5%BF%83%E9%97%AE%E9%A2%98)

[✅ 今天学到的关键理解](#%E2%9C%85%20%E4%BB%8A%E5%A4%A9%E5%AD%A6%E5%88%B0%E7%9A%84%E5%85%B3%E9%94%AE%E7%90%86%E8%A7%A3)

[1\. LLM 的运作机制](#1.%20LLM%20%E7%9A%84%E8%BF%90%E4%BD%9C%E6%9C%BA%E5%88%B6)

[2\. Control Layers 层级体系](#2.%20Control%20Layers%20%E5%B1%82%E7%BA%A7%E4%BD%93%E7%B3%BB)

[3\. Tokenizer 分词机制](#3.%20Tokenizer%20%E5%88%86%E8%AF%8D%E6%9C%BA%E5%88%B6)

[4\. Multimodal 现状](#4.%20Multimodal%20%E7%8E%B0%E7%8A%B6)

[5\. Hallucination 幻觉的本质](#5.%20Hallucination%20%E5%B9%BB%E8%A7%89%E7%9A%84%E6%9C%AC%E8%B4%A8)

[6\. Schema Validation 校验机制](#6.%20Schema%20Validation%20%E6%A0%A1%E9%AA%8C%E6%9C%BA%E5%88%B6)

[初学问题](#%E5%88%9D%E5%AD%A6%E9%97%AE%E9%A2%98)

[learning agent答案](#learning%20agent%E7%AD%94%E6%A1%88)

[第一个问题](#%E7%AC%AC%E4%B8%80%E4%B8%AA%E9%97%AE%E9%A2%98)

[第二个问题](#%E7%AC%AC%E4%BA%8C%E4%B8%AA%E9%97%AE%E9%A2%98)

[第三个问题](#%E7%AC%AC%E4%B8%89%E4%B8%AA%E9%97%AE%E9%A2%98)

[第四个问题](#%E7%AC%AC%E5%9B%9B%E4%B8%AA%E9%97%AE%E9%A2%98)

[第五个问题](#%E7%AC%AC%E4%BA%94%E4%B8%AA%E9%97%AE%E9%A2%98)

[第六个问题](#%E7%AC%AC%E5%85%AD%E4%B8%AA%E9%97%AE%E9%A2%98)

[额外提升](#%E9%A2%9D%E5%A4%96%E6%8F%90%E5%8D%87)

[结语](#%E7%BB%93%E8%AF%AD)

**前言**

经过第一天的learning agent部署，以及当晚的co-learning，我了解到许多新颖的知识，并且我认识到我所部署的hermes只是初级阶段，还能进一步提升，我决心加快基础学习，尽快享受其高阶玩法！

今天主要是根据learning agent提示的学习仓库创建（锻炼git的操作流程）、并加以整理，以及AI基础的LLM和Prompt

## **创建AI + Web3 学习仓库**

> 此步骤不再过多赘述，只记录几点新知识:

NaN.  License和.gitignore部分的作用
      
NaN.  以及github远程仓库的操作能由终端直接完全代替（这是高阶玩法）
      

## **git两种工作流**

> 理解并掌握这两种方式，几乎可以应对大部分场景了！！！

**先有本地项目**

创建项目文件夹

NaN.  初始化仓库 git init
      
NaN.  连接远程仓库 git remote add origin <repository\_url>
      
NaN.  切换并命名分支 git branch -M main
      
NaN.  添加提交文件 git add .（作用只限于当前目录，这个可以涵盖整个仓库的改变git add -A）
      
NaN.  提交说明 git commit -m 'Your commit message here!'
      
NaN.  首次推送 git push -u origin main（后面只需要 git push）
      

**先有远程仓库**

流程：远程 → 下载到本地 → 修改 → 推送

```
git clone 仓库地址
# 后续就是同样的操作了
git add .
git commit -m "说明"
git push
```

## **LLM 基础概念**

> LLM = Large Language Model （大语言模型）

**🎯 核心问题**

> 核心问题、今天学到的关键理解是由我的learning agent总结的（非常全面）

LLM 的本质是什么？它能做什么？不能做什么？

**✅ 今天学到的关键理解**

**1\. LLM 的运作机制**

-   不是"理解意图"，而是"概率性续写"
    
-   Token 序列预测下一个 Token，重复直到结束
    
-   Context Window = 工作内存（Qwen3.5 = 128K tokens）
    
-   Temperature = 随机性控制杆（0=确定，1+发散）
    

**2\. Control Layers 层级体系**

-   **Prompt**：人类全控，适合一次性问答
    
-   **Workflow**：预定义流程，中间可插人工审核
    
-   **Agent**：模型自主决策，需要人类验证输出
    

**3\. Tokenizer 分词机制**

-   不是按输入顺序编号，是预训练的词表
    
-   中文常见字 ≈ 1 token，生僻字可能切更细
    
-   代码/JSON/长标识符吃 token 是因为未针对编程优化
    
-   词汇表约 50k-100k 项
    

**4\. Multimodal 现状**

-   早期：多模态输入被编码成文本代理
    
-   现在：原生多模态模型（像素/音波直接进入统一空间）
    
-   本质不变：最终都是 Token 序列，预测下一个 Token
    

**5\. Hallucination 幻觉的本质**

-   不是道德欺骗，是训练目标 ≠ 追求真相
    
-   必须输出一个答案时选最可能的模式
    
-   解决方案：显式降级（承认不知道）
    

**6\. Schema Validation 校验机制**

-   JSON Schema / Pydantic 校验结构
    
-   Function Calling 参数合法性检查
    
-   不校验直接运行 = 高风险！
    

* * *

> 初学问题是第一遍都文档学习所疑惑的地方；

**初学问题**

> 我认为应该记忆的内容，不过我目前大脑比较混乱疲惫，故留下后续记忆。我觉得LLM的概念非常好，但我更好奇是如何实现的，把超多的文本、代码等数据和多模态信号压进概率模型，听起来像是把一个个相似的东西在一条线上放置，看谁离这条线近。我也不确定我的理解对不对。

NaN.  模型负责理解用户意图，还是生成内容？它只是在回答问题，还是能调用工具？它的错误会停留在文本里，还是会进入真实工作流？
      
NaN.  把输出变成可检查对象
      
NaN.  把不确定性前移暴露中：让系统显式降级
      
NaN.  什么是tokenizer(分词器)？
      
NaN.  代码、JSON、长标识符、表格和混合语言文本经常比普通段落更吃 token是因为模型参数问题吗？
      
NaN.  Multimodal其实还是依据文本内容进行分析的吗？（各种形式的输入）
      

**learning agent答案**

> 看到其回答，我是彻底接受了LLM是概率模型，不是事实！！！

**第一个问题**

> 模型负责理解用户意图，还是生成内容？它只是在回答问题，还是能调用工具？它的错误会停留在文本里，还是会进入真实工作流？

我一开始有疑惑，是因为我停留在LLM是概率模型的问题中，并未认识到有数据层、编排层、执行层、安全层。

总之一个公式解释LLM的本质：

给定已有序列（上下文窗口里的所有 Token） → 预测下一个最可能的 Token → 把新 Token 拼到序列末尾 → 重复直到结束

Hermes提到：**其既不"理解意图"，也不"生成内容"——它只是在做概率性的序列续写。**

其中让我真的接受其是概率模型的是它给出的一个例子：

```
打个比方：
你以为它在：
  "用户想了解 Token → 我理解了这个需求 → 我解释 Token"
​
实际上它在：
  "用户说了'什么是Token' → 我最常接的模式是解释 Token 的文章开头 → 
   输出 'Token是模型的最小文本单位...' → 接下来最可能接什么..."
```

最常接的模式？？？什么是最常接？ 不应该是最直接嘛！！！

而且对于真实工作流，我联想到day 1 的co-learning中老师提到的一些安全问题，恰如模型调用工具时输出的参数错误，未成功校验便被当作参数传入工具，传回的数据必然不可信，再进入真实工作流必然会出现安全问题。

**第二个问题**

> 把输出变成可检查对象

首先我对于可检查/校验是十分清楚的，我疑惑的地方是：模型输出如何去校验？像JS中数据类型给schema校验？

Hermes给出的解释是举例：

```
不好的用法：               好的用法：
"帮我解释Token"           "帮我解释 Token，输出 JSON 格式：
→ 自然语言段落展示          {concept: "...", mechanism: "...", 
  ✓ 但不可检查               analogy: "..."}
                            → 可以程序化检查每个字段是否合理"
```

确实，按照概率模型来讲没办法保真，只是靠近更接近，输出又不是一对一定义格式的让你校验！

疑问终结：说对了，还真就是1v1定义格式校验，只不过分的更大，规格更多。不过我对此保持观望，因为模型最后的校验必须包含很多安全问题。

**第三个问题**

> 把不确定性前移暴露中：让系统显式降级

这个问题能解决，只不过有一些特殊的疑惑，先看Hermes给出的答案：

```
# 伪代码
def agent_respond(query):
    confidence = model.evaluate_confidence(query)
    if confidence > 0.9:
        return model.generate_answer(query)
    elif confidence > 0.5:
        return model.generate_answer(query) + "\n⚠️ 建议验证以下来源..."
    else:
        return "我不确定这个问题，建议你参考官方文档..."
```

首先我能理解，就是看概率模型参数了，概率高就是你了，概率低自然而然是可信度更低的数据，直接强制输出后三行类似即可！

但是我的特殊疑惑：

NaN.  如果没有显式降级，为什么模型会给出虚假、甚至欺骗的回答（或者说输出参数）？
      

疑问终结：模型问题，因为用户输入必须要回应，如果没有相关的数据，也会按照最接近的数据输出，导 致出现错误，犯错多了，总结最后发现是其出现类似幻觉/欺骗，并不是真的幻觉/欺骗！

2.  难道模型参数概率低到一定程度必然会出现这种情况？（想必是设定了）
    

疑问终结：概率模型，要深刻理解其本质（输出必须相关，没有最最低，只有最高，即便是0.0001%）

**第四个问题**

> 什么是tokenizer(分词器)？（主要是为了理解什么是token）

显而易见，就是把输入参数分开。

Hermes的答案：

```
原始文本："我是一个AI助手"
                  ↓
Tokenizer（分词器）
                  ↓
Token序列：[我] [是] [一] [个] [AI] [助] [手]
           (3 tokens)      (2 tokens)   (2 tokens)
                  ↓
每个 Token 对应一个数字 ID
                  ↓
模型看到的是：[1123] [4567] [8901] [2345] [6789] [9876] [5432]
```

这一点我能理解，但是最后一行，如何排列？还是一定参数模型先排列吗？从第一个输入参数到最后一个输入参数，依次分配数字ID吗？

疑问终结：不是如何排列、也不是依次分配ID；要明白其是概率模型，即已经设定好了 “词表” ，输入数据会被tokenizer切分后自动按照对应 “词表” 相应数字ID，然后再去进行选择！

**第五个问题**

> 代码、JSON、长标识符、表格和混合语言文本经常比普通段落更吃 token是因为模型参数问题吗？

Hermes答案：

因为代码里有大量的标识符、特殊符号、空格缩进，Tokenizer 没有为这些优化，所以它们比自然语言"密"很多。

```
模型上下文窗口 = 128K tokens
自然语言 = 可以放 ~10 万字的书
代码 = 可能只能放几千行
混合语言 = 中间地带
```

所以这就是为什么大家疯狂使用编程模型消耗token大的原因了(0.0怪不得要花这么多钱才能体会更高的代码体验)

依旧又产生新的疑问：为什么不对编程方面进行调整，譬如说：自然语言先行处理，输出的参数直接校验转换提供给实际编程模型，再对编程模型进行tokenizer优化，那岂不是0.0（而且开源代码这么多，你懂的(～￣▽￣)～）

疑惑终结：

-   Tokenizer 对编程语言的优化不足？→ Code-specific Tokenizer 已有项目尝试
    
-   为什么不分离自然语言和编程处理？→ Plan-Execute 架构正在探索中
    

**第六个问题**

> Multimodal其实还是依据文本内容进行分析的吗？（各种形式的输入）

这个问题我彻底明白了

无论是文本还是图片、视频等，从自然语言、代码等到图片视频类的编码，不再是单一的参数比对输出。

```
Qwen3.5 / GPT-4o 等模型：
  ┌──────────────────────┐
  │ 文本 Token → 统一     │
  │ 图片 Token → 编码空间 │
  │ 语音 Token →          │
  └──────────────────────┘
           ↓
     放在一起做自回归预测
​
模型真正在看"像素"和"音波"了
```

**额外提升**

这里给出一个额外问题和答案：

问：模型怎么实现的？

答：(新词：表征学习)

```
是一个几百到几千维的"超大空间"
​
每个概念（Token、词、句子）在这个空间里有一个位置
​
相似的概念距离近：  "猫" 🐱 ──── "狗" 🐶 （近）
不相似的概念距离远：  "猫" ────────────────── "量子力学" （远）
​
"国王 - 男人 + 女人 ≈ 女王" 这个经典例子就是空间向量运算
```

## **结语**

> **LLM 生成的是概率上合理的输出，而不是天然可信的事实。**（这句话真棒！！！）

**📝 LLM收获汇总**

NaN.  ✅ 模型不关心真假，只是预测下一个 token
      
NaN.  ✅ 显式降级是为了让模型承认"我不知道"而不是瞎编
      
NaN.  ✅ Tokenizer 是预训练的词表，不是按输入顺序编号
      
NaN.  ✅ 代码吃 token 多是因为没有为代码优化的 Tokenizer
      
NaN.  ✅ 解决方案已经存在（Code-specific Tokenizer、Plan-Execute 架构）
      
NaN.  ✅ 校验靠 Schema（JSON Schema、Pydantic 等）
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->


## **目录**

[前言](#%E5%89%8D%E8%A8%80)

[部署爱马仕(Hermes)](#%E9%83%A8%E7%BD%B2%E7%88%B1%E9%A9%AC%E4%BB%95\(Hermes\))

[首先服务器推荐选择：](#%E9%A6%96%E5%85%88%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%8E%A8%E8%8D%90%E9%80%89%E6%8B%A9%EF%BC%9A)

[安装docker](#%E5%AE%89%E8%A3%85docker)

[配置镜像源](#%E9%85%8D%E7%BD%AE%E9%95%9C%E5%83%8F%E6%BA%90)

[安装爱马仕(Hermes)](#%E5%AE%89%E8%A3%85%E7%88%B1%E9%A9%AC%E4%BB%95\(Hermes\))

[出现的问题](#%E5%87%BA%E7%8E%B0%E7%9A%84%E9%97%AE%E9%A2%98)

[无法连接tg](#%E6%97%A0%E6%B3%95%E8%BF%9E%E6%8E%A5tg)

[模型的配置](#%E6%A8%A1%E5%9E%8B%E7%9A%84%E9%85%8D%E7%BD%AE)

[结语](#%E7%BB%93%E8%AF%AD)

## **前言**

我是20年考入大学的，虽说是本科，我也在26年，也就是今年才毕业，具体原因是由于在校期间学习态度过于恶劣，导致挂了许多学分（超恐怖的数量），于是花了两年左右压缩着自己赶完课业，，目前在家躺平中。

在此之前，我已经几个月没有深度的使用AI了，它的发展太快了，快到我几乎绝望；我是一个比较懒散、拖延的人，我在博客的必须技能html、css、js上迂回了好几次，本来想着再次深入学习js，顺便把ts、vue学一学。

上周碰巧在X上看到了大神 [DIYGOD](https://x.com/DIYgod) 的分享的推文，也就是本次学习课程，我选择了报名，因为AI再恐怖，我也必须拥抱它。

昨天的开营仪式很精彩，在大学时我也参加过字节跳动举办的类似夏令营/冬令营活动，但毕竟我不是专业出身，又较为懒散，也无成就可言，本来想发言，可是奈何过于羞愧，便撰写自我介绍发在了tg群组里。

今天主要部署了hermes，并打通了与tg的连接（毕竟我的服务器在大陆），就是有一点，模型的配置让我苦恼了几个小时，不过也都解决了（毕竟是免费的模型），下面记录一下我使用 docker部署learning agent> 的过程与问题：

> 注意：除了服务器，咱对于模型主打的就是一个字：白嫖！！！

## **部署爱马仕(Hermes)**

> 对于learning agent来说，无论是Hermes还是openclaw亦或者是课程中提到的其他，自行选择即可。

**首先服务器推荐选择：**

> 这是官方文档中给出的规格 详见 [Hermes](https://hermes-agent.nousresearch.com/docs/)

| 资源 | 最低限度 | 受到推崇的 |
| --- | --- | --- |
| 记忆 | 1 GB | 2–4 GB |
| 中央处理器 | 1 个核心 | 2个核心 |
| 磁盘（数据卷） | 500 MB | 2GB以上（随会话/技能提升而增长） |

我的阿里云服务器规格是：

```
CPU&内存:2H2G
带宽:3M
系统：Alibaba Cloud Linux 3.2104 LTS 64位
```

部署过程流畅，在tg上对话速度稍慢

**安装docker**

> 我是在购买服务器时便选择docker了
> 
> 问题：由于缺少相关知识，对于docker的安装我有疑问，但能解决。后面会重新整理关于docker的知识！

不过我找了一个一键脚本安装：

```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

**配置镜像源**

> 由于我的服务器在大陆所以部署Hermes时会超时，找个合适的镜像源比较好

终端切换目录找到`daemon.json`文件并打开编辑

```
cd /etc/docker # 一般安装后都在这里
ls # 会输出daemon.json
vim daemon.json # 可以使用你喜欢的编辑方式，vim操作不多赘述，浏览器自行搜索
​
# 将其中内容改成下列
​
{
  "registry-mirrors": [
                        "https://mirror.ccs.tencentyun.com",
                        "https://docker.1ms.run",
                        "https://hub.rat.dev",
                        "https://dockerpull.org"
  ]
}
​
# 记得重启生效
sudo systemctl reload docker
sudo systemctl restart docker
```

查看已经配置的镜像源：

```
docker info | grep -A 5 "Registry Mirrors"
```

**安装爱马仕(Hermes)**

> 详细依旧在 [Hermes](https://hermes-agent.nousresearch.com/docs/)

我们的项目树如下：

```
hermes/
├── data/
│   ├── config.yaml
│   ├── skills/
│   └── ...
├── docker-compose.yml
└── .env(省略)
```

提前创建目录以保持整洁

```
mkdir -p hermes/data
mkdir docker-compose.yml
```

使用vim编辑docker-compose.yml，保存退出即可

```
services:
  hermes:
    image: nousresearch/hermes-agent:latest
    container_name: hermes
    restart: unless-stopped
    command: gateway run
    ports:
      - "8642:8642"   # gateway API
      - "9119:9119"   # dashboard (only reached when HERMES_DASHBOARD=1)
    volumes:
      - ./data:/opt/data  # 如果你设置的不一样，这里也要改
    environment:
      - TZ=Asia/Shanghai  # 时区，加不加都可以，自己时区网上搜索
​
      - HERMES_DASHBOARD=1 # 面板建议开启
​
      - GATEWAY_ALLOW_ALL_USERS=true # 谁能访问面板0.0
      
      #你的tg_id
      - TELEGRAM_ALLOWED_USERS=${TELEGRAM_ALLOWED_USERS}
      
      # 下面两个无所谓，后面直接更改data/config.yaml文件设置模型
      - OPENAI_BASE_URL=${OPENAI_BASE_URL}
      - OPENAI_API_KEY=${OPENAI_API_KEY}
      
      # 根据官方文档获取输入tg_bot token将下面内容直接替换即可
      - TELEGRAM_BOT_TOKEN=${TELEGRAM_BOT_TOKEN}
​
# 下面五行代码后续问题中会提到，先别使用
     # - HTTP_PROXY=http://host.docker.internal:7890
     # - HTTPS_PROXY=http://host.docker.internal:7890
     # - ALL_PROXY=socks5://host.docker.internal:7890
​
    #extra_hosts:
     # - "host.docker.internal:host-gateway"
​
networks:
  default:
    driver: bridge
```

执行 `docker compose up -d` 启动

访问 `http://IP:9119` 便可看到面板了，那么恭喜你，成功部署Hermes，这位还可以的learning agent

模型配置这里就不多赘述！请看下面 ↓

## **出现的问题**

在部署过程中出现了各种各样的问题，毕竟我是零基础，且环境不一样啊，只能遇到问题解决问题，这里总结一下比较困难的问题。

> 自建节点可以看一下我之前的博客 [ahyun的爱孤岛](https://ahyun.org.cn/projects/self-built-node-record/)

**无法连接tg**

由于服务器在大陆所以爱马仕即便部署成功，也很难访问到tg

不信你可以执行一下下面的命令：

```
curl https://api.telegram.org
```

你看看有没有反应0.0(～￣▽￣)～

接下来就是给服务器走一个代理（切莫自建节点违规使用，本文档只做学习记录）

我选择的是docker部署一个singbox来让Hermes独享我自建的节点

同样：

```
# 创建目录
mkdir -p ~/proxy-singbox
cd ~/proxy-singbox
# 配置，这部分不多赘述（你会自建节点就会这部分），可以自行ai学习
vim config.json
# 配置镜像 将下面复制进去
vim docker-compose.yml
​
services:
  sing-box:
    image: ghcr.io/sagernet/sing-box:latest
    container_name: sing-box
    restart: unless-stopped
​
    volumes:
      - ./config.json:/etc/sing-box/config.json
​
    command: run -c /etc/sing-box/config.json
​
    ports:
      - "7890:7890"
      
      
# 最后点火启动
docker compose up -d
```

再把上面注释掉的部分启用配合使用

不用测试，去面板刷新就能看到tg连接成功了。

**模型的配置**

这部分我是使用阿里百炼提供的几十个模型（每个都有100万token），配置了一下午，最后也搞定了，也很方便切换。对于这方面我很是疑惑，无论是之前的龙虾，还是其他的工具，对于模型的调用究竟是如何运作的，我想这一点明白后，大概率没有这个问题了。

先说我的方案：

阿里百炼获取key → vim编辑data/config.yaml文件 →

更改其部分内容：(注释很多，在其中找对应输入即可)

```
model:
  default: qwen3.5-flash # 你想先使用的模型 比如 qwen3.5-flash
  provider: custom
  api_key: your-key
  base_url: https://dashscope.aliyuncs.com/compatible-mode/v1
```

在tg中如果遇到模型token使用完，可以输入 `/model 模型` 来直接更改（就能继续白嫖了0.0），再输入对话即可！

其中在课程网站 → 个人资料页 最下方的key，到现在我不知道这个是干啥用的0.0超疑惑！！！

## **结语**

今天学习任务其实很少，因为我没有仔细的去阅读学习页面，不过嘛，些许知识的翻涌罢了，大家肯定能跟我一样速度灌输近脑海的。

对了，记得给你的 learning agent 加上课程专属 skill (在对话框直接输入)

```
请作为我的 AI × Web3 School Learning Agent，先阅读启动 Prompt：https://aiweb3.school/learning-agent.zh.txt，并结合 Handbook：https://aiweb3.school/zh/handbook/，帮我初始化个人学习计划、GitHub 学习仓库、每日打卡草稿和 Handbook feedback 流程。
```
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
