# 管理员接口

管理员接口前缀为 `/api`，需要：

```text
Authorization: Bearer <jwt>
```

并且当前用户必须是管理员。

## 系统设置

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/settings` | 无 | 无 | 系统设置对象。 |
| `PUT` | `/api/settings` | 无 | 系统设置字段。 | 更新后的系统设置对象或成功响应。 |

设置字段包含站点名称、注册开关、OIDC、SMTP、支付、主题、状态页、公开价格、聊天页面模式等。字段以 `SystemAPI` 当前结构为准。

## 状态监控

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/status-monitors` | 无 | 无 | 状态监控列表。 |
| `POST` | `/api/status-monitors` | 无 | 监控名称、类型、目标、启用状态等。 | 新建的状态监控。 |
| `PUT` | `/api/status-monitors/:id` | Path: `id`。 | 监控名称、类型、目标、启用状态等。 | 更新后的状态监控。 |
| `DELETE` | `/api/status-monitors/:id` | Path: `id`。 | 无 | 删除成功响应。 |
| `POST` | `/api/status-monitors/:id/check` | Path: `id`。 | 无 | 本次检查结果。 |

## 公告

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/announcements` | 无 | 无 | 公告列表。 |
| `POST` | `/api/announcements` | 无 | `title`、`content`、`enabled`、`sort_order`。 | 新建公告。 |
| `PUT` | `/api/announcements/:id` | Path: `id`。 | `title`、`content`、`enabled`、`sort_order`。 | 更新公告。 |
| `DELETE` | `/api/announcements/:id` | Path: `id`。 | 无 | 删除成功响应。 |

## 上级渠道

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/channels` | 无 | 无 | 上级渠道列表。 |
| `POST` | `/api/channels` | 无 | 渠道名称、类型、Base URL、API Key、权重、优先级、启用状态、用户渠道等。 | 新建渠道。 |
| `PUT` | `/api/channels/:id` | Path: `id`。 | 渠道字段。 | 更新后的渠道。 |
| `DELETE` | `/api/channels/:id` | Path: `id`。 | 无 | 删除成功响应。 |
| `PUT` | `/api/channels/:id/group-multipliers` | Path: `id`。 | 分组倍率配置。 | 更新成功响应。 |
| `GET` | `/api/channels/:id/models` | Path: `id`。 | 无 | 渠道模型配置列表。 |
| `POST` | `/api/channels/:id/models` | Path: `id`。 | 模型配置字段。 | 新建渠道模型配置。 |
| `POST` | `/api/channels/sync` | 无 | 可选渠道 ID 列表。 | 同步结果。 |

渠道类型包括 `openai`、`responses`、`openai-video`、`kling`、`claude`、`gemini` 等。

## 全局模型

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/models` | 无 | 无 | 全局模型列表。 |
| `POST` | `/api/models` | 无 | 模型名称、供应商、价格、限流、计费类型、视频计费配置等。 | 新建模型。 |
| `PUT` | `/api/models/:id` | Path: `id`。 | 模型字段。 | 更新后的模型。 |
| `DELETE` | `/api/models/:id` | Path: `id`。 | 无 | 删除成功响应。 |
| `POST` | `/api/models/sync` | 无 | 同步选项。 | 同步结果。 |
| `POST` | `/api/models/sync/preview` | 无 | 渠道和同步格式。 | 预览结果。 |
| `POST` | `/api/models/sync/preview/browser` | 无 | 浏览器获取的原始内容和来源。 | 预览结果。 |
| `POST` | `/api/models/sync/apply` | 无 | 预览项。 | 应用结果。 |
| `POST` | `/api/models/prices/sync/preview` | 无 | 渠道和价格同步格式。 | 价格预览结果。 |
| `POST` | `/api/models/prices/sync/preview/browser` | 无 | 浏览器获取的价格原始内容和来源。 | 价格预览结果。 |
| `POST` | `/api/models/prices/sync/apply` | 无 | 价格预览项。 | 应用结果。 |

## 渠道模型配置

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `PUT` | `/api/channel-models/:id` | Path: `id`。 | 渠道模型字段，如上游模型名、价格覆盖、启用状态。 | 更新后的渠道模型配置。 |
| `DELETE` | `/api/channel-models/:id` | Path: `id`。 | 无 | 删除成功响应。 |
| `PUT` | `/api/channel-models/:id/group-multipliers` | Path: `id`。 | 分组倍率配置。 | 更新成功响应。 |

## 用户渠道

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/user-channels` | 无 | 无 | 用户渠道列表。 |
| `POST` | `/api/user-channels` | 无 | 名称、路由算法、启用状态。 | 新建用户渠道。 |
| `PUT` | `/api/user-channels/:id` | Path: `id`。 | 用户渠道字段。 | 更新后的用户渠道。 |
| `DELETE` | `/api/user-channels/:id` | Path: `id`。 | 无 | 删除成功响应。 |

## 分组

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/groups` | 无 | 无 | 分组列表。 |
| `POST` | `/api/groups` | 无 | 分组名称、倍率、默认标记等。 | 新建分组。 |
| `PUT` | `/api/groups/:id` | Path: `id`。 | 分组字段。 | 更新后的分组。 |
| `DELETE` | `/api/groups/:id` | Path: `id`。 | 无 | 删除成功响应。 |

## 用户

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/users` | Query: 分页、搜索等。 | 无 | 用户列表或分页对象。 |
| `PUT` | `/api/users/:id` | Path: `id`。 | 用户字段，如余额、分组、管理员状态、启用状态。 | 更新后的用户。 |
| `DELETE` | `/api/users/:id` | Path: `id`。 | 无 | 删除成功响应。 |
| `GET` | `/api/referral-commissions` | Query: 分页、时间范围。 | 无 | 邀请返佣记录。 |

## 统计

| 方法 | 路径 | 参数 | 请求体 | 返回值 |
| --- | --- | --- | --- | --- |
| `GET` | `/api/logs` | Query: 分页、用户、模型、时间范围等。 | 无 | 用量日志或分页对象。 |
| `GET` | `/api/stats` | 无 | 无 | 管理员仪表盘统计。 |
| `GET` | `/api/channel-usage` | Query: 时间范围。 | 无 | 用户渠道和上级渠道用量统计。 |
