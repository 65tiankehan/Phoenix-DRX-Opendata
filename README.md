# Phoenix-DRX-Opendata

Phoenix DRX 公告与远程急停的公开数据仓库。客户端启动时从本仓库拉取 `announcement.json`（raw.githubusercontent → ghfast.top 反代 → jsDelivr 三镜像依次尝试，全部失败回退本地缓存）。

## announcement.json 格式

```json
{
  "version": 3,
  "killSwitch": false,
  "announcements": [
    {
      "id": "唯一短标识（必填，非空）",
      "title": "公告标题（必填，非空）",
      "body": "公告正文（必填，非空）",
      "actionLabel": "可选，动作按钮文字",
      "actionUrl": "可选，动作按钮跳转链接",
      "date": "可选，发布日期 YYYY-MM-DD"
    }
  ]
}
```

字段纪律：

- `version` 必填（数字）。缺失或解析失败时客户端视为载荷损坏，自动换下一个镜像。
- `killSwitch` 设为 `true` 时客户端将公告视为空（远程急停，用于紧急下架客户端版本）。
- 单条公告缺 `id` / `title` / `body` 任一非空字段即被客户端丢弃，不影响其余条目。
- `date` 等额外字段客户端不消费，可自由补充。

## 发布流程

直接编辑本文件并推送到 `main` 分支即可生效；jsDelivr 有约 12 小时缓存，前两个镜像为实时。
