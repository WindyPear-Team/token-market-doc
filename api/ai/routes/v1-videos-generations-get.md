# GET `/v1/videos/generations/:id`

旧版视频任务查询兼容入口。用于查询通过旧版 `/v1/videos/generations` 或兼容任务接口创建的视频任务。

## 请求

| 项 | 内容 |
| --- | --- |
| 方法 | `GET` |
| 路径 | `/v1/videos/generations/:id` |
| 鉴权 | API Key 或登录 JWT |

## 参数

Header、Query、Path 参数同 [GET /v1/tasks/:id](/api/ai/routes/v1-tasks-id)。

## 返回值

返回格式同统一任务查询：

```json
{
  "code": 200,
  "data": {
    "id": "task_xxx",
    "status": "succeeded",
    "result": {},
    "upstream_response": {}
  }
}
```
