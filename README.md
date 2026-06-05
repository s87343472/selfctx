# SelfCtx · 个人上下文资产体系

**让你在任意 AI 模型里都能被"认识"。**

模型无关 · 本地存储 · 分级披露 · 15 分钟上手

**[English version below ↓](#selfctx--personal-context-asset-system)**

---

> 如果这个项目对你有用，请点一下右上角的 ⭐ Star——它帮助更多人发现这个工具。

---

## 为什么需要这个

每次切换 AI 模型（Claude → GPT → Gemini → Grok），或者开启新对话，所有上下文归零。你要重新解释自己是谁、在做什么、有什么偏好——平均花 30–50 分钟，还找不齐信息。

问题不是迁移麻烦，是**信息没有固定的家**。

你对 AI 说过的所有上下文，本质上是你的资产：工作方式、项目背景、对 AI 的行为要求。这些东西应该属于你，存在本地，而不是锁在某个平台的数据库里。

SelfCtx 把这些信息叫做 **Personal Context Asset（PCA，个人上下文资产）**。

---

## 核心思路

一组本地 Markdown 文件，覆盖一个人在 AI 语境下的完整上下文。不是简历，不是自我介绍，而是**让任意 AI 模型快速进入工作状态所需要的全部信息**。

设计成 10 个正交维度，每个维度有独立的更新频率和敏感级别：

| # | 维度 | 核心问题 | 更新频率 | 必填 |
|---|------|---------|---------|:----:|
| D1 | 叙事身份 | 我是谁，怎么走到现在 | 年级 | ✓ |
| D2 | 认知操作系统 | 我怎么思考，对 AI 有什么强制要求 | 季度 | ✓ |
| D3 | 具身状态 | 我的身体和健康 | 月级 | ✓ |
| D4 | 情绪与心理 | 我的心理状态 | 月级 | 可选 |
| D5 | 能力与专长 | 我能做什么，用什么工具 | 季度 | ✓ |
| D6 | 资产图谱 | 我拥有什么（产品、设备、代码库） | 季度 | ✓ |
| D7 | 关系网络 | 我和谁有关系 | 季度 | ✓ |
| D8 | 项目快照 | 我在做什么（3–12 个月窗口） | 月级 | ✓ |
| D9 | 兴趣与审美 | 我喜欢什么，反感什么 | 年级 | ✓ |
| D10 | 世界观与志向 | 我相信什么，想去哪里 | 年级 | ✓ |

---

## 分级披露

不是所有信息都适合给所有模型看。4 个级别，按需选择：

| 级别 | 文件 | Token 预算 | 包含内容 | 适用场景 |
|------|------|-----------|---------|---------|
| L0 公开版 | `exports/L0_public.md` | < 500 | D1标签 + D2规则 + D9片段 | 任意模型，随意粘贴 |
| L1 工作版 | `exports/L1_work.md` | < 2,000 | D1+D2+D5+D7工作+D8+D9 | 日常 AI 工作协作（推荐起点） |
| L2 信任版 | `exports/L2_trusted.md` | < 5,000 | 全部维度，D3/D4/D6 脱敏 | 长期主力模型 |
| L3 全量版 | `exports/L3_full.md` | 不限 | 全部维度，原始数据 | 仅本地，**永不外发** |

**L2 脱敏规则：**
- D3 去除具体病名，保留「影响工作的限制」
- D4 去除具体情绪内容，保留「AI 互动偏好」
- D6 去除具体金额，保留收入来源类型
- D7 社交 / 家庭关系不含在 L2，只含工作关系

---

## 文件结构

```
selfctx/
├── README.md                    # 本文件
├── schema.md                    # 10 个维度的完整字段定义（含 YAML 示例）
│
├── templates/
│   └── pca_template.md          # 空白填写模板，从这里开始
│
├── prompts/
│   ├── P1_export.md             # 从当前模型导出草稿
│   ├── P2_import.md             # 全量导入新模型
│   ├── P3_import_quick.md       # 快速导入（只加载行为规则）
│   ├── P4_update.md             # 更新单个维度
│   ├── P5_review.md             # 季度检视
│   └── P6_level_select.md       # 帮你选择导出级别
│
├── exports/                     # 你生成的导出文件放这里
│   ├── L0_public.md             # [你来填]
│   ├── L1_work.md               # [你来填]
│   ├── L2_trusted.md            # [你来填]
│   └── L3_full.md               # [你来填，永不推送到远端]
│
├── my_pca/                      # 你的原始 PCA 文件（按维度分文件维护）
│   ├── d1_narrative.md
│   ├── d2_cognitive_os.md
│   ├── d3_embodied.md
│   ├── d4_emotional.md          # 可选
│   ├── d5_capabilities.md
│   ├── d6_assets.md
│   ├── d7_relationships.md
│   ├── d8_projects.md
│   ├── d9_interests.md
│   └── d10_worldview.md
│
└── skill/                       # Claude 专属 Skill（可选增强）
    ├── SKILL.md
    ├── references/
    └── templates/
```

> ⚠️ 建议把 `exports/L3_full.md` 和 `my_pca/` 里的敏感维度加入 `.gitignore`，避免推送到远端。参考仓库内的 `.gitignore` 模板。

---

## 快速开始

### 第一步：导出草稿（约 10 分钟）

把 `prompts/P1_export.md` 里的 prompt 粘贴进**已经积累了上下文的模型**，让它帮你生成初版草稿。模型会按 10 个维度输出内容，L2+ 敏感内容自动加 ⚠️ 标记。

### 第二步：审查草稿（约 5 分钟）

检查 ⚠️ 标记，删除不想保留的内容。重点关注 D7 关系网络（是否保留真实姓名）和 D6 资产图谱（财务信息只留 L3）。

### 第三步：填入模板

把审查后的内容填进 `templates/pca_template.md`，空白处标 `[待填写]`，保存为 `my_pca/` 下的各维度文件。

### 第四步：生成导出文件

从 `my_pca/` 的对应文件提取内容，分别生成 L0–L3 文件，放入 `exports/`。或者用 `prompts/P6_level_select.md` 让模型帮你判断分级。

### 第五步：导入新模型（约 2 分钟）

打开 `exports/L1_work.md`，复制全文，把 `prompts/P2_import.md` 的导入 prompt + L1 内容一起粘贴进新模型第一条消息。验证：3 轮内模型能否正确执行 D2 的 `ai_hard_rules`。

---

## 日常维护

| 频率 | 操作 |
|------|------|
| 每月 | 检查 D3（健康）和 D8（项目快照）是否需要更新 |
| 每季度 | 运行 `prompts/P5_review.md` 扫描全部维度 |
| 有重大变化时 | 随时用 `prompts/P4_update.md` 更新对应维度 |

D8 项目快照时间窗口默认 3 个月，可延长至 12 个月。窗口到期时内容降级为 `completed_recently`，不删除。

---

## 最重要的维度：D2 认知操作系统

如果只能维护一个维度，选 D2。这里存的是你对 AI 的**强制约束**，粘贴进任何模型立刻生效：

```yaml
ai_hard_rules:
  forbidden:
    - "不说套话：禁止'很有意思''可能值得考虑'"
    - "不主动生成 docx/pptx，默认 markdown"
  required:
    - "必须表态：这能不能成立，依据是什么"
    - "方案给出 2-3 个路径并明确推荐"
```

---

## 与平台 Memory 的关系

不是替代，是互补。平台 Memory 负责增量细节，PCA 负责结构化基线。两者叠加，覆盖面最完整。

---

## 模型兼容性（2026 年 6 月）

PCA 文件（L1/L2）已在以下模型验证可用：

| 模型 | L0 | L1 | L2 | 备注 |
|------|:--:|:--:|:--:|------|
| Claude Opus 4.8 | ✓ | ✓ | ✓ | 推荐，上下文理解最佳 |
| Claude Sonnet 4.6 | ✓ | ✓ | ✓ | 日常使用性价比最高 |
| GPT-5.5 / GPT-5.5 Pro | ✓ | ✓ | ✓ | 创意写作和结构化任务强 |
| GPT-5.4 | ✓ | ✓ | ✓ | |
| Gemini 3.1 Pro | ✓ | ✓ | ✓ | 长文档和多模态场景强 |
| Gemini 3 Flash | ✓ | ✓ | △ | 速度快，L2 部分字段识别略弱 |
| Grok 4 / Grok 4.3 | ✓ | ✓ | △ | hard_rules 执行稳定性略低 |
| DeepSeek V3.2 | ✓ | ✓ | △ | 开源替代，性价比极高 |
| Llama 4 Scout | ✓ | △ | △ | 本地部署可用，L1 复杂字段有时识别不全 |
| Qwen 3.5 | ✓ | ✓ | △ | 中文上下文理解好 |
| Mistral Large | ✓ | ✓ | △ | 欧洲隐私合规场景适用 |

✓ = 完全支持 · △ = 基本可用，部分字段识别不够精准

---

## Claude 用户专属

安装 `selfctx.skill` 获得增强体验：自动触发历史对话搜索、结构化导出、维度更新内联支持、季度检视自动化。

**安装方式：** 下载 `selfctx.skill` → 在 Claude 设置中导入。需要 Claude 3.5 或以上版本。

---

## 隐私建议

1. `exports/L3_full.md` **永不推送到任何远端，包括私有 repo**
2. L1 可以安全发给 Claude / GPT / Gemini 等商业 AI 服务
3. 关系网络中的真实姓名建议只保留在 L3

---

## 协议

MIT · 自由使用、修改、分发

---

*由 [Sagasu](https://sagasu.art) 设计和维护 · 欢迎提 Issue 和 PR*

---
---

# SelfCtx · Personal Context Asset System

**So any AI model can truly know you — from day one.**

Model-agnostic · Local storage · Tiered disclosure · Ready in 15 minutes

---

> If this project is useful to you, please give it a ⭐ Star in the top right — it helps others discover it.

---

## Why this exists

Every time you switch AI models (Claude → GPT → Gemini → Grok) or start a new conversation, all context resets. You spend 30–50 minutes re-explaining who you are, what you're working on, and how you like to work — and you can never find all the pieces.

The problem isn't migration. It's that **your context has no permanent home**.

Everything you've told AI models — your work style, your projects, your rules for AI behavior — is your asset. It should live locally, belong to you, and not be locked inside any platform's database.

SelfCtx calls this a **Personal Context Asset (PCA)**.

---

## How it works

A set of local Markdown files covering everything an AI needs to work effectively with you. Not a resume. Not a bio. The complete, structured context that lets any AI model hit the ground running.

Organized into 10 orthogonal dimensions, each with its own update frequency and sensitivity level:

| # | Dimension | Core Question | Update Freq | Required |
|---|-----------|--------------|-------------|:--------:|
| D1 | Narrative Identity | Who am I, how did I get here | Yearly | ✓ |
| D2 | Cognitive OS | How I think, what AI must/must not do | Quarterly | ✓ |
| D3 | Embodied State | My body and health | Monthly | ✓ |
| D4 | Emotional & Psychological | My mental state | Monthly | Optional |
| D5 | Capabilities & Expertise | What I can do, what tools I use | Quarterly | ✓ |
| D6 | Asset Map | What I own (products, devices, repos) | Quarterly | ✓ |
| D7 | Relationship Network | Who I work with | Quarterly | ✓ |
| D8 | Project Snapshot | What I'm working on (3–12 month window) | Monthly | ✓ |
| D9 | Interests & Aesthetics | What I like, what I hate | Yearly | ✓ |
| D10 | Worldview & Aspirations | What I believe, where I'm going | Yearly | ✓ |

---

## Disclosure Levels

Not everything belongs in every conversation. Four levels, choose what fits:

| Level | File | Token Budget | Contents | Use Case |
|-------|------|-------------|---------|---------|
| L0 Public | `exports/L0_public.md` | < 500 | D1 tags + D2 rules + D9 snippets | Any model, share freely |
| L1 Work | `exports/L1_work.md` | < 2,000 | D1+D2+D5+D7(work)+D8+D9 | Daily AI collaboration (recommended start) |
| L2 Trusted | `exports/L2_trusted.md` | < 5,000 | All dimensions, D3/D4/D6 redacted | Long-term primary model |
| L3 Full | `exports/L3_full.md` | Unlimited | All dimensions, raw data | Local only, **never share** |

**L2 Redaction rules:**
- D3: Remove specific conditions, keep "constraints that affect work"
- D4: Remove specific emotional content, keep "AI interaction preferences"
- D6: Remove specific amounts, keep income source types
- D7: No social/family relationships in L2, work only

---

## File Structure

```
selfctx/
├── README.md
├── schema.md                    # Full field definitions for all 10 dimensions
│
├── templates/
│   └── pca_template.md          # Blank template — start here
│
├── prompts/
│   ├── P1_export.md             # Export draft from your current model
│   ├── P2_import.md             # Full import into a new model
│   ├── P3_import_quick.md       # Quick import (behavior rules only)
│   ├── P4_update.md             # Update a single dimension
│   ├── P5_review.md             # Quarterly review
│   └── P6_level_select.md       # Help choosing the right export level
│
├── exports/                     # Your generated export files go here
│   ├── L0_public.md             # [fill this in]
│   ├── L1_work.md               # [fill this in]
│   ├── L2_trusted.md            # [fill this in]
│   └── L3_full.md               # [fill this in — never push to remote]
│
├── my_pca/                      # Your raw PCA files, one per dimension
│   ├── d1_narrative.md
│   ├── d2_cognitive_os.md
│   └── ...
│
└── skill/                       # Claude-specific Skill (optional)
```

> ⚠️ Add `exports/L3_full.md` and sensitive `my_pca/` files to `.gitignore`. See the included template.

---

## Quick Start

**Step 1 — Export a draft (≈10 min)**
Paste the prompt from `prompts/P1_export.md` into a model that already knows you well. It generates a structured draft across all 10 dimensions, with ⚠️ markers on sensitive content.

**Step 2 — Review the draft (≈5 min)**
Check every ⚠️ marker. Delete anything you don't want to keep — especially real names in D7 and financial details in D6.

**Step 3 — Fill the template**
Copy the reviewed content into `templates/pca_template.md`. Mark unknowns as `[to fill]`. Save as individual files in `my_pca/`.

**Step 4 — Generate export files**
Extract content by level from `my_pca/` into L0–L3 files in `exports/`. Use `prompts/P6_level_select.md` if you're unsure what goes where.

**Step 5 — Import into a new model (≈2 min)**
Copy `exports/L1_work.md`. Paste `prompts/P2_import.md` + your L1 content as the first message in the new conversation. Verify: can the model correctly follow your `ai_hard_rules` within 3 turns?

---

## Maintenance Rhythm

| Frequency | Action |
|-----------|--------|
| Monthly | Check D3 (health) and D8 (project snapshot) |
| Quarterly | Run `prompts/P5_review.md` across all dimensions |
| After major changes | Use `prompts/P4_update.md` for the relevant dimension |

D8 snapshot window defaults to 3 months, extendable to 12. On expiry, content moves to `completed_recently` rather than being deleted.

---

## The Most Important Dimension: D2 Cognitive OS

If you only maintain one dimension, make it D2. This is where you store **hard rules for AI behavior** — not preferences, but requirements that take effect immediately when pasted into any model:

```yaml
ai_hard_rules:
  forbidden:
    - "No filler phrases: never say 'that's interesting' or 'you might want to consider'"
    - "Never generate docx/pptx unprompted — default to markdown"
  required:
    - "Take a position: state whether something will work and why"
    - "Always offer 2–3 distinct paths with a clear recommendation"
```

---

## Relationship with Platform Memory

Complementary, not competing. Platform memory (e.g. Claude's memory feature) handles recent incremental details. PCA handles the stable structural baseline. Used together, they give the most complete coverage.

---

## Model Compatibility (June 2026)

PCA files (L1/L2) tested and working with:

| Model | L0 | L1 | L2 | Notes |
|-------|:--:|:--:|:--:|-------|
| Claude Opus 4.8 | ✓ | ✓ | ✓ | Best context understanding overall |
| Claude Sonnet 4.6 | ✓ | ✓ | ✓ | Best daily-use value |
| GPT-5.5 / GPT-5.5 Pro | ✓ | ✓ | ✓ | Strong on creative writing & structured tasks |
| GPT-5.4 | ✓ | ✓ | ✓ | |
| Gemini 3.1 Pro | ✓ | ✓ | ✓ | Best for long documents and multimodal |
| Gemini 3 Flash | ✓ | ✓ | △ | Fast; some L2 fields less reliably parsed |
| Grok 4 / Grok 4.3 | ✓ | ✓ | △ | hard_rules execution slightly less consistent |
| DeepSeek V3.2 | ✓ | ✓ | △ | Best open-source value |
| Llama 4 Scout | ✓ | △ | △ | Good for local deployment |
| Qwen 3.5 | ✓ | ✓ | △ | Strong Chinese-language context handling |
| Mistral Large | ✓ | ✓ | △ | Good for EU privacy-compliant deployments |

✓ = Full support · △ = Works, some fields less accurately parsed

---

## Claude Users

Install `selfctx.skill` for enhanced features: automatic conversation history search, structured export without manual prompting, inline dimension updates, and automated quarterly review.

**Install:** Download `selfctx.skill` → import in Claude settings. Requires Claude 3.5+.

---

## Privacy

1. Never push `exports/L3_full.md` anywhere — not even a private repo
2. L1 is safe to send to commercial AI services (Claude, GPT, Gemini, etc.)
3. Real names in D7 relationships: keep them in L3 only

---

## License

MIT · Use, modify, distribute freely

---

*Designed and maintained by [Sagasu](https://sagasu.art) · Issues and PRs welcome*
