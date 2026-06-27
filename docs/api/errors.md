# 错误处理

当 API 请求失败时，优先从响应中的 `code` 和 `message` 判断原因。控制台的用量与错误请求页面也可用于定位问题。

## 常见错误

### API_KEY_REQUIRED

含义：请求没有携带 API Key。

示例响应：

```json
{
  "code": "API_KEY_REQUIRED",
  "message": "API key is required in Authorization header (Bearer scheme), x-api-key header, or x-goog-api-key header"
}
```

处理方式：

- 添加 `Authorization: Bearer <API Key>` 请求头。
- 确认 SDK 使用的是 `api_key` 或 `apiKey`。
- 确认请求没有被代理或网关移除鉴权头。

### 密钥不可用

可能原因：

- API Key 被禁用。
- API Key 已删除。
- API Key 已过期。
- API Key 超过额度。
- IP 白名单或黑名单不匹配。

处理方式：进入 [API Keys](https://aigateway.akile.ai/keys) 检查密钥状态和限制。

### 余额或额度不足

可能原因：

- 账户余额不足。
- 订阅额度已用完。
- 单个 API Key 的配额已耗尽。

处理方式：进入充值、订阅或 API Key 页面检查额度。

### 模型不可用

可能原因：

- 模型名称拼写错误。
- 当前账号分组无权访问该模型。
- 渠道维护或不可用。
- 请求参数不被该模型支持。

处理方式：进入 [可用渠道](https://aigateway.akile.ai/available-channels) 页面确认模型和渠道状态。

## 排查顺序

1. 确认 Base URL 是 `https://aigateway.akile.ai/v1`。
2. 确认请求头携带有效 API Key。
3. 确认 API Key 启用、未过期、额度充足。
4. 确认账号余额或订阅额度充足。
5. 确认可用渠道页面存在目标模型。
6. 查看用量记录和错误请求详情。
