# GET `/v1/images/generations/:id`

查询图片生成任务状态和结果。适用于上游以异步任务形式返回的图片模型，例如 Seedream、GPT Image、Gemini Image 等兼容任务。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `GET` |
| 路径 | `/v1/images/generations/:id` |
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

## Query 参数

| 参数 | 必填 | 说明 |
| --- | --- | --- |
| `key` | 否 | 可替代 Header。 |

## 返回值

返回兼容任务对象；如果结果中能提取图片 URL，后端会额外在顶层返回 `url`。

```json
{
  "id": "task_xxx",
  "task_id": "task_xxx",
  "status": "succeeded",
  "cost": "0.12",
  "url": "https://example.com/image.png",
  "result": {},
  "upstream_id": "provider-task-id",
  "upstream_response": {}
}
```
