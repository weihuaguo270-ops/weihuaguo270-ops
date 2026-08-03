# 仓库 About / Bio 建议文案（需在 GitHub 网页或 `gh` 更新）

> 与 README 同步；口径：**个人学习/实验项目**，项目负责人视角。  
> 版本核对日：**2026-08-03**。

## Profile bio（建议）

```text
哈工程计算机 · 大三 · 大模型算法（推理/结构）/ Agent / LLM 评测
四条线：ReAct Agent · Trace Debugger · LLM Eval Engine · LLM 推理链路优化
```

## 各仓 About description（建议）

| 项目 | 仓库 | 版本 | 建议简介 |
|------|------|------|----------|
| ReAct Agent | react-agent | **v0.5.1** | `Agent 运行时 — 三类应用（编码/客服/RAG）· 多 app HTTP · 证据化文档排障 · Harness/StepWatcher（v0.5.1）` |
| Trace Debugger | trace-debugger | **v0.2.6** | `Agent 回归测试与失败治理门禁 — scan/compare baseline、7 类失败检测、golden CI、Format B 本地轨迹（v0.2.6）` |
| LLM Eval Engine | llm-eval-engine | **v0.2.0** | `过程级 LLM 评测 — Process Reward、Benchmark 32 条、Judge 校准 v5（held_out n=53）` |
| LLM 推理链路优化 | llm-inference-pipeline | **v0.2.0** | `LLM 推理链路优化 — Prefill/Decode 基准、KV Cache、GQA/MLA、Spec Decoding（v0.2.0）` |

> 废止：`transformer-attention` 已更名为 `llm-inference-pipeline`（2026-07-28）。

### 命令（需有效 `gh auth`）

```bash
gh repo edit weihuaguo270-ops/react-agent --description "Agent 运行时 — 三类应用（编码/客服/RAG）· 多 app HTTP · 证据化文档排障 · Harness/StepWatcher（v0.5.1）"
gh repo edit weihuaguo270-ops/trace-debugger --description "Agent 回归测试与失败治理门禁 — scan/compare baseline、7 类失败检测、golden CI、Format B 本地轨迹（v0.2.6）"
gh repo edit weihuaguo270-ops/llm-eval-engine --description "过程级 LLM 评测 — Process Reward、Benchmark 32 条、Judge 校准 v5（held_out n=53）"
gh repo edit weihuaguo270-ops/llm-inference-pipeline --description "LLM 推理链路优化 — Prefill/Decode 基准、KV Cache、GQA/MLA、Spec Decoding（v0.2.0）"
```

Profile bio：GitHub → Settings → Profile → Bio。
