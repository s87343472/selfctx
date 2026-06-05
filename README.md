# SelfCtx

> Your personal context, portable across every AI model.

切换模型不再从零开始。把你对 AI 说过的一切——工作方式、项目背景、行为规则——存成一组本地 Markdown 文件，粘贴进任何模型，立刻生效。

**[English ↓](#english)**

---

⭐ 如果这个项目对你有用，请点右上角的 Star——帮助更多人发现它。

---

## 它解决什么问题

| 现状 | SelfCtx |
|------|---------|
| 切换模型要重新「调教」，花 30–50 分钟 | 粘贴一个文件，2 分钟恢复上下文 |
| 上下文散落在各平台，找不齐 | 10 个维度，一个地方存所有 |
| 平台 Memory 不能跨模型迁移 | 纯 Markdown，模型无关，本地掌控 |
| 不知道哪些信息能给模型、哪些不能 | 4 个披露级别，按需选择 |

## 和同类方案的区别

- **vs 平台 Memory**：平台 Memory 是增量细节，SelfCtx 是结构化基线。两者互补，不是替代。
- **vs 手写 System Prompt**：System Prompt 只有偏好设置，SelfCtx 覆盖完整的人的上下文：叙事身份、能力专长、资产图谱、关系网络、项目状态……
- **vs Second Brain（Notion/Obsidian）**：Second Brain 存的是知识，SelfCtx 存的是「我是谁」和「AI 应该怎么对待我」。

---

## 10 个维度

| # | 维度 | 更新频率 |
|---|------|---------|
| D1 | 叙事身份 — 我是谁 | 年级 |
| D2 | **认知操作系统 — 对 AI 的强制要求** | 季度 |
| D3 | 具身状态 — 健康与能量 | 月级 |
| D4 | 情绪与心理（可选） | 月级 |
| D5 | 能力与专长 | 季度 |
| D6 | 资产图谱 — 产品/设备/代码库 | 季度 |
| D7 | 关系网络 | 季度 |
| D8 | 项目快照（3–12 个月窗口） | 月级 |
| D9 | 兴趣与审美 | 年级 |
| D10 | 世界观与志向 | 年级 |

**D2 是核心。** 它存的不是偏好，是规则——粘贴进任何模型立刻强制执行：

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

## 4 个披露级别

| 级别 | Token | 包含 | 用途 |
|------|-------|------|------|
| L0 公开版 | < 500 | 身份标签 + 行为规则 | 随意粘贴，零风险 |
| L1 工作版 | < 2,000 | + 项目 / 能力 / 工作关系 | 日常 AI 协作（推荐起点） |
| L2 信任版 | < 5,000 | 全部维度，敏感信息脱敏 | 长期主力模型 |
| L3 全量版 | 不限 | 原始数据 | 仅本地，永不外发 |

---

## 快速开始

```
1. 复制 prompts/P1_export.md 里的 prompt
2. 粘贴进已有上下文的模型 → 获得草稿
3. 检查 ⚠️ 标记，删除不想保留的内容
4. 填入 templates/pca_template.md
5. 生成 exports/L1_work.md
6. 粘贴进新模型 → 完成迁移
```

首次建立约 15–30 分钟。之后每次迁移约 2 分钟。

---

## 文件结构

```
selfctx/
├── schema.md              # 10 个维度的完整字段定义
├── templates/
│   └── pca_template.md    # 空白模板，从这里开始
├── prompts/
│   ├── P1_export.md       # 从当前模型导出草稿
│   ├── P2_import.md       # 导入新模型
│   ├── P3_import_quick.md # 快速导入（只加载行为规则）
│   ├── P4_update.md       # 更新单个维度
│   ├── P5_review.md       # 季度检视
│   └── P6_level_select.md # 帮你选择披露级别
├── exports/               # 你的导出文件（L0–L3）
├── my_pca/                # 你的原始 PCA 文件（按维度）
└── skill/                 # Claude 专属 Skill（可选）
```

> ⚠️ 把 `exports/L3_full.md` 和 `my_pca/` 里的敏感维度加入 `.gitignore`。

---

## 模型兼容性（2026 年 6 月）

| 模型 | L0 | L1 | L2 |
|------|:--:|:--:|:--:|
| Claude Opus 4.8 / Sonnet 4.6 | ✓ | ✓ | ✓ |
| GPT-5.5 / GPT-5.4 | ✓ | ✓ | ✓ |
| Gemini 3.1 Pro | ✓ | ✓ | ✓ |
| Gemini 3 Flash | ✓ | ✓ | △ |
| Grok 4 / 4.3 | ✓ | ✓ | △ |
| DeepSeek V3.2 | ✓ | ✓ | △ |
| Llama 4 Scout | ✓ | △ | △ |
| Qwen 3.5 | ✓ | ✓ | △ |
| Mistral Large | ✓ | ✓ | △ |

✓ 完全支持 · △ 基本可用，部分字段识别不够精准

---

## Claude 用户

安装 `selfctx.skill` 获得增强：自动触发历史对话搜索、结构化导出、维度内联更新。

下载 `selfctx.skill` → Claude 设置中导入。需要 Claude 3.5+。

---

## 协议

MIT · [Sagasu](https://sagasu.art) · [博客文章](https://sagasu.art)

---

---

<a name="english"></a>

# SelfCtx

> Your personal context, portable across every AI model.

Stop re-introducing yourself every time you switch models. Store everything you've ever told an AI — your work style, projects, behavior rules — as a set of local Markdown files. Paste into any model. Works instantly.

---

⭐ If this is useful, please Star it — it helps others find it.

---

## What problem it solves

| Before | With SelfCtx |
|--------|-------------|
| 30–50 min to re-onboard a new model | Paste one file, context restored in 2 min |
| Context scattered across platforms | 10 dimensions, one place for everything |
| Platform memory can't cross models | Plain Markdown, model-agnostic, locally owned |
| Unsure what's safe to share | 4 disclosure levels, you decide what goes where |

## How it compares

- **vs Platform Memory**: Memory handles recent incremental details. SelfCtx handles the stable structural baseline. Complementary, not competing.
- **vs System Prompts**: System prompts carry preferences. SelfCtx carries the full picture: narrative identity, expertise, asset map, relationships, active projects…
- **vs Second Brain (Notion/Obsidian)**: Second Brain stores knowledge. SelfCtx stores *who you are* and *how AI should treat you*.

---

## 10 Dimensions

| # | Dimension | Update Freq |
|---|-----------|-------------|
| D1 | Narrative Identity — who I am | Yearly |
| D2 | **Cognitive OS — hard rules for AI** | Quarterly |
| D3 | Embodied State — health & energy | Monthly |
| D4 | Emotional & Psychological (optional) | Monthly |
| D5 | Capabilities & Expertise | Quarterly |
| D6 | Asset Map — products / devices / repos | Quarterly |
| D7 | Relationship Network | Quarterly |
| D8 | Project Snapshot (3–12 month window) | Monthly |
| D9 | Interests & Aesthetics | Yearly |
| D10 | Worldview & Aspirations | Yearly |

**D2 is the core.** It stores not preferences but enforced rules — active the moment you paste them into any model:

```yaml
ai_hard_rules:
  forbidden:
    - "No filler: never say 'that's interesting' or 'you might want to consider'"
    - "Never generate docx/pptx unprompted — default to markdown"
  required:
    - "Take a position: state whether something will work and why"
    - "Always offer 2–3 distinct paths with a clear recommendation"
```

---

## 4 Disclosure Levels

| Level | Tokens | Contents | Use Case |
|-------|--------|----------|---------|
| L0 Public | < 500 | Identity tags + behavior rules | Share freely, zero risk |
| L1 Work | < 2,000 | + Projects / expertise / work relationships | Daily AI collaboration (recommended start) |
| L2 Trusted | < 5,000 | All dimensions, sensitive fields redacted | Long-term primary model |
| L3 Full | Unlimited | Raw data | Local only, never share |

---

## Quick Start

```
1. Copy the prompt from prompts/P1_export.md
2. Paste into a model that already knows you → get a draft
3. Review ⚠️ markers, remove anything you don't want
4. Fill in templates/pca_template.md
5. Generate exports/L1_work.md
6. Paste into a new model → done
```

First setup: ~15–30 min. Every migration after: ~2 min.

---

## File Structure

```
selfctx/
├── schema.md              # Full field definitions for all 10 dimensions
├── templates/
│   └── pca_template.md    # Blank template — start here
├── prompts/
│   ├── P1_export.md       # Export draft from current model
│   ├── P2_import.md       # Import into new model
│   ├── P3_import_quick.md # Quick import (behavior rules only)
│   ├── P4_update.md       # Update a single dimension
│   ├── P5_review.md       # Quarterly review
│   └── P6_level_select.md # Help choosing the right level
├── exports/               # Your export files (L0–L3)
├── my_pca/                # Your raw PCA files (one per dimension)
└── skill/                 # Claude-specific Skill (optional)
```

> ⚠️ Add `exports/L3_full.md` and sensitive `my_pca/` files to `.gitignore`.

---

## Model Compatibility (June 2026)

| Model | L0 | L1 | L2 |
|-------|:--:|:--:|:--:|
| Claude Opus 4.8 / Sonnet 4.6 | ✓ | ✓ | ✓ |
| GPT-5.5 / GPT-5.4 | ✓ | ✓ | ✓ |
| Gemini 3.1 Pro | ✓ | ✓ | ✓ |
| Gemini 3 Flash | ✓ | ✓ | △ |
| Grok 4 / 4.3 | ✓ | ✓ | △ |
| DeepSeek V3.2 | ✓ | ✓ | △ |
| Llama 4 Scout | ✓ | △ | △ |
| Qwen 3.5 | ✓ | ✓ | △ |
| Mistral Large | ✓ | ✓ | △ |

✓ Full support · △ Works, some fields less accurately parsed

---

## Claude Users

Install `selfctx.skill` for enhanced features: automatic conversation history search, structured export, inline dimension updates.

Download `selfctx.skill` → import in Claude settings. Requires Claude 3.5+.

---

## License

MIT · [Sagasu](https://sagasu.art) · [Blog post](https://sagasu.art)
