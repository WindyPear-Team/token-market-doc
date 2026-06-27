# API 文档

这里按接口类型拆分记录后端 HTTP API。每个页面包含请求方式、路径、参数和返回值。

## 鉴权

| 类型 | 使用位置 | 凭据 |
| --- | --- | --- |
| 公开 | 健康检查、公开配置、支付回调、初始化 | 无 |
| 登录认证 | `/api/user/*` | `Authorization: Bearer <jwt>` |
| 管理员 | `/api/*` 管理接口 | `Authorization: Bearer <jwt>`，且用户为管理员 |
| 网关 API | `/v1/*`、`/v1beta/*` | `Authorization: Bearer sk-...`，也支持 `x-api-key` 和 `?key=` |

## 社区版接口

| 页面 | 内容 |
| --- | --- |
| [公开接口](/api/public) | 健康检查、公开设置、公开模型、初始化。 |
| [支付回调](/api/payment) | 易支付、OpenPayment 回调和提交页。 |
| [认证接口](/api/auth) | 密码登录、注册、Passkey、OIDC。 |
| [AI 网关](/api/gateway) | OpenAI、Claude、Gemini、图片、视频任务、Kling 兼容接口。 |
| [管理员接口](/api/admin) | 系统设置、渠道、模型、分组、用户、统计。 |
| [用户接口](/api/user) | 当前用户、目录、日志、签到、支付、Passkey、API Key。 |

## 高级版接口

高级版接口通过 route hook 额外挂载，社区版不会注册这些路由。

| 页面 | 内容 |
| --- | --- |
| [高级版接口](/api/premium) | 订阅、兑换码、Meta Model、高级聊天、连接器设备、Agent、Skill。 |

## 通用响应

错误响应：

```json
{
  "error": "message"
}
```

分页响应：

```json
{
  "items": [],
  "total": 0,
  "page": 1,
  "page_size": 20
}
```

常见分页参数：

| 参数 | 位置 | 类型 | 说明 |
| --- | --- | --- | --- |
| `page` | Query | integer | 页码，从 `1` 开始。 |
| `page_size` | Query | integer | 每页数量。 |
| `from` | Query | string | 起始时间，部分列表接口支持。 |
| `to` | Query | string | 结束时间，部分列表接口支持。 |
