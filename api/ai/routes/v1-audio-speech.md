# POST `/v1/audio/speech`

文本转语音接口，兼容 OpenAI Audio Speech 路径。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `POST` |
| 路径 | `/v1/audio/speech` |
| 鉴权 | API Key 或登录 JWT |
| Content-Type | `application/json` |

## Body 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `model` | 否 | string | 不传时默认 `gpt-4o-mini-tts`。 |
| `input` | 是 | string | 要合成为语音的文本。 |
| `voice` | 否 | string | 语音角色，按上游支持透传。 |
| `format` | 否 | string | 输出格式，按上游支持透传。 |

## 返回值

直接透传上游音频响应。后端会根据输入文本和音频输出大小计费。
