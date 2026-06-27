# GET `/v1/user/balance`

查询当前登录用户的账户余额和总已用金额。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `GET` |
| 路径 | `/v1/user/balance` |
| 鉴权 | API Key 或登录 JWT |

## 返回值

```json
{
  "success": true,
  "remain_balance": "10.5",
  "remain_credits": 10500000,
  "used_balance": "1.2",
  "used_credits": 1200000
}
```
