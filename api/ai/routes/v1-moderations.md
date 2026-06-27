# POST `/v1/moderations`

内容审核接口，兼容 OpenAI Moderations 路径。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `POST` |
| 路径 | `/v1/moderations` |
| 鉴权 | API Key 或登录 JWT |
| Content-Type | `application/json` |

## Body 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `model` | 否 | string | 不传时默认 `omni-moderation-latest`。 |
| `input` | 是 | string/array/object | 待审核内容，支持上游兼容结构。 |

## 返回值

直接透传上游审核响应。后端会按输入内容和响应文本计费。
