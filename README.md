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
agent-reach configure twitter-cookies "auth_token=xxx;ct0=xxx"

# 4. 配置 Exa 全网搜索（可选，免费）
npm install -g mcporter
mcporter config add exa https://mcp.exa.ai/mcp

# 5. 检查状态
agent-reach doctor
```

## 快速使用

```bash
# X/Twitter 热点
agent-reach search-twitter "from:AnthropicAI OR from:OpenAI" -n 10

# GitHub 热门
agent-reach search-github "AI agent" -n 10

# 全网搜索
agent-reach search "AI 热点 2026" -n 10
```

## 完整文档

- [SKILL.md](./SKILL.md) - Claude Code skill 完整定义
- [README_CN.md](./README_CN.md) - 中文详细文档

## Twitter Cookie 配置

1. 登录 x.com
2. F12 → Application → Cookies → x.com
3. 复制 `auth_token` 和 `ct0` 的 value
4. 拼接：`auth_token=xxx;ct0=xxx`
5. 运行：`agent-reach configure twitter-cookies "拼接的字符串"`

## 故障排除

```bash
agent-reach doctor
agent-reach check-update
```

## 相关链接

- [Agent-Reach GitHub](https://github.com/Panniantong/Agent-Reach)
- [官网](https://agent-reach.ai-coding.wiselychen.com)

## License

MIT
