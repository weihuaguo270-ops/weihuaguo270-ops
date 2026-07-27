# 仓库 About / Bio 建议文案（需在 GitHub 网页或 `gh` 更新）

> 本地 README 已统一为学习/实验口径；下面用于同步 **Profile bio** 与各仓 **About description**。

## Profile bio（建议）

```text
哈工程计算机 · 大三 · 大模型算法 / Agent / LLM 评测
主仓 react-agent（证据化文档排障 + Harness 闭环）；另三条为算法/评测/轨迹配套
```

## 各仓 About description（建议）

| 仓库 | 建议简介 |
|------|----------|
| react-agent | `Agent 运行时 — 证据化文档排障、四套离线 eval、Harness 轨迹、跨仓闭环（非生产沙箱）` |
| llm-eval-engine | `LLM 评估实验 — Process Reward / 人机校准；对接 react-agent 轨迹` |
| transformer-attention | `Attention 手写对照 — MHA、GQA、MLA absorb、小规模 PyTorch` |
| trace-debugger | `Harness 轨迹复盘 — 失败分类、回放、批量扫描（配套）` |

### 命令（需有效 `gh auth`）

```bash
gh repo edit weihuaguo270-ops/react-agent --description "Agent 运行时 — 证据化文档排障、四套离线 eval、Harness 轨迹、跨仓闭环（非生产沙箱）"
gh repo edit weihuaguo270-ops/llm-eval-engine --description "LLM 评估实验 — Process Reward / 人机校准；对接 react-agent 轨迹"
gh repo edit weihuaguo270-ops/transformer-attention --description "Attention 手写对照 — MHA、GQA、MLA absorb、小规模 PyTorch"
gh repo edit weihuaguo270-ops/trace-debugger --description "Harness 轨迹复盘 — 失败分类、回放、批量扫描（配套）"
```

Profile bio：GitHub → Settings → Profile → Bio。
