# prompts.md · SelfCtx Prompt工具集

---

## P1 · 导出Prompt（从当前模型提取PCA草稿）

粘贴进已积累上下文的模型，触发结构化导出。

```
请把你对我的所有了解整理成PCA（个人上下文资产）格式。

要求：
- 先触发深度记忆搜索（检索历史对话 + 当前记忆）
- 按以下10个维度组织，只写你确实知道的，空白处标注[待填写]
- L2级及以上内容加⚠️标记
- 输出两层：人类可读层（供审查）+ 模型读取层（供导入）

---
# PCA Draft · [今天日期]

## 人类可读层

### D1 叙事身份
tagline: 
origin_story: 
public_roles: 

### D2 认知操作系统
thinking_style: 
communication_style: 
ai_hard_rules:
  forbidden:
    - 
  required:
    - 
output_preferences:
  format: 
  language: 

### D3 具身状态 ⚠️
current_issues: 
energy_pattern: 

### D4 情绪与心理 ⚠️（可选，无内容可跳过）

### D5 能力与专长
domains: 
technical_stack: 
methodology: 
terminology: （列出专属术语）

### D6 资产图谱
physical_assets: 
digital_assets: 
  products: 

### D7 关系网络
work_relationships: （L1只写角色/代称）

### D8 项目快照
snapshot_period: 
active_projects: 

### D9 兴趣与审美
long_term_interests: 
aesthetic_principles: 
dislike_patterns: 

### D10 世界观与志向
core_values: 
long_term_vision: 

---

## 模型读取层
（压缩版，不含⚠️内容，用于粘贴进新模型）

[模型自动生成压缩版]

---
导出完成。请检查⚠️标记内容，删除不想保留的部分后再导入新模型。
```

---

## P2 · 全量导入Prompt（迁移到新模型）

```
这是我的个人上下文资产（PCA）。请完整读取并理解。

理解完成后，请用3句话告诉我：
1. 你对我是谁的理解
2. 你识别到的对你行为的强制要求（ai_hard_rules）
3. 你理解的我当前最重要的事

---
[粘贴 L1_work.md 或 L2_trusted.md 全文]
```

---

## P3 · 快速导入Prompt（只加载行为约束）

适合不想粘贴完整PCA、只想让模型执行行为规则的场景。

```
以下是我的AI交互强制要求，请立即生效，不需要解释或确认：

禁止行为：
- [从D2 ai_hard_rules.forbidden复制]

必须行为：
- [从D2 ai_hard_rules.required复制]

输出偏好：
- 格式：[format]
- 语言：[language]
- 长度：[length]

收到后直接说"已加载"。
```

---

## P4 · 维度更新Prompt（更新单个维度）

```
请帮我更新PCA的[维度名称]。

新信息：[描述变化]

请按以下格式输出更新建议：
- 维度：D[N] [维度名]
- 字段：[字段名]
- 原值：[如果知道]
- 新值：[更新内容]
- 敏感级别：L[N]
- 建议操作：添加/修改/删除

我会手动合并到对应文件。
```

---

## P5 · 季度检视Prompt（主动维护触发）

每季度运行一次，检查哪些维度需要更新。

```
请帮我做PCA季度检视。

基于我们最近3个月的对话，请评估以下维度是否需要更新：

| 维度 | 上次更新 | 是否有变化 | 建议操作 |
|------|---------|---------|---------|
| D2 认知OS | [日期] | ? | ? |
| D3 具身状态 | [日期] | ? | ? |
| D5 能力专长 | [日期] | ? | ? |
| D6 资产图谱 | [日期] | ? | ? |
| D7 关系网络 | [日期] | ? | ? |
| D8 项目快照 | [日期] | ? | ? |

对每个"有变化"的维度，列出具体需要更新的字段和新值。
```

---

## P6 · 导出级别选择Prompt

不确定用哪个级别时，用这个prompt让模型帮你判断。

```
我要把PCA导入[模型名称]，用于[使用场景]。

请帮我判断应该使用哪个导出级别：
- L0（公开版，<500 tokens，无敏感信息）
- L1（工作版，<2000 tokens，含项目和工作关系）
- L2（信任版，<5000 tokens，含脱敏健康和资产信息）

以及：是否需要删除或脱敏某些字段？
```
