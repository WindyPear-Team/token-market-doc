# AI 网关接口

AI 网关接口使用 API Key 或登录 JWT。

```text
Authorization: Bearer sk-your-key
```

也支持：

```text
x-api-key: sk-your-key
```

本页是 AI 网关索引。每一个 AI 路由都有单独页面，页面内写明 Header、Query、Path、Body/Form 参数和返回值。

## 按类型查看

| 分类 | 路由 |
| --- | --- |
| [账户与额度](/api/ai/account) | `GET /v1/balance`、`GET /v1/user/balance` |
| [模型列表](/api/ai/models) | `GET /v1/models` |
| [OpenAI Chat / Completions](/api/ai/openai-chat) | `POST /v1/chat/completions`、`POST /v1/completions` |
| [OpenAI Responses](/api/ai/responses) | `POST /v1/responses` |
| [音频接口](/api/ai/audio) | `POST /v1/audio/speech`、`POST /v1/audio/transcriptions` |
| [审核接口](/api/ai/moderations) | `POST /v1/moderations` |
| [上传接口](/api/ai/uploads) | `POST /v1/uploads/images` |
| [图片接口](/api/ai/images) | `POST /v1/images/generations`、`GET /v1/images/generations/:id`、`POST /v1/images/edits` |
| [Seedream 图片](/api/ai/images-seedream) | Seedream 图片生成、查询、编辑和上传参考图 |
| [Midjourney](/api/ai/midjourney) | Midjourney 生成、动作和查询接口 |
| [OpenAI 风格视频](/api/ai/video-openai) | OpenAI 风格视频路由和兼容别名 |
| [Veo 视频](/api/ai/video-veo) | Veo 视频生成、查询和 remix |
| [Seedance 视频](/api/ai/video-seedance) | Seedance 视频生成、查询和私有数字人素材 |
| [Kling 视频](/api/ai/video-kling) | Kling 图生视频创建和查询接口 |
| [Claude](/api/ai/claude) | `POST /v1/messages` |
| [Gemini](/api/ai/gemini) | `POST /v1/models/:modelAction`、`POST /v1beta/models/:modelAction` |

## 每个路由

| 路由 | 页面 |
| --- | --- |
| `GET /v1/balance` | [详情](/api/ai/routes/v1-balance) |
| `GET /v1/user/balance` | [详情](/api/ai/routes/v1-user-balance) |
| `GET /v1/models` | [详情](/api/ai/routes/v1-models) |
| `POST /v1/chat/completions` | [详情](/api/ai/routes/v1-chat-completions) |
| `POST /v1/completions` | [详情](/api/ai/routes/v1-completions) |
| `POST /v1/responses` | [详情](/api/ai/routes/v1-responses) |
| `POST /v1/audio/speech` | [详情](/api/ai/routes/v1-audio-speech) |
| `POST /v1/audio/transcriptions` | [详情](/api/ai/routes/v1-audio-transcriptions) |
| `POST /v1/moderations` | [详情](/api/ai/routes/v1-moderations) |
| `POST /v1/uploads/images` | [详情](/api/ai/routes/v1-uploads-images) |
| `POST /v1/images/generations` | [详情](/api/ai/routes/v1-images-generations) |
| `GET /v1/images/generations/:id` | [详情](/api/ai/routes/v1-images-generations-get) |
| `POST /v1/images/edits` | [详情](/api/ai/routes/v1-images-edits) |
| `POST /v1/videos/generations` | [详情](/api/ai/routes/v1-videos-generations) |
| `GET /v1/videos/generations/:id` | [详情](/api/ai/routes/v1-videos-generations-get) |
| `POST /v1/videos/:id/remix` | [详情](/api/ai/routes/v1-videos-id-remix) |
| `POST /v1/seedance2/private-avatar` | [详情](/api/ai/routes/v1-seedance2-private-avatar) |
| `GET /v1/tasks/:id` | [详情](/api/ai/routes/v1-tasks-id) |
| `POST /v1/video/generations` | [详情](/api/ai/routes/v1-video-generations-post) |
| `GET /v1/video/generations/:id` | [详情](/api/ai/routes/v1-video-generations-get) |
| `POST /v1/videos/image2video` | [详情](/api/ai/routes/v1-videos-image2video-post) |
| `GET /v1/videos/image2video/:id` | [详情](/api/ai/routes/v1-videos-image2video-get) |
| `POST /v1/video/tasks` | [详情](/api/ai/routes/v1-video-tasks-post) |
| `GET /v1/video/tasks/:id` | [详情](/api/ai/routes/v1-video-tasks-get) |
| `POST /v1/videos/tasks` | [详情](/api/ai/routes/v1-videos-tasks-post) |
| `GET /v1/videos/tasks/:id` | [详情](/api/ai/routes/v1-videos-tasks-get) |
| `POST /v1/midjourney/generations` | [详情](/api/ai/routes/v1-midjourney-generations) |
| `POST /v1/midjourney/generations/imagine` | [详情](/api/ai/routes/v1-midjourney-generations-imagine) |
| `POST /v1/midjourney/generations/:action` | [详情](/api/ai/routes/v1-midjourney-generations-action) |
| `GET /v1/midjourney/:id` | [详情](/api/ai/routes/v1-midjourney-id) |
| `POST /v1/messages` | [详情](/api/ai/routes/v1-messages) |
| `POST /v1/models/:modelAction` | [详情](/api/ai/routes/v1-models-model-action) |
| `POST /v1beta/models/:modelAction` | [详情](/api/ai/routes/v1beta-models-model-action) |

## 通用错误

| 状态码 | 说明 |
| --- | --- |
| `400` | 请求体不合法、缺少模型、上游协议不支持、计费档位不允许。 |
| `401` | 缺少或无效凭据。 |
| `402` | 余额不足或 API Key 额度不足。 |
| `403` | API Key 不允许访问模型、来源 IP 不允许。 |
| `429` | 触发限流。 |
| `502` | 上游请求失败或响应读取失败。 |
