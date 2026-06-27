# POST `/v1/videos/:id/remix`

Veo 等视频模型的 remix 兼容入口。后端会把 `id` 写入请求体的 `parent_task_id`，并转发到上游 `/v1/videos/{id}/remix`。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `POST` |
| 路径 | `/v1/videos/:id/remix` |
| 鉴权 | API Key 或登录 JWT |
| Content-Type | `application/json` |

## Path 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `id` | 是 | string | 父视频任务 ID 或上游兼容任务 ID。 |

## Body 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `model` | 是 | string | 平台视频模型名。 |
| `prompt` | 否 | string | Remix 提示词。 |
| `duration` | 否 | integer/string | 输出时长，按上游支持透传。 |
| `resolution` | 否 | string | 分辨率，按上游支持透传。 |
| `callback_url` | 否 | string | 如上游支持，可作为任务完成回调地址透传。 |

未列出的上游 remix 字段会保留并转发。

## 返回值

返回本地兼容视频任务对象，可用 [GET /v1/tasks/:id](/api/ai/routes/v1-tasks-id) 或视频查询接口获取后续状态。
