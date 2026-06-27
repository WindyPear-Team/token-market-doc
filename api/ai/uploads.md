# 上传接口

上传接口用于把本地图片转换为可直接传给图片、视频接口的 data URL。当前后端会读取 multipart 文件并返回 base64 data URL，不会把文件持久化到对象存储。

## 路由

| 路由 | 说明 |
| --- | --- |
| [POST /v1/uploads/images](/api/ai/routes/v1-uploads-images) | 上传图片，返回 `data:<content-type>;base64,...` URL。 |

## 限制

| 项 | 说明 |
| --- | --- |
| 字段名 | `file` |
| 最大大小 | 20 MB |
| 支持格式 | JPEG、PNG、GIF、WebP |
