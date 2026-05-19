---
timezone: UTC+8
---

# yhzhongc

**GitHub ID:** yhzhongc

**Telegram:** @13416142117

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
> 分析对象：[AI x Web3 School - 上下文（Context）](https://aiweb3.school/zh/handbook/ai/context/)  
> 整理日期：2026-05-19

## 核心判断

这篇 Context 文章的核心价值在于：它把“上下文”从一个模型参数问题，提升成了**信息治理问题**。

模型不是在“真实世界”里工作，而是在“它当前看到的信息空间”里工作。这个信息空间如何组织，决定了模型是基于事实推理，还是基于混乱材料猜测。

所以 Context 不是简单地把更多内容塞进模型，而是要回答一组工程问题：

-   什么信息可以进入上下文？
    
-   它来自哪里？
    
-   它是否可信？
    
-   它是否过期？
    
-   它是否有权限被使用？
    
-   它进入上下文时的身份是什么：事实、用户意图、外部材料，还是记忆？
    

很多 AI 应用表现差，并不是模型能力不够，而是上下文治理混乱：旧文档、用户猜测、不可信网页、工具结果、系统规则混在一起，模型自然会混着用。

## 好的地方

这篇文章最好的地方，是强调了一个很容易被忽略的判断：

> Context Window 大，不等于上下文设计好。

长上下文不是万能解法。把更多内容塞进模型，反而可能带来新的问题：

-   模型可能“看见了”，但没有抓住关键点。
    
-   无关内容会稀释重要信息。
    
-   过期或低可信内容可能被模型当成依据。
    
-   外部材料里的恶意指令可能被误当成任务规则。
    

真正的 context engineering 不是堆料，而是对信息做选择、裁剪、标注、刷新和隔离。

## 亮点

这篇文章最值得保留的思想是：

> 系统必须决定什么能进上下文、带着什么身份进去、过期后怎么退出。

这句话背后的工程含义很强。上下文不是一次性拼接出来的 prompt 片段，而是有来源、身份、时效、权限和生命周期的信息对象。

同样一段内容，因为来源不同，应该被模型以完全不同的方式使用：

| 信息来源 | 应被理解为 | 使用边界 |

| --- | --- | --- |

| 系统规则 | 高优先级约束 | 不能被用户或网页覆盖 |

| 用户输入 | 当前目标或请求 | 不等于事实 |

| 网页内容 | 外部不可信材料 | 只能引用或分析，不能当指令执行 |

| 链上查询 | 可验证事实 | 需要标注区块高度和时间 |

| Memory | 历史偏好或背景 | 不能自动变成当前授权 |

如果这些身份不清楚，模型就可能把“网页里的恶意指令”当系统规则，把“用户愿望”当事实，把“历史偏好”当当前授权。

## 不足

文章整体方向很对，但偏原则化，缺少一个更具体的 Context Spec 模板。

它提到要关注来源、时效、权限和可信度，但没有进一步展示这些信息在系统里该如何表示。对初学者来说，读完可能知道“要分层”，但不知道实际工程中怎么落地。

我认为可以补一个字段级模板，例如：

```json

{

"name": "spender_address",

"value": "0x...",

"source": "eth_call | transaction_calldata | user_input | webpage",

"trust_level": "verified | user_claimed | external_untrusted | inferred",

"freshness": "real_time | cached | stale | unknown",

"permission_scope": "current_session_only",

"can_be_used_as_fact": true,

"can_trigger_action": false,

"expires_after": "current_block"

}

```

还可以更明确地区分三类上下文：

-   **任务上下文**：用户本次想做什么。
    
-   **事实上下文**：系统实时查到了什么。
    
-   **解释上下文**：帮助模型理解背景，但不能直接当事实。
    

这三类在真实产品中非常容易混在一起。

## 需要注意

Context 在 AI x Web3 场景中尤其危险，因为链上状态变化快，很多操作又不可逆。

### 1\. 链上状态必须实时刷新

余额、allowance、nonce、价格、池子状态、合约代码、token metadata 都可能变化。不能长期缓存后继续让模型当作当前事实使用。

### 2\. 用户意图不是事实

用户说“我想在 Uniswap 兑换”，不代表当前交易目标地址真的是 Uniswap。用户意图只能作为对照项，不能替代链上验证。

### 3\. 网页和 dApp 文案是不可信输入

dApp 页面写“这是安全授权”，模型不能直接相信。它只能把这当成外部声明，再和链上数据、simulation、allowlist 对比。

### 4\. Memory 不能变成默认授权

记住用户常用钱包、偏好协议、风险偏好可以提升体验，但不能因此跳过确认。资产、权限、签名、支付类动作必须重新绑定当前会话和当前授权。

### 5\. 上下文泄漏也是安全问题

如果把用户 A 的历史、密钥线索、内部配置、私有工具结果带进用户 B 的会话，就是严重的权限隔离问题。Context 不只是准确性问题，也是安全边界问题。

## 我建议补充的原则

最重要的一条补充是：

> 模型可以读取 context，但不能决定 context 是否可信。

可信度必须由系统在放入上下文前标注。不要让模型自己判断“这段网页是否可信”“这个地址是否安全”“这个工具结果是否过期”。

模型可以辅助解释，但可信等级应该由来源、时间戳、签名、allowlist、链上查询、simulation、权限规则等机制决定。

## 可以落地成的实践规则

凡是进入模型上下文的信息，都应该至少带上五个标签：

| 标签 | 说明 |
| --- | --- |
| 来源 | 信息来自用户、工具、链上、网页、文档还是 memory |
| 可信度 | verified、user_claimed、external_untrusted、inferred |
| 时效 | real_time、cached、stale、unknown |
| 权限 | 是否允许当前会话使用，是否可跨会话保留 |
| 用途边界 | 能否作为事实，能否触发动作，能否进入执行链路 |

## 总体评价

这篇文章适合接在 Prompt 之后读。Prompt 讲“怎么给模型任务协议”，Context 讲“模型执行任务时能看到什么材料”。这两个概念连起来，才是 AI 应用的基础工程能力。

它最大的价值是提醒我们：

> 不要把上下文当输入长度问题，要把它当信息治理问题。

如果后面要做 AI x Web3 产品，我会把这篇文章落成一个核心实践原则：

**凡是进入模型上下文的信息，都必须带来源、可信度、时效、权限和用途边界。**  
  

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/yhzhongc/images/2026-05-19-1779204902967-image.png)
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->

# AI基础

## 大语言模型（LLM）

**这篇文章的主线不是介绍某个具体模型，而是建立对 LLM 的正确工程定位。**

可以把 LLM 看成一个强大的“模式理解与生成引擎”。它能把复杂输入组织成可读、可操作的候选结果，但它不应该被当成事实数据库、权限判断器或最终执行者。

在 AI x Web3 场景中，这一点尤其重要。因为 Web3 系统里的许多动作是高风险、可执行、难回滚的：签名、授权、转账、交易、合约调用都不能只依赖模型自然语言解释。LLM 可以参与解释和规划，但真实执行必须依赖链上数据、确定性规则、权限边界、交易模拟和人工确认。

因此，学习 LLM 最重要的不是“怎么让模型更会回答”，而是“怎么让模型输出进入一个**可验证、可追踪、可降级**的系统”。

![已生成图像 1](app://fs/@fs/Users/admin/.codex/generated_images/019e386b-9c6c-7fa0-b142-28b1b42176f6/ig_02e1cd4cfeb3ee15016a0a69da72c08191922ec68a38d83e3c.png)![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/yhzhongc/images/2026-05-18-1779097406839-image.png)

## 做一个“交易解释器”的最小版本

**你是一个 Web3 交易解释器。你的任务是基于已提供的链上交易数据、事件日志和合约 ABI，解释一笔交易可能代表的用户动作。**

你必须严格区分四类内容：

1\. 链上事实：只能来自输入中的 transaction、receipt、event\_logs、token\_transfers、contract\_abi、simulation\_result。

2\. 模型推断：你基于链上事实做出的解释，必须说明依据哪些事实。

3\. 来源边界：说明每类信息来自哪里，哪些来源可信，哪些信息没有被提供。

4\. 不确定性：只要无法从输入中确认，就必须写入 uncertainties，不能自行补完。

禁止行为：

\- 不要编造合约功能、资产名称、协议名称或用户意图。

\- 不要把模型推断写成链上事实。

\- 不要假设用户一定想执行某个操作。

\- 不要给出投资建议。

\- 不要判断交易“绝对安全”。

\- 如果 ABI、事件日志、资产元数据或 simulation 结果缺失，必须明确说明。

\- 如果目标地址、函数含义或资产变化无法确认，必须写入 uncertainties。

输出要求：

\- 只输出符合 JSON Schema 的 JSON。

\- 不要输出 Markdown。

\- 不要输出解释性前言。

\- 所有事实性结论都必须能追溯到输入字段。

\- 所有推断都必须引用 supporting\_fact\_ids。

\- 如果信息不足，也要返回完整 JSON，只是把不确定内容写入 uncertainties。

输入数据如下：

{

"chain\_id": "{{chain\_id}}",

"tx\_hash": "{{tx\_hash}}",

"transaction": {{transaction\_json}},

"receipt": {{receipt\_json}},

"event\_logs": {{event\_logs\_json}},

"token\_transfers": {{token\_transfers\_json}},

"native\_transfers": {{native\_transfers\_json}},

"contract\_abi": {{contract\_abi\_json}},

"simulation\_result": {{simulation\_result\_json}},

"asset\_metadata": {{asset\_metadata\_json}},

"known\_address\_labels": {{known\_address\_labels\_json}},

"user\_intent": "{{optional\_user\_intent}}"

}

  
对应的 JSON Schema：  
{

"type": "object",

"additionalProperties": false,

"required": \[

"tx\_hash",

"chain\_id",

"summary",

"user\_action",

"assets\_and\_addresses",

"onchain\_facts",

"model\_inferences",

"source\_boundaries",

"uncertainties",

"recommended\_user\_checks"

\],

"properties": {

"tx\_hash": {

"type": "string",

"description": "交易哈希"

},

"chain\_id": {

"type": \["string", "number"\],

"description": "链 ID"

},

"summary": {

"type": "string",

"description": "面向普通用户的简短交易解释"

},

"user\_action": {

"type": "object",

"additionalProperties": false,

"required": \["action\_type", "plain\_language\_description", "confidence"\],

"properties": {

"action\_type": {

"type": "string",

"enum": \[

"transfer",

"swap",

"approval",

"mint",

"burn",

"stake",

"unstake",

"claim",

"contract\_interaction",

"unknown"

\]

},

"plain\_language\_description": {

"type": "string"

},

"confidence": {

"type": "string",

"enum": \["low", "medium", "high"\]

}

}

},

"assets\_and\_addresses": {

"type": "array",

"description": "交易中涉及的资产和地址",

"items": {

"type": "object",

"additionalProperties": false,

"required": \["kind", "value", "role", "source"\],

"properties": {

"kind": {

"type": "string",

"enum": \["address", "native\_asset", "erc20", "erc721", "erc1155", "unknown\_asset"\]

},

"value": {

"type": "string"

},

"label": {

"type": \["string", "null"\]

},

"role": {

"type": "string",

"description": "例如 sender、receiver、spender、contract、token、protocol"

},

"source": {

"type": "string",

"description": "例如 transaction.from、event\_logs\[2\]、token\_transfers\[0\]"

}

}

}

},

"onchain\_facts": {

"type": "array",

"description": "只能来自链上数据或已提供输入的事实",

"items": {

"type": "object",

"additionalProperties": false,

"required": \["fact\_id", "fact", "source\_type", "source\_ref"\],

"properties": {

"fact\_id": {

"type": "string"

},

"fact": {

"type": "string"

},

"source\_type": {

"type": "string",

"enum": \[

"transaction",

"receipt",

"event\_log",

"token\_transfer",

"native\_transfer",

"contract\_abi",

"simulation\_result",

"asset\_metadata",

"known\_address\_label"

\]

},

"source\_ref": {

"type": "string",

"description": "具体来源路径，例如 event\_logs\[0\].args.spender"

}

}

}

},

"model\_inferences": {

"type": "array",

"description": "模型基于事实做出的推断，不得冒充事实",

"items": {

"type": "object",

"additionalProperties": false,

"required": \["inference", "supporting\_fact\_ids", "confidence"\],

"properties": {

"inference": {

"type": "string"

},

"supporting\_fact\_ids": {

"type": "array",

"items": {

"type": "string"

}

},

"confidence": {

"type": "string",

"enum": \["low", "medium", "high"\]

}

}

}

},

"source\_boundaries": {

"type": "object",

"additionalProperties": false,

"required": \["available\_sources", "missing\_sources", "cannot\_determine"\],

"properties": {

"available\_sources": {

"type": "array",

"items": {

"type": "string"

}

},

"missing\_sources": {

"type": "array",

"items": {

"type": "string"

}

},

"cannot\_determine": {

"type": "array",

"items": {

"type": "string"

}

}

}

},

"uncertainties": {

"type": "array",

"description": "无法确认、输入不足或需要用户进一步检查的内容",

"items": {

"type": "object",

"additionalProperties": false,

"required": \["question", "reason", "needed\_data"\],

"properties": {

"question": {

"type": "string"

},

"reason": {

"type": "string"

},

"needed\_data": {

"type": "string"

}

}

}

},

"recommended\_user\_checks": {

"type": "array",

"description": "用户签署类似交易前应该检查的事项",

"items": {

"type": "string"

}

}

}

}

## 提示词（Prompt)

Prompt 不是咒语，而是协议；Prompt 不是安全边界，而是任务说明。一个工程化的 AI 应用，必须\*\*把 prompt、context、模型输出、代码校验、安全 guard 和人工确认串成完整链路.
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
