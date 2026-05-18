---
timezone: UTC+8
---

# @0xMrByte

**GitHub ID:** panrui1984

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->
对照着[LLM API 调用入门](https://www.youtube.com/watch?v=mnJJPltybBM)（视频）：边看边跟着写 API 调用

学习了基础使用，我使用了deepseek,

```
from openai import OpenAI

client = OpenAI(api_key="<DeepSeek API Key>", base_url="https://api.deepseek.com")

response = client.chat.completions.create(
    model="deepseek-chat",
    messages=[
        {"role": "system", "content": "You are a helpful assistant"},
        {"role": "user", "content": "Hello"},
    ],
    stream=False
)
```

此外，
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
