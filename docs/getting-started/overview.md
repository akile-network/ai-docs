# 服务概览

AK AI Gateway 是一个 OpenAI 兼容的 AI API Gateway。它把多个模型供应商和渠道聚合到同一个入口，开发者只需要维护一个 Base URL 和一组 API Key，就可以在业务代码中切换不同模型。

## 访问地址

- 官网与控制台：[https://aigateway.akile.ai](https://aigateway.akile.ai)
- 控制台入口：[https://aigateway.akile.ai/dashboard](https://aigateway.akile.ai/dashboard)
- API Base URL：`https://aigateway.akile.ai/v1`

## 核心能力

- OpenAI 兼容：支持 OpenAI SDK、curl 和兼容 OpenAI 协议的工具。
- 多模型聚合：可接入 GPT、Claude、Gemini、DeepSeek、通义千问、GLM、Llama、Grok 等模型系列。
- 智能路由与容灾：按渠道可用性、价格和分组配置转发请求。
- 实时用量：按 API Key、模型、时间范围查看调用与消费。
- 额度管理：支持余额、充值、兑换码、订阅、订单等账户能力。
- 可用渠道：用户可在控制台查看自己当前可用的平台、分组和模型。

## 适合谁使用

- 已经使用 OpenAI SDK，希望统一接入多个模型的开发者。
- 需要在不同模型之间快速切换的应用或脚本。
- 需要团队维度控制 API Key、额度、速率限制和用量记录的项目。
- 需要稳定备用渠道和更清晰调用成本的业务。

## 与直接调用模型厂商的区别

直接调用模型厂商时，通常需要分别管理供应商账号、密钥、接口格式、模型名称、账单和失败重试。AK AI Gateway 把这些能力收敛到一个入口，业务侧主要关心：

- 使用哪个模型。
- 使用哪个 API Key。
- 当前账号是否有足够余额或订阅额度。
- 请求是否命中限速、配额、渠道不可用或鉴权错误。
