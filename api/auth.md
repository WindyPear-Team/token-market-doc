# 认证接口

认证接口用于登录、注册、Passkey 和 OIDC。登录成功后返回 JWT，后续用户接口和管理接口使用：

```text
Authorization: Bearer <jwt>
```

## 密码认证

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `POST` | `/auth/password/login` | 无 | `identifier`、`password`、`captcha_token`、`agreement_accepted` | `{ "token": "...", "user": { ... } }` |
| `POST` | `/auth/password/register` | 可通过 cookie 或请求体传 referral。 | `username`、`email`、`password`、`email_code`、`captcha_token`、`referral_code`、`agreement_accepted` | `{ "token": "...", "user": { ... } }` |
| `POST` | `/auth/password/email-code` | 无 | `email`、`captcha_token` | `{ "message": "Verification code sent" }` |

登录请求：

```json
{
  "identifier": "alice@example.com",
  "password": "change-me",
  "captcha_token": "",
  "agreement_accepted": true
}
```

注册请求：

```json
{
  "username": "alice",
  "email": "alice@example.com",
  "password": "change-me",
  "email_code": "123456",
  "captcha_token": "",
  "referral_code": "",
  "agreement_accepted": true
}
```

## Passkey 登录

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `POST` | `/auth/passkey/login/options` | 无 | Passkey 登录标识，如用户名或邮箱。 | WebAuthn 登录挑战。 |
| `POST` | `/auth/passkey/login` | 无 | WebAuthn 登录响应。 | `{ "token": "...", "user": { ... } }` |

## OIDC

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/auth/login` | Query: `ref`、`agreement_accepted`。 | 无 | 重定向到 OIDC Provider。 |
| `GET` | `/auth/callback` | Query: `code`、`state`。 | 无 | 重定向回前端并携带登录 token。 |

## 错误

| 状态码 | 说明 |
| --- | --- |
| `400` | 参数不合法、未同意协议、验证码错误。 |
| `401` | 凭据无效。 |
| `409` | 需要初始化或初始化状态冲突。 |
| `503` | OIDC 未配置或不可用。 |
