# 后台功能概览

本页面面向管理员。普通用户不需要阅读本章节。

管理员入口通常在：

```text
https://aigateway.akile.ai/admin
```

## 管理员页面

后台包含以下模块：

- Admin Dashboard：全站数据概览。
- Ops Monitoring：运维监控、QPS 和错误日志。
- User Management：用户管理。
- Group Management：分组管理。
- Channel Management：渠道和价格管理。
- Channel Monitor：渠道监控。
- Subscription Management：订阅管理。
- Account Management：上游账号或渠道账号管理。
- Announcements：公告管理。
- Proxy Management：代理管理。
- Redeem Code Management：兑换码管理。
- Promo Code Management：优惠码管理。
- System Settings：系统设置。
- Risk Control：风控设置。
- Usage Records：全站用量记录。
- Affiliate Records：邀请、返利、转账记录。
- Payment Dashboard：支付数据概览。
- Order Management：订单管理。
- Subscription Plans：支付套餐管理。

## 管理建议

- 渠道、分组、价格变更前先确认影响范围。
- 高风险配置变更应保留操作记录。
- 定期查看渠道监控和错误日志。
- 兑换码、优惠码和支付套餐应设置清晰有效期。
- 对异常用户、异常 Key 和异常用量建立处理流程。

## 不建议公开的信息

管理员文档和公告中不要暴露：

- 上游 API Key。
- 支付密钥。
- 数据库密码。
- Cookie、Token 或私钥。
- 代理认证信息。
