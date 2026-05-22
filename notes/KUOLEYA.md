---
timezone: UTC+8
---

# KUOLEYA

**GitHub ID:** KUOLEYA

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->
今天完成模块A的任务3：

第一个任务点：择一个 Week 1 概念（这里我选的是LLM）让 agent 帮你生成一个可交互产物：小页面、CLI、流程图、quiz、概念卡片或最小 demo。这里我让他生成了一个前端页面预览图如下(Github：[ai-web3-study/demos/llm-token-predictor/index.html at main · KUOLEYA/ai-web3-study](https://github.com/KUOLEYA/ai-web3-study/blob/main/demos/llm-token-predictor/index.html))

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/KUOLEYA/images/2026-05-22-1779433682845-image.png)

操作说明如下：**1\. 选一个示例 prompt** 页面中间有一排浅色小按钮，随便点一个，比如：

\- `"The meaning of life is"` — 哲理类

\- `"Once upon a time, a young wizard"` — 故事类

\- `def quicksort(arr):` — 代码类

点一下，输入框自动填上文字。

**2\. 点「▶ 生成」** 页面会逐 token 往外蹦文字，像 LLM 在打字一样。同时右边会显示这个位置 top-5 候选 token 的概率柱状图，选中的那个标蓝 ✓

**3\. 拉 🌡️ Temperature 滑条试不同效果**

\- **拉到左边 0.1–0.3** → 每次生成的 token 基本一样，稳定的（精确模式）

\- **拉到中间 0.5–0.9** → 偶尔变化，有创意但不离谱（均衡模式）

\- **拉到右边 1.0–2.0** → 每次生成五花八门，可能蹦出很意外的词（创意模式）

你观察概率分布的变化：低 T 时蓝色柱子又高又细，高 T 时各柱子高度差不多——这就是 LLM 里 temperature 的实际效果。

**4\. 🐢 速度滑条** 控制 token 蹦出来的速度，1 最慢（看得清每一步），5 最快（一眨眼生成完）。

**5\. 点 ✕ 清除** 重新开始。

第二个任务点：把产物放入 GitHub repo，并在 README 中说明：你让 agent 做了什么、你人工修改了什么、哪些输出不可靠、下一步准备如何改进。

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/KUOLEYA/images/2026-05-22-1779433385543-image.png)
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->


今天接着昨天的任务1完成任务2。

仓库链接：[KUOLEYA/ai-web3-study: AI × Web3 课程学习实验仓库](https://github.com/KUOLEYA/ai-web3-study)

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/KUOLEYA/images/2026-05-21-1779345178303-image.png)

README 截图

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/KUOLEYA/images/2026-05-21-1779345227060-image.png)

learning agent 配置说明:

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/KUOLEYA/images/2026-05-21-1779345294756-image.png)

Agent协助日志：

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/KUOLEYA/images/2026-05-21-1779345353105-image.png)
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->



今天完成了模块a的任务1,包括搭建hermes-agent并完成一次对话式学习任务

![屏幕截图 2026-05-20 100141.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/KUOLEYA/images/2026-05-20-1779290806560-_____2026-05-20_100141.png)

![屏幕截图 2026-05-20 101853.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/KUOLEYA/images/2026-05-20-1779290823067-_____2026-05-20_101853.png)
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->




今天补一下AI背景的基础明天开始正式的部署，这里主要是对课程的核心知识点进行一些总结，首先LLM 本质是基于上下文逐 token 做概率生成，擅长语言理解、代码生成和推理，但不擅长精确记忆、确定性计算与跨会话状态保持。控制它靠四层：上下文窗口是“工作内存”，系统指令设身份和边界，提示词传意图，工具调用让它从说变成做。调用 LLM 门槛很低，通过 MaaS 用 API Key 按量付费，核心入参就 model、messages、temperature 和 max\_tokens，跑通官方 Quick Start 即可。应用分为三种形态：Prompt 是模型回答、人决策；Workflow 是固定流程，模型只是节点；Agent 则自主规划、动态调工具、跨轮管状态，三者失控风险完全不同。AI Coding 工具能快速生成样板代码和原型，但代码审查、测试和架构决策仍依赖人。AI 输出必须验证，常见问题包括事实编造、假引用、推理漂移、越权操作和工具误用，需要用 guardrails、tracing 和人工介入防范。Agent 的核心组件涵盖状态管理、长期记忆、MCP、Skills、Tool Calling、Tracing、Guardrails、Handoff 和错误恢复。只有当目标开放、步骤无法预设、需多工具协作且中间结果决定策略时才需要 Agent；一次性问答用 Prompt，固定流程用脚本，高合规用人工审核，确定性数据直接查库，复杂度越高越要避免过度 agent 化
<!-- DAILY_CHECKIN_2026-05-19_END -->
<!-- Content_END -->
