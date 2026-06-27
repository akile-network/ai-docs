# AK AI Gateway 文档

AK AI Gateway 是 Akile 提供的 AI API 中转与多模型聚合服务，面向需要统一接入 GPT、Claude、Gemini、DeepSeek、通义千问等模型的开发者和团队。

正式站点：[https://aigateway.akile.ai](https://aigateway.akile.ai)

API Base URL：

```text
https://aigateway.akile.ai/v1
```

## 你可以用它做什么

- 用 OpenAI 兼容接口调用多家模型。
- 在控制台创建和管理 API Key。
- 查看模型、渠道、可用分组和计费倍率。
- 查询调用用量、错误请求和消费记录。
- 通过充值、兑换码或订阅获得可用额度。
- 使用邀请返利、余额通知、订单记录等账户能力。

## 快速开始

1. 打开 [AK AI Gateway](https://aigateway.akile.ai)。
2. 注册账号并完成邮箱验证。
3. 进入控制台创建 API Key。
4. 把现有 OpenAI SDK 的 `base_url` 改成 `https://aigateway.akile.ai/v1`。
5. 选择模型并发起调用。

Python 示例：

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://aigateway.akile.ai/v1",
    api_key="AK-xxxxxxxx",
)

resp = client.chat.completions.create(
    model="claude-opus-4-8",
    messages=[
        {"role": "user", "content": "你好"}
    ],
)

print(resp.choices[0].message.content)
```

更多接入方式、控制台说明和常见问题见左侧目录。
