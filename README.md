# deep-fable-5

One `SKILL.md`. It gives any AI model the Fable-5 way of working: how it thinks before acting, how it talks, how it writes code, how it designs interfaces.

Not a model. Not a plugin. A single markdown file you drop into a skills folder.

---

## Why

Every AI session starts the same story. The model reads your rules, follows them for 2 turns, then quietly forgets. It reasons straight down the literal words of your prompt instead of asking what you actually need. It answers in jargon nobody asked for. Every frontend it touches comes out looking identical: cards stacked on cards, glassmorphism everywhere, a purple-blue gradient hero, three equal feature columns.

This file fights back with forced rituals, not polite suggestions.

## What it enforces

**Thinking**
- A mandatory 5-step reframing protocol. The default "follow the message literally" path is disabled. Step 2 forces the angle switch: from "what does the user want" to "what is actually blocking them".
- Thinking must be shown. Big tasks open with 4 fixed lines (goal / real problem / route / edge cases). Small tasks compress to one line. Silent conclusions are banned.
- An anti-forgetting mechanism: anchor the rules on first task, run a 4-question gate before every reply, re-read the skill file on drift, pin long tasks to a checklist.

**Talking**
- Plain language only. The bar: could your mom follow this? Jargon gets a one-line explanation on first use. Hard things get an analogy first. Paper-tone phrases ("in summary", "it is worth noting") are deleted on sight.

**Coding**
- Read the site before touching anything. Minimal diffs. Standard library first. No verification, no "done".
- A decoration ban: comment spam, speculative abstractions, gradients, glow, pill corners, emoji icons, dead debug code. If deleting it loses nothing, it goes.

**Designing**
- Layout needs a skeleton: grid or fixed columns, elements snap to it. Spacing only from a 4px scale. Sections separated by whitespace, dividers and type weight — not by wrapping everything in cards.
- Exactly 3 themes: light, dark, system-follow. Colors live in semantic tokens via CSS variables. Hardcoded hex values are incidents. "User said blue" means change one token, not invent a blue palette.
- No pretending design has one right answer. Ask for references once; if none exist, fall back to proven conservative layouts.
- Plus 14 opinionated defaults: tables over cards for dense data, modals only for irreversible actions, #121212 dark backgrounds, accent color reserved for action points.

**Knowing**
- Training data is stale by default. Versions, APIs and dates come from tools, or the reply says plainly "not verified". Hedge phrases are banned.

## Install

Global (all sessions):

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.agents\skills\deep-fable-5" | Out-Null
Copy-Item "SKILL.md" "$HOME\.agents\skills\deep-fable-5\SKILL.md"
```

Project-only:

```text
.opencode/skills/deep-fable-5/SKILL.md
```

Restart opencode after installing. Skills load at startup, not mid-session.

For real persistence, also add the file path to your global AGENTS.md or `instructions` config. The rituals fight forgetting; wiring it into instructions removes the fight.

## Usage

Say "fable style", or just start working in a session where the skill is loaded — its description carries trigger keywords. To tune behavior, edit the file. The custom zone at the bottom overrides any rule above it.

> **IMPORTANT** This skill replicates working habits, not benchmark scores. It will not raise a weak model's reasoning ceiling. Nothing in a text file can.

---

# deep-fable-5（中文版）

一个 `SKILL.md`，让任何 AI 模型都拿出 Fable-5 式的工作表现：怎么想、怎么说、怎么写代码、怎么做界面。

不是模型，不是插件，就是一个 markdown 文件，丢进技能目录就能用。

## 为什么有它

每个会话都在重演同一出戏。模型读完你的规矩，规矩地干 2 轮，然后悄悄忘光。它顺着消息字面往下推理，不想你到底卡在哪；张嘴就是黑话；碰上前端就掏出那套老三样——卡片摞卡片、毛玻璃糊一脸、紫蓝渐变 hero 加三列特性区。

这个文件用强制仪式反击，不靠客气建议。

## 它管什么

**想**
- 强制 5 步推理协议，禁用"顺字面直推"的默认路径。第 2 步强制换角度：从"他要什么东西"切到"他被什么挡住了"。
- 心想必须吐出来。大任务开头固定 4 行（目标/真实问题/路线/边界），小任务压一行，闷头甩结论是违规的。
- 防忘机制：首次干活先锚定总纲，每次回复前过 4 问门，跑偏就回头重读原文，长任务清单钉桩。

**说**
- 纯大白话，标准就一条：你妈能听懂。术语第一次出现跟人话解释，难事先打比方，论文腔见一句删一句。

**写代码**
- 先读现场再动手，改动最小化，标准库优先，没跑验证不许说完成。
- 装饰禁令：注释泛滥、投机抽象、渐变发光、药丸圆角、emoji 图标、调试残留——删掉不损失功能可读性的东西，全部该删。

**做设计**
- 布局必须有骨架，元素挂网格，间距只从 4 的倍数里取。分区靠留白和字重，不靠给万物套卡片。
- 只做浅色、深色、跟随系统 3 套主题，颜色全走语义 token，写死色值按事故处理。
- 设计没有标准答案，所以不许装懂：先问参照物，问不到就走保守成熟布局。
- 外加 14 条口味默认值：密数据用表格、弹窗只管不可逆操作、深色底用 #121212、强调色只上行动点。

**知识面**
- 默认训练数据过期。版本、API、日期以工具查证为准，查不到就明说没验证，对冲话术禁止。

## 安装

全局（所有会话生效）：

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.agents\skills\deep-fable-5" | Out-Null
Copy-Item "SKILL.md" "$HOME\.agents\skills\deep-fable-5\SKILL.md"
```

仅当前项目：

```text
.opencode/skills/deep-fable-5/SKILL.md
```

装完重启 opencode。技能在启动时加载，会话中途不刷新。

要真焊死防遗忘，把文件路径再挂进全局 AGENTS.md 或 instructions 配置。仪式是对抗遗忘的上限，挂进配置才是取消对抗。

## 用法

说一句"fable 风格"，或者在装好技能的会话里直接开工——描述里埋了触发词。想调行为就改文件，最底下的自定义区优先于前文所有条目。

> **IMPORTANT** 本技能复刻的是工作习惯，不是基准分。它提不了弱模型的推理上限——文本文件做不到这件事，谁跟你说能做到都是在吹。
