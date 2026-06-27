# CC Switch 接入教程

CC Switch 是一个用于管理 Claude Code、Claude Desktop、Codex、Gemini CLI、OpenCode、OpenClaw、Hermes 等 AI 编程工具配置的桌面应用。使用它可以把 AK AI Gateway 配成一个可切换的 Provider，避免手动改多个配置文件。

官方入口：

- 官网：[https://ccswitch.io](https://ccswitch.io)
- GitHub：[https://github.com/farion1231/cc-switch](https://github.com/farion1231/cc-switch)

只从官网、GitHub Releases 或源码仓库下载 CC Switch。任何要求付费、充值或索取登录凭据的“CC Switch”网站或客户端都不是官方渠道。

## 准备工作

先准备三样东西：

1. AK AI Gateway 账号。
2. 一个可用的 API Key。
3. 一个可用模型名。

API Key 在 [API Keys](https://aigateway.akile.ai/keys) 页面创建。模型名在 [Available Channels](https://aigateway.akile.ai/available-channels) 页面查看。

## 安装 CC Switch

macOS 推荐用 Homebrew：

```bash
brew install --cask cc-switch
```

Windows 和 Linux 用户可以从 [GitHub Releases](https://github.com/farion1231/cc-switch/releases) 下载对应安装包。

安装后启动 CC Switch。如果系统提示权限或安全确认，按系统提示允许打开。

## 接入 Claude Code

Claude Code 不是普通 OpenAI SDK，它通常走 Anthropic 协议。AK AI Gateway 对外提供 OpenAI 兼容接口，因此在 CC Switch 里接 Claude Code 时，需要让 CC Switch 做本地路由和协议转换。

### 1. 打开 Claude Code 配置页

1. 启动 CC Switch。
2. 在顶部应用切换处选择 `Claude Code`。
3. 点击右上角 `+` 添加 Provider。
4. 选择 `App-specific Provider` 或 `Universal Provider`。
5. 在预设里选择 `Custom`，或选择带 OpenAI Chat Completions 能力的预设。

### 2. 填写 Provider 信息

推荐配置：

| 字段 | 填写 |
| --- | --- |
| Name | `AK AI Gateway` |
| API Key | 控制台创建的 API Key |
| Endpoint URL | `https://aigateway.akile.ai` |
| API Format | `OpenAI Chat Completions` |
| Main Model | 选择或填写可用模型名 |
| Haiku / Sonnet / Opus | 按速度、日常、强推理三个档位分别映射模型 |

注意：Claude Code 这里的 `Endpoint URL` 推荐填 `https://aigateway.akile.ai`，不要重复加 `/v1`。CC Switch 在 OpenAI Chat Completions 转换模式下会拼接 `/v1/chat/completions`。

### 3. 获取模型列表

填写 API Key 和 Endpoint URL 后，点击模型输入框旁边的 Fetch Models 按钮。CC Switch 会调用 OpenAI 兼容的 `/v1/models` 接口拉取模型。

如果拉取失败，可以手动填写模型名。模型名以可用渠道页面为准。

### 4. 启用本地路由

使用 OpenAI Chat Completions 格式接 Claude Code 时，需要 CC Switch 的本地代理运行并启用 Claude 路由。

操作路径：

1. 打开 `Settings`。
2. 进入 `Advanced`。
3. 打开 `Proxy Service` 或 `Routing Service`。
4. 启动代理服务。默认地址是 `http://127.0.0.1:15721`。
5. 在应用路由区域开启 `Claude` 路由。

保存后，在 Provider 卡片上点击 `Enable`。

### 5. 验证

打开终端运行：

```bash
claude
```

输入一条测试提示：

```text
你好，请用一句话介绍 AK AI Gateway。
```

如果 Claude Code 正常返回内容，说明配置已生效。

## 接入 Codex

Codex 可通过 OpenAI 兼容配置接入。

1. 在 CC Switch 顶部应用切换处选择 `Codex`。
2. 点击 `+` 添加 Provider。
3. 选择 `App-specific Provider` 或 `Universal Provider`。
4. 在预设里选择 `Custom`、`OpenAI Compatible` 或类似选项。
5. 填写：

| 字段 | 填写 |
| --- | --- |
| Name | `AK AI Gateway` |
| Base URL | `https://aigateway.akile.ai/v1` |
| API Key | 控制台创建的 API Key |
| Model | 可用渠道页面里的模型名 |

如果选择的上游是 Chat Completions 协议，开启 `Needs Local Routing`，并在模型映射中添加实际模型名。然后在路由设置里启动本地代理并开启 `Codex` 路由。CC Switch 会把 Codex 配置指向 `http://127.0.0.1:15721/v1`，由本地路由把 Codex 的 Responses 请求转换成上游 Chat Completions 请求。

修改模型映射后，重启 Codex 让模型列表刷新。

## 接入 OpenCode / OpenClaw

OpenCode 和 OpenClaw 通常使用 OpenAI 兼容配置：

| 字段 | 填写 |
| --- | --- |
| Provider Name | `AK AI Gateway` |
| Base URL | `https://aigateway.akile.ai/v1` |
| API Key | 控制台创建的 API Key |
| Model | 可用渠道页面里的模型名 |

保存后启用 Provider，再启动对应 CLI 测试。

## 常见问题

### 提示 API_KEY_REQUIRED

说明请求没有带上 API Key。检查：

- CC Switch Provider 里 API Key 是否填写。
- 是否启用了正确 Provider。
- 请求是否被本地代理改掉了鉴权头。

### 提示 404 或路径里出现 v1/v1

通常是 Base URL 填错：

- Claude Code + OpenAI Chat Completions 转换：填 `https://aigateway.akile.ai`。
- Codex / OpenCode / 普通 OpenAI 兼容工具：填 `https://aigateway.akile.ai/v1`。

### 切换 Provider 后没有生效

检查：

- CC Switch 是否仍在运行。
- 当前工具对应的 Provider 是否已经 Enable。
- 本地代理是否启动。
- 对应应用路由是否开启，例如 Claude 路由或 Codex 路由。
- Codex、OpenCode、Gemini 等 CLI 是否需要重启。

路由模式下切换供应商通常可以即时生效；非路由模式下，CLI 工具通常需要重启。

### 模型列表拉不出来

先确认：

- API Key 有效且未禁用。
- 账号余额或订阅额度充足。
- Endpoint URL 没有填错。
- 当前网络可以访问 `https://aigateway.akile.ai`。

如果 Fetch Models 不可用，可以手动填写模型名。

## 使用建议

- 为 CC Switch 单独创建一个 API Key，便于查看用量和限制额度。
- 开发、测试、生产使用不同 Key。
- 给长期使用的 Key 设置余额提醒和合理配额。
- 在可用渠道页面确认模型和价格后再映射到 Haiku、Sonnet、Opus 档位。
