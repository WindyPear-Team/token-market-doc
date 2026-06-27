# AI 网关接口

网关接口使用 API Key 或登录 JWT。API Key 认证方式：

```text
Authorization: Bearer sk-your-key
```

也支持：

```text
x-api-key: sk-your-key
```

## 端点

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/v1/models` | 无 | 无 | OpenAI 风格模型列表：`{ "object": "list", "data": [...] }`。 |
| `POST` | `/v1/chat/completions` | 无 | OpenAI Chat Completions 请求体。 | OpenAI Chat Completions 响应或 SSE。 |
| `POST` | `/v1/completions` | 无 | OpenAI Completions 请求体。 | OpenAI Completions 响应。 |
| `POST` | `/v1/responses` | 无 | OpenAI Responses 请求体。 | OpenAI Responses 响应。 |
| `POST` | `/v1/images/generations` | 无 | `model`、`prompt`、`n`、`size` 等。 | OpenAI 图片生成响应。 |
| `POST` | `/v1/images/edits` | 无 | multipart form，包含 `model`、`image`、`prompt` 等。 | OpenAI 图片编辑响应。 |
| `POST` | `/v1/videos/generations` | 无 | `model`、`prompt`、`size/resolution/aspect_ratio`、`duration` 等。 | 上游原始视频生成响应。 |
| `POST` | `/v1/video/generations` | 无 | OpenAI 风格视频任务请求体。 | 本地视频任务对象。 |
| `GET` | `/v1/video/generations/:id` | Path: `id`。 | 无 | 本地视频任务对象。 |
| `POST` | `/v1/videos/image2video` | 无 | Kling 风格图生视频请求体，支持 `model_name`。 | 本地视频任务对象。 |
| `GET` | `/v1/videos/image2video/:id` | Path: `id`。 | 无 | 本地视频任务对象。 |
| `POST` | `/v1/video/tasks` | 无 | 视频任务请求体。 | 本地视频任务对象。 |
| `GET` | `/v1/video/tasks/:id` | Path: `id`。 | 无 | 本地视频任务对象。 |
| `POST` | `/v1/videos/tasks` | 无 | 视频任务请求体。 | 本地视频任务对象。 |
| `GET` | `/v1/videos/tasks/:id` | Path: `id`。 | 无 | 本地视频任务对象。 |
| `POST` | `/v1/messages` | 无 | Claude Messages 请求体。 | Claude Messages 响应或转换后的响应。 |
| `POST` | `/v1/models/:modelAction` | Path: `modelAction`，例如 `gemini-pro:generateContent`。 | Gemini 请求体。 | Gemini 响应。 |
| `POST` | `/v1beta/models/:modelAction` | Path: `modelAction`。 | Gemini 请求体。 | Gemini 响应。 |

## Chat Completions

请求：

```json
{
  "model": "gpt-4o",
  "messages": [
    { "role": "user", "content": "Hello" }
  ],
  "stream": false
}
```

返回：

```json
{
  "id": "chatcmpl_xxx",
  "object": "chat.completion",
  "choices": [],
  "usage": {}
}
```

## 图片生成

请求：

```json
{
  "model": "image-model",
  "prompt": "A pear on a windy table",
  "n": 1,
  "size": "1024x1024"
}
```

返回：

```json
{
  "created": 1760000000,
  "data": [
    { "url": "https://example.com/image.png" }
  ]
}
```

## OpenAI 风格视频任务

请求：

```json
{
  "model": "video-model",
  "prompt": "A cinematic pear falling into water",
  "size": "720p",
  "duration": 5
}
```

返回：

```json
{
  "id": "vtask_xxx",
  "object": "video.generation",
  "model": "video-model",
  "status": "queued",
  "cost": "0.35",
  "upstream_id": "provider-task-id",
  "created_at": 1760000000,
  "updated_at": 1760000000,
  "upstream_response": {},
  "data": []
}
```

## Kling 图生视频

请求：

```json
{
  "model_name": "kling-video-model",
  "image": "https://example.com/input.png",
  "prompt": "A pear dancing in the wind",
  "aspect_ratio": "16:9",
  "duration": "5"
}
```

说明：

| 字段 | 位置 | 类型 | 说明 |
| --- | --- | --- | --- |
| `model_name` | Body | string | 客户端模型名，也支持 `model`。 |
| `image` | Body | string | 图片 URL 或上游支持的图片数据。 |
| `prompt` | Body | string | 提示词。 |
| `negative_prompt` | Body | string | 负面提示词。 |
| `aspect_ratio` | Body | string | 例如 `16:9`、`9:16`、`1:1`。 |
| `duration` | Body | string/integer | 视频时长。 |

返回同本地视频任务对象。

## 常见错误

| 状态码 | 说明 |
| --- | --- |
| `400` | 请求体不合法、缺少 `model`、不支持的上游协议、视频计费档位不允许。 |
| `401` | 缺少或无效凭据。 |
| `403` | API Key 不允许访问该模型或来源 IP 不允许。 |
| `402` | 余额不足或 API Key 额度不足。 |
| `429` | 触发限流。 |
| `502` | 上游请求失败或响应读取失败。 |
