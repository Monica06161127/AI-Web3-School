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
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
\# 2026-05-20 学习日志

\## 今日主题

\*\*智能合约（Smart Contract）\*\* —— \[Handbook 章节\]([https://aiweb3.school/zh/handbook/web3/smart-contract/](https://aiweb3.school/zh/handbook/web3/smart-contract/))

cohort Week 1 / Web3 侧打基础。

\## Agent 整理的精炼摘要（读完 Handbook 后用自己的话再写一遍）

\*\*一句话\*\*：合约 = 部署在链上的程序。把规则、资产、状态放进公开可验证的执行环境 —— 同时把错误、权限和升级风险也暴露给所有人。

\*\*第一性原理\*\*：合约的价值来自\*\*可验证执行\*\*，不是"代码看起来聪明"。三条引申：

\- 状态公开可查（链上不是私有 DB）

\- 调用有成本和顺序（gas / 区块顺序 / 外部状态影响）

\- 权限必须显式（mint / pause / upgrade / withdraw 不能靠默认信任）

\*\*5 个知识节点\*\*：

| 节点 | 难度 | 一句话 |

|---|---|---|

| \*\*Solidity\*\* | 初级 | EVM 合约语言。关键：storage / msg.sender / modifier / event / external call / revert / 权限控制 |

| \*\*EVM\*\* | 中级 | 合约执行环境。解释 gas 贵、storage 贵、外部调用风险、多链兼容来源 |

| \*\*ABI\*\* | 初级 | "能调用什么"的机器可读接口。\*\*不是\*\*安全说明书。是 Agent 理解合约能力的关键上下文 |

| \*\*Event\*\* | 初级 | 合约对外的可索引日志。前端列表/历史/看板大多读 event 不直接读 storage |

| \*\*Upgrade\*\* | 高级 | "可升级 vs 不可升级"的权衡。判断升级风险 4 问：升级权限谁手里 / 用户能否提前看提案 / 升级能否改资产/权限逻辑 / 管理员密钥泄漏最坏结果 |

\*\*一次调用怎么发生\*\*（vote(proposalId) 为例）：

\`\`\`

前端读钱包+网络 → 前端用 ABI 编码 vote(proposalId) → 钱包确认签名

→ 广播到 RPC 节点 → 验证者打包进区块 → EVM 执行

↳ 成功：更新 storage + emit event

↳ 失败：revert

→ 前端监听回执 → 索引器读 event 更新看板

\`\`\`

\*\*5 个常见错误\*\*：

1\. view 函数和写交易混（读不需签名，写需要）

2\. 没处理 decimals（amount ≠ 用户看到的 "1.5"，是按 decimals 放大的整数）

3\. 只测成功路径（权限/余额/重复/过期/暂停都得测）

4\. owner 当永远可信

5\. 忽略事件设计

\*\*AI × Web3 中的位置\*\*：

\> AI 做建议和编排，钱包做授权确认，合约做可验证执行，监控系统记录结果。

即使 AI 输出不稳定，链上规则仍有明确边界。

\## 我用自己的话复述（边讲边问模式，对话中已完成）

\> 今天换了模式：没有先读再答，是 Agent 一节一节讲，每节我答一题。下面是对话中真实输出过的我的版本（不是 Agent 摘要）。

\- \*\*第一性原理\*\*：合约 vs Web 后端最锋利的差别是"\*\*事先能验证规则\*\*" —— 链上合约源码公开，部署前就能读"付款 = 转账 + emit Paid 事件"；Web 后端代码私有，你只能信"机构事后裁决"。所以"可验证执行"指\*\*任何人 + 任何时间 + 链上交易记录 + 链上规则源码\*\*四件一起公开。

\- \*\*Solidity / `msg.sender` 为什么最关键\*\*：所有权限判断如果不显式绑定它，合约就无从知道"谁在操作"—— 它是 Solidity 给你的\*\*唯一\*\*身份原语，没有 HTTP header / session / JWT 这种东西。

\- \*\*EVM / 无限循环\*\*：不是被拒绝执行，是\*\*先付 gas 后执行\*\*，超出 gas limit 自动 out-of-gas → revert，但 gas 不退。这是 EVM 的"经济熔断"，让 EVM 敢执行陌生合约。

\- \*\*ABI / 自动转账最容易踩的坑\*\*：decimals 单位 —— Agent 看 ABI 调 `transfer(to, 100)` 以为转 100 USDC，实际转 0.0001 USDC（USDC decimals=6）。ABI \*\*不告诉你\*\* decimals，必须先调 `decimals()` 读再放大。

\- \*\*Event vs Storage / 审计\*\*：链上审计核心需求是"可追溯、不可篡改的行为日志"。Event 写 transaction log，成本低 + 永久存档；Storage 可被后续交易覆盖 + Gas 贵很多。\*\*拿最贵的资源做最不该被修改的事 = 错配\*\*。

\- _Agent 补的 nuance_：合约自己读不到 event。所以场景判断 = 合约自己要读 → storage；链外读 → event；两者都要 → 双写。

\- \*\*Upgrade 4 问 audit / "我们通过多签控制升级" 这句话\*\*：

\- Q1 多签几/几 没说

\- Q2 用户能提前看 没说

\- Q3 能改资产逻辑吗 没说

\- Q4 密钥泄漏后果 没说

\- \*\*判断：4 问回答了 ≈ 0.25/4。这句话是信号词，不是承诺。\*\*

\*\*今日 best\*\*（综合题）：构造了一个用满 5 节点的攻击场景 —— 透明代理 + 无 timelock 升级，把 withdraw() 提款逻辑换成转给攻击者地址。\*\*关键洞察\*\*："日志里有 Event 留痕，但资金已经走了" → \*\*可验证 ≠ 安全\*\*。Event = 事后追溯，Solidity/EVM/ABI = 发生时，\*\*Upgrade = 发生前\*\*（最可怕，改的是规则本身）。三个时间轴都要审才完整。

\## 读 Handbook 时的 scratchpad

\> 今天没用上 —— 因为没读 Handbook 自己，而是走"Agent 边讲边问"模式。

\> 元观察：这模式让"嗯？"瞬间被实时纠正了（Agent 立刻在下一句话补），所以本来想记的点都消化在对话里了。

\> 后续观察：是不是边讲边问比闭卷读 + 复述更高效？需要再过几天看对比。

\## 今日最小实验

\*\*今天没做\*\* —— 选择把时间留在对话引导 + 打卡。

\*\*Follow-up 转化\*\*：原计划的 etherscan 读 USDC 推迟。考虑明天 Account Abstraction 后做"读 AA 钱包合约 + 对比 USDC"组合实验 —— 一举两得。

\## 我的卡点

\- 今天没卡（边讲边问模式实时纠错了），但 \*\*元观察待验证\*\*：边讲边问 vs 闭卷读+复述，哪种长期更高效？需要再过几天对比。

\- ✋ 还想自己确认的点：\*\*透明代理 vs UUPS 代理 vs Beacon 代理\*\*的区别 —— 今天 Upgrade 节点只讲了 transparent proxy，没区分模式。下次读到 OpenZeppelin Upgrades 文档时补。

\## Follow-up

\- \[ \] etherscan 读 USDC 合约（今天推迟到明天，和 AA 合约一起做对比实验）

\- \[ \] \*\*AI × Web3 联想\*\*：把今天的"三时间轴 audit 框架"（事前 Upgrade / 事中 Solidity-EVM-ABI / 事后 Event）写成一个 hackathon 候选项目雏形 —— \*\*Web3 合约审计 Agent\*\*，用 Handbook 4 问 + 三时间轴当 prompt 框架。归到 `hackathon/ideation.md`。

\- \[ \] OpenZeppelin Contracts / Upgrades 文档 —— Handbook 给的扩展阅读，作为 Solidity / Upgrade 节点的深化。

\## Handbook / 课程反馈

\- \[ \] 建议：Upgrade 节点里如果能加一段对比 transparent / UUPS / Beacon proxy 的快速表格，对学员更友好（现在 4 问框架很好，但读者可能不知道这 4 问应用到哪种 proxy 模式）。考虑整理成正式 feedback 进 `handbook-feedback/`。

\## 打卡草稿（粘到 [intensivecolearn.ing](http://intensivecolearn.ing) Check-in 表单的 Markdown）

\`\`\`markdown

\*\*智能合约（Smart Contract）—— 第一性原理与三时间轴 audit 框架\*\*

今天读 Handbook 智能合约章节，最锋利的认知：\*\*合约 vs Web 后端的本质差别不是"自动化"或"去中心化"，而是事先能验证规则\*\*。Web 后端代码私有，你只能事后让支付机构裁决；合约源码公开，部署前就能确认"付款=转账+emit Paid 事件"。"可验证执行" = 任何人 + 任何时间 + 链上交易记录 + 链上规则源码，四件一起公开。

走完 5 个节点：Solidity`msg.sender` 是合约\*\*唯一\*\*身份原语，没有 HTTP/session/JWT）、EVM（gas 不是技术限制，是\*\*经济熔断保险丝\*\*，让节点敢执行陌生合约）、ABI（机器可读接口，但\*\*不告诉你\*\*安全性 —— Agent 调 `transfer(to, 100)` 没读 decimals 就把 100 USDC 转成 0.0001 USDC）、Event（拿最贵的 storage 做最不该被修改的事 = 错配；审计应该用 event 写 transaction log）、Upgrade（产品分"可升级"和"不可升级"两类，不是同一种产品的两种实现）。

最重要的产出是\*\*三时间轴 audit 框架\*\*：把 5 节点按"调用时间轴"重排 → Solidity/EVM/ABI 管"发生时"、Event 管"发生后"、\*\*Upgrade 管"发生前"\*\*。Upgrade 是最可怕的一类风险，因为它改的是\*\*规则本身\*\*：今天有人用透明代理 + 无 timelock 升级，把 withdraw 逻辑换成转给攻击者地址 —— 日志里 Event 留痕，但\*\*资金已经走了\*\*。这是 Handbook 第一性原理隐含但没显式写的关键洞察：\*\*可验证 ≠ 安全\*\*。

实操收获：Handbook 给的 Upgrade 4 问（升级权限谁手里 / 用户能否提前看 / 能改资产逻辑吗 / 密钥泄漏最坏结果）今天用一个真实信号词"我们通过多签控制升级"反向 audit，结果 4 问回答了 ≈ 0.25/4 —— 这是产品方常用的安全话术，但只是信号词不是承诺。下次看到一律追问到底。

明天主题 Account Abstraction，正好把 etherscan 读合约的最小实验和 AA 钱包合约对比做。

\`\`\`

\- 提交入口：[https://intensivecolearn.ing/en](https://intensivecolearn.ing/en) → 登录 → AI × Web3 School → 左侧 "Check-in"

\- 提交后回填提交时间 / 截图：
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

\# 2026-05-19 学习日志

\## 留给自己的作业

如果 Hermes Agent 帮你完成了一个"自动整理邮件"的任务，它在背后经历了哪几个步骤？它下次再做类似任务时，会有什么不同？  

\- 第一次：用 LLM 决定调用什么工具 → 调用邮件 API → 返回结果 → 判断"这个流程有用 → 生成 [SKILL.md](http://SKILL.md) 描述步骤、入参、典型陷阱"

\- 第二次：检索到 skill → 直接按 skill 步骤执行 → 完成后自问"这次有没有更好的写法" → 增量更新 skill

\- 关键差异：从"每次让 LLM 重新推理工具序列"变成"读已有 skill + 必要时小幅改写"，token 成本和延迟都下降。  

\## 今日主题

\*\***模型上下文协议（MCP）**\*\* —— \[Handbook 章节\]([https://aiweb3.school/zh/handbook/ai/mcp/](https://aiweb3.school/zh/handbook/ai/mcp/))

\## Agent 整理的精炼摘要（看完 Handbook 后用自己的话再写一遍）

\*\***一句话**\*\*：MCP 把"模型 ↔ 外部工具/数据/上下文"的连接标准化成协议，让工具接入变得可描述、可发现、可限制。

\*\***第一性原理**\*\*：模型不应该直接拥有世界，应该通过明确协议访问被授权的上下文和工具。

\*\***4 个知识节点**\*\*：

| 节点 | 它是谁 | 设计要点 |

|—|—|—|

| \*\***Server**\*\* | 提供能力的一侧（暴露 resources / tools / prompts） | 边界：只读 vs 副作用、schema 清晰、错误明确、需否授权、审计日志 |

| \*\***Client**\*\* | 连接模型和 server（IDE / Agent runtime / 聊天客户端） | 发现能力 → 传给模型 → 用户确认 → 权限提示 → 会话隔离 |

| \*\***Tool Schema**\*\* | 描述工具名 / 用途 / 参数 / 返回 / 约束 | 不只是字段类型：何时用、参数含义、必填、是否改外部状态、失败返回什么 |

| \*\***Permission**\*\* | 最容易被低估 | 区分：只读/写、会话/长期、需否确认、敏感访问、可撤销、可审计 |

\*\***AI × Web3 中的位置**\*\*：

\- ✅ MCP 可作为 Agent 接链上工具的接口层：读区块浏览器、查合约文档、调 RPC、生成交易草稿

\- ❌ MCP \*\***不是**\*\*钱包安全方案 —— 最终权限和执行边界归 Web3 账户系统

\- 稳的设计 = MCP（工具发现/调用格式）+ Web3 账户系统（最终权限/执行边界）

\## 我用自己的话复述（读完 Handbook 后填）

\- \*\***Server**\*\*：提供能力的一侧。暴露 resources / tools / prompts 给 Client，用 schema 描述。设计要点是边界 —— 哪些暴露、哪些只读、哪些有副作用、错误怎么返回、要不要授权。

\- _自我纠错_：第一次把"tools"错答成"协议"；漏了 schema 这个关键词。

\- \*\***Client**\*\*：夹在模型和 Server 中间的"外壳层"，本身不思考也不执行业务。例：Claude Code / Cursor / ChatGPT Desktop（Claude 这个模型本身\*\***不是**\*\* Client）。

\- 3 步搬运：①从 Server 拉工具清单 ②把清单递给模型 ③双向中转模型的调用请求和 Server 的返回。

\- 4 件用户那一面的事（容易漏）：用户确认、权限提示、会话隔离、工具调用展示 —— 因为模型看不见屏幕，必须 Client 代劳。

\- _自我纠错_：把模型和 Client 混了；以为 Client 指挥工具（其实工具属于 Server，调谁由模型决定）；完全漏掉用户那一面的 4 件事。

\- \*\***Tool Schema**\*\*：工具的"说明书" —— 描述名字、用途、参数、返回、约束。\*\***模型唯一看得见的工具就是 schema 本身**\*\*：它读不到 Server 代码、运行时风险、副作用、用法约定，全靠 schema 文本来决定调不调、怎么调。所以 schema 不是 Server 的实现细节，是 \*\***Model ↔ Tool 之间的接口契约**\*\*，是 prompt engineering 和 API design 的交集。schema 模糊 → 模型用错误参数填空。

\- _自我纠错_：知道 schema 重要，但"模型只能读 schema"这点没立刻想到 —— 是为什么 schema 这么关键的根。

\- \*\***Permission**\*\*：权限边界，控制 AI 能做什么、不能做什么。Handbook 把它列为"最容易被低估"的问题 —— 因为 MCP 让工具一接就跑，方便≠安全。读 doc 和发转账风险完全不同，必须拆 \*\***6 个维度**\*\*：①只读 vs 写入 ②会话授权 vs 长期授权 ③是否需用户确认 ④是否敏感访问 ⑤是否有外部副作用 ⑥是否可撤销 / 可审计。

\- _自我纠错_：6 个维度只想出 3 个（只读/确认/敏感），漏了"会话 vs 长期"“副作用”“可撤销可审计” —— 但这三条恰恰是今天 audit Notion server 时直接看到反面教材的（env token 长期、协议层无确认、默认无审计）。说明今天的 audit 没和 Permission 节点形成回路。

\- \*\***第一性原理（我的话）**\*\*：MCP 就像\*\***带白名单和权限标签的 USB**\*\*。

\- \*\***标准化半**\*\*：没有 USB 之前每个设备都要定制接口；有了 USB 之后任何合规设备插上就用。MCP 对 AI 生态做的就是 USB 对硬件生态做的事 —— 标准化 Client ↔ Server 接口，避免 N×M 适配。

\- \*\***授权半（普通 USB 不覆盖）**\*\*：MCP 默认\*\***禁止**\*\* —— 模型不能直接拥有世界，必须 schema 显式描述、permission 显式授权才看得到工具。普通 USB 是 plug-and-play，MCP 是 plug-and-审批。

\- _自我纠错_：USB 比喻刚开始只抓到"标准化"那半，漏了"授权 / 受限"那半 —— 这恰恰是 Handbook 原句两段并列的下半段。

\## 我的卡点

\- 读 Handbook + 做 audit 时\*\***实时没卡**\*\* —— 但闭卷复述时暴露 5 个错点（见复述节"自我纠错"行）。

\- 元观察：\*\***不卡 ≠ 懂**\*\*。读的时候顺，是因为我把"看着合理"当成"理解了"。明天起读 Handbook 旁边开个 scratchpad，凡是"嗯？……哦"的地方都先记一笔，别让它无痕过去。

\## 今日最小实验：拆 Notion 官方 MCP server 的 `query-data-source` schema

\> 不写代码，纯 audit。产物：\[experiments/mcp-notion-audit/[README.md](http://README.md)\](…/experiments/mcp-notion-audit/[README.md](http://README.md))

\*\***意外发现** #1\*\***：Notion 不是手写每个 tool，而是把 REST API 的 OpenAPI v3 spec（66KB）丢给** `MCPProxy` **自动转 MCP Tool。22 个工具几乎零成本派生。**

\*\***意外发现** #2\*\***：proxy.ts 有专门的** `deserializeParams` **函数，注释指向 \[issue** #176\]([https://github.com/makenotion/notion-mcp-server/issues/176](https://github.com/makenotion/notion-mcp-server/issues/176)) —— Claude Code / Cursor 会把递归 schema 双重序列化。这是真实工程坑。

\*\***Handbook 四维度对照**\*\*：

| 维度 | Notion `query-data-source` 实际 |

|—|—|

| name | ✅ 干净的 `query-data-source` |

| description | ⚠️ 偏弱 —— 没说"何时用 vs `retrieve-a-data-source`"、没说有无副作用 |

| inputSchema | ✅ 大部分清晰；⚠️ filter 是递归 schema，body 整体无 required（空 body 即全量读取） |

| 副作用 / 权限 | ❌ OpenAPI `security:[]` 假装无 auth，实际靠 HttpClient 注入 env token —— 长期、不可会话隔离、无审计、协议层无确认 |

\*\***最大启发**\*\*：MCP 不能假装权限是协议层的事。Notion README 自己警告"暴露给 LLM 有非零风险"。\*\***只读和写入应分 server，或加 capability flag。**\*\*

\## Follow-up

\- \[ \] \*\***AI × Web3 联想**\*\*：Notion MCP 把 OpenAPI auto-derive 成工具的模式 —— Web3 RPC / 合约 ABI 是不是也能自动派生成 MCP tool？这对应 Handbook Bridge 的 \[Web3 Tool Use\]([https://aiweb3.school/zh/handbook/bridge/web3-tool-use/](https://aiweb3.school/zh/handbook/bridge/web3-tool-use/)) 章节，是 Hackathon Dev Tooling 赛道的候选方向。

\- \[ \] 把"只读 vs 写入分 server"做成真实最小例子（对应 Handbook MCP 章节最小实践 A 方案），下次实验。

\- \[ \] 看一下 Notion \*\***Remote MCP**\*\*（OAuth）vs \*\***Local**\*\*（env token）两种授权模型的对比 —— OAuth 路线是不是 Handbook \*\***Permission**\*\* 章节里"会话授权"的标准答案？

\## Handbook / 课程反馈

\- \[ \]

\## 打卡草稿（粘到 [intensivecolearn.ing](http://intensivecolearn.ing) Check-in 表单的 Markdown）

\`\`\`markdown

\*\***MCP（模型上下文协议）—— 拆 Notion 官方 MCP server**\*\*

今天读 Handbook 的 MCP 章节，第一性原理一句话总结：模型不应该直接拥有世界，应该通过明确协议访问被授权的上下文和工具。MCP 把这层标准化成 Server / Client / Tool Schema / Permission 四个节点。

为了不停留在概念，找了 \[makenotion/notion-mcp-server\]([https://github.com/makenotion/notion-mcp-server](https://github.com/makenotion/notion-mcp-server)) 拆 `query-data-source` 这个 tool。两个意外：

1\. \*\***OpenAPI → MCP 自动派生**\*\*：Notion 不手写每个 tool，把 REST API 的 OpenAPI v3 spec 丢给 `MCPProxy` 类自动转成 22 个 MCP Tool。Web3 那边的 RPC / 合约 ABI 同理可派生 —— 这是 Dev Tooling 方向的一个明显切入点。

2\. \*\***协议** `security:[]` **假装无 auth，实际靠 HttpClient 注入 env token**\*\*。是长期授权、不可会话隔离、协议层无确认、默认无审计 —— Handbook Permission 节里说"权限要在协议外也成立"，这里就是反面教材。

把四维度（name / description / inputSchema / 副作用）扣到 `query-data-source` 上发现：description 没说"何时用 vs `retrieve-a-data-source`"，body schema 也没声明 required —— 空 body 即全量读取。Notion README 自己警告"暴露给 LLM 有非零风险"。

\*\***给自己的 checklist**\*\*：以后写 MCP server 必须把"副作用 / 是否需要用户确认"放进 description，只读和写入要分 server 或加 capability flag，每次调用要写审计日志。

完整 audit：[https://github.com/HeliosLz/ai-web3-school-cohort-0/blob/master/experiments/mcp-notion-audit/README.md](https://github.com/HeliosLz/ai-web3-school-cohort-0/blob/master/experiments/mcp-notion-audit/README.md)

\*\***今日复盘**\*\*：闭卷复述 Server / Client / Tool Schema / Permission / 第一性原理 5 个概念，暴露 5 个错点 —— 其中 Permission 那 6 维度漏的 3 个（会话 vs 长期、副作用、可撤销/可审计）恰好是今天 audit Notion server 时亲眼看见反面教材的。读 Handbook 时实时没卡，但闭卷暴露了 gap。元教训：“不卡 ≠ 懂”；明天起读 Handbook 旁边开 scratchpad，记任何"嗯？……哦"的瞬间。

\`\`\`

\- 提交位置：[https://intensivecolearn.ing/en](https://intensivecolearn.ing/en) → 登录 → AI × Web3 School 详情页 → 左侧 “Check-in” 按钮

\- 提交后回填提交时间 / 截图：
<!-- DAILY_CHECKIN_2026-05-19_END -->

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
