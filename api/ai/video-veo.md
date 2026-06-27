# Veo 视频接口

Veo 视频不使用单独路径，而是通过统一的视频任务路由调用。调用时在 `model` 中填写平台配置的 Veo 模型名，例如 `veo3`、`veo-3`、`veo3-official` 或管理员实际配置的对外模型名。

## 路由

| 路由 | 说明 |
| --- | --- |
| [POST /v1/video/generations](/api/ai/routes/v1-video-generations-post) | 创建 Veo 视频生成任务。 |
| [GET /v1/video/generations/:id](/api/ai/routes/v1-video-generations-get) | 查询 Veo 视频任务状态和结果。 |
| [POST /v1/videos/:id/remix](/api/ai/routes/v1-videos-id-remix) | Veo remix 兼容入口。 |
| [GET /v1/tasks/:id](/api/ai/routes/v1-tasks-id) | 统一任务查询入口。 |

## 常用字段

| 字段 | 说明 |
| --- | --- |
| `model` | Veo 模型名，必须与平台模型配置一致。 |
| `prompt` | 视频提示词。 |
| `image_url` / `first_frame_image` | 图生视频或首帧控制字段，按上游 Veo 渠道能力透传。 |
| `resolution` / `size` / `quality` | 分辨率或质量档位，参与计费。 |
| `duration` / `seconds` | 视频时长，参与计费。 |
| `aspect_ratio` | 视频比例，按上游支持透传。 |
| `callback_url` | 如上游支持，可作为任务完成回调地址透传。 |

## 示例

```json
{
  "model": "veo3",
  "prompt": "A cinematic shot of a futuristic city at sunrise",
  "duration": 8,
  "resolution": "1080p",
  "aspect_ratio": "16:9"
}
```

## 与 APIMart Veo 文档的对应关系

| APIMart 能力 | 本项目入口 |
| --- | --- |
| VEO3 Video Generation | `POST /v1/video/generations`，`model` 使用平台配置的 Veo 模型名。 |
| VEO3 Official Video Generation | 同统一入口，通过不同 `model` 或渠道配置区分。 |
| VEO3 Video Remix | `POST /v1/videos/:id/remix`，后端会注入 `parent_task_id` 并转发上游 remix 路径。 |

更多通用视频任务字段见 [OpenAI 风格视频接口](/api/ai/video-openai)。
