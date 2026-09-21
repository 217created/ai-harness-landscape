# AI Agent Harness 全景研究

> Claude Code / Codex / OpenClaw / omp (oh-my-pi) / Hermes Agent
> —— 五款 AI Agent 工具的设计原理与市场反应对比研究

## 项目简介

2025-2026 年，"harness"（工具脚手架）成为 AI 编程代理领域的核心关键词。
模型能力趋同之后，围绕模型的工程层——工具调用、沙箱、权限、上下文管理、记忆、编排——成为产品间的主要差异点。

本研究对比五款代表性 AI Agent 工具的：

1. **设计原理**（架构决策与设计哲学）
2. **市场反应**（增长曲线、关键事件、社区口碑）

## 研究对象一览

| 工具 | 发布 | 出身 | 一句话定位 |
|---|---|---|---|
| Claude Code | 2025.2 预研 / 2025.5 GA | Anthropic 官方 | "模型自主 + 富基础设施"的 harness 标杆，商业上最成功 |
| Codex CLI | 2025.4 开源 | OpenAI 官方 | Rust 重写的本地优先终端 agent，靠 ChatGPT 订阅捆绑放量 |
| OpenClaw | 2025.11（Clawdbot 起家） | 个人项目 → 基金会 | 史上涨星最快，经历爆火→安全危机→4月翻车→2.0 的完整周期 |
| omp (oh-my-pi) | 2025 年底 | Mario Zechner 的 Pi 之 fork | 社区驱动的"全家桶"型 coding agent，极客圈小众口碑 |
| Hermes Agent | 2025 年 | Nous Research | 主打"自我改进闭环"（技能/记忆/跨会话），多端 + 模型自由 |

## 提纲（v1）

### 一、开篇：什么是 harness，为什么它突然成了关键词

- 定义：harness = 模型外的一切工程（工具、沙箱、权限、上下文管理、记忆、编排）
- 核心论据：模型趋同后，harness 质量成为主要差异点
  - 同一模型仅换 harness，长任务成绩可相差 18 分（Ding et al., 2026）
  - Claude Code 约 1.6% 代码是决策逻辑，98.4% 是 operational harness
- 为什么 2025-2026 出现"第三代 Agent"：从 workflow 编排（LangGraph）到 harness 工程

### 二、逐个产品深挖

每款产品按统一框架分析：设计原理 → 市场反应 → 关键数据 → 遗留问题。

#### 2.1 Claude Code

- 设计原理：模型最大自主权 + 富操作性 harness；ReAct 循环；harness 不替模型做决策
- 市场反应：6 个月 $1B ARR（企业软件史上最快）→ 2026.5 约 $8B ARR；54% AI 编码市场份额；约 4% 的全球公共 GitHub commit 由它产生
- 关键数据：131k+ stars（2026.6）；Pragmatic Engineer 调查 46% "most loved"
- 遗留问题：结构化工作流的缺失导致长任务漂移；上下文窗口管理

#### 2.2 Codex CLI

- 设计原理：本地优先 + OS 级沙箱（macOS Seatbelt / Linux Landlock）；开源 Apache-2.0；TypeScript → Rust 重写
- 市场反应：发布一年 500 万周活；免费 CLI + ChatGPT 订阅捆绑的分发策略
- 关键数据：约 96k stars（2026.7）；CLI 是 Codex 全产品线中使用最多的表面
- 遗留问题：模型单一（只吃 OpenAI 模型）；终端可扩展性落后 Claude Code

#### 2.3 OpenClaw

- 设计原理：消息平台（WhatsApp/Telegram）作为 agent 入口；本地运行 + 接外部 LLM；"我发布我没读过的代码"式快速迭代（→ 危机的根源）
- 市场反应：完整 hype 周期——
  - 2025.11 以 Clawdbot 之名发布；2026.1 改名事件反而助推增长
  - 60 天超越 React 十年 star 记录；48 小时 34,168 stars
  - 2026.3 达 25 万 star；创造者加入 OpenAI；项目移交基金会
  - 2026.4 "至暗一周"：插件迁移事故 + Anthropic 断供 + 中国市场退潮
  - 2026.8 发布 2.0 修复大部分问题
- 关键数据：38 万+ stars（2026.8）；HN 月提及量从峰值 759 跌至 ~72（-90%）；但 npm 周下载 6 月创历史新高（428 万/周）
- 遗留问题：热议已死但项目未死——热度曲线与使用曲线是两条不同的钟
- 值得单独一节：为什么它的创新被原厂收编（消息入口 → 官方 agent 产品化）

#### 2.4 omp (oh-my-pi)

- 设计原理：Pi（Mario Zechner）之 fork；TypeScript 全家桶 + Rust 混合；"IDE wired in"；hash-anchored edits；持久 Python/Bun 内核可回调 agent 工具
- 市场反应：小众但高粘性；29k stars；fork 生态活跃（oh-omp 等）
- 关键数据：21k+ commits（一年内）；围绕它的规格驱动开发框架（AEF）社区
- 遗留问题：fork 文化 = 社区驱动 harness 的样本；与官方重装路线的对照

#### 2.5 Hermes Agent

- 设计原理：唯一主打"自我改进闭环"的 harness——技能从经验自动生成、使用中自我改进、跨会话记忆（FTS5 检索 + 用户建模）
- 市场反应：Nous Research（模型训练公司）出品；科研系出身；提供 `hermes claw migrate` 直接承接 OpenClaw 用户
- 关键数据：（待补充——公开数据最少，可能需官方渠道）
- 遗留问题：模型自由（OpenRouter/自定义端点）vs 官方 harness 的模型锁定，哪条路线对用户更友好

### 三、横向对比分析（研究核心）

#### 3.1 设计哲学光谱

- 官方重装（Claude Code / Codex）vs 社区轻量（omp）vs 个人爆款（OpenClaw）vs 科研系（Hermes）

#### 3.2 对比维度

| 维度 | 对比点 |
|---|---|
| 入口选择 | 终端 CLI vs 消息平台（WhatsApp/Telegram）vs 桌面 |
| 模型策略 | 锁定自家 vs 模型自由（provider 无关） |
| 权限/沙箱 | 审批流 vs OS 级隔离 |
| 扩展机制 | Skills / MCP / 插件 |
| 记忆与自我改进 | 谁真做了闭环 |

#### 3.3 市场反应的三种模式

- 商业成功（Claude Code $8B ARR）
- 文化现象（OpenClaw 25 万星 + 全民养虾 + 退潮）
- 小众存活（omp、Hermes——数据少但社区高粘性）

#### 3.4 OpenClaw 案例专析

- 为什么热度死了但项目没死
- harness 创新被原厂收编意味着什么

### 四、趋势判断与启示

- harness 工程的收敛点：各家为什么长得越来越像
- 入口战争：终端 vs 消息平台 vs 桌面
- 对独立开发者的启示

## 目录结构（计划）

```
docs/
  01-what-is-harness.md      # 第一章：概念与背景
  02-case-studies/           # 第二章：逐个产品深挖
    claude-code.md
    codex.md
    openclaw.md
    omp.md
    hermes.md
  03-comparison.md           # 第三章：横向对比
  04-trends.md               # 第四章：趋势与启示
data/
  sources.md                 # 参考资料与数据来源
```

## 进度

- [x] 提纲 v1
- [ ] 第一章
- [ ] 各产品案例
- [ ] 横向对比
- [ ] 趋势与启示
