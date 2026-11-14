# 视频号数据接口（WeChat Channels API）：视频搜索、账号作品、评论、直播回放、互动数据

**视频号数据 API · 视频号视频搜索 · 视频号评论采集 · 视频号账号作品 · 视频号直播回放 · 视频号互动数据。**

这个仓库是 [okdata](https://okdata.online/zh/?src=gh-wechat-channels-api) 的微信视频号接口示例：15 个接口在线可用，一个 API Key 调用，按次计费（$0.015 起），失败不扣费。不用登录平台账号，不用 Cookie，不开浏览器，所以也不存在账号被风控的问题。

[免费注册拿 Key（送 $0.1 试用额度）](https://okdata.online/zh/signup/?src=gh-wechat-channels-api) · [全部接口文档](https://okdata.online/zh/apis/?src=gh-wechat-channels-api) · [接入 AI（MCP）](https://okdata.online/zh/mcp/?src=gh-wechat-channels-api)

## 接口清单

| 接口 | 说明 | 价格 | 路径 |
|---|---|---|---|
| [视频号视频搜索](https://okdata.online/zh/apis/wechat_channels/videos/search/) | 通过微信搜一搜按关键词搜视频号视频，可按相关、最新或最热排，可按发布时间筛选：描述、账号名称和头像、发布时间、时长和封面（url）。id 是 export/ 开头的加密 ID，传给 wechat_channels.videos.get 可以拿到视频、数字 ID 和账号 ID；它会过期，搜到后尽快用。 | $0.02 / 次 | `GET /v1/wechat_channels/videos/search` |
| [视频号账号搜索](https://okdata.online/zh/apis/wechat_channels/users/search/) | 通过微信搜一搜按名称找视频号账号：账号 ID（v2_…@finder）、名称、头像和认证主体。搜一搜通常只返回名称最匹配的那一个。 | $0.02 / 次 | `GET /v1/wechat_channels/users/search` |
| [视频号账号信息](https://okdata.online/zh/apis/wechat_channels/users/get/) | 按账号 ID 取视频号账号：名称、签名、头像、IP 属地、作品数、累计直播时长和关联的公众号。微信不公开时，粉丝数和获赞数为 null。 | $0.02 / 次 | `GET /v1/wechat_channels/users/get` |
| [视频号账号作品](https://okdata.online/zh/apis/wechat_channels/users/videos/list/) | 账号发布的视频，从新到旧，每页约 15 条：描述、发布时间、点赞、评论、转发和收藏、时长。url 是视频文件地址（已加密，用同一次返回的 ext.decode_key 解密）。 | $0.02 / 次 | `GET /v1/wechat_channels/users/videos/list` |
| [视频号作品详情](https://okdata.online/zh/apis/wechat_channels/videos/get/) | 按作品 ID、搜索结果的 export/ 加密 ID 或分享链接取一个视频：描述、作者（含账号 ID）、发布时间、点赞、评论、转发、收藏和位置。url 是视频文件地址（已加密，用同一次返回的 ext.decode_key 解密）。 | $0.02 / 次 | `GET /v1/wechat_channels/videos/get` |
| [视频号作品评论](https://okdata.online/zh/apis/wechat_channels/videos/comments/list/) | 视频的一级评论，按热度排：内容、评论者、点赞、回复数、发布时间和 IP 属地。 | $0.015 / 次 | `GET /v1/wechat_channels/videos/comments/list` |
| [视频号评论回复](https://okdata.online/zh/apis/wechat_channels/comments/replies/list/) | 按评论 ID 和所在作品 ID 取一级评论下的回复：内容、回复者、点赞、发布时间和 IP 属地。 | $0.015 / 次 | `GET /v1/wechat_channels/comments/replies/list` |
| [视频号直播回放](https://okdata.online/zh/apis/wechat_channels/users/live_replays/list/) | 账号的直播回放，从新到旧，每页最多约 50 条：标题、时间、点赞、评论和转发。url 是视频文件地址（已加密，用同一次返回的 ext.decode_key 解密）。 | $0.02 / 次 | `GET /v1/wechat_channels/users/live_replays/list` |
| [视频号作品分享链接](https://okdata.online/zh/apis/wechat_channels/videos/share_link/get/) | 按作品 ID 生成一条能在微信里打开的分享链接（weixin.qq.com/sph/ 开头）。每次生成的链接都不同，旧链接仍然有效；链接无法用 ID 自己拼出来。 | $0.02 / 次 | `GET /v1/wechat_channels/videos/share_link/get` |
| [视频号账号合集](https://okdata.online/zh/apis/wechat_channels/users/collections/list/) | 视频号账号公开的全部合集，一次返回：名称、简介、封面、视频数和最近更新时间。合集的 id 传给 wechat_channels.collections.videos.list 取里面的视频。 | $0.02 / 次 | `GET /v1/wechat_channels/users/collections/list` |
| [视频号合集视频](https://okdata.online/zh/apis/wechat_channels/collections/videos/list/) | 视频号合集里的视频，按合集自己的顺序（从最早的开始），每页 20 条：描述、账号、发布时间、点赞、评论、转发和收藏、时长。url 是视频文件地址（已加密，用同一次返回的 ext.decode_key 解密）。 | $0.02 / 次 | `GET /v1/wechat_channels/collections/videos/list` |
| [视频号作品互动数据](https://okdata.online/zh/apis/wechat_channels/videos/metrics/) | 按作品 ID 取视频号作品最近的数字：点赞、评论、转发和收藏，带作品描述和发布账号。数字可能是几小时前的，ext.counted_at 写明取数时间。比取整个作品（wechat_channels.videos.get）便宜。 | $0.015 / 次 | `GET /v1/wechat_channels/videos/metrics` |
| [视频号账号信息（备用版）（备用版）](https://okdata.online/zh/apis/wechat_channels/backup/users/get/) | wechat_channels.users.get 的备用版，另一来源：参数和返回相同，不给作品数。 | $0.03 / 次 | `GET /v1/wechat_channels/backup/users/get` |
| [视频号账号作品（备用版）（备用版）](https://okdata.online/zh/apis/wechat_channels/backup/users/videos/list/) | wechat_channels.users.videos.list 的备用版，另一来源：参数和返回相同，每页 15 条（正在直播时第一条是直播）。 | $0.06 / 次 | `GET /v1/wechat_channels/backup/users/videos/list` |
| [视频号视频搜索（备用版）（备用版）](https://okdata.online/zh/apis/wechat_channels/backup/videos/search/) | wechat_channels.videos.search 的备用版，另一来源：参数和返回相同，另带评论数和转发数（没有收藏数）。 | $0.15 / 次 | `GET /v1/wechat_channels/backup/videos/search` |

## 快速开始

1. 在 [okdata 控制台](https://okdata.online/zh/signup/?src=gh-wechat-channels-api) 用邮箱注册，拿到 `okd_` 开头的 Key。
2. 调一次接口：

```bash
export OKDATA_API_KEY=okd_...
curl -G "https://api.okdata.online/v1/wechat_channels/videos/search" \
  -H "Authorization: Bearer $OKDATA_API_KEY" \
  --data-urlencode 'query=露营装备推荐'
```

Python 版在 [examples/quickstart.py](examples/quickstart.py)（只用标准库，会顺带演示翻页）：`python3 examples/quickstart.py`。

返回统一的结构：列表在 `data.items`，下一页用 `page.next_cursor` 传回 `cursor`，这次扣了多少钱在 `meta.billing.amount`，平台不提供的字段为 null 并在 `meta.unavailable` 里写明原因。

## 让 AI 直接用（MCP）

Claude Code：

```bash
claude mcp add --transport http --scope user okdata https://api.okdata.online/mcp --header "Authorization: Bearer $OKDATA_API_KEY"
```

Cursor、Cherry Studio、WorkBuddy 等支持远程 MCP 的客户端：

```json
{
  "mcpServers": {
    "okdata": {
      "url": "https://api.okdata.online/mcp",
      "headers": {
        "Authorization": "Bearer okd_..."
      }
    }
  }
}
```

接好以后直接用中文说需求，比如「视频号视频搜索：露营装备推荐」。AI 会先用免费的 `find`、`describe` 找接口和看价格，再用 `call` 取数据。

## 常见问题

**要登录平台账号吗？** 不用。数据是公开内容，okdata 在服务端获取，你的账号完全不参与。

**怎么收费？** 每个接口单独定价，表里写的就是一次调用的价格；按条计费的接口按实际返回条数算。调用失败（包括超时）不扣费。新账号送 $0.1 试用额度，之后按需充值，没有订阅。价格页：https://okdata.online/zh/pricing/

**和官方开放平台有什么区别？** 官方开放平台只能读授权给你的账号自己的数据，而且要企业资质和审核；这里是平台上任何人都能看到的公开数据，比如搜索结果、别人的笔记或视频、评论、热榜。

**能翻页吗？** 列表接口每页一次调用，把 `page.next_cursor` 原样传回 `cursor` 就是下一页，24 小时内有效。

**出错了怎么办？** 每个错误都有固定的 `code`、中文说明 `message_zh`，以及会不会扣费（`charged`）和要不要重试（`retry`）。全部错误码：https://okdata.online/zh/docs/errors/

## English

Examples for the okdata WeChat Channels API: 15 live endpoints behind one API key, pay per call from $0.015, failed calls free, no platform login or cookies. Sign up at https://okdata.online/signup/?src=gh-wechat-channels-api, docs at https://okdata.online/apis/, MCP at https://okdata.online/mcp/.

## License

MIT. The data comes from the okdata API; its terms apply to API use.
