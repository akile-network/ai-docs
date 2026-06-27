# 常见问题

## Base URL 应该填什么？

填写：

```text
https://aigateway.akile.ai/v1
```

注意必须包含 `/v1`。

## API Key 放在哪里？

放在服务端环境变量中。不要写进前端代码，也不要提交到 Git 仓库。

## OpenAI SDK 能直接用吗？

可以。把 SDK 的 Base URL 改成 `https://aigateway.akile.ai/v1`，把 API Key 改成控制台生成的 Key。

## 为什么提示 API_KEY_REQUIRED？

请求没有携带 API Key。请添加：

```http
Authorization: Bearer AK-xxxxxxxx
```

也可以使用 `x-api-key` 或 `x-goog-api-key` 请求头，但推荐使用标准 Bearer Token。

## 模型名在哪里看？

登录后打开 [Available Channels](https://aigateway.akile.ai/available-channels) 页面，查看当前账号可用的平台、分组和模型。

## 余额消耗太快怎么办？

先到 Usage 页面按 API Key、模型和时间范围排查。必要时禁用异常 Key，并给不同业务设置独立 Key 和额度。

## 支付成功但余额没更新怎么办？

打开 Orders 页面查看订单状态，并刷新支付结果页。如果仍未到账，保留订单号后联系支持。

## 可以公开分享 API Key 吗？

不可以。公开分享后别人可以消耗你的额度。需要给他人使用时，建议创建单独 Key，并设置额度、过期时间和 IP 限制。
