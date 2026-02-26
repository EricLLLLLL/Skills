# Liaolei Agent Reach Scanner

> Claude Code / OpenClaw / Cursor 热点扫描工具

让 AI Agent 支持多平台热点发现：Twitter、X、GitHub、YouTube、B站、Reddit、全网搜索。

## 功能

| 平台 | 命令 | 状态 |
|------|------|------|
| GitHub | `agent-reach search-github` | ✅ |
| YouTube | `agent-reach search-youtube` | ✅ |
| Reddit | `agent-reach read URL` | ✅ |
| B站 | `agent-reach search-bilibili` | ✅ |
| Twitter/X | `agent-reach search-twitter` | ✅ |
| 全网搜索 | `agent-reach search` | ✅ |
| 网页读取 | `agent-reach read URL` | ✅ |

## 安装

```bash
# 1. 安装 Agent-Reach
pip install https://github.com/Panniantong/agent-reach/archive/main.zip

# 2. 初始化
agent-reach install --env=auto

# 3. 配置 Twitter Cookie（可选但推荐）
# 从浏览器导出 X 的 Cookie，运行：
agent-reach configure twitter-cookies "auth_token=xxx;ct0=xxx"

# 4. 配置 Exa 全网搜索（可选，免费）
npm install -g mcporter
mcporter config add exa https://mcp.exa.ai/mcp

# 5. 检查状态
agent-reach doctor
```

## 使用

### 热点扫描

```bash
# GitHub 热点
agent-reach search-github "AI agent" -n 5

# YouTube 热点
agent-reach search-youtube "AI 编程 2026" -n 5

# B站 热点
agent-reach search-bilibili "AI 教程" -n 5

# Twitter 热点
agent-reach search-twitter "Kimi K2.5" -n 5

# 全网搜索
agent-reach search "AI 热点 2026" -n 5
```

### 读取内容

```bash
# 读取 Reddit 热门
agent-reach read "https://www.reddit.com/r/LocalLLaMA/"

# 读取 Hacker News
agent-reach read "https://news.ycombinator.com/"

# 读取任意网页
agent-reach read "https://www.jiqizhixin.com"
```

## 快速扫描命令

### X/Twitter 大V（最全）

```bash
# 国外 AI 公司
agent-reach search-twitter "from:AnthropicAI OR from:OpenAI OR from:GoogleAI OR from:MetaAI OR from:xai OR from:NVIDIA" -n 20

# 国内AI
agent-reach search-twitter "from:deepseek_ai OR from:Minimax_AI OR from:MoonshotAI OR from:zhipuai" -n 15

# 马斯克（最有流量）
agent-reach search-twitter "from:elonmusk" -n 20
```

### 开发者工具

```bash
agent-reach search-twitter "from:github" -n 10
agent-reach search-twitter "from:anysphere" -n 10  # Cursor
agent-reach search-twitter "from:vercel" -n 10
```

## Twitter Cookie 配置

1. 登录 x.com
2. F12 打开开发者工具
3. Application → Cookies → x.com
4. 复制 `auth_token` 和 `ct0` 的 value
5. 拼接：`auth_token=xxx;ct0=xxx`
6. 运行：`agent-reach configure twitter-cookies "拼接的字符串"`

## 故障排除

```bash
# 检查状态
agent-reach doctor

# 更新
agent-reach check-update
```

## 路由规则

- 用户说"看看热点/选题/今天有什么热点" → 用 Agent Reach 扫描 X/Twitter + GitHub
- 用户说"看看马斯克" → `agent-reach search-twitter "from:elonmusk"`
- 用户说"搜一下X/推特" → `agent-reach search-twitter`
- 用户说"看看GitHub" → `agent-reach search-github`
- 用户说"研究这个页面" → `agent-reach read <URL>`

## 相关链接

- Agent-Reach GitHub: https://github.com/Panniantong/Agent-Reach
- 官网: https://agent-reach.ai-coding.wiselychen.com

## License

MIT
