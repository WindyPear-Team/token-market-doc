# 用户接口

用户接口前缀为 `/api/user`，需要登录 JWT：

```text
Authorization: Bearer <jwt>
```

## 当前用户与目录

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/user/me` | 无 | 无 | 当前用户信息、余额、分组等。 |
| `GET` | `/api/user/catalog` | 无 | 无 | 当前用户可用渠道、模型、价格、视频计费配置。 |
| `GET` | `/api/user/stats` | 无 | 无 | 当前用户仪表盘统计。 |
| `GET` | `/api/user/logs` | Query: 分页、模型、时间范围等。 | 无 | 当前用户用量日志或分页对象。 |

## 邀请与签到

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/user/referral` | 无 | 无 | 当前用户邀请码、邀请统计、返佣配置。 |
| `GET` | `/api/user/check-in/status` | 无 | 无 | 签到配置和今日签到状态。 |
| `GET` | `/api/user/check-in/records` | Query: 分页。 | 无 | 签到记录。 |
| `POST` | `/api/user/check-in` | 无 | 无 | 签到奖励结果。 |

## 支付与订单

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/user/payment/config` | 无 | 无 | 支付开关、币种、汇率、最小充值金额、可用支付方式。 |
| `GET` | `/api/user/payment/orders` | Query: 分页、时间范围。 | 无 | 充值订单列表或分页对象。 |
| `POST` | `/api/user/payment/orders` | 无 | `amount`、`method`。 | 新建订单，包含 `payment_url`。 |
| `GET` | `/api/user/payment/orders/:order_no` | Path: `order_no`。 | 无 | 充值订单详情。 |

创建订单请求：

```json
{
  "amount": "10",
  "method": "alipay"
}
```

订单返回：

```json
{
  "order_no": "20260101000000xxxx",
  "amount": "10",
  "rmb_amount": "72.00",
  "method": "alipay",
  "status": "pending",
  "payment_url": "https://..."
}
```

## Passkey 管理

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/user/passkeys` | 无 | 无 | 当前用户 Passkey 列表。 |
| `POST` | `/api/user/passkeys/register/options` | 无 | 注册选项，如设备名。 | WebAuthn 注册挑战。 |
| `POST` | `/api/user/passkeys/register` | 无 | WebAuthn 注册响应。 | 新建 Passkey 或成功响应。 |
| `DELETE` | `/api/user/passkeys/:id` | Path: `id`。 | 无 | 删除成功响应。 |

## 修改密码与 OIDC

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/user/password/method` | 无 | 无 | 当前账号可用的修改密码方式。 |
| `POST` | `/api/user/password/email-code` | 无 | `email`、`captcha_token`。 | 发送成功响应。 |
| `POST` | `/api/user/password/change` | 无 | 当前密码或邮箱验证码、新密码。 | 修改成功响应。 |
| `POST` | `/api/user/oidc/bind-url` | 无 | 无 | `{ "auth_url": "https://..." }`。 |

## API Key

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/user/api-keys` | 无 | 无 | 当前用户 API Key 列表。 |
| `POST` | `/api/user/api-keys` | 无 | 名称、允许模型、允许用户渠道、IP 限制、额度等。 | 新建 API Key，包含明文 key。 |
| `PUT` | `/api/user/api-keys/:id` | Path: `id`。 | API Key 配置字段。 | 更新后的 API Key。 |
| `POST` | `/api/user/api-keys/:id/rotate` | Path: `id`。 | 无 | 新明文 API Key。 |
| `POST` | `/api/user/api-keys/:id/reset-usage` | Path: `id`。 | 无 | 重置成功响应。 |
| `DELETE` | `/api/user/api-keys/:id` | Path: `id`。 | 无 | 删除成功响应。 |
| `POST` | `/api/user/api-key/rotate` | 兼容旧接口，可通过 body 或上下文定位 key。 | 可选 API Key 标识。 | 新明文 API Key。 |
