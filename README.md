# Deep-Forge

深度学习对标账号的写作方法论，用策略驱动写作，不模仿词汇。

## 它解决什么问题

你给 Agent 喂了几百篇对标文章学习风格，但 Agent 只学到了高频词汇（"说白了""讲真""离谱"），然后每篇文章机械地塞这些词——读起来像 AI 在背诵关键词录。

Deep-Forge 换一种方式：学写作灵魂，不抄写作皮肤。皮肤 = 词汇。灵魂 = "作者为什么在这里做这个动作？"

## 怎么用

### 1. 学习对标文章

```
# 在 OpenClaw 中说：
学习这批文章，路径在 /home/ubuntu/.openclaw/workspace/gefei/txt
```

Agent 启动子 Agent，逐篇分析，提取可迁移的写作策略，自动分层（情境→模式→核心），写入 workspace 的策略库。

一次可喂任意数量（1 篇、50 篇、700 篇）。前 50 篇大量新策略，50-100 篇少量补充，100 篇后几乎全是验证。

### 2. 写作

```
写一篇关于[主题]的文章
这是知识库：[资料]
```

Agent 从策略库中按文章类型匹配策略，策略驱动写作（不是词汇驱动），自检后输出。

### 3. 精炼

```
精炼策略库
```

所有文章学完后运行。过滤不可复制项 → 合并重叠 → 输出精炼版。精炼版是日常写作的策略源。

## 适用场景

- 公众号/知乎/自媒体写作
- 有对标账号需要学习其风格
- 希望 AI 每篇不同但风格一致
- 信息搬运+解读型内容

## 不适用场景

- 没有对标文章可学（至少需要 3-5 篇）
- 纯文学创作
- 需要 100% 原创观点（本 skill 做风格迁移，不做观点生成）

## 安装

将 `deep-forge/` 目录复制到 OpenClaw 的 skills 目录。

Workspace 数据文件会自动创建在 `{workspace}/deep-forge/` 下。

## 文件结构

```
deep-forge/                        # Skill 目录（只读）
├── SKILL.md
├── README.md
└── references/
    ├── strategy-memory-template.md
    ├── strategy-format.md
    ├── learning-workflow.md
    ├── writing-workflow.md
    └── refining-workflow.md

{workspace}/deep-forge/            # 数据目录（Agent 可读写）
├── strategy-memory.md
├── refined-strategies.md
└── recent-outputs.md
```

## License

MIT
