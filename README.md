# 🔁 别调 Prompt 了，去写 Loop

> Loop Engineering 实战。中英双语。
>
> 讲清楚一件事：**Prompt 已死，Loop 必将取代。**

<div align="center">

<img src="https://img.shields.io/badge/版本-中英双语-blueviolet" alt="Bilingual">
<img src="https://img.shields.io/badge/字数-6.5万-blue" alt="Words">
<img src="https://img.shields.io/badge/审稿-已修复10处-brightgreen" alt="Reviewed">
<img src="https://img.shields.io/badge/MindApex-VokoForge-blueviolet" alt="MindApex">
<img src="https://img.shields.io/github/stars/VokoForge/loop-engineering?style=social" alt="Stars">

</div>

---

## 这本书讲什么

**核心论点**（吸收 Addy Osmani / Karpathy / Peter Steinberger）：

1. **76% 的 Agent 性能提升与模型无关** -- Karpathy autoresearch 700 次实验证明，性能瓶颈在 Loop 设计，不在模型
2. **Loop 的核心不是循环，是知道什么时候停** -- 没有停止条件的 loop 是 `while(true)`，必然退化成 loopmaxxing
3. **Agent Loop ≠ Loop Engineering** -- 前者是"模型怎么转"，后者是"你怎么造让模型一直转、转对方向、知道什么时候停的系统"

### Prompt → Context → Harness → Loop 四代演进

```
Prompt Engineering（2022-2024）-> 优化你写给模型的话
Context Engineering（2025）    -> 优化模型能看到的所有信息
Harness Engineering（2026 上）  -> 优化 Agent 运行的整体环境
Loop Engineering（2026-06 起） -> 优化驱动 Agent 持续工作的迭代循环
```

Loop Engineering 是 AI 工程方法论的第四代演进。这本书就是讲它。

---

## 📖 章节结构

### 🇨🇳 中文版

[完整中文版](content/01-中文版.md)（约 4 万字）

含序、五大部分、附录：
- 第一部分：为什么 Loop 比 Prompt 重要
- 第二部分：Loop 的五个工程问题
- 第三部分：7 步搭建法
- 第四部分：实战与翻车
- 第五部分：未来
- 附录：工具清单、术语表

### 🇬🇧 English Version

[English Version](content/02-English-Version.md) (~24k words)

Contains Preface, Part I-V, Appendices.

---

## 💡 核心金句

> "你不应该再手动写 Prompt 给 Agent 了，你应该设计能自动驱动 Agent 的 Loop。" -- Peter Steinberger

> "我不再手动 Prompt Claude 了。我有 Loops 在运行，是它们在驱动 Claude、决定下一步做什么。我的工作是写 Loops。" -- Boris Cherny

> "Loop Engineering 关心的重点不在 Agent 跑了几轮，重点在每一轮有没有目标、证据、边界和停止条件。" -- Addy Osmani

> "AI 编程 Agent 性能提升中 76% 与模型本身无关。" -- Karpathy autoresearch

---

## 🎯 适合谁读

- 🧑‍💻 **工程师**：从手动 Prompt 跃迁到设计 Loop
- 🏗️ **AI 基础设施工程师**：系统要支持 Loop 元语（可调度、可终止、有预算、有状态）
- 👔 **团队技术负责人**：团队生产力天花板已经是"Loop 设计得多可靠"
- 🎓 **学生**：理解 2026 年最火的 AI 工程概念

---

## 🚀 怎么用这本书

### 30 分钟快速入门
1. 读 [中文版](content/01-中文版.md) 第一部分（建立 Loop Engineering 认知）
2. 读第三部分 7 步法（搭建最小 loop）
3. 照着 30 分钟跑通清单实践

### 1 天深入
读完整中文版，对照姊妹专栏《给AI当老板》第 17 章（多 Agent 协作协议栈）

### 1 周实战
- Day 1-2：中文版通读
- Day 3-4：英文版对照读（术语国际化）
- Day 5-7：照 7 步法搭一个自己的 loop

---

## 🔧 配套工具

读完想真跑起来？用 [**知途**](https://app.madapexai.com)（app.madapexai.com）。

知途是 MindApex 出品的 AI 决策产品，把 Loop Engineering 的方法论做成了产品--扔一个诉求，它自己拆解、求解、验证、调优、进化。读完书，用产品，你会更懂"扔诉求 -> 拿验证过的结果"是什么感觉。

> 📖 **这本书是方法论，知途是产品形态。** 两者一脉相承。

想要代码级 Loop 框架？看姊妹项目 [rexloop](https://github.com/VokoForge/rexloop) -- M-LOOP 框架，1 个 Rex 中枢 + 4 条反馈闭环 + 7 个质量门禁。

---

## 📝 审稿说明

每章末尾有 `<!-- 审稿记录 -->` 注释块。共修复 **10 处**问题（主要是标题层级跳级检测，保留原结构未自动修改）。原文未改写，仅限格式修复。

发现新问题？欢迎提 Issue。

---

## 📚 姊妹专栏

| 专栏 | 链接 |
|------|------|
| 🤖 给AI当老板：Agent 作战团队 | [managing-ai-agents](https://github.com/VokoForge/managing-ai-agents) |
| 🚗 智驾时代：Agent 进化简史 | [agent-evolution-history](https://github.com/VokoForge/agent-evolution-history) |
| ⚒️ VokoForge 主页 | [VokoForge](https://github.com/VokoForge) |
| 🔄 rexloop 框架 | [rexloop](https://github.com/VokoForge/rexloop) |

---

## 📄 License

MIT - 自由使用、转载请注明出处

<div align="center">

**⭐ 如果这本书帮到了你，给个 Star 是对我们最大的鼓励。**

*Forged by MindApex · 2026*

</div>
