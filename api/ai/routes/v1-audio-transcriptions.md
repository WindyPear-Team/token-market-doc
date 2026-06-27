# POST `/v1/audio/transcriptions`

音频转写接口，兼容 OpenAI Audio Transcriptions 路径。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `POST` |
| 路径 | `/v1/audio/transcriptions` |
| 鉴权 | API Key 或登录 JWT |
| Content-Type | `multipart/form-data` |

## Form 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `file` | 是 | file | 待转写音频文件，最大 25 MB。 |
| `model` | 否 | string | 不传时默认 `whisper-1`。 |
| `prompt` | 否 | string | 提示词，按上游支持透传并参与计费估算。 |
| `response_format` | 否 | string | 返回格式，按上游支持透传。 |
| `language` | 否 | string | 语言代码，按上游支持透传。 |

## 返回值

直接透传上游转写响应。后端会根据音频文件大小、提示词和响应文本计费。
