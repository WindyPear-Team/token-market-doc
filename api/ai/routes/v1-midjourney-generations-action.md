# POST `/v1/midjourney/generations/:action`

Midjourney 动作入口。后端支持以下 `action`：

`blend`、`describe`、`edits`、`high-variation`、`inpaint`、`low-variation`、`modal`、`pan`、`reroll`、`upscale`、`variation`、`video`、`zoom`、`remix`。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `POST` |
| 路径 | `/v1/midjourney/generations/:action` |
| 鉴权 | API Key 或登录 JWT |
| Content-Type | `application/json` |

## Path 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `action` | 是 | string | Midjourney 动作名。 |

## Body 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `model` | 否 | string | 不传时默认 `midjourney`。 |
| `task_id` | 否 | string | 来源任务 ID，动作类接口通常需要。 |
| `index` | 否 | integer/string | 图片序号或按钮序号，按上游支持透传。 |
| `prompt` | 否 | string | 动作提示词。 |
| `mask` | 否 | string/object | Inpaint 或 modal 等动作使用，按上游支持透传。 |
| `callback_url` | 否 | string | 如上游支持，可作为任务完成回调地址透传。 |

未列出的 Midjourney 动作字段会保留并转发。

## 返回值

返回本地兼容任务对象，可通过 [GET /v1/midjourney/:id](/api/ai/routes/v1-midjourney-id) 或 [GET /v1/tasks/:id](/api/ai/routes/v1-tasks-id) 查询。
