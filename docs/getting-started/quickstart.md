# 三步接入

已有 OpenAI SDK 项目时，接入 AK AI Gateway 通常只需要三步。

## 1. 创建 API Key

登录后进入 [API Keys](https://aigateway.akile.ai/keys) 页面，创建一个新的 API Key。

创建时建议：

- 名称写清楚用途，例如 `prod-web`、`dev-test`、`billing-job`。
- 按项目设置额度上限。
- 如果请求来源固定，配置 IP 白名单。
- 为临时测试 Key 设置过期时间。

## 2. 替换 Base URL

把原来的 OpenAI Base URL 替换为：

```text
https://aigateway.akile.ai/v1
```

API Key 使用控制台生成的密钥。

## 3. 发起请求

Python 示例：

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://aigateway.akile.ai/v1",
    api_key="AK-xxxxxxxx",
)

response = client.chat.completions.create(
    model="claude-opus-4-8",
    messages=[
        {"role": "user", "content": "用一句话介绍 AK AI Gateway"}
    ],
)

print(response.choices[0].message.content)
```

curl 示例：

```bash
curl https://aigateway.akile.ai/v1/chat/completions \
  -H "Authorization: Bearer AK-xxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "claude-opus-4-8",
    "messages": [
      {"role": "user", "content": "你好"}
    ]
  }'
```

## 接入检查

如果请求失败，先检查：

- `base_url` 是否包含 `/v1`。
- 请求头是否为 `Authorization: Bearer <API Key>`。
- API Key 是否已启用、未过期、未超过额度。
- 账号余额或订阅额度是否充足。
- 模型名是否在可用渠道页面中能看到。
