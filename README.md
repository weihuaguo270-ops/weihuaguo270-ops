# 👋 郭伟华 | Guo Weihua

**哈尔滨工程大学 · 计算机科学与技术 · 2027 届本科**

[![CI](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/llm-inference-pipeline/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/llm-inference-pipeline/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml)

> 围绕 LLM/Agent 业务，将“任务执行 → 质量验收 → 失败定位 → 成本优化”拆成四个可复现、可审计的工程项目。
> 当前均为个人主导的研究/工程原型，不声称已经接入真实企业流量、SLA 或多租户生产环境；README 中的证据、假设和缺口均单独标注。

---

## 业务组合（2026-08-13）

当前发布矩阵已同步至 2026-08-20：各仓库按实际改进幅度分别发布 patch 版本；其中 ReAct Agent
包含真实 Podman sandbox 验证，其余项目主要为证据契约和介绍文档同步。

四个项目按业务决策链分工，共用 **Format B** 轨迹约定，分别回答四个问题：Agent 能否稳定完成任务、出了问题在哪里、评测结果是否可信、单位请求成本是否可控。

| 线 | 项目 | 仓库 | 版本 | 我负责推到的状态 |
|----|------|------|------|------------------|
| **业务执行** | **ReAct Agent** | [react-agent](https://github.com/weihuaguo270-ops/react-agent) | [v0.10.1](https://github.com/weihuaguo270-ops/react-agent/releases/tag/v0.10.1) | 运行时、权限、容器工具隔离、Podman live evidence、业务终态评测和 Episode 导出 |
| **质量治理** | **Trace Debugger** | [trace-debugger](https://github.com/weihuaguo270-ops/trace-debugger) | [v0.5.1](https://github.com/weihuaguo270-ops/trace-debugger/releases/tag/v0.5.1) | 将 Format B / Episode 轨迹转为失败分类、回归差异和 CI 门禁；不依赖轨迹生产方 SDK |
| **评测决策** | **LLM Eval Engine** | [llm-eval-engine](https://github.com/weihuaguo270-ops/llm-eval-engine) | [v0.5.1](https://github.com/weihuaguo270-ops/llm-eval-engine/releases/tag/v0.5.1) | 跨 Agent Episode、真实 SDK 适配、业务/过程/失败/性能分栏发布判断 |
| **成本性能** | **LLM 推理链路优化** | [llm-inference-pipeline](https://github.com/weihuaguo270-ops/llm-inference-pipeline) | [v0.3.1](https://github.com/weihuaguo270-ops/llm-inference-pipeline/releases/tag/v0.3.1) | 用 TTFT/TPOT、Cache、质量探针和硬件元数据生成可复核发布性能证据；不声称生产收益 |

**近期完成的业务闭环：**

- Agent 执行产出 Format B 轨迹，StepWatcher 边运行边记录失败事件，Trace Debugger 再按 baseline 做发版前比较。
- Eval Engine 将过程评分与人工标注、数据切分、安全用例和漂移检查分开，输出“通过 / 复核 / 暂缓”依据，而不是只报一个总分。
- 推理链路项目把 TTFT、TPOT、吞吐和 Cache 容量作为成本决策输入；CPU/共享 CI 数字仅作冒烟，GPU 收益需要固定环境复测。
- 目前最重要的业务缺口是：尚无外部团队真实流量、真实 PR hold 记录和线上时序告警；这些被列为下一阶段验收条件。

---

## 建议阅读顺序

1. **[ReAct Agent](https://github.com/weihuaguo270-ops/react-agent)** — 主仓：Agent 运行时 + 三类应用、Harness、跨仓闭环入口
2. **[Trace Debugger](https://github.com/weihuaguo270-ops/trace-debugger)** — 失败怎么检、怎么记、怎么汇总；不绑特定 Agent 框架
3. **[LLM Eval Engine](https://github.com/weihuaguo270-ops/llm-eval-engine)** — 过程分怎么打、κ 怎么算、什么时候不能当 SLA
4. **[LLM 推理链路优化](https://github.com/weihuaguo270-ops/llm-inference-pipeline)** — 推理线：Prefill/Decode、KV Cache、解码策略与微基准

---

## 职责边界（我 deliberately 不声称的）

| 项目 | 负责什么 | 不声称什么 | CI |
|------|----------|------------|:--:|
| [**ReAct Agent**](https://github.com/weihuaguo270-ops/react-agent) | Agent 运行时 + 三类应用 HTTP；Harness + StepWatcher；容器工具隔离；业务终态与轨迹验收 | 自动 API 根因诊断；完整企业权限平台或多租户隔离 | ✅ |
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
- 离线一键：`python examples/eval/harness_closed_loop.py --fixture`（ReAct Agent CI `integration` 会跑）
- StepWatcher 证据：`python examples/eval/run_step_watcher_evidence.py --publish`
- MCP / 本机路径：**不入库**；用 `mcp_servers.example.json` → 本地 `mcp_servers.json`

---

## P0 证据（四层分栏，不合成总分）

数字截至 **2026-08-12**（版本以各仓最新 Release 为准）；完整地图见 [ReAct Agent · P0_EVIDENCE_MAP](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/P0_EVIDENCE_MAP.md)。

| 层 | 问题 | 数字 | 报告 |
|----|------|------|------|
| **Execution** | 任务能不能干成 | offline **12/12**；agent **36/36** | [agent v3](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/execution_agent_snapshot_20260716_v3.md) |
| **Reliability** | 坏了能不能撑住 | live flaky n=20：**error_obs 0 vs 3.1** | [live v2](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/reliability_live_live_20260716_v2.md) |
| **Failure** | 坏在哪 | golden **27/27**；StepWatcher **6/6**；100 条重扫 offtrack **6→1** | [golden](https://github.com/weihuaguo270-ops/trace-debugger/blob/master/docs/golden_evidence_baseline.md) · [StepWatcher](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/step_watcher_evidence_baseline.md) |
| **Judge** | 评得清不清 | held_out **live** κ≈**0.73**（n=**53**，CI[0.58,0.88]）；r1↔r2 κ≈**0.80** | [v5 live](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/calibration_snapshot_20260807_live_held_out.md) · [怎么读](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/METRICS_TRUST.md) |

> **废止口径：** v4 的 held_out live n=20 / κ≈0.69 是历史快照，对外以 v5 n=53 为准。

**跨日稳定性：** daily smoke 持续 PASS → [`VARIANCE.md`](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/daily_smoke/VARIANCE.md)

---

## 目前能核对的内容

| 方向 | 证据 |
|------|------|
| Agent 运行时 / 多 app | **ReAct Agent** [v0.8.0](https://github.com/weihuaguo270-ops/react-agent/releases/tag/v0.8.0)：容器工具隔离、可移植运行数据、Expense dev/golden/held_out 和 Episode 导出 |
| 文档排障 eval | golden 34 + fault 12 + production 5 + git 5（CI 四门禁） |
| StepWatcher 跨仓 | Harness 录制时实时写 failure 标记；6 场景 golden e2e |
| Trace Debugger | [v0.4.0](https://github.com/weihuaguo270-ops/trace-debugger/releases/tag/v0.4.0)：SDK 无关 Episode 导入、可移植 failure log、75 项回归；[RISKS](https://github.com/weihuaguo270-ops/trace-debugger/blob/master/docs/RISKS.md) |
| Judge 与发布判断 | **LLM Eval Engine** [v0.4.0](https://github.com/weihuaguo270-ops/llm-eval-engine/releases/tag/v0.4.0)：校准 v5、真实 LangGraph/OpenAI Agents SDK 接入、四类证据门禁函数 |
| 推理链路 | **LLM 推理链路优化** [v0.2.0](https://github.com/weihuaguo270-ops/llm-inference-pipeline/releases/tag/v0.2.0)：RTX 4060 记录负载 TTFT 2.68 ms、缓存 TPOT 2.71 ms；仅对记录环境有效 |
| 诚实边界 | process Sandbox 只隔离崩溃/超时；container 才是工具执行 OS 边界；启发式失败分类不是 LLM Judge |

---

## 技术栈

| 领域 | 具体 |
|------|------|
| **语言** | Python（主力）、TypeScript（基础）、C++（基础） |
| **深度学习** | PyTorch、NumPy、Transformer 架构、GQA / MLA、RoPE |
| **Agent** | 三类应用 HTTP（default / docs_troubleshoot / expense）；证据化文档排障；ReAct + LangGraph 对照、MCP（配置外置） |
| **推理优化** | Prefill/Decode 分离、Static/Paged/Prefix KV Cache、Speculative Decoding、Continuous Batching |
| **工程工具** | Git / GitHub Actions、pytest、flake8、FastAPI |
| **评测 / 轨迹** | 文档排障四套 eval、Capability 规则打分、Process Reward Judge、Format B Schema、StepWatcher |

---

## 联系

- **Email:** weihuaguo270@gmail.com  
- **GitHub:** [weihuaguo270-ops](https://github.com/weihuaguo270-ops)

> 当前状态：寻找 2026 暑期实习 · 大模型算法（推理/结构）/ Agent 研发 / LLM 评测方向
