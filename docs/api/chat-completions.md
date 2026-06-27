# 聊天补全

AK AI Gateway 支持 OpenAI 兼容的聊天补全调用。大多数 OpenAI SDK 项目只需要替换 Base URL 和 API Key。

## 请求地址

```text
POST https://aigateway.akile.ai/v1/chat/completions
```

## Python

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://aigateway.akile.ai/v1",
    api_key="AK-xxxxxxxx",
)

completion = client.chat.completions.create(
    model="claude-opus-4-8",
    messages=[
        {"role": "system", "content": "你是一个简洁的助手。"},
        {"role": "user", "content": "给我一个 API 网关的定义。"},
    ],
)

print(completion.choices[0].message.content)
```

## Node.js

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "https://aigateway.akile.ai/v1",
  apiKey: process.env.OPENAI_API_KEY,
});

const completion = await client.chat.completions.create({
  model: "claude-opus-4-8",
  messages: [
    { role: "user", content: "你好" },
  ],
});

console.log(completion.choices[0].message.content);
```

## curl

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

## 流式输出

如果 SDK 和模型支持流式输出，可以设置 `stream: true`：

```python
stream = client.chat.completions.create(
    model="claude-opus-4-8",
    messages=[{"role": "user", "content": "写一段短文"}],
    stream=True,
)

for event in stream:
    delta = event.choices[0].delta.content
    if delta:
        print(delta, end="")
```

## 模型名称

模型名称以控制台可用渠道页面为准。不同模型系列的参数支持程度可能不同，如果某个参数不生效或报错，先在控制台确认该模型和渠道是否可用。
