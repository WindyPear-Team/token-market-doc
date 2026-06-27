# GET `/v1/midjourney/:id`

查询 Midjourney 任务状态、结果图片和可执行按钮。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `GET` |
| 路径 | `/v1/midjourney/:id` |
| 鉴权 | API Key 或登录 JWT |

## Path 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `id` | 是 | string | 本地 Midjourney 任务 ID。 |

## 返回值

```json
{
  "id": "task_xxx",
  "task_id": "task_xxx",
  "status": "succeeded",
  "progress": 100,
  "cost": "0.12",
  "credits_cost": 120000,
  "image_urls": ["https://example.com/grid.png"],
  "grid_image_url": "https://example.com/grid.png",
  "result": {},
  "buttons": [],
  "upstream_id": "provider-task-id",
  "upstream_response": {}
}
```
