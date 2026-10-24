# 夏羽 / xixi

**独立 AI builder（2026 届本科）｜以「人做架构与评测 + AI 协作实现」的方式，持续交付可运行的 AI 系统**

正在寻找：**深圳 / 远程 · AI 应用方向（RAG / Agent / 评测）** ｜ learninginloops@outlook.com

---

## 🔧 产品侧（已上线 / 运行中）

| 项目 | 是什么 | 关键数字 |
|---|---|---|
| **岐黄典籍 · 测算师**（小程序，已上线运营） | 术数/中医典籍 RAG 问答产品：「程序管事实、模型管语言」闸门架构，每句结论强制带出典籍出处 | 36 万段语料 · 1,800+ 项测试 · 14 次上线零回滚 · Web/Windows/Android/小程序多端 |
| **体质调理**（商业化推进中） | 基于 GB/T 46939—2025 九体质分类的自测与调理内容服务，执业中医师审定内容后发布 | 小程序功能已上线 · 会员制付费链路设计中 |
| **Agent 劳务市场**（MVP） | 多模型任务执行平台：委托撮合、双模型并行执行、人工放行、熔断与积分结算 | 224 项数据库测试 · Vercel/Railway/Supabase 全栈部署 |
| **小说数据底座** | 三平台小说采集→去重→结构原子化流水线，支撑内容生成实验 | 75,358 书库候选 · 4,550 章节快照 · 10,149 结构原子 |
| **脑启发 Agent**（实验） | 8 脑区命名架构在 8GB 显存笔记本上的分级落地（L0 规则/L1 代码/L2 LLM 的 3 调用回环） | 本地 Qwen9B/MiMo7B · GBNF 约束输出 |

> 工作方式：所有系统以「评测先行」构建——封存测试集、基线对照、上线前全量预检、可回滚。敢报负结果（纳甲断卦书例评测 18.5%，如实记录并指导了下一步路线）。

## 🔬 研究侧（开源，下方英文为原始记录）

- [lorenz-world-model](https://github.com/xiayu23123/lorenz-world-model) — learned latent transition 到底有没有用？六组对照实验，答案是诚实的负结果
- [yi-world-model](https://github.com/xiayu23123/yi-world-model) — 易经结构拓扑上的可微世界模型，含全部失败记录
- [learning-in-loops](https://github.com/xiayu23123/learning-in-loops) — 博客与写作：[learning-in-loops.pages.dev](https://learning-in-loops.pages.dev)

---

### xixi

I build small world models and write down the parts that fail.

**The arc so far.** I started by encoding the I Ching as a differentiable
state-space model — 64 hexagrams as vertices of a signed 6-cube, the King Wen
permutation and 错/综/互 relations hard-coded, only the continuous parts
learning. It solved no real problem. On the one test designed to be
falsifiable — change-point detection against a tuned PELT baseline — it lost by
2×.

One methodological result survived: a representation trained to serve a
*controller* is not good enough to *plan* with. Learn it from the dynamics
directly, with an anti-collapse regulariser, and action-sensitivity goes up
~16×. Reproduced across 5 seeds with an ablation.

But every environment there was one I had written myself — a tautology engine,
where the model learns to invert a generator I control. So I pointed the same
pipeline at dynamics nobody designed and asked whether the latent transition
earns its place at all. Six regimes later:

| regime | what actually carries the load |
|---|---|
| observation = state | plain MLP in observation space |
| observation < state | delay embedding (Takens), not a learned latent |
| high-D pixels | reconstruction-trained encoder — for rollout *stability* only |
| stochastic dynamics | heteroscedastic output head (not a latent, not an ensemble) |
| planning | dynamics that transfer across task instances |
| long-term memory | recurrence **+ a dense predictive objective** |

The learned latent transition is the active ingredient in zero of the six.

**Writing**

- [When Does a Latent World Model Actually Help? Six Regimes](https://learning-in-loops.pages.dev/posts/when-does-a-latent-world-model-help/)
- [Every Dead End Named the Next Step: An I Ching World Model](https://learning-in-loops.pages.dev/posts/i-ching-world-model/)

Negative results, reproduced and ablated. They are the part that saves the next
person the weeks.
