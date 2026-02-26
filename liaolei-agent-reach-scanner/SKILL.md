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

| 类别 | 平台 | 说明 |
|------|------|------|
| 🌐 网页 | 任意网页 | 阅读任意网页内容，无需配置 |
| 📺 视频 | YouTube、B站 | 字幕提取、视频搜索，无需配置 |
| 📡 RSS | RSS/Atom | 阅读 RSS 源，无需配置 |
| 🔍 搜索 | 全网搜索 | AI 语义搜索（免费，需配置 MCP） |
| 🐦 社交 | Twitter/X | 搜索推文、浏览时间线（需配置 Cookie） |
| 📦 代码 | GitHub | 搜索仓库、查看 Issue |
| 📖 社区 | Reddit | 搜索帖子 |
| 🔗 代理 | 代理配置 | 全局代理支持 |
| 📕 小红书 | 小红书 | 阅读、搜索（需配置 Docker） |
| 🎵 抖音 | 抖音 | 视频解析、无水印下载（需配置 MCP） |
| 💼 招聘 | LinkedIn、Boss直聘 | 职位搜索（需配置 MCP） |

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
| 看看GitHub/trending | `agent-reach search-github` |
| 看视频/YouTube/B站 | `agent-reach search-youtube` / `agent-reach search-bilibili` |
| Reddit 搜索 | `agent-reach search-reddit` |
| 研究这个页面/读这个链接 | `agent-reach read <URL>` |
| 搜一下/全网搜索 | `agent-reach search` |
| 订阅 RSS | `agent-reach read <RSS_URL>` |

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
