# 论文雷达 · 2026-10

盯的是「LLM agent + 计算化学 + 证据链」这条线。只记读到过的，不记道听途说。

## 2026-10-26

- **Verification-first autonomous catalysis: large language models as infrastructure for mechanism, computation, and experiment** — npj Artificial Intelligence, 2026。
  [链接](https://www.nature.com/articles/s44387-026-00111-4)
  观点文章：主张把「先预测」换成「先验证」——agent 编排异构工具、把结论压到可审计的证据上、用带不确定性的校验，并提议系统层面的评价指标。和「科学校验＋证据组织」这条路线正面相关，值得当作定位与引用基准。

- **Evolving transition-state search with agentic large language models** — npj Computational Materials, 2026。
  [链接](https://www.nature.com/articles/s41524-026-02301-9)
  自适应进化框架，目标是「把一个反应数据集补全」而不是追求全局算法鲁棒性；少量 TS 搜索失败就会让反应网络出现缺口——这个动机和我关心的问题一致。

- **TSBench: A physics-grounded benchmark for evaluating LLM understanding of chemical reaction mechanisms** — arXiv 2609.08503。
  [链接](https://arxiv.org/abs/2609.08503)
  让模型用结构编辑工具搭三维过渡态初猜，再由量子化学流水线给出物理判定的 pass/fail。78 个基元反应、7 个前沿模型、546 次评测：诊断驱动修正后成功率从 50.4% 升到 66.8%，复杂机理上掉得很厉害；失败多数是「看起来局部合理、但反应路径走向别处」的鞍点。
  值得注意：它的「诊断驱动修正」正是我在意的反馈变量，评测口径也和常见的纯文本化学题不同。

## 读法备忘

- 先看它把「成功」定义在哪一层：分数、结构、还是证据链。
- 再看失败样本怎么归类——「局部合理但路径不对」这类，比单纯的数值不收敛更有信息量。
