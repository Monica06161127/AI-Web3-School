---
timezone: UTC+8
---

# Qsa3Ger

**GitHub ID:** Qsa3Ger

**Telegram:** @Qsa3Ger

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
260519

已在tg部署hermes\*^ ^\*

部署途径：

1.直接用cursor进行部署（成功）

\*部署期间重要节点：在Powershell让hermes调用dsv4flash的api

[2.win](http://2.win)+wsl进行部署（失败）

\*部署期间成功节点：下载wsl打开linux虚拟机

\*部署期间失败节点：linux虚拟机无法配置win代理，vpn无法找到监听地址。群内小伙伴提出可以使用ssh key配置。未验证。
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

0518 AI时代，Web3开发者需要更扎实的基础知识与架构能力

# 1\. **引**

![](file:///C:\Users\asus\AppData\Local\Temp\ksohtml27744\wps1.jpg)

# 2\. **web3支付与web2区别**

![](file:///C:\Users\asus\AppData\Local\Temp\ksohtml27744\wps2.jpg)

A. 支付环境

B. Off chain方式计算

# 3\. **web3信任（私钥-数学方式）、钱包**

Signature+message IP=验证（without private key）

![](file:///C:\Users\asus\AppData\Local\Temp\ksohtml27744\wps3.jpg)![](file:///C:\Users\asus\AppData\Local\Temp\ksohtml27744\wps4.jpg)

| 名词 | 核心定义 |
| EOA 钱包（私钥钱包） | 由私钥直接控制的账户，是区块链原生的基础账户。私钥在本地生成并签名交易，链上可见为单一地址，如 MetaMask。 |
| 合约钱包（Safe 等） | 地址本身是智能合约，由合约代码逻辑控制。支持多签、社交恢复、批量交易等复杂功能，灵活性高。 |
| AA 钱包（账户抽象） | 基于账户抽象标准（如 ERC-4337）实现的智能钱包，让合约账户也能像 EOA 一样发起交易，大幅优化用户体验（如无 Gas 费、会话密钥）。 |
| MPC 多签（GG18/20...） | 链下实现的多方计算多签：把一个私钥分片给多个参与方，链下共同计算生成 1 个有效签名，链上只显示常规签名，隐私性强。 |
| 合约多签（Safe 等） | 链上智能合约实现的多签：由多把独立私钥签名，链上合约验证是否达到签名阈值（如 3/5），规则公开透明，可审计。 |
| 自托管钱包 | 用户完全掌控私钥，第三方无法访问资产。安全责任由用户承担，去中心化程度最高，如硬件钱包、非托管软件钱包。 |
| 全托管钱包 | 私钥由第三方服务商（如交易所）保管，用户通过账号密码访问资产。服务商承担安全责任，但存在中心化风险。 |
| 混合托管钱包 | 私钥由用户和服务商共同持有或分片保管，兼顾便捷性与安全性，常见于企业级钱包或部分合规产品。 |

# **EXTRA:**

速记极简释义（Web3 全套精简版）

1\. **助记词（XUYYAO）** 12/24个单词，\*\*私钥母源\*\*，丢了彻底丢资产，万能找回凭证。

2\. **私钥** 账户最高权限密钥，拥有即拥有资产，绝对不能外泄。

3\. **公钥** 私钥算出，用来生成钱包地址，公开无害。

4\. **钱包地址** 链上收款账号，公开可分享，类似银行卡号。

5\. **Gas费** 区块链转账/交互手续费，给节点打包记账。

6\. **链上** 数据公开记录在区块链，所有人可查可溯源。

7\. **链下** 不在区块链存数据，离线/第三方处理，速度快隐私高。

8\. **冷钱包** 离线存储私钥，不联网，极致安全=硬件钱包。

9\. **热钱包** 联网钱包，方便易用，风险高于冷钱包。

10\. **快照** 某一时间点持仓资产数据备份，多用于空投、分红。

11\. **空投** 项目免费发放代币/NFT，引流用户。

12\. **质押Stake** 锁定代币挖矿生息、获取收益或权益。

13\. **流动性LP** 往交易池放两种代币，做市赚手续费。

14\. **滑点** 实际成交价格和预估价格偏差，行情波动越大越高。

15\. **铸币Mint** 免费/付费铸造NFT，直接上链生成藏品。

16\. **白名单WL** 优先购买/铸造资格，抢先低价拿筹码。

17\. **灰度** 场外大额机构持仓情绪，影响大盘走势。

18\. **撸毛** 零成本参与项目，薅空投、福利、代币。

19\. **溯源** 通过链上地址追踪资金流向、交易记录。
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->


0517start meeting

1.CARA from [Z.AI](http://Z.AI)\-brief introduction of GLM

base on the paper

arXiv Preprint (free full text):

[https://arxiv.org/pdf/2103.10360.pdf](https://arxiv.org/pdf/2103.10360.pdf)

2\. Talent Onboarding Funnel

![](file:///C:\Users\asus\AppData\Local\Temp\ksohtml10008\wps1.jpg)

\*Every Monday/Wednesday/Friday has co-learning(about some sharing by mentors) without replay

\*their are some tasks to win the credit and we can find the tasks in the registration webpage.Different levels of difficulty will result in different scores.We need to clock in at least five days a [week.In](http://week.In) all,scores learning is optional.

3.teaching assistant

![](file:///C:\Users\asus\AppData\Local\Temp\ksohtml10008\wps2.jpg)

3\. how to use hermes as a agent assistant

Markdown:请作为我的 AI × Web3 School Learning Agent，先阅读启动 Prompt：[https://aiweb3.school/learning-agent.zh.txt，并结合](https://aiweb3.school/learning-agent.zh.txt，并结合) Handbook：[https://aiweb3.school/zh/handbook/，帮我初始化个人学习计划、GitHub](https://aiweb3.school/zh/handbook/，帮我初始化个人学习计划、GitHub) 学习仓库、每日打卡草稿和 Handbook feedback 流程。

Tasks:download the Hermes agent in telegram and upload the markdown to get the learning plan.(5\\19)

![](file:///C:\Users\asus\AppData\Local\Temp\ksohtml10008\wps3.jpg)
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
