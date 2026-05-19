---
timezone: UTC+8
---

# Eliana-web07

**GitHub ID:** Eliana-web07

**Telegram:** @ElianaLU

## Self-introduction

来学习了！

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
严肃学习5.18PPT

## Web2 支付系统基础模型

三个对象：电商平台 → 支付服务 → 银行机构（Bank Institution）

请求流

• 支付如何完成：三方协作完成资金流转

资金流

• 用户银行账户 → 支付服务控制的银行账户 → 定期清结算至电商平台

安全检查点

• 服务之间相互 notify 的认证（API Key）

• 用户支付验证（支付密码、MFA 等）

• 潜在风险：数据篡改、伪造鉴权（Fake Authentication）

关键认知

用户的钱表面上自己控制，实际是 Bank Institution 控制的记账数据（Alice: 20 USD, Bob: 10 USD）。

## Web3 资金收付

升级场景：支付服务扩展稳定币支付业务。

• Bank Institution → 替换为 Web3 区块链

• 资金流：用户 Web3 账户 → 支付服务的 Deposit Account → 清结算至电商平台 Web3 账户

各条链（Layer1、Layer2）可以简单理解为不同的 Bank Institution，区块链就是另一种形式的银行机构。

## 区块链的信任机制

• 数据不可篡改

• 逻辑即代码，公开透明（Smart Contract ≈ Python Interpreter）

• 共识协议（信任模型）：PoW、PoS、DPoS、PoH 等

### 本质：

• 执行 Smart Contract 代码，将旧状态转换为新状态的计算引擎

• 通过用户私钥签名进行鉴权

区块链不止是数据库，还是一个全球共享的、确定的状态机。

## 钱包的本质

• 私钥管理：对资产的绝对控制权

• 签名能力：与区块链交互的唯一合法身份

• 核心价值：通往 Web3 世界的唯一凭证

钱包不是存储资产的容器，而是管理开启资产大门钥匙的工具。

## 钱包类型

安全与易用性是核心 Trade-off 决策：

• 按实现原理分类（热钱包 / 冷钱包 / MPC 钱包等）

• 按托管方式分类（自托管 / 托管型）

• 特殊类型：多签钱包、硬件钱包、隐私钱包（Railgun）、分层钱包（BTC / ToB）等

### 钱包安全威胁

① 私钥泄露（Key Leakage）

资产丢失不可逆，私钥即是一切。

② 签名欺骗（Phishing）

伪造交互意图，诱导用户签署恶意交易。防御手段：EIP-712 签名可视化 / 禁用 eth\_sign。

③ 权限滥用（Approve）

无限额度授权给恶意合约，导致资产被盗。

安全结论：无法解释系统行为，就无法保证资产安全。

## Web3 交易生命周期

• 构造（Construct）：定义交互意图，封装 to、Gas、Nonce、Data 等关键参数

• 签名（Sign）：使用私钥赋予交易技术效力，确保所有权不可篡改

• 广播（Broadcast）：提交至网络节点，进入 Mempool 等待矿工打包与共识确认

## 交易关键参数

Gas：系统动力源

• gas fee = gas count × gas price（以原生币支付）

• EIP-1559：Base Fee / Tip Fee / Max Fee 三层模型

Nonce：顺序守护者

• 防止重放攻击与交易乱序执行，确保账户状态变更的原子性

• 不同链实现差异（EVM / TRON / BTC / Solana）

Data：智能合约指令集

• 定义复杂业务逻辑与参数传递，是链上应用交互的灵魂

## 交易监听逻辑

• 交易确认（Tracking）：实时追踪 Pending → Confirmed 全生命周期状态

• Event 监听（Signals）：捕获合约抛出的业务信号，触发后端清分、对账与通知

• 不确定性挑战：链分叉、区块重组、网络延迟的容错能力

## 交易模拟（Simulate）

• 在提交交易前验证执行结果，精准预测结果，避免不必要资产损耗

• 未经模拟的交易可能导致资产被盗、逻辑归零或状态不一致

• 模拟是 Debug 的前置核心步骤，是构建高健壮性支付系统的必然选择

## 服务器端钱包安全

• 权限拆分：MPC、SAFE 等多签方案，以及资金量进一步拆分

• 完善的 Web2 安全流程 + 风控 + Web3 规则（Web2 能力不可或缺）

• 完善的交易可视化和模拟：只签名可信交易

「在 Web3 世界中，安全理解力 = 资产保护力。」

## 架构师能力模型

三位一体的进化

架构能力（Architecture）

设计高可用、高安全的分布式系统，在去中心化与性能之间寻找最优解。

Debug 能力（Analysis）

能够深入底层协议，精准解释每一个逻辑背后的深层技术原因。

基础能力（Fundamentals）

对底层共识机制、密码学原理与链上状态模型拥有深刻且直觉化的理解。
<!-- DAILY_CHECKIN_2026-05-19_END -->
<!-- Content_END -->
