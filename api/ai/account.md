# 账户与额度接口

账户接口用于查询当前 API Key 或用户账户的余额、已用额度和剩余额度。后端同时提供根路径和 `/v1` 路径兼容入口。

## 路由

| 路由 | 说明 |
| --- | --- |
| [GET /v1/balance](/api/ai/routes/v1-balance) | 查询当前 API Key 的剩余额度和已用额度。 |
| [GET /v1/user/balance](/api/ai/routes/v1-user-balance) | 查询当前用户账户余额和已用额度。 |

## 兼容路径

| 路由 | 说明 |
| --- | --- |
| `GET /balance` | 与 `GET /v1/balance` 相同。 |
| `GET /user/balance` | 与 `GET /v1/user/balance` 相同。 |
