# GET `/v1/tasks/:id`

统一任务查询入口。可查询由图片、视频、Midjourney 等兼容生成接口创建的本地任务。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `GET` |
| 路径 | `/v1/tasks/:id` |
| 鉴权 | API Key 或登录 JWT |

## Header 参数

| 参数 | 必填 | 说明 |
| --- | --- | --- |
| `Authorization` | 是 | `Bearer sk-...` 或 `Bearer <jwt>`。 |
| `x-api-key` | 否 | 可替代 `Authorization`。 |

## Path 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `id` | 是 | string | 本地任务 ID。 |

## 返回值

```json
{
  "code": 200,
  "data": {
    "id": "task_xxx",
    "task_id": "task_xxx",
    "status": "processing",
    "progress": 50,
    "cost": "0.12",
    "result": {},
    "upstream_id": "provider-task-id",
    "upstream_response": {}
  }
}
```
