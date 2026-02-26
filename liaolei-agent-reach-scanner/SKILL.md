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
| 研究这个页面/读这个链接 | `agent-reach read <URL>` |
| 搜一下/全网搜索 | `agent-reach search` |
| 订阅 RSS | `agent-reach read <RSS_URL>` |

---

## 故障排除

```bash
# 检查所有渠道状态
agent-reach doctor

# 更新到最新版本
agent-reach check-update
```

---

## 相关链接

- Agent-Reach GitHub: https://github.com/Panniantong/Agent-Reach
- 官网: https://agent-reach.ai-coding.wiselychen.com
- 安装文档: https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/install.md

---

## License

MIT
