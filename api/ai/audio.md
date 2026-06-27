# 音频接口

音频接口兼容 OpenAI 风格的语音合成和语音转写路径。

## 路由

| 路由 | 说明 |
| --- | --- |
| [POST /v1/audio/speech](/api/ai/routes/v1-audio-speech) | 文本转语音。 |
| [POST /v1/audio/transcriptions](/api/ai/routes/v1-audio-transcriptions) | 音频转写。 |

## 默认模型

| 路由 | 默认模型 |
| --- | --- |
| `POST /v1/audio/speech` | `gpt-4o-mini-tts` |
| `POST /v1/audio/transcriptions` | `whisper-1` |
