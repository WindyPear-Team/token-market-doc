# AI API 全路由

本文档按能力分类整理 AI 网关对外暴露的所有路由，结构参考 APIMart 的 API 文档索引：先按文本、图片、视频、任务、模型与协议兼容能力分组，再在每组内列出可直接调用的接口。所有接口默认使用 OpenAI 风格鉴权：`Authorization: Bearer sk-...`，也兼容 `x-api-key` Header 或 `?key=sk-...` 查询参数。

## 快速选择

| 场景 | 推荐入口 | 说明 |
| --- | --- | --- |
| 查询 API Key 额度 | [GET /v1/balance](/api/ai/routes/v1-balance) | 查询当前 API Key 剩余额度和已用额度。 |
| 获取可用模型 | [GET /v1/models](/api/ai/routes/v1-models) | 查询当前 API Key 或 JWT 可访问的模型列表。 |
| 通用文本对话 | [POST /v1/chat/completions](/api/ai/routes/v1-chat-completions) | OpenAI Chat Completions 兼容入口，适合绝大多数 SDK 和客户端。 |
| 新版 OpenAI 多模态 | [POST /v1/responses](/api/ai/routes/v1-responses) | OpenAI Responses 兼容入口，适合多模态输入、工具调用和结构化输出。 |
| 语音合成 | [POST /v1/audio/speech](/api/ai/routes/v1-audio-speech) | OpenAI 风格 TTS 接口。 |
| 音频转写 | [POST /v1/audio/transcriptions](/api/ai/routes/v1-audio-transcriptions) | Whisper 风格转写接口。 |
| 内容审核 | [POST /v1/moderations](/api/ai/routes/v1-moderations) | OpenAI Moderations 兼容接口。 |
| Claude 客户端 | [POST /v1/messages](/api/ai/routes/v1-messages) | Claude Messages 兼容入口。 |
| Gemini 客户端 | [POST /v1/models/:modelAction](/api/ai/routes/v1-models-model-action) | Gemini v1 原生格式兼容入口。 |
| 上传参考图 | [POST /v1/uploads/images](/api/ai/routes/v1-uploads-images) | 上传图片并获得 data URL。 |
| 图片生成 | [POST /v1/images/generations](/api/ai/routes/v1-images-generations) | OpenAI 风格图片生成。 |
| Seedream 图片 | [POST /v1/images/generations](/api/ai/routes/v1-images-generations) | 使用统一图片入口，`model` 填写 Seedream 模型名。 |
| 图片编辑 | [POST /v1/images/edits](/api/ai/routes/v1-images-edits) | OpenAI 风格图片编辑。 |
| 视频生成任务 | [POST /v1/video/generations](/api/ai/routes/v1-video-generations-post) | 推荐的视频任务创建入口。 |
| Veo 视频 | [POST /v1/video/generations](/api/ai/routes/v1-video-generations-post) | 使用统一视频任务入口，`model` 填写 Veo 模型名。 |
| Seedance 视频 | [POST /v1/video/generations](/api/ai/routes/v1-video-generations-post) | 使用统一视频任务入口，`model` 填写 Seedance 模型名。 |
| 查询视频任务 | [GET /v1/video/generations/:id](/api/ai/routes/v1-video-generations-get) | 查询本地视频任务状态和结果。 |

## 公共规则

| 项 | 说明 |
| --- | --- |
| Base URL | 使用站点部署的 API 网关域名，例如 `https://your-domain.example`。 |
| 鉴权 | `Authorization: Bearer sk-...`、`x-api-key: sk-...` 或 `?key=sk-...`。 |
| 登录态 | 控制台登录 JWT 也可访问部分接口，生产调用建议使用 API Key。 |
| JSON 接口 | 文本、模型、图片生成、视频任务默认使用 `application/json`。 |
| 文件上传 | 图片编辑可使用 `multipart/form-data`，字段按上游协议透传。 |
| 流式输出 | 文本类接口通过 `stream: true` 返回 `text/event-stream`。 |
| 透传策略 | 未在文档表格中列出的上游兼容字段通常会保留并转发。 |
| 计费 | 后端优先读取上游 `usage`；无 `usage` 时按模型、输入、输出、图片数、视频规格等估算。 |

## 模型

| 路由 | 用途 | 文档 |
| --- | --- | --- |
| `GET /v1/balance` | 查询当前 API Key 额度。 | [查看](/api/ai/routes/v1-balance) |
| `GET /v1/user/balance` | 查询当前用户账户余额。 | [查看](/api/ai/routes/v1-user-balance) |
| `GET /v1/models` | 列出当前凭据可访问的模型。 | [查看](/api/ai/routes/v1-models) |

## 文本与对话

| 路由 | 协议 | 用途 | 文档 |
| --- | --- | --- | --- |
| `POST /v1/chat/completions` | OpenAI Chat Completions | 通用对话、工具调用、流式输出。 | [查看](/api/ai/routes/v1-chat-completions) |
| `POST /v1/completions` | OpenAI legacy Completions | 旧版补全文本接口。 | [查看](/api/ai/routes/v1-completions) |
| `POST /v1/responses` | OpenAI Responses | 新版多模态输入、工具调用、结构化响应。 | [查看](/api/ai/routes/v1-responses) |
| `POST /v1/audio/speech` | OpenAI Audio | 文本转语音。 | [查看](/api/ai/routes/v1-audio-speech) |
| `POST /v1/audio/transcriptions` | OpenAI Audio | 音频转写。 | [查看](/api/ai/routes/v1-audio-transcriptions) |
| `POST /v1/moderations` | OpenAI Moderations | 内容审核。 | [查看](/api/ai/routes/v1-moderations) |
| `POST /v1/messages` | Claude Messages | Claude 原生消息格式。 | [查看](/api/ai/routes/v1-messages) |
| `POST /v1/models/:modelAction` | Gemini v1 | Gemini `generateContent`、`streamGenerateContent` 等动作入口。 | [查看](/api/ai/routes/v1-models-model-action) |
| `POST /v1beta/models/:modelAction` | Gemini v1beta | Gemini v1beta 兼容入口。 | [查看](/api/ai/routes/v1beta-models-model-action) |

## 图片

| 路由 | 用途 | 文档 |
| --- | --- | --- |
| `POST /v1/uploads/images` | 上传参考图，返回 data URL。 | [查看](/api/ai/routes/v1-uploads-images) |
| `POST /v1/images/generations` | 文生图、按上游支持透传尺寸、质量、格式等字段。 | [查看](/api/ai/routes/v1-images-generations) |
| `GET /v1/images/generations/:id` | 查询图片异步任务状态和结果。 | [查看](/api/ai/routes/v1-images-generations-get) |
| `POST /v1/images/edits` | 图像编辑、参考图、遮罩等 OpenAI 风格字段。 | [查看](/api/ai/routes/v1-images-edits) |

## 视频与异步任务

| 路由 | 用途 | 推荐程度 | 文档 |
| --- | --- | --- | --- |
| `POST /v1/video/generations` | 创建 OpenAI 风格视频任务。 | 推荐 | [查看](/api/ai/routes/v1-video-generations-post) |
| `GET /v1/video/generations/:id` | 查询视频任务状态和结果。 | 推荐 | [查看](/api/ai/routes/v1-video-generations-get) |
| `POST /v1/video/tasks` | 创建视频任务兼容别名。 | 兼容 | [查看](/api/ai/routes/v1-video-tasks-post) |
| `GET /v1/video/tasks/:id` | 查询视频任务兼容别名。 | 兼容 | [查看](/api/ai/routes/v1-video-tasks-get) |
| `POST /v1/videos/tasks` | 创建视频任务兼容别名。 | 兼容 | [查看](/api/ai/routes/v1-videos-tasks-post) |
| `GET /v1/videos/tasks/:id` | 查询视频任务兼容别名。 | 兼容 | [查看](/api/ai/routes/v1-videos-tasks-get) |
| `POST /v1/videos/generations` | 旧版视频生成转发接口。 | 旧版 | [查看](/api/ai/routes/v1-videos-generations) |
| `GET /v1/videos/generations/:id` | 旧版视频任务查询兼容入口。 | 兼容 | [查看](/api/ai/routes/v1-videos-generations-get) |
| `POST /v1/videos/:id/remix` | Veo 等视频模型的 remix 兼容入口。 | 兼容 | [查看](/api/ai/routes/v1-videos-id-remix) |
| `POST /v1/seedance2/private-avatar` | Seedance 2.0 私有数字人素材提交任务。 | 专用 | [查看](/api/ai/routes/v1-seedance2-private-avatar) |
| `POST /v1/videos/image2video` | Kling 图生视频创建任务。 | 兼容 | [查看](/api/ai/routes/v1-videos-image2video-post) |
| `GET /v1/videos/image2video/:id` | Kling 图生视频查询任务。 | 兼容 | [查看](/api/ai/routes/v1-videos-image2video-get) |

## 任务

| 路由 | 用途 | 文档 |
| --- | --- | --- |
| `GET /v1/tasks/:id` | 统一查询图片、视频、Midjourney 等兼容任务。 | [查看](/api/ai/routes/v1-tasks-id) |

## Midjourney

| 路由 | 用途 | 文档 |
| --- | --- | --- |
| `POST /v1/midjourney/generations` | Imagine 默认创建入口。 | [查看](/api/ai/routes/v1-midjourney-generations) |
| `POST /v1/midjourney/generations/imagine` | Imagine 显式入口。 | [查看](/api/ai/routes/v1-midjourney-generations-imagine) |
| `POST /v1/midjourney/generations/:action` | Blend、Describe、Upscale、Variation、Video、Remix 等动作入口。 | [查看](/api/ai/routes/v1-midjourney-generations-action) |
| `GET /v1/midjourney/:id` | 查询 Midjourney 任务状态和结果。 | [查看](/api/ai/routes/v1-midjourney-id) |

## 与 APIMart 索引的能力映射

| APIMart 分类 | 本项目对应路由 | 说明 |
| --- | --- | --- |
| Account | `/v1/balance`、`/v1/user/balance` | API Key 额度和用户余额查询已覆盖。 |
| Texts | `/v1/chat/completions`、`/v1/responses`、`/v1/messages`、Gemini 路由 | 文本和多模态对话能力已覆盖。 |
| Audios | `/v1/audio/speech`、`/v1/audio/transcriptions` | 语音合成和音频转写已覆盖。 |
| Moderations | `/v1/moderations` | 内容审核已覆盖。 |
| Uploads | `/v1/uploads/images` | 图片上传返回 data URL。 |
| Images | `/v1/images/generations`、`/v1/images/generations/:id`、`/v1/images/edits`、Midjourney 路由 | 按 OpenAI 风格入口统一转发到上游图片模型，支持 Seedream 和 Midjourney。 |
| Videos | `/v1/video/generations`、视频任务别名、Veo remix、Seedance 私有素材、Kling 图生视频 | 采用任务化接口，创建后通过任务 ID 查询。 |
| Tasks | `GET /v1/tasks/:id`、视频/图片专用查询路径 | 可统一查询图片、视频、Midjourney 等兼容任务。 |
| Uploads | 无独立 AI 上传路由 | 需要上传的字段按图片编辑或上游协议字段透传。 |
| Audios | 当前 AI 网关未暴露音频路由 | 未列入本项目 AI 全路由。 |
| Moderations | 当前 AI 网关未暴露审核路由 | 敏感词和安全校验在网关内部执行。 |
