# 👋 郭伟华 | Guo Weihua

**哈尔滨工程大学 · 计算机科学与技术 · 2027 届本科**

[![CI](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/transformer-attention/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/transformer-attention/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml)

> 求职方向：大模型算法 / Agent 研发 / LLM 评测 · 2026 年 7 月起可实习  
> 下列项目均为**个人学习与实验实现**，用于理解原理与工程结构，**非生产交付物**。

---

## 怎么读这些仓库

1. **先看** [react-agent](https://github.com/weihuaguo270-ops/react-agent) — 主仓：证据化文档排障 + Workflow 运行时 + Harness 跨仓闭环 · [v0.3.0](https://github.com/weihuaguo270-ops/react-agent/releases/tag/v0.3.0)
2. **再看** [transformer-attention](https://github.com/weihuaguo270-ops/transformer-attention) — 算法线：MHA / GQA / MLA（含 absorb）手写对照
3. **选看** [llm-eval-engine](https://github.com/weihuaguo270-ops/llm-eval-engine) — 评测线：过程级 Judge / 人机校准（小样本，分栏报数）
4. **了解** [trace-debugger](https://github.com/weihuaguo270-ops/trace-debugger) — 配套：轨迹失败分类 / 回放（非主项目）

---

## 核心项目与职责边界

| 项目 | 负责什么 | 不声称什么 | CI |
|------|----------|------------|:--:|
| [**react-agent**](https://github.com/weihuaguo270-ops/react-agent) | 证据化文档/Runbook 问答（Workflow v5、引用/拒答）；传入式现场证据 + 规则 diagnosis；四套离线 eval；Harness + capability；跨仓闭环 | 自动 API 根因诊断；生产级沙箱 | ✅ |
| [**llm-eval-engine**](https://github.com/weihuaguo270-ops/llm-eval-engine) | 过程级 LLM-as-Judge、Eval Loop、人机校准 | 训练型 PRM / 替代 react-agent 的 capability 主评测集 | ✅ |
| [**transformer-attention**](https://github.com/weihuaguo270-ops/transformer-attention) | Attention 教学实现与微基准（NumPy / 小规模 PyTorch） | 大规模预训练效果 | ✅ |
| [**trace-debugger**](https://github.com/weihuaguo270-ops/trace-debugger) | 轨迹启发式复盘（工具失败 / 跑偏 / 溢出等） | Agent 可观测「平台」 | ✅ |

### 跨仓闭环（可复现 demo）

```text
Agent 执行 → Harness 轨迹 (Format B, 1-based step)
          → trace-debugger 失败分类
          → llm-eval-engine 过程级 Judge 评分
```

- Schema：[`react-agent/schemas/harness_trajectory.schema.json`](https://github.com/weihuaguo270-ops/react-agent/blob/main/schemas/harness_trajectory.schema.json)  
- 一键脚本：`python examples/harness_closed_loop.py --fixture`（react-agent CI `integration` 会跑）  
- MCP / 本机路径：**不入库**；用 `mcp_servers.example.json` → 本地 `mcp_servers.json`  
- 核心依赖轻量；语义检索 / RAG：`pip install -e ".[rag]"`

---

## P0 证据地图（四层一张表）

讲四层证据时，从 [react-agent P0_EVIDENCE_MAP](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/P0_EVIDENCE_MAP.md) 起；Execution / Reliability / Failure / Judge **分开报**，不要合成一个总分：

| 层 | 数字（2026-07） | 公开页 |
|----|-----------------|--------|
| Execution | offline **12/12**；agent **36/36** | [agent v3](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/execution_agent_snapshot_20260716_v3.md) |
| Reliability | live flaky n=20：**error_obs 0 vs 3.1** | [live v2](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/reliability_live_live_20260716_v2.md) |
| Failure | 同批 100 条：`llm_offtrack` **6→1** | [飞轮闭环](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/flywheel_closed_loop_20260716.md) |
| Judge | **held_out live** κ≈**0.69**（n=20，CI[0.46,0.92]）；offline held_out=1.0（n=20，冻结） | [live](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/calibration_snapshot_20260716_live.md) · [怎么读](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/METRICS_TRUST.md) |

---

## 目前能核对的内容（2026-07）

| 方向 | 证据 |
|------|------|
| 文档排障 eval | [v0.3.0](https://github.com/weihuaguo270-ops/react-agent/releases/tag/v0.3.0)：golden 34 + fault 12 + production 5 + git 5 · [DOCS_TROUBLESHOOT_EVAL](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/DOCS_TROUBLESHOOT_EVAL.md) |
| Agent ↔ 评测闭环 | Format B Schema + 离线 fixture；CI clone tdebug / eval-engine |
| P0 四层证据 | 见上表 · [P0_EVIDENCE_MAP](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/P0_EVIDENCE_MAP.md) |
| Judge 校准 | held_out live κ≈0.69（n=20）；第二标注者 protocol_ready，尚无 r2 |
| 算法线 | MLA absorb 数值对齐 + 微基准 CSV；PyTorch 套件进 CI |
| 权限 / 沙箱 | 文档写明学习级闸门与超时隔离，**不是**安全边界 |

---

## 技术栈

| 领域 | 具体 |
|------|------|
| **语言** | Python（主力）、TypeScript（基础）、C++（基础） |
| **深度学习** | PyTorch、NumPy、Transformer 架构、GQA / MLA、RoPE |
| **Agent** | docs_troubleshoot Workflow、引用/拒答、diagnosis schema；ReAct + LangGraph 对照、MCP（配置外置） |
| **工程工具** | Git / GitHub Actions、pytest、flake8、FastAPI |
| **评测 / 轨迹** | 文档排障四套 eval、Capability 规则打分、过程级 Judge、Harness Schema |

---

## 联系

- **Email:** weihuaguo270@gmail.com  
- **GitHub:** [weihuaguo270-ops](https://github.com/weihuaguo270-ops)

> 当前状态：寻找 2026 暑期实习 · 大模型算法 / Agent 研发 / LLM 评测方向
