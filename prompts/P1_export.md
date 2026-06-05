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