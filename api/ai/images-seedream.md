# Seedream 图片接口

Seedream 图片通过 OpenAI 风格图片接口调用。后端会把 `seedream` 渠道类型识别为 OpenAI 图片协议，使用 `/v1/images/generations` 或 `/v1/images/edits` 转发到上游。

## 路由

| 路由 | 说明 |
| --- | --- |
| [POST /v1/images/generations](/api/ai/routes/v1-images-generations) | 创建 Seedream 图片生成任务或同步生成请求。 |
| [GET /v1/images/generations/:id](/api/ai/routes/v1-images-generations-get) | 查询图片生成任务状态和结果。 |
| [POST /v1/images/edits](/api/ai/routes/v1-images-edits) | Seedream 图片编辑、参考图、重绘等能力。 |
| [POST /v1/uploads/images](/api/ai/routes/v1-uploads-images) | 上传本地图片并获得可作为参考图的 data URL。 |
| [GET /v1/tasks/:id](/api/ai/routes/v1-tasks-id) | 统一任务查询入口，可查询图片兼容任务。 |

## 常用字段

| 字段 | 说明 |
| --- | --- |
| `model` | Seedream 模型名，例如平台配置的 `seedream-4.0`、`seedream-4.5`、`seedream-5.0-lite` 等。 |
| `prompt` | 图片提示词。 |
| `image` / `image_url` / `images` | 如上游支持，可用于图生图、参考图或编辑。 |
| `size` / `resolution` | 图片尺寸或清晰度档位，按上游支持透传。 |
| `n` | 生成图片数量，参与计费估算。 |
| `response_format` | `url` 或 `b64_json`，按上游支持透传。 |
| `output_format` | 输出图片格式，按上游支持透传。 |

## 示例

```json
{
  "model": "seedream-4.5",
  "prompt": "A clean product render of a pear-shaped smart speaker",
  "size": "2K",
  "n": 1
}
```
