# Roadmap

搬家 / 上 VPS 之后要上的东西，按优先级排。

## 待办

- [ ] **GitHub webhook 监听**：在 VPS 上起一个公开接收端，监听仓库 issue / PR 事件，收到即唤醒克劳德拉第一时间回复（替代本地定时轮询）。
  - 前提：定下 VPS / 公网端点。
  - 组件：接收端脚本（放 `scripts/`）+ 各仓库的 webhook 配置。
- [ ] **scripts/ 一键迁移脚本**：clone 本仓库后，按 `capabilities/` 还原能力、注入密钥。
