# 👋 郭伟华 | Guo Weihua

**哈尔滨工程大学 · 计算机科学与技术 · 2027 届本科**

[![CI](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/react-agent/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/llm-eval-engine/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/transformer-attention/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/transformer-attention/actions/workflows/test.yml)
[![CI](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml/badge.svg)](https://github.com/weihuaguo270-ops/trace-debugger/actions/workflows/test.yml)

> 求职方向：大模型算法 / Agent 研发 / LLM 评测 · 2026 年 7 月起可实习  
> 下列项目均为**个人学习与实验实现**，用于理解原理与工程结构，**非生产交付物**。

---

## 推荐阅读顺序（面试向）

1. **先看** [react-agent](https://github.com/weihuaguo270-ops/react-agent) — 主作品：ReAct 运行时 + Harness 轨迹 + capability 公开快照  
2. **再看** [transformer-attention](https://github.com/weihuaguo270-ops/transformer-attention) — 算法线：MHA / GQA / MLA（含 absorb 路径）手写对照  
3. **选看** [llm-eval-engine](https://github.com/weihuaguo270-ops/llm-eval-engine) — 评测线：过程级 LLM-as-Judge / 人机校准（小样本诚实报告）
4. **了解** [trace-debugger](https://github.com/weihuaguo270-ops/trace-debugger) — 配套：轨迹失败分类 / 回放（非独立主项目）

---

## 核心项目与职责边界

| 项目 | 负责什么 | 不声称什么 | CI |
|------|----------|------------|:--:|
| [**react-agent**](https://github.com/weihuaguo270-ops/react-agent) | 手写 ReAct + LangGraph 对照；Harness 轨迹 Schema；capability 规则评测；跨仓一键闭环 | 生产级安全沙箱 / 不可信代码隔离 | ✅ |
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

面试时建议从 [react-agent P0_EVIDENCE_MAP](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/P0_EVIDENCE_MAP.md) 起讲，四层指标**刻意分开**：

| 层 | 数字（2026-07） | 公开页 |
|----|-----------------|--------|
| Execution | offline **12/12**；agent **36/36** | [agent v3](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/execution_agent_snapshot_20260716_v3.md) |
| Reliability | live flaky n=20：**error_obs 0 vs 3.1** | [live v2](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/reliability_live_live_20260716_v2.md) |
| Failure | 同批 100 条：`llm_offtrack` **6→1** | [飞轮闭环](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/flywheel_closed_loop_20260716.md) |
| Judge | live κ≈**0.68**（n=28） | [calibration live](https://github.com/weihuaguo270-ops/llm-eval-engine/blob/master/docs/calibration_snapshot_20260716_live.md) |

---

## 近期可验证点（2026-07）

| 方向 | 证据 |
|------|------|
| Agent ↔ 评测闭环 | Format B Schema + 离线 fixture + CI 安装 tdebug / eval-engine |
| P0 四层证据 | 见上表 + [P0_EVIDENCE_MAP](https://github.com/weihuaguo270-ops/react-agent/blob/main/docs/P0_EVIDENCE_MAP.md) |
| 公开评测诚实性 | capability / execution 快照；eval-engine live Judge κ≈0.68（单人标注、无 held-out） |
| 算法线 | transformer-attention MLA absorb 数值对齐 + 微基准 CSV；PyTorch 套件进 CI |
| 工程克制 | 权限 / 子进程执行写明「学习级提示与超时隔离，非安全边界」 |

---

## 技术栈

| 领域 | 具体 |
|------|------|
| **语言** | Python（主力）、TypeScript（基础）、C++（基础） |
| **深度学习** | PyTorch、NumPy、Transformer 架构、GQA / MLA、RoPE |
| **Agent** | 手写 ReAct Loop、LangGraph 对照、MCP（配置外置）、多 Agent 编排实验 |
| **工程工具** | Git / GitHub Actions、pytest、flake8、FastAPI |
| **评测 / 轨迹** | Capability 规则打分、过程级 LLM-as-Judge、人机校准、Harness Schema |

---

## 联系

- **Email:** weihuaguo270@gmail.com  
- **GitHub:** [weihuaguo270-ops](https://github.com/weihuaguo270-ops)

> 当前状态：寻找 2026 暑期实习 · 大模型算法 / Agent 研发 / LLM 评测方向
