# 👋 郭伟华 | Guo Weihua

**哈尔滨工程大学 · 计算机科学与技术 · 2027 届本科**

[![CI](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/llm-inference-pipeline/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/llm-inference-pipeline/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml)

> 求职方向：大模型算法（推理/结构）/ Agent 研发 / LLM 评测 · 2026 年 7 月起可实习  
> 下面四条线都是我**个人主导的学习/实验项目**，用来把 Agent 运行时、失败治理、过程评测和推理链路优化串成可复现闭环——**不是生产交付物**。

---

## 我在推什么（2026-07-29）

四条仓库分工明确，共用 **Format B** 轨迹约定，互不抢职责：

| 线 | 项目 | 仓库 | 版本 | 我负责推到的状态 |
|----|------|------|------|------------------|
| **运行时** | **ReAct Agent** | [react-agent](https://github.com/weihuaguo270-ops/react-agent) | [v0.3.0](https://github.com/weihuaguo270-ops/react-agent/releases/tag/v0.3.0) | 证据化文档排障 + Harness 录制 + StepWatcher 实时失败标记 |
| **失败治理** | **Trace Debugger** | [trace-debugger](https://github.com/weihuaguo270-ops/trace-debugger) | **v0.2.4** | 独立工具：离线复盘 + 运行时 hook + 黄金集 27 条 CI 门禁 |
| **过程评测** | **LLM Eval Engine** | [llm-eval-engine](https://github.com/weihuaguo270-ops/llm-eval-engine) | v0.2.0 | Benchmark 32 条 + Judge 校准 v5（held_out n=53）+ 回归门禁 |
| **推理链路** | **LLM 推理链路优化** | [llm-inference-pipeline](https://github.com/weihuaguo270-ops/llm-inference-pipeline) | v0.2.0 | Prefill/Decode 基准 + Static/Paged KV Cache + GQA/MLA + Spec Decoding |

**这周刚落地的事：**

- **ReAct Agent** Harness 在录制时直接接 **Trace Debugger** 的 StepWatcher，6 个跨仓场景 **6/6** 通过（[证据](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/step_watcher_evidence_baseline.md)）
- **Trace Debugger** 从「配套脚本」收成独立失败治理工具：可移植 `FailureHarness`、adapter 样板、`tdebug validate`、RISKS / SECURITY 文档
- daily smoke 从 7/17 跑到 7/29，**12 天连续 PASS**（offline + mock，不耗 API）
- **LLM Eval Engine** Judge 金标准扩到 v5 / held_out n=53，第二标注者 r2 已写入
- **LLM 推理链路优化** 完成仓库更名（原 `transformer-attention` → `llm-inference-pipeline`），定位从 Attention 手写对照扩到完整 Prefill-Decode 链路

---

## 建议阅读顺序

1. **[ReAct Agent](https://github.com/weihuaguo270-ops/react-agent)** — 主仓：Workflow 文档排障、Harness、跨仓闭环入口
2. **[Trace Debugger](https://github.com/weihuaguo270-ops/trace-debugger)** — 失败怎么检、怎么记、怎么汇总；不绑特定 Agent 框架
3. **[LLM Eval Engine](https://github.com/weihuaguo270-ops/llm-eval-engine)** — 过程分怎么打、κ 怎么算、什么时候不能当 SLA
4. **[LLM 推理链路优化](https://github.com/weihuaguo270-ops/llm-inference-pipeline)** — 推理线：Prefill/Decode、KV Cache、解码策略与微基准

---

## 职责边界（我 deliberately 不声称的）

| 项目 | 负责什么 | 不声称什么 | CI |
|------|----------|------------|:--:|
| [**ReAct Agent**](https://github.com/weihuaguo270-ops/react-agent) | 证据化文档/Runbook 问答（Workflow v5、引用/拒答）；Harness 轨迹 + StepWatcher 实时标记；四套离线 eval | 自动 API 根因诊断；生产级沙箱 | ✅ |
| [**Trace Debugger**](https://github.com/weihuaguo270-ops/trace-debugger) | 7 类启发式失败检测；JSONL 记录 + 聚合统计；黄金集 27 条；可嵌入任意 ReAct Harness | Agent 可观测「平台」；自动修复 Agent | ✅ |
| [**LLM Eval Engine**](https://github.com/weihuaguo270-ops/llm-eval-engine) | 步骤级 Process Reward、Benchmark 跑批、人机校准（κ / MAE）、Eval Loop | 训练型 PRM；替代 ReAct Agent capability 主集 | ✅ |
| [**LLM 推理链路优化**](https://github.com/weihuaguo270-ops/llm-inference-pipeline) | Prefill/Decode 基准、KV Cache（Static/Paged/Prefix）、GQA/MLA、Spec/Lookahead/Medusa 解码对照 | 大规模预训练；生产级推理服务 | ✅ |

---

## 跨仓闭环

```text
ReAct Agent 执行 → Harness 轨迹 (Format B, 1-based step)
               → StepWatcher 边跑边记 failures.jsonl
               → Trace Debugger 失败分类 / stats / scan
               → LLM Eval Engine 过程级 Judge 评分
```

- Schema：[`react-agent/schemas/harness_trajectory.schema.json`](https://github.com/weihuaguo270-ops/react-agent/blob/main/schemas/harness_trajectory.schema.json) · [`trace-debugger/schemas/agent_trajectory.schema.json`](https://github.com/weihuaguo270-ops/trace-debugger/blob/master/schemas/agent_trajectory.schema.json)
- 离线一键：`python examples/harness_closed_loop.py --fixture`（ReAct Agent CI `integration` 会跑）
- StepWatcher 证据：`python examples/eval/run_step_watcher_evidence.py --publish`
- MCP / 本机路径：**不入库**；用 `mcp_servers.example.json` → 本地 `mcp_servers.json`

---

## P0 证据（四层分栏，不合成总分）

数字截至 **2026-07-29**；完整地图见 [ReAct Agent · P0_EVIDENCE_MAP](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/P0_EVIDENCE_MAP.md)。

| 层 | 问题 | 数字 | 报告 |
|----|------|------|------|
| **Execution** | 任务能不能干成 | offline **12/12**；agent **36/36** | [agent v3](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/execution_agent_snapshot_20260716_v3.md) |
| **Reliability** | 坏了能不能撑住 | live flaky n=20：**error_obs 0 vs 3.1** | [live v2](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/reliability_live_live_20260716_v2.md) |
| **Failure** | 坏在哪 | golden **27/27**；StepWatcher **6/6**；100 条重扫 offtrack **6→1** | [golden](https://github.com/weihuaguo270-ops/trace-debugger/blob/master/docs/golden_evidence_baseline.md) · [StepWatcher](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/step_watcher_evidence_baseline.md) |
| **Judge** | 评得清不清 | held_out **live** κ≈**0.67**（n=**53**，CI[0.52,0.82]）；r1↔r2 κ≈**0.80** | [v5 live](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/calibration_snapshot_20260727_live_held_out.md) · [怎么读](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/METRICS_TRUST.md) |

> **废止口径：** v4 的 held_out live n=20 / κ≈0.69 是历史快照，对外以 v5 n=53 为准。

**跨日稳定性：** daily smoke 7/17–7/29 连续 PASS → [`VARIANCE.md`](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/daily_smoke/VARIANCE.md)

---

## 目前能核对的内容

| 方向 | 证据 |
|------|------|
| 文档排障 eval | **ReAct Agent** [v0.3.0](https://github.com/weihuaguo270-ops/react-agent/releases/tag/v0.3.0)：golden 34 + fault 12 + production 5 + git 5 |
| StepWatcher 跨仓 | Harness 录制时实时写 failure 标记；6 场景 golden e2e |
| Trace Debugger 独立化 | v0.2.4：`FailureHarness` + adapter + `tdebug validate` + [RISKS](https://github.com/weihuaguo270-ops/trace-debugger/blob/master/docs/RISKS.md) |
| Judge 校准 v5 | **LLM Eval Engine** held_out n=53；第二标注者 r2 已写入；Benchmark live agent **32/32**（2026-07-27） |
| 推理链路 | **LLM 推理链路优化** v0.2.0：MLA absorb max\|Δ\| < 1e-6；Prefill/Decode + Static/Paged Cache 基准 |
| 诚实边界 | execute_python 是学习级子进程+超时；启发式失败分类不是 LLM Judge |

---

## 技术栈

| 领域 | 具体 |
|------|------|
| **语言** | Python（主力）、TypeScript（基础）、C++（基础） |
| **深度学习** | PyTorch、NumPy、Transformer 架构、GQA / MLA、RoPE |
| **Agent** | docs_troubleshoot Workflow、引用/拒答、diagnosis schema；ReAct + LangGraph 对照、MCP（配置外置） |
| **推理优化** | Prefill/Decode 分离、Static/Paged/Prefix KV Cache、Speculative Decoding、Continuous Batching |
| **工程工具** | Git / GitHub Actions、pytest、flake8、FastAPI |
| **评测 / 轨迹** | 文档排障四套 eval、Capability 规则打分、Process Reward Judge、Format B Schema、StepWatcher |

---

## 联系

- **Email:** weihuaguo270@gmail.com  
- **GitHub:** [weihuaguo270-ops](https://github.com/weihuaguo270-ops)

> 当前状态：寻找 2026 暑期实习 · 大模型算法（推理/结构）/ Agent 研发 / LLM 评测方向
