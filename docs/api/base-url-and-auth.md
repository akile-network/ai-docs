# 基础配置

## Base URL

所有 OpenAI 兼容 API 请求使用：

```text
https://aigateway.akile.ai/v1
```

常见错误是只填写 `https://aigateway.akile.ai`，导致 SDK 拼出的请求路径不完整。使用 OpenAI SDK 时，Base URL 要包含 `/v1`。

## 鉴权方式

推荐使用标准 Bearer Token：

```http
Authorization: Bearer AK-xxxxxxxx
```

网关也支持从下列请求头读取 API Key：

- `Authorization: Bearer <key>`
- `x-api-key: <key>`
- `x-goog-api-key: <key>`

优先推荐 `Authorization`，兼容性最好。

## 环境变量示例

不要把密钥硬编码到代码仓库。推荐使用环境变量：

```bash
export OPENAI_BASE_URL="https://aigateway.akile.ai/v1"
export OPENAI_API_KEY="AK-xxxxxxxx"
```

Python：

```python
from openai import OpenAI

client = OpenAI()
```

Node.js：

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: process.env.OPENAI_BASE_URL,
  apiKey: process.env.OPENAI_API_KEY,
});
```

## 不要在浏览器暴露 API Key

API Key 应该只在服务端使用。不要放在：

- 前端源代码。
- 小程序包。
- App 安装包。
- GitHub、GitLab 等公开仓库。
- 可被用户查看的配置文件。

需要从浏览器调用时，应先请求自己的后端，由后端再转发到 AK AI Gateway。
