# PCA · 个人上下文资产
> 创建时间: 
> 最后更新: 
> 导出级别: L1（工作版）

---

## D1 · 叙事身份
> 更新频率：年级 | 敏感级别：L0-L1

```yaml
narrative_identity:
  tagline: ""
  origin_story: ""
  defining_moments:
    - ""
  self_perception: ""
  public_roles:
    - ""
```

---

## D2 · 认知操作系统
> 更新频率：季度 | 敏感级别：L0-L1

```yaml
cognitive_os:
  thinking_style: ""
  decision_pattern: ""
  communication_style: ""
  
  ai_hard_rules:
    forbidden:
      - ""
    required:
      - ""
      
  ai_workflow_modes:
    - trigger: ""
      mode: ""
      description: ""
      
  output_preferences:
    format: "markdown"
    length: ""
    language: ""
```

---

## D3 · 具身状态
> 更新频率：月级 | 敏感级别：L2-L3

```yaml
embodied_state:
  health_conditions: []
  current_issues:
    - condition: ""
      status: ""
      impact: ""
      since: ""
  energy_pattern: ""
  physical_constraints: []
  sensory_preferences: {}
  last_updated: ""
```

---

## D4 · 情绪与心理（可选）
> 更新频率：月级 | 敏感级别：L3 | 可整个维度为空

```yaml
emotional_state:
  current_mood_baseline: ""
  stress_sources: []
  ai_interaction_notes: ""
  last_updated: ""
```

---

## D5 · 能力与专长
> 更新频率：季度 | 敏感级别：L0-L1

```yaml
capabilities:
  domains: []
  depth_map: {}
  
  technical_stack:
    languages: []
    tools: []
    frameworks: []
    
  methodology: []
  
  terminology:
    - term: ""
      meaning: ""
      
  known_blind_spots: []
```

---

## D6 · 资产图谱
> 更新频率：季度 | 敏感级别：L1-L3

```yaml
asset_map:
  physical_assets:
    devices: []
    infrastructure: []
    
  digital_assets:
    products:
      - name: ""
        url: ""
        status: ""
    domains: []
    repositories: []
    
  financial_snapshot:
    income_streams: []
    burn_rate_level: ""
    last_updated: ""
```

---

## D7 · 关系网络
> 更新频率：季度 | 敏感级别：L1-L2
> 人名策略：L1默认写角色/代称，L2+可写真名，用户自主决定

```yaml
relationship_network:
  work_relationships:
    - name: ""          # 角色/代称/真名，自主决定
      role: ""
      organization: ""
      relationship_type: ""   # 上级/下属/同级/外部合作方/客户
      current_status: ""      # 活跃/维护中/暂停
      notes: ""
      
  social_relationships: []
  
  network_gaps: []
```

---

## D8 · 项目快照
> 更新频率：月级触发 | 敏感级别：L1-L2
> 时间窗口：默认3个月，可延长至12个月

```yaml
project_snapshot:
  snapshot_period: ""     # 如：2026-03 至 2026-05
  window_months: 3        # 3-12，按项目节奏自定义
  
  active_projects:
    - name: ""
      type: ""            # 公司项目/个人产品/研究/其他
      status: ""          # 进行中/暂停/收尾
      priority: 1         # 1-5，1最高
      current_focus: ""
      blockers: []
      next_milestone: ""
      
  active_decisions: []
  
  completed_recently: []
  
  on_hold: []
```

---

## D9 · 兴趣与审美
> 更新频率：年级 | 敏感级别：L0-L1

```yaml
interests_aesthetics:
  long_term_interests: []
  
  aesthetic_principles: []
  
  consumption_habits:
    reading: []
    media: []
    
  dislike_patterns: []
  
  creative_sensibility: ""
```

---

## D10 · 世界观与志向
> 更新频率：年级 | 敏感级别：L0-L1

```yaml
worldview_aspirations:
  core_values: []
  
  mental_models: []
  
  long_term_vision: ""
  
  non_negotiables: []
  
  current_philosophy: ""
  
  relationship_with_ai: ""
```
