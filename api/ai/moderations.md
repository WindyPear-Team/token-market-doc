# 审核接口

审核接口兼容 OpenAI Moderations 路径。未传 `model` 时，后端默认使用 `omni-moderation-latest`。

## 路由

| 路由 | 说明 |
| --- | --- |
| [POST /v1/moderations](/api/ai/routes/v1-moderations) | 内容审核，支持文本、图片或上游兼容输入结构。 |
