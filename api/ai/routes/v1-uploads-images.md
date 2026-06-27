# POST `/v1/uploads/images`

上传图片并返回 data URL，可用于图片编辑、图生图、图生视频等接口的参考图字段。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `POST` |
| 路径 | `/v1/uploads/images` |
| 鉴权 | API Key 或登录 JWT |
| Content-Type | `multipart/form-data` |

## Form 参数

| 参数 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| `file` | 是 | file | 图片文件，最大 20 MB，支持 JPEG、PNG、GIF、WebP。 |

## 返回值

```json
{
  "url": "data:image/png;base64,...",
  "filename": "input.png",
  "content_type": "image/png",
  "bytes": 12345,
  "created_at": 1760000000
}
```
