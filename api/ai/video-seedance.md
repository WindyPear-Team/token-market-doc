# Seedance 视频接口

Seedance 视频通过统一视频任务路由调用。后端会把 `seedance` 渠道类型识别为 OpenAI 风格视频协议，并转发到上游 `/v1/video/generations`。

## 路由

| 路由 | 说明 |
| --- | --- |
| [POST /v1/video/generations](/api/ai/routes/v1-video-generations-post) | 创建 Seedance 视频任务。 |
| [GET /v1/video/generations/:id](/api/ai/routes/v1-video-generations-get) | 查询 Seedance 视频任务状态和结果。 |
| [POST /v1/seedance2/private-avatar](/api/ai/routes/v1-seedance2-private-avatar) | 提交 Seedance 2.0 私有数字人素材任务。 |
| [GET /v1/tasks/:id](/api/ai/routes/v1-tasks-id) | 统一任务查询入口，可查询 Seedance 兼容任务。 |

## 常用字段

| 字段 | 说明 |
| --- | --- |
| `model` | Seedance 模型名，例如平台配置的 `doubao-seedance-1-5-pro`、`doubao-seedance-2.0` 等。 |
| `prompt` | 视频提示词。 |
| `image_url` / `first_frame_image` | 图生视频首帧。 |
| `last_frame_image` | 如上游支持，可用于首尾帧视频。 |
| `resolution` / `size` / `quality` | 分辨率或质量档位，参与计费。 |
| `duration` / `seconds` | 视频时长，参与计费。 |
| `aspect_ratio` | 视频比例，按上游能力透传。 |
| `audio` / `generate_audio` | 如上游支持，可控制是否生成音频。 |
| `callback_url` | 如上游支持，可作为任务完成回调地址透传。 |

## 私有数字人素材

`POST /v1/seedance2/private-avatar` 默认模型为 `doubao-seedance-2.0`。如果请求体没有 `model`，后端会自动补该默认值；请求体其他字段会透传到上游 `/v1/seedance2/private-avatar`。

## 示例

```json
{
  "model": "doubao-seedance-2.0",
  "prompt": "A product demo video with smooth camera movement",
  "duration": 8,
  "resolution": "1080p",
  "aspect_ratio": "16:9"
}
```
