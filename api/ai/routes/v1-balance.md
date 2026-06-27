# GET `/v1/balance`

查询当前 API Key 的剩余额度、已用额度和是否无限额度。使用登录 JWT 且没有 API Key 时，返回用户余额并标记为无限 API Key 额度。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `GET` |
| 路径 | `/v1/balance` |
| 鉴权 | API Key 或登录 JWT |

## 返回值

```json
{
  "success": true,
  "remain_balance": "10.5",
  "remain_credits": 10500000,
  "used_balance": "1.2",
  "used_credits": 1200000,
  "unlimited_quota": false
}
```
