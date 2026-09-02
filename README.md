# 👋 郭伟华 | Guo Weihua

**哈尔滨工程大学 · 计算机科学与技术 · 2027 届本科**

[![CI](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/llm-inference-pipeline/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/llm-inference-pipeline/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml)

> 我把 LLM/Agent 项目拆成四条可以独立验收的线：任务执行、质量验收、失败定位和推理成本。
> 这些仓库由我设计、实现和维护，定位是个人主导的研究与工程原型；我会把已经验证的内容、
> 仍然缺失的证据和不能外推的结论分开写清楚。

---

## 业务组合（2026-09-02）

我目前维护四个相互衔接的仓库，共用 Format B 轨迹约定。最近一轮更新中，ReAct Agent 完成了
真实 Podman sandbox 验证，并完成可选 Milvus 后端的本机 Compose 联调；另外三个项目补齐了评测、
证据和复现契约。版本号按实际变化分别递增，没有为了看起来整齐而统一改版本。

四个项目按业务决策链分工，共用 **Format B** 轨迹约定，分别回答四个问题：Agent 能否稳定完成任务、出了问题在哪里、评测结果是否可信、单位请求成本是否可控。

| 线 | 项目 | 仓库 | 版本 | 我目前负责的结果 |
|----|------|------|------|------------------|
| **业务执行** | **ReAct Agent** | [react-agent](https://github.com/weihuaguo270-ops/react-agent) | [v0.10.1](https://github.com/weihuaguo270-ops/react-agent/releases/tag/v0.10.1) | 运行时、权限、容器工具隔离、Podman live evidence、可选 Milvus RAG、业务终态评测和 Episode 导出 |
| **质量治理** | **Trace Debugger** | [trace-debugger](https://github.com/weihuaguo270-ops/trace-debugger) | [v0.5.1](https://github.com/weihuaguo270-ops/trace-debugger/releases/tag/v0.5.1) | 将 Format B / Episode 轨迹转为失败分类、回归差异和 CI 门禁；不依赖轨迹生产方 SDK |
| **评测决策** | **LLM Eval Engine** | [llm-eval-engine](https://github.com/weihuaguo270-ops/llm-eval-engine) | [v0.5.1](https://github.com/weihuaguo270-ops/llm-eval-engine/releases/tag/v0.5.1) | 跨 Agent Episode、真实 SDK 适配、业务/过程/失败/性能分栏发布判断 |
| **成本性能** | **LLM 推理链路优化** | [llm-inference-pipeline](https://github.com/weihuaguo270-ops/llm-inference-pipeline) | [v0.3.1](https://github.com/weihuaguo270-ops/llm-inference-pipeline/releases/tag/v0.3.1) | 用 TTFT/TPOT、Cache、质量探针和硬件元数据生成可复核发布性能证据；不声称生产收益 |

**我最近完成的工作：**

- 我让 Agent 执行、轨迹记录、失败分析和过程评测连成一条可回放的离线闭环。
- 我把业务结果、过程分数、人工标注、数据切分、安全用例和漂移检查分栏，发布判断不再压成一个总分。
- 我在 Podman machine 上实际创建并运行 sandbox 容器，验证了身份、namespace、seccomp、文件系统、资源、断网、密钥隔离和超时清理，共 23 项检查全部通过。
- 我新增了可选 Milvus RAG 后端，并在本机 Docker Compose 中验证 Agent、Milvus、etcd、MinIO 的健康状态，以及 HNSW 写入、检索、来源枚举、清理和文档排障 `/v1/chat`。这属于 `local_integration`，不等同多实例容量、鉴权、备份或生产 SLA。
- 我把推理项目的 TTFT、TPOT、吞吐、Cache 和质量探针整理成可复现证据；共享 CI/CPU 数字只用于工程回归，GPU 结论仍绑定具体硬件和负载。
- 下一阶段我会补真实团队任务、线上时序告警、长期稳定性和真实 PR hold 记录；这些目前都没有被我包装成生产能力。

---

## 建议阅读顺序

1. **[ReAct Agent](https://github.com/weihuaguo270-ops/react-agent)** — 主仓：Agent 运行时 + 三类应用、Harness、跨仓闭环入口
2. **[Trace Debugger](https://github.com/weihuaguo270-ops/trace-debugger)** — 失败怎么检、怎么记、怎么汇总；不绑特定 Agent 框架
3. **[LLM Eval Engine](https://github.com/weihuaguo270-ops/llm-eval-engine)** — 过程分怎么打、κ 怎么算、什么时候不能当 SLA
4. **[LLM 推理链路优化](https://github.com/weihuaguo270-ops/llm-inference-pipeline)** — 推理线：Prefill/Decode、KV Cache、解码策略与微基准

---

## 我不会把这些说成已经完成

| 项目 | 我已经做到 | 目前仍不能声称 | CI |
|------|----------|------------|:--:|
| [**ReAct Agent**](https://github.com/weihuaguo270-ops/react-agent) | Agent 运行时 + 三类应用 HTTP；Harness + StepWatcher；容器工具隔离；本地 / 可选 Milvus RAG；业务终态与轨迹验收 | 自动 API 根因诊断；完整企业权限平台、多租户隔离，或 Milvus 生产容量与 SLA | ✅ |
| [**Trace Debugger**](https://github.com/weihuaguo270-ops/trace-debugger) | 8 类启发式失败检测；JSONL 记录 + 聚合统计；黄金集 27 条；可嵌入任意 ReAct Harness | Agent 可观测「平台」；自动修复 Agent | ✅ |
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

本节于 **2026-09-02** 核对；表内数字仍以各报告自身的证据快照日期为准（版本以各仓当前发布矩阵为准）。
完整地图见 [ReAct Agent · P0_EVIDENCE_MAP](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/P0_EVIDENCE_MAP.md)。我不把不同证据层合成一个总分。

| 层 | 问题 | 数字 | 报告 |
|----|------|------|------|
| **Execution** | 任务能不能干成 | expense business pilot **8/8**；公开 GitHub 只读任务 **50/50** | [business pilot](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/reports/business_pilot_execution_20260820.md) |
| **Reliability** | 坏了能不能撑住 | live flaky n=20：**error_obs 0 vs 3.1** | [live v2](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/reliability_live_live_20260716_v2.md) |
| **Failure** | 坏在哪 | golden **27/27**；StepWatcher **6/6**；sandbox fault 回流为 `acceptance_failed` | [golden](https://github.com/weihuaguo270-ops/trace-debugger/blob/master/docs/golden_evidence_baseline.md) · [fault feedback](https://github.com/weihuaguo270-ops/agent-delivery-sandbox/blob/main/evidence/failure_feedback_20260814.json) |
| **Judge** | 评得清不清 | held_out **live** κ≈**0.73**（n=**53**，CI[0.58,0.88]）；r1↔r2 κ≈**0.80** | [v5 live](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/calibration_snapshot_20260807_live_held_out.md) · [怎么读](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/METRICS_TRUST.md) |

> **废止口径：** v4 的 held_out live n=20 / κ≈0.69 是历史快照，对外以 v5 n=53 为准。

**跨日稳定性：** daily smoke 持续 PASS → [`VARIANCE.md`](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/daily_smoke/VARIANCE.md)

**运行隔离补充证据：** ReAct Agent 的 Podman live check 在本机 rootless WSL2 环境完成
23/23 项检查，覆盖 UID/GID、user/IPC namespace、`--init`、seccomp、capability、只读根文件系统、
`/tmp` noexec、资源上限、默认断网、宿主密钥隔离和超时清理。这证明了当前实现可在该环境运行，
不等于生产节点逃逸测试或安全认证。

---

## 目前能核对的内容

| 方向 | 证据 |
|------|------|
| Agent 运行时 / 多 app | **ReAct Agent** [v0.10.1](https://github.com/weihuaguo270-ops/react-agent/releases/tag/v0.10.1)：容器工具隔离、Podman live check 23/23、可选 Milvus HNSW 本机 Compose 联调、可移植运行数据、业务 pilot 和 Episode 导出；Milvus 证据仅为 `local_integration` |
| 文档排障 eval | golden 34 + fault 12 + production 5 + git 5（CI 四门禁） |
| StepWatcher 跨仓 | Harness 录制时实时写 failure 标记；6 场景 golden e2e |
| Trace Debugger | [v0.5.1](https://github.com/weihuaguo270-ops/trace-debugger/releases/tag/v0.5.1)：SDK 无关 Episode 导入、可移植 failure log、失败分类和 75 项回归；[RISKS](https://github.com/weihuaguo270-ops/trace-debugger/blob/master/docs/RISKS.md) |
| Judge 与发布判断 | **LLM Eval Engine** [v0.5.1](https://github.com/weihuaguo270-ops/llm-eval-engine/releases/tag/v0.5.1)：校准 v5、真实 LangGraph/OpenAI Agents SDK 接入、多模态证据和四类发布门禁 |
| 推理链路 | **LLM 推理链路优化** [v0.3.1](https://github.com/weihuaguo270-ops/llm-inference-pipeline/releases/tag/v0.3.1)：Prefill/Decode、KV Cache、RTX 4060 记录负载和模型质量探针；结果仅对记录环境有效 |
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

> 当前状态：寻找大模型推理 / Agent 研发 / LLM 评测方向的实习或工程机会
