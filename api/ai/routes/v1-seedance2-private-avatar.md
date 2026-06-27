# POST `/v1/seedance2/private-avatar`

Seedance 2.0 私有数字人素材提交接口。该路由会创建一个兼容视频任务，默认模型为 `doubao-seedance-2.0`。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `POST` |
| 路径 | `/v1/seedance2/private-avatar` |
| 鉴权 | API Key 或登录 JWT |
| Content-Type | `application/json` |

## Header 参数

| 参数 | 必填 | 说明 |
| --- | --- | --- |
| `Authorization` | 是 | `Bearer sk-...` 或 `Bearer <jwt>`。 |
| `x-api-key` | 否 | 可替代 `Authorization`。 |
| `Content-Type` | 是 | `application/json`。 |

## Body 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `model` | 否 | string | 不传时后端默认使用 `doubao-seedance-2.0`。 |
| `assets` | 否 | array | 私有素材列表，按上游 Seedance 协议透传。 |
| `asset_group_id` | 否 | string | 素材组 ID，按上游支持透传。 |
| `callback_url` | 否 | string | 如上游支持，可作为任务完成回调地址透传。 |

未列出的 Seedance 私有素材字段会保留并转发。

## 返回值

返回本地兼容任务对象，可使用 [GET /v1/tasks/:id](/api/ai/routes/v1-tasks-id) 查询后续状态。
