# Midjourney 接口

Midjourney 接口采用异步任务模式。创建任务后，使用任务 ID 查询结果和可执行按钮。

## 创建任务

| 路由 | 说明 |
| --- | --- |
| [POST /v1/midjourney/generations](/api/ai/routes/v1-midjourney-generations) | 默认 Imagine 创建入口。 |
| [POST /v1/midjourney/generations/imagine](/api/ai/routes/v1-midjourney-generations-imagine) | Imagine 显式入口。 |
| [POST /v1/midjourney/generations/blend](/api/ai/routes/v1-midjourney-generations-action) | 多图混合。 |
| [POST /v1/midjourney/generations/describe](/api/ai/routes/v1-midjourney-generations-action) | 图像反推提示词。 |
| [POST /v1/midjourney/generations/edits](/api/ai/routes/v1-midjourney-generations-action) | 图片编辑。 |
| [POST /v1/midjourney/generations/high-variation](/api/ai/routes/v1-midjourney-generations-action) | 强变化。 |
| [POST /v1/midjourney/generations/inpaint](/api/ai/routes/v1-midjourney-generations-action) | 局部重绘。 |
| [POST /v1/midjourney/generations/low-variation](/api/ai/routes/v1-midjourney-generations-action) | 弱变化。 |
| [POST /v1/midjourney/generations/modal](/api/ai/routes/v1-midjourney-generations-action) | 提交 Modal 参数。 |
| [POST /v1/midjourney/generations/pan](/api/ai/routes/v1-midjourney-generations-action) | 平移扩图。 |
| [POST /v1/midjourney/generations/reroll](/api/ai/routes/v1-midjourney-generations-action) | 重新生成。 |
| [POST /v1/midjourney/generations/upscale](/api/ai/routes/v1-midjourney-generations-action) | 放大。 |
| [POST /v1/midjourney/generations/variation](/api/ai/routes/v1-midjourney-generations-action) | 变体。 |
| [POST /v1/midjourney/generations/video](/api/ai/routes/v1-midjourney-generations-action) | 图生视频。 |
| [POST /v1/midjourney/generations/zoom](/api/ai/routes/v1-midjourney-generations-action) | 缩放扩图。 |
| [POST /v1/midjourney/generations/remix](/api/ai/routes/v1-midjourney-generations-action) | Remix。 |

## 查询任务

| 路由 | 说明 |
| --- | --- |
| [GET /v1/midjourney/:id](/api/ai/routes/v1-midjourney-id) | 查询 Midjourney 任务结果。 |
