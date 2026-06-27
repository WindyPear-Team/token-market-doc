# POST `/v1/midjourney/generations`

Midjourney 默认 Imagine 创建入口。后端会以 `midjourney` 作为默认模型创建兼容图片任务。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `POST` |
| 路径 | `/v1/midjourney/generations` |
| 鉴权 | API Key 或登录 JWT |
| Content-Type | `application/json` |

## Body 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `model` | 否 | string | 不传时默认 `midjourney`。 |
| `prompt` | 是 | string | 图片提示词。 |
| `image_urls` | 否 | array | 参考图 URL，按上游支持透传。 |
| `callback_url` | 否 | string | 如上游支持，可作为任务完成回调地址透传。 |

未列出的 Midjourney 字段会保留并转发。

## 返回值

返回本地兼容任务对象，可通过 [GET /v1/midjourney/:id](/api/ai/routes/v1-midjourney-id) 或 [GET /v1/tasks/:id](/api/ai/routes/v1-tasks-id) 查询。
