# 仓库 About / Bio 建议文案（需在 GitHub 网页或 `gh` 更新）

> 与 README 同步；口径：**我个人负责的研究/工程原型**。
> 版本核对日：**2026-08-21**。

## Profile bio（建议）

```text
哈工程计算机 · 2027 届 · 大模型推理 / Agent 研发 / LLM 评测
我维护四条线：ReAct Agent · Trace Debugger · LLM Eval Engine · LLM 推理链路优化
```

## 各仓 About description（建议）

| 项目 | 仓库 | 版本 | 建议简介 |
|------|------|------|----------|
| ReAct Agent | react-agent | **v0.10.1** | `Agent 运行时 — 受控工具执行、Podman Sandbox 实测、可移植运行数据、业务终态评测与 Episode 导出（v0.10.1）` |
| Trace Debugger | trace-debugger | **v0.5.1** | `Agent 失败治理门禁 — scan/compare、8 类失败检测、SDK 无关 Episode 导入、可移植 failure log（v0.5.1）` |
| LLM Eval Engine | llm-eval-engine | **v0.5.1** | `跨 Agent 评测决策 — Process Reward、Judge 校准、多模态证据和四类发布门禁（v0.5.1）` |
| LLM 推理链路优化 | llm-inference-pipeline | **v0.3.1** | `LLM 推理链路优化 — Prefill/Decode、KV Cache、质量探针和硬件约束证据（v0.3.1）` |

> 废止：`transformer-attention` 已更名为 `llm-inference-pipeline`（2026-07-28）。

### 命令（需有效 `gh auth`）

```bash
gh repo edit weihuaguo270-ops/react-agent --description "Agent 运行时 — 受控工具执行、Podman Sandbox 实测、可移植运行数据、业务终态评测与 Episode 导出（v0.10.1）"
gh repo edit weihuaguo270-ops/trace-debugger --description "Agent 失败治理门禁 — scan/compare、8 类失败检测、SDK 无关 Episode 导入、可移植 failure log（v0.5.1）"
gh repo edit weihuaguo270-ops/llm-eval-engine --description "跨 Agent 评测决策 — Process Reward、Judge 校准、多模态证据和四类发布门禁（v0.5.1）"
gh repo edit weihuaguo270-ops/llm-inference-pipeline --description "LLM 推理链路优化 — Prefill/Decode、KV Cache、质量探针和硬件约束证据（v0.3.1）"
```

Profile bio：GitHub → Settings → Profile → Bio。
