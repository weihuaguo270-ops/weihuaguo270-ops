# 仓库 About / Bio 建议文案（需在 GitHub 网页或 `gh` 更新）

> 与 README 同步；口径：**个人学习/实验项目**。
> 版本核对日：**2026-08-13**。

## Profile bio（建议）

```text
哈工程计算机 · 大三 · 大模型算法（推理/结构）/ Agent / LLM 评测
四条线：ReAct Agent · Trace Debugger · LLM Eval Engine · LLM 推理链路优化
```

## 各仓 About description（建议）

| 项目 | 仓库 | 版本 | 建议简介 |
|------|------|------|----------|
| ReAct Agent | react-agent | **v0.8.0** | `Agent 运行时 — 受控工具执行、容器 Sandbox、可移植运行数据、业务终态评测与 Episode 导出（v0.8.0）` |
| Trace Debugger | trace-debugger | **v0.4.0** | `Agent 失败治理门禁 — scan/compare、7 类失败检测、SDK 无关 Episode 导入、可移植 failure log（v0.4.0）` |
| LLM Eval Engine | llm-eval-engine | **v0.4.0** | `跨 Agent 评测决策 — Process Reward、Judge 校准、Episode、SDK 接入和四类证据发布判断（v0.4.0）` |
| LLM 推理链路优化 | llm-inference-pipeline | **v0.2.0** | `LLM 推理链路优化 — Prefill/Decode 基准、KV Cache、GQA/MLA、Spec Decoding（v0.2.0）` |

> 废止：`transformer-attention` 已更名为 `llm-inference-pipeline`（2026-07-28）。

### 命令（需有效 `gh auth`）

```bash
gh repo edit weihuaguo270-ops/react-agent --description "Agent 运行时 — 受控工具执行、容器 Sandbox、可移植运行数据、业务终态评测与 Episode 导出（v0.8.0）"
gh repo edit weihuaguo270-ops/trace-debugger --description "Agent 失败治理门禁 — scan/compare、7 类失败检测、SDK 无关 Episode 导入、可移植 failure log（v0.4.0）"
gh repo edit weihuaguo270-ops/llm-eval-engine --description "跨 Agent 评测决策 — Process Reward、Judge 校准、Episode、SDK 接入和四类证据发布判断（v0.4.0）"
gh repo edit weihuaguo270-ops/llm-inference-pipeline --description "LLM 推理链路优化 — Prefill/Decode 基准、KV Cache、GQA/MLA、Spec Decoding（v0.2.0）"
```

Profile bio：GitHub → Settings → Profile → Bio。
