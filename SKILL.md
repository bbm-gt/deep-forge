---
name: deep-forge
description: 深度学习对标账号写作方法论，用策略驱动写作，不模仿词汇
---

# Deep-Forge

学习对标账号的写作方法论——不是记词汇，是理解"作者为什么在这里做这个动作"。然后用策略地图写新文章，每篇不同但风格一致。

## 核心原则

> **学写作灵魂，不抄写作皮肤。** 皮肤 = 词汇。灵魂 = "为什么这样做？想对读者产生什么效果？"

不做词汇频率统计。只问一个问题：**作者在这里做了什么，为什么有效？**

## 三个模式

| 模式 | 何时用 | 怎么执行 | 详细流程 |
|------|--------|---------|---------|
| 学习 | 用户提供对标文章 | **子 Agent** | `{baseDir}/references/learning-workflow.md` |
| 写作 | 用户给主题+知识库 | 主会话 | `{baseDir}/references/writing-workflow.md` |
| 精炼 | 所有文章学完后 | **子 Agent** | `{baseDir}/references/refining-workflow.md` |

学习/精炼用子 Agent 的原因：需要跨批次累积状态（计数器、去重、升级），子 Agent 的长会话完整保留这些状态，结束一次性写入 workspace。

## 路径约定

本文档中 `{workspace}` = OpenClaw agent 的工作目录（通常为 `~/.openclaw/workspace`）。Agent 运行时 OpenClaw 自动注入。

```
只读 Skill 目录:
  {baseDir}/SKILL.md + {baseDir}/references/*.md

Agent 可读写数据:
  {workspace}/deep-forge/
  ├── strategy-memory.md       # 策略库 + 计数器 + 匹配表
  ├── refined-strategies.md    # 精炼后策略（写作时优先读取）
  └── recent-outputs.md        # 最近输出记录（保持最近 10 条）

初始化模板:
  {baseDir}/references/strategy-memory-template.md
  子 Agent 首次执行时，如 {workspace}/deep-forge/strategy-memory.md 不存在，
  复制此模板创建。之后子 Agent 在副本上增量更新。

## 策略分层

| 层 | 含义 | 选择规则 |
|----|------|---------|
| 🔴 核心 | 定义对标作者写作灵魂 | 每篇必选 2-3 条 |
| 🟡 模式 | 按文章类型匹配 | 根据类型选 2-3 条 |
| 🟢 情境 | 特定技巧，首次发现默认层级 | 按需 0-1 条 |

每篇 4-7 条，不超过 7 条。升级降级规则见 `{baseDir}/references/strategy-format.md`。

## 写作前自检

1. 这篇文章的类型是什么？（从策略库的类型匹配表选策略）
2. 话题可能触发什么默认语感？（赚钱≠营销号语气。策略库定义语感，不由话题或知识库定义）
3. 与上篇策略重叠 > 60%？（读 recent-outputs.md）

## 写完后自检

逐条检查：同一口语词 > 3 次？AI 标志词？连续 3 段同长度？每个策略真被执行了？触发常见错误？反模式？语感被话题绑架？收尾在总结全文？数字具体？知识库信息被篡改？与上篇策略重叠 > 60%？

## 关键约束

- 策略库 < 3 条时拒绝写作
- 知识库是信息来源，不是语感来源。只取信息，不取语气
- 数据文件只写 workspace，不写 Skill 目录
