# DSH 插件工坊（dsh-atelier）

用户给 desktop profile 装了 [@zfdx123/dsh-atelier](https://github.com/zfdx123/dsh-atelier)（第三方 DSH 插件工坊），一条包带 7 个插件：

| 插件 | 干什么 |
|---|---|
| dsh-mcp-manager | 设置页配置 MCP 服务器，宿主侧热挂载/卸载 |
| dsh-skills-manager | 技能（SKILL.md）诊断、新建、编辑、开关 |
| dsh-memery | 跨会话记忆：工作区 sqlite + 首轮注入 + 关键词命中 + `memory_*` 工具 |
| dsh-codegraph | 代码知识图谱，包成 `codegraph_*` 工具 |
| dsh-hooks-ordering | Cordis waterfall / serial 钩子的确定性排序 |
| dsh-session-cleaner | 彻底删除会话（store / 工作区 / 磁盘产物） |
| dsh-superpowers | 软件开发方法论技能（brainstorming / TDD / debugging…） |

## 记录

- 装进 `desktop` profile：`@zfdx123/dsh-atelier ^1.0.14`
- **desktop profile 由 Electron 应用独占管理**，CLI `dsh plugin --profile desktop add` 会报错，只能走 app 的插件市场 / 设置页。
- 生效后新增工具：`memory_*`、`skill_manager`、`codegraph_*`，以及 Superpowers 方法论技能。
