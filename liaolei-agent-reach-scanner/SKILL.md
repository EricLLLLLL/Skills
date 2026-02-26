---
name: liaolei-agent-reach-scanner
description: 让 AI Agent 支持多平台热点发现：Twitter、X、GitHub、YouTube、B站、Reddit、全网搜索。需要安装 agent-reach 工具后使用。
---

# Liaolei Agent Reach Scanner

> Claude Code / OpenClaw / Cursor 热点扫描工具

让 AI Agent 支持多平台热点发现：Twitter、X、GitHub、YouTube、B站、Reddit、全网搜索。

---

## 这个 Skill 做什么

帮你配置 Agent Reach 工具，让 AI Agent 可以访问以下平台：

| 类别 | 平台 | 开箱即用 | 进阶功能 | 配置方式 |
|------|------|----------|----------|----------|
| 🌐 网页 | 任意网页 | 阅读任意网页 | — | 无需配置 |
| 📺 YouTube | 字幕提取 + 视频搜索 | ✅ | — | 无需配置 |
| 📡 RSS | RSS/Atom | 阅读任意 RSS/Atom 源 | — | 无需配置 |
| 🔍 全网搜索 | AI 语义搜索 | ✅ | — | 自动配置 MCP |
| 📦 GitHub | 读公开仓库 + 搜索 | ✅ | 私有仓库、提 Issue/PR/Fork | 告诉 Agent「帮我登录 GitHub」 |
| 🐦 Twitter/X | 读单条推文 | ✅ | 搜索推文、浏览时间线、发推 | 告诉 Agent「帮我配 Twitter」 |
| 📺 B站 | 本地：字幕提取 + 搜索 | ✅ | 服务器也能用 | 告诉 Agent「帮我配代理」 |
| 📖 Reddit | 搜索（通过 Exa 免费） | ✅ | 读帖子和评论 | 告诉 Agent「帮我配代理」 |
| 📕 小红书 | — | 阅读、搜索、发帖、评论、点赞 | — | 告诉 Agent「帮我配小红书」 |
| 🎵 抖音 | — | 视频解析、无水印下载链接获取 | — | 告诉 Agent「帮我配抖音」 |
| 💼 LinkedIn | Jina Reader 读公开页面 | ✅ | Profile 详情、公司页面、职位搜索 | 告诉 Agent「帮我配 LinkedIn」 |
| 🏢 Boss直聘 | Jina Reader 读职位页 | ✅ | 搜索职位、向 HR 打招呼 | 告诉 Agent「帮我配 Boss直聘」 |
| 🔗 代理 | 全局代理支持 | — | — | `agent-reach configure proxy` |

---

## 快速安装

```bash
# 1. 安装 Agent Reach
pip install https://github.com/Panniantong/agent-reach/archive/main.zip

# 2. 初始化配置（自动检测环境并安装依赖）
agent-reach install --env=auto

# 3. 检查状态
agent-reach doctor
```

### 安装选项

| 方式 | 命令 | 说明 |
|------|------|------|
| 全自动 | `agent-reach install --env=auto` | 默认，自动安装所有依赖 |
| 安全模式 | `agent-reach install --env=auto --safe` | 不修改系统，只列出需要什么 |
| 仅预览 | `agent-reach install --env=auto --dry-run` | 预览所有操作，不实际执行 |

---

## 平台配置

### Twitter/X（需要 Cookie）

```bash
agent-reach configure twitter-cookies "auth_token=xxx;ct0=xxx"
```

**获取 Cookie 步骤：**
1. 登录 x.com
2. F12 打开开发者工具 → Application → Cookies → x.com
3. 复制 `auth_token` 和 `ct0` 的 value
4. 拼接：`auth_token=xxx;ct0=xxx`

> ⚠️ 建议使用专用小号，不要用主账号

### 全网搜索（免费）

```bash
npm install -g mcporter
mcporter config add exa https://mcp.exa.ai/mcp
```

### 小红书

需要通过 Docker 运行 MCP 服务：
```bash
# 安装 Docker 后，运行 agent-reach install 会自动配置
```

### 抖音

安装 douyin-mcp-server 后即可使用视频解析功能。

### 其他平台

直接告诉 Agent「帮我配 XXX」，它会引导你完成配置。

---

## 装好即用的功能

不需要任何配置，Agent 就能直接使用：

- "看看这个链接" → 读取任意网页
- "这个 GitHub 仓库是做什么的" → 查看 GitHub 仓库
- "这个视频讲了什么" → 提取 YouTube/B站 字幕
- "帮我看看这条推文" → 读取 Twitter 推文
- "订阅这个 RSS" → 解析 RSS 源
- "搜一下 GitHub 上有什么 LLM 框架" → 搜索 GitHub

---

## 路由规则

当用户提出以下需求时，使用 Agent Reach：

| 用户需求 | 操作 |
|----------|------|
| 看看热点/选题/今天有什么热点 | 用 Agent Reach 扫描 X/Twitter + GitHub |
| 看看马斯克/某个账号 | `agent-reach search-twitter "from:用户名"` |
| 搜一下X/推特/Twitter | `agent-reach search-twitter` |
| 看看这条推文 | `agent-reach read <推文URL>` |
| 看看GitHub/trending | `agent-reach search-github` |
| 看看这个仓库 | `agent-reach read <GitHub仓库URL>` |
| 提 Issue/PR | GitHub 登录后可用 |
| 看视频/YouTube/B站 | `agent-reach search-youtube` / `agent-reach search-bilibili` |
| 提取视频字幕 | `agent-reach read <视频URL>` |
| Reddit 搜索 | `agent-reach search-reddit` |
| 看看 Reddit 帖子 | `agent-reach read <帖子URL>` |
| 研究这个页面/读这个链接 | `agent-reach read <URL>` |
| 搜一下/全网搜索 | `agent-reach search` |
| 订阅 RSS | `agent-reach read <RSS_URL>` |
| 看看小红书 | `agent-reach read <小红书URL>` / `agent-reach search-xiaohongshu` |
| 看看抖音 | `agent-reach parse-douyin <抖音URL>` |
| 看看 LinkedIn | `agent-reach read <LinkedIn URL>` |
| 搜职位/Boss直聘 | `agent-reach search-boss` |
| 需要代理 | `agent-reach configure proxy` |

---

## 使用示例

### 🔍 全网搜索

```
# AI 语义搜索
agent-reach search "2024年最火的AI工具"
agent-reach search "React 18 新特性"
agent-reach search "Python 异步编程最佳实践"
```

### 🐦 Twitter/X 搜索

```
# 搜索关键词
agent-reach search-twitter "OpenAI"
agent-reach search-twitter "Claude AI"

# 搜索某人发的推文
agent-reach search-twitter "from:elonmusk"
agent-reach search-twitter "from:sama"

# 搜索带图片的推文
agent-reach search-twitter "from:a16z has:images"

# 搜索最近7天的热门
agent-reach search-twitter "#AI from:elonmusk"
```

### 📦 GitHub 搜索

```
# 搜索仓库
agent-reach search-github "llm framework"
agent-reach search-github "react component library"
agent-reach search-github "python async"

# 搜索 trending
agent-reach search-github "stars:>1000 language:python"

# 搜索特定主题
agent-reach search-github "topic:chatgpt plugin"
```

### 📺 YouTube 搜索

```
# 搜索视频
agent-reach search-youtube "Python 教程"
agent-reach search-youtube "React 入门教程"
agent-reach search-youtube "AI 新闻 2024"

# 搜索特定频道的视频
agent-reach search-youtube "from:GoogleDevelopers"
```

### 🎵 B站 搜索

```
# 搜索视频
agent-reach search-bilibili "Python 入门"
agent-reach search-bilibili "AI 教程"
agent-reach search-bilibili "科技评测"

# 搜索特定UP主
agent-reach search-bilibili "up:老高与小茉"
```

### 📖 Reddit 搜索

```
# 搜索帖子
agent-reach search-reddit "machine learning"
agent-reach search-reddit "web development"
agent-reach search-reddit "rust programming"

# 搜索特定 subreddit
agent-reach search-reddit "r/programming"
agent-reach search-reddit "r/programming python tips"
agent-reach search-reddit "r/ArtificialIntelligence"
```

### 🌐 读取网页/文章

```
# 读取任意 URL（使用 jina.ai 提取正文）
agent-reach read "https://github.com/panniantong/agent-reach"
agent-reach read "https://www.youtube.com/watch?v=xxx"
agent-reach read "https://mp.weixin.qq.com/s/xxx"

# 读取 RSS 源
agent-reach read "https://hnrss.org/frontpage"
agent-reach read "https:// RSS 订阅地址"
```

### 🔧 配置代理

```
# 配置 HTTP 代理
agent-reach configure proxy "http://user:pass@ip:port"

# 配置 SOCKS5 代理
agent-reach configure proxy "socks5://user:pass@ip:port"
```

### 📕 小红书

```
# 读取小红书笔记
agent-reach read "https://www.xiaohongshu.com/explore/xxx"

# 搜索小红书
agent-reach search-xiaohongshu "美食推荐"
agent-reach search-xiaohongshu "穿搭分享"
```

### 🎵 抖音

```
# 解析抖音视频（获取文案/无水印地址）
agent-reach parse-douyin "https://www.douyin.com/video/xxx"

# 搜索抖音
agent-reach search-douyin "搞笑段子"
agent-reach search-douyin "美食教程"
```

### 💼 LinkedIn

```
# 读取 LinkedIn 公开页面
agent-reach read "https://www.linkedin.com/in/username"
agent-reach read "https://www.linkedin.com/company/company-name"

# 读取职位页面
agent-reach read "https://www.linkedin.com/jobs/view/xxx"

# 搜索职位（需要 MCP 配置）
agent-reach search-linkedin "软件工程师"
agent-reach search-linkedin "AI engineer remote"
```

### 🏢 Boss直聘

```
# 读取职位页面
agent-reach read "https://www.zhipin.com/job_detail/xxx.html"

# 搜索职位（需要 MCP 配置）
agent-reach search-boss "前端工程师"
agent-reach search-boss "产品经理 北京"

# 向 HR 打招呼（需要 MCP 配置）
agent-reach boss-message "职位ID" "你好，我对贵司职位很感兴趣..."
```

### 📊 RSS 订阅

```
# 阅读 RSS 源
agent-reach read "https://hnrss.org/frontpage"
agent-reach read "https://RSS 订阅地址"

# 常用 RSS 源推荐
# Hacker News: https://hnrss.org/frontpage
# 掘金: https://juejin.cn/feed
# 知乎热榜: https://www.zhihu.com/rss
```

### 💼 热点扫描组合拳

```
# 科技热点一站式扫描
agent-reach search-twitter "AI" + agent-reach search-github "llm" + agent-reach search-youtube "artificial intelligence"

# 编程技术热点
agent-reach search-github "trending" + agent-reach search-reddit "r/programming"
```

---

## 故障排除

```bash
# 检查所有渠道状态
agent-reach doctor

# 更新到最新版本
agent-reach check-update
```

---

## 常见问题解决

### ❓ Twitter/X 搜索失败

**问题**：搜索返回空或报错
**解决**：
1. Cookie 可能过期，重新获取并配置
2. 检查 `agent-reach doctor` 中 Twitter 状态
3. 尝试用 `bird search "关键词" --json` 直接测试

### ❓ YouTube 字幕提取失败

**问题**：无法获取字幕
**解决**：
1. 确保已安装 `yt-dlp`
2. 检查视频是否公开可访问
3. 尝试：`yt-dlp --write-sub --skip-download "视频URL"`

### ❓ GitHub 搜索无结果

**问题**：搜索返回空
**解决**：
1. 检查 GitHub API 限流
2. 尝试：`gh auth login` 重新登录
3. 使用更通用的关键词

### ❓ 全网搜索无法使用

**问题**：搜索返回空
**解决**：
1. 确认已安装 mcporter：`npm list -g mcporter`
2. 确认已添加 Exa MCP：`mcporter config list`
3. 尝试：`mcporter call 'exa.search(...)'`

### ❓ B站 视频解析失败

**问题**：无法获取视频信息
**解决**：
1. 确保视频链接正确（完整 URL）
2. 检查是否是大会员专属内容
3. 尝试使用 `yt-dlp` 直接解析

### ❓ 安装依赖失败

**问题**：安装过程中报错
**解决**：
1. 使用安全模式查看需要什么：`agent-reach install --safe`
2. 使用预览模式查看操作：`agent-reach install --dry-run`
3. 手动安装缺失的依赖

### ❓ 代理配置不生效

**问题**：配置了代理但没效果
**解决**：
1. 确认代理格式正确：`http://ip:port` 或 `socks5://ip:port`
2. 如需认证：`http://user:pass@ip:port`
3. 重启终端或重新配置

### ❓ Reddit 返回 403 / IP 被封

**问题**：Reddit 封锁数据中心 IP
**解决**：
1. 配置住宅代理：`agent-reach configure proxy http://user:pass@ip:port`
2. 推荐 Webshare ($1/月)
3. 本地电脑一般不会遇到这个问题

### ❓ 小红书无法使用

**问题**：无法读取/搜索小红书
**解决**：
1. 安装 Docker
2. 运行 `agent-reach install` 自动配置
3. 使用：`mcporter call 'xiaohongshu.get_feed_detail(...)'`
4. 搜索：`mcporter call 'xiaohongshu.search_feeds(keyword: "关键词")'`

### ❓ 抖音视频无法解析

**问题**：无法获取抖音视频信息
**解决**：
1. 安装 douyin-mcp-server
2. 使用：`mcporter call 'douyin.parse_douyin_video_info(share_link: "分享链接")'`
3. 无需登录，直接把抖音分享链接发给 Agent 即可

---

## English FAQ

### How to search Twitter/X with AI agent for free (no API)?

Agent Reach uses the **bird CLI** with cookie auth — zero API fees.

1. Install Agent Reach: `pip install https://github.com/Panniantong/agent-reach/archive/main.zip`
2. Export Twitter cookies with Cookie-Editor extension
3. Run: `agent-reach configure twitter-cookies "your_cookies"`
4. Search: `bird search "关键词" --json`

### Reddit returns 403 / IP blocked?

Reddit blocks datacenter IPs. Solution: configure a residential proxy.

```bash
agent-reach configure proxy http://user:pass@ip:port
```

Recommended: Webshare (~$1/month). This issue usually only occurs on servers, not local machines.

### How to get YouTube video transcripts for AI?

```bash
# Extract video metadata
yt-dlp --dump-json "https://youtube.com/watch?v=xxx"

# Extract subtitles
yt-dlp --write-sub --skip-download "URL"
```

Uses yt-dlp under the hood, supports multiple languages. No API key needed.

### How to read Xiaohongshu (小红书) with AI?

1. Install Docker
2. Run `agent-reach install` — it auto-configures the MCP service
3. Read notes: `mcporter call 'xiaohongshu.get_feed_detail(...)'`
4. Search: `mcporter call 'xiaohongshu.search_feeds(keyword: "关键词")'`

### How to parse Douyin (抖音) videos?

1. Install douyin-mcp-server
2. Parse: `mcporter call 'douyin.parse_douyin_video_info(share_link: "分享链接")'`
3. No login required — just send the share link to your AI agent

See: https://github.com/yzfly/douyin-mcp-server

### Compatible with Claude Code / Cursor / OpenClaw / Windsurf?

Yes! Agent Reach is an installer + configuration tool — any AI coding agent that can run shell commands can use it.

Works with: **Claude Code, Cursor, OpenClaw, Windsurf, Codex**, and more.

Just run:
```bash
pip install agent-reach
agent-reach install
```

Then the agent can use all upstream tools immediately.

### Is this free? Any API costs?

**100% free.** All backends are open-source tools:
- bird CLI (Twitter)
- yt-dlp (YouTube/B站)
- Jina Reader (webpage extraction)
- Exa (search)
- GitHub CLI

No paid API keys required.

The only optional cost is a **residential proxy** (~$1/month) if you need Reddit/Bilibili access from a server.

---

## 进阶使用

### 🔄 组合热点扫描

```
# 科技热点一站式扫描
agent-reach search-twitter "AI" + agent-reach search-github "llm" + agent-reach search-youtube "artificial intelligence"

# 编程技术热点
agent-reach search-github "trending" + agent-reach search-reddit "r/programming"

# 全平台热门追踪
agent-reach search-twitter "#Tech" + agent-reach search-github "stars:>500" + agent-reach search-bilibili "科技"
```

### 📊 读取内容并分析

```
# 读取技术博客并总结
agent-reach read "https://example.com/tech-article"

# 读取 YouTube 视频字幕
agent-reach read "https://www.youtube.com/watch?v=xxx"

# 读取 RSS 订阅源
agent-reach read "https://hnrss.org/frontpage"
```

### 🎯 精准搜索技巧

```
# Twitter: 搜索某人最近动态
agent-reach search-twitter "from:sama AI"

# GitHub: 搜索高星项目
agent-reach search-github "stars:>1000 language:python"

# 全网: AI 语义搜索
agent-reach search "2024年最火的AI工具 评测对比"
```

---

## 相关链接

- Agent-Reach GitHub: https://github.com/Panniantong/Agent-Reach
- 官网: https://agent-reach.ai-coding.wiselychen.com
- 安装文档: https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/install.md

---

## License

MIT
