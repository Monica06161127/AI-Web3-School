---
timezone: UTC+8
---

# HirongVSuen

**GitHub ID:** HirongVSuen

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
> **今日学习内容：**
> 
> -   阅读了 Learning Agent 启动 Prompt，了解全部流程规则
>     
> -   阅读了 Handbook 首页，了解整体知识地图（AI 基础 → Web3 基础 → AI × Web3 Bridge → 前沿探索）
>     
> -   完成学员画像确认
>     
> -   安装并登录 GitHub CLI
>     
> -   创建并初始化个人学习仓库 `ai-web3-school-cohort-0`
>     
> 
> **学习时长：** 约 1 小时
> 
> **心得 / 收获：**
> 
> 1.  Handbook 的学习路径设计很清晰，从 AI 基础到 Web3 再到交叉领域循序渐进
>     
> 2.  Learning Agent 作为学习伙伴，能帮助养成每日记录和打卡的习惯
>
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->

# wls2安装hermes agent

_1.执行命令_

```
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

遇见的问题

-   安装依赖时报404
    
    -   更新到最新库，sudo apt update
        
-   uv.lock 被锁
    
    -   进入 ~/.hermes/hermes-agent 下 执`uv lock`
        

_2.配置deepseek_

1.  执行\`hermes model\`
    
2.  选择deepseek
    
3.  输入apikey 和 baseurl，然后选择需要的模型 参考[首次调用 API | DeepSeek API Docs](https://api-docs.deepseek.com/zh-cn/)
    

_3.集成飞书_

1.  在飞书创建智能体应用，保存好**App ID** and **App Secret**
    
2.  执行`hermes gateway setup`
    
3.  选择飞书
    
4.  输入appid 和 appsecret
    
5.  使用websocket
    
6.  其余使用推荐选项
    
7.  配置完成后，使用当前用户启动services
    
8.  和飞书中的助手聊天，助理会推一个命令，然后执行
    
    ![Pasted image 20260518160309.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/HirongVSuen/images/2026-05-18-1779093098555-Pasted_image_20260518160309.png)

_参考文档_

[Feishu / Lark | Hermes Agent (](https://hermes-agent.nousresearch.com/docs/zh-Hans/user-guide/messaging/feishu)[nousresearch.com](http://nousresearch.com)[)](https://hermes-agent.nousresearch.com/docs/zh-Hans/user-guide/messaging/feishu)

_4.生成学习助手_

告诉助手一下提示词：

请作为我的 AI × Web3 School Learning Agent，先阅读启动 Prompt：[https://aiweb3.school/learning-agent.zh.txt](https://aiweb3.school/learning-agent.zh.txt) ，并结合 Handbook：[https://aiweb3.school/zh/handbook/](https://aiweb3.school/zh/handbook/) ，帮我初始化个人学习计划、GitHub 学习仓库、每日打卡草稿和 Handbook feedback 流程。  
  
助理自动生成github仓库和个人学习推荐
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
