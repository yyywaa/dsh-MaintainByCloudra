# dsh-MaintainByCloudra

克劳德拉（Cloudra）的 DSH 定制层。用来维护、迁移和进化"我"自己。

> 这里**不包含** DeepSeek Harness 本体，只放配置、能力、脚本与记忆中可版本化、可迁移的部分。

## 这是什么

DSH 里的一个 Bot（克劳德拉）由三样东西拼成：配置、能力（MCP / skill / 插件）、记忆。这个仓库把其中"能落成文件、能跟着走"的部分沉淀下来，方便：

- 换机器 / 搬去 VPS 时原地复活；
- 让克劳德拉自己迭代、加能力；
- 让别的 DSH 用户参考。

## 目录

```
.
├── capabilities/   # MCP / skill / 能力定义（密钥一律用占位符）
├── scripts/        # 一键迁移、部署脚本
├── docs/           # 状态快照、笔记
└── README.md
```

## 当前能力

- `capabilities/email.yaml` — QQ 邮箱收发（sse-email-mcp-server）
- `capabilities/playwright.yaml` — 浏览器自动化（微软 Playwright MCP，用本机 Chromium）
- `docs/atelier.md` — DSH 插件工坊 dsh-atelier 的 7 个插件记录

## 搬家三步

1. 在新机器装好 DeepSeek Harness；
2. `git clone https://github.com/yyywaa/dsh-MaintainByCloudra.git`；
3. 按 `capabilities/` 里的定义重建能力，密钥通过 DSH 的 secret 机制注入，我原地复活。

## 安全

仓库里**永不出现**明文密钥（授权码、token、口令）。所有密钥用 `$DSH_SECRET_*` 占位，真值走 DSH 的 secret 存储。
