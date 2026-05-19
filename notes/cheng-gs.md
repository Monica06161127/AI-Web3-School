---
timezone: UTC+8
---

# cheng-gs

**GitHub ID:** cheng-gs

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
# Daily Note - 2026-05-19

## 今日概览

今天的主要工作是把 Week 1 里已经完成的 Web3 实践和学习材料系统化整理进 GitHub 仓库，形成可以提交、可以复盘、也可以继续扩展的公开 proof-of-work。

我没有继续停留在“做过一次测试”这个层面，而是把测试钱包、Sepolia 测试交易、SimpleStorage 合约、Web3 基础概念和账户权限差异都整理成了结构化文档。

## 今天完成了什么

### 1\. 补齐了 Web3 基础概念文档

我新增了 [tasks/web3-basic-concepts.md](/F:/ai-web3/ai-web3-school-cohort-0/tasks/web3-basic-concepts.md)，用自己的话整理了 Web3 入门阶段最核心的一组概念，包括：

-   account
    
-   address
    
-   wallet
    
-   seed phrase
    
-   private key
    
-   signature
    
-   transaction
    
-   gas
    
-   smart contract
    
-   testnet
    
-   block explorer
    
-   EOA / smart account / multisig
    

每个概念都包含一句话解释、一个例子和一个安全提醒或常见误区，并特别说明了为什么私钥、助记词、签名和授权必须谨慎处理。

### 2\. 记录了测试网交易信息

我确认并保留了一笔 Sepolia 测试网普通转账的关键记录：

-   测试网：Sepolia
    
-   测试钱包地址：`0x7A26dFA802c664DB65e03454bFAFe042e3f14266`
    
-   交易哈希：`0xcb2586107f160f4431d5107085a3d16aa152f384179b11ce12b14c68c57f55ac`
    
-   区块浏览器链接： `https://sepolia.etherscan.io/tx/0xcb2586107f160f4431d5107085a3d16aa152f384179b11ce12b14c68c57f55ac`
    

我还写出了一段简短说明，解释了这笔交易由哪个地址发起、转账给谁、交易状态如何、所在区块是多少、Gas 使用量和手续费大致是多少。

### 3\. 保存了最小智能合约代码

我把测试合约保存到了仓库中：

-   [experiments/contracts/SimpleStorage.sol](/F:/ai-web3/ai-web3-school-cohort-0/experiments/contracts/SimpleStorage.sol)
    

这个合约用于练习最基础的链上读写逻辑：

-   `constructor(uint256 _initialNumber)`
    
-   `setNumber(uint256 _number)`
    
-   `getNumber()`
    

它对应的是我在 Remix 上完成的最小合约部署与调用练习。

### 4\. 整理了合约部署与调用记录

我新增了 [submissions/week-1-contract-practice.md](/F:/ai-web3/ai-web3-school-cohort-0/submissions/week-1-contract-practice.md)，把当前可提交的合约实践信息整理成了规范格式，包括：

-   合约地址：`0xA4B6b39A7D0dC7EFb55608A886a71e09b4080272`
    
-   区块浏览器链接： `https://sepolia.etherscan.io/address/0xA4B6b39A7D0dC7EFb55608A886a71e09b4080272`
    
-   合约代码 GitHub 链接
    
-   我部署和调用了哪些函数
    
-   哪些步骤必须人工确认
    

目前这份记录里，读取或写入的具体返回值还可以继续补全。

### 5\. 比较了 EOA、智能账户和多签账户

我新增了 [tasks/eoa-vs-smart-account-vs-multisig.md](/F:/ai-web3/ai-web3-school-cohort-0/tasks/eoa-vs-smart-account-vs-multisig.md)，重点比较了三类账户在这些维度上的差异：

-   谁持有控制权
    
-   谁可以发起交易
    
-   是否支持多人确认
    
-   是否支持恢复、限额或自动化策略
    
-   典型使用场景
    
-   主要风险点
    

这份文档的核心收获是：不同账户类型的差别，不只是技术实现不同，而是它们对“谁能动手、谁来批准、谁承担风险”给出了不同答案。

### 6\. 已把今天新增内容推送到 GitHub

今天整理的材料已经提交并推送到远端仓库，最新一次相关提交是：

-   `1dc0543 Add Web3 practice notes and contract files`
    

仓库地址：

-   `https://github.com/cheng-gs/ai-web3-school-cohort-0`
    

## 今天的学习收获

今天最大的收获不是“我做了一笔测试网交易”或“我部署了一个合约”，而是开始能把这些操作放进一条完整的链上学习路径里理解：

-   钱包不是普通登录
    
-   签名不等于交易
    
-   授权不等于无风险
    
-   Gas 不只是手续费
    
-   区块浏览器才是链上结果验证入口
    
-   不同账户结构对应不同的权限和风险分配方式
    

相比昨天偏 AI learning workflow 的整理，今天更像是在补齐 Web3 执行层的基础认知。

## 还缺什么

今天的材料已经基本可提交，但还有几个点后续可以补得更完整：

-   `SimpleStorage` 的实际部署交易哈希
    
-   `getNumber()` 的真实读取结果
    
-   `setNumber(...)` 的真实写入参数和写入后结果
    
-   对应的区块浏览器函数调用或交易链接
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->

# Week 1 配置记录与运行记录

## 1\. 我选择的 Agent / AI 工具

-   工具：Codex
    
-   使用场景：作为我的 AI × Web3 School learning agent，协助我初始化学习仓库、整理学习计划、生成打卡草稿、沉淀课程笔记和 Handbook feedback 流程。
    

## 2\. 我让 Agent 帮我完成的学习任务

这次我让 Codex 帮我完成了几类实际任务：

-   阅读 AI × Web3 School Learning Agent 启动 Prompt 和 Handbook
    
-   根据我的背景初始化个人学习计划
    
-   在本地创建并初始化 GitHub 学习仓库
    
-   生成 `README.md`、`profile.md`、`learning-plan.md`、`daily/2026-05-18.md`
    
-   根据 WCB Learning 页面内容补齐 Week 1 学习目标和交付清单
    
-   生成 AI 基础概念整理文档
    
-   整理 Handbook feedback 工作流
    

## 3\. 一段关键 Prompt / 配置说明

我给 Codex 的关键任务说明大意如下：

> 请作为我的 AI × Web3 School Learning Agent，先阅读启动 Prompt 和 Handbook，帮我初始化个人学习计划、GitHub 学习仓库、每日打卡草稿和 Handbook feedback 流程。

本次使用中的关键配置和边界：

-   主工具选择：Codex
    
-   输出语言：中文
    
-   学习背景：AI 熟悉，Web3 新手，会基础脚本
    
-   每日投入时间：2 小时
    
-   仓库策略：公开 GitHub repo，作为 proof-of-work workspace
    
-   安全边界：不把 API key、私钥、助记词、密码、隐私信息写入公开仓库
    
-   执行边界：涉及 GitHub 仓库创建、提交、推送等写入动作时，先确认再执行
    
-   平台边界：WCB 打卡和正式提交以人工手动提交为准，不假设 Agent 能自动代提
    

## 4\. 一次成功输出记录

一次明确成功的输出是：Codex 帮我完成了本地仓库初始化、首个 commit、远端 GitHub repo 创建和首次 push。

相关结果：

-   GitHub repo：[https://github.com/cheng-gs/ai-web3-school-cohort-0](https://github.com/cheng-gs/ai-web3-school-cohort-0)
    
-   本地目录：`F:\ai-web3\ai-web3-school-cohort-0`
    
-   首次提交信息：`Initialize AI Web3 School learning repo`
    

同时，Codex 还生成了以下学习材料：

-   [README.md](/F:/ai-web3/ai-web3-school-cohort-0/README.md)
    
-   [learning-plan.md](/F:/ai-web3/ai-web3-school-cohort-0/learning-plan.md)
    
-   [daily/2026-05-18.md](/F:/ai-web3/ai-web3-school-cohort-0/daily/2026-05-18.md)
    
-   [tasks/ai-basic-concepts.md](/F:/ai-web3/ai-web3-school-cohort-0/tasks/ai-basic-concepts.md)
    
-   [tasks/week-1-deliverables.md](/F:/ai-web3/ai-web3-school-cohort-0/tasks/week-1-deliverables.md)
    

## 5\. 一次人工复核、修正或拒绝 Agent 建议的记录

这次过程里，我至少做了两次明确的人工复核：

### 记录 A：WCB Learning 内容人工确认

一开始 Agent 只能拿到 WCB Learning 页面入口，但没有读到完整的学习内容。这里没有让 Agent 猜测“今天任务是什么”，而是由我手动打开 WCB Learning 页面，把 Week 1 的真实目标和任务内容贴回对话，再由 Agent 写入 repo。

这次人工复核的意义是：

-   避免 Agent 在页面内容不完整时编造课程安排
    
-   保证学习计划和交付清单与课程平台实际内容一致
    

### 记录 B：GitHub 登录与远端创建问题修正

在创建远端仓库时，Agent 第一次遇到了认证和权限问题，后来又遇到 PAT 权限不足的问题。这里没有让 Agent 继续盲目重试，而是由我手动重新执行 `gh auth login`，改用正确的登录方式后，再让 Agent 继续创建远端仓库并推送。

这次人工修正的意义是：

-   防止错误认证状态下继续执行写入动作
    
-   把“创建公开仓库”这个外部写入动作保留在人可确认的范围内
    

## 6\. 这次使用 Codex 的体会

我目前最直接的感受是：

-   Codex 很适合做 repo 初始化、文档整理、任务拆解和学习材料沉淀
    
-   对于结构化工作，例如创建目录、写 Markdown、维护学习计划，它的效率很高
    
-   但涉及外部平台状态、认证、权限、打卡提交、敏感信息时，仍然必须人工确认和复核
    

## 7\. 后续准备

接下来我会继续用 Codex 处理这些学习任务：

-   整理 Web3 基础概念笔记
    
-   设计并记录测试网交互流程
    
-   生成最小 AI × Web3 交叉实验说明
    
-   维护 daily notes、提交记录和 handbook feedback
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
