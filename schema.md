# schema.md
> SelfCtx 个人上下文资产体系 · 数据模型
> 版本：v0.1
> 日期：2026-05-25

---

## 设计原则

1. **正交性**：10个维度互不重叠，每条信息只属于一个维度
2. **时间感知**：每个维度都有更新频率标注，区分"慢变量"和"快变量"
3. **可脱敏**：每个字段标注敏感级别（L0/L1/L2/L3），支持分级导出
4. **模型可读**：字段名和结构对LLM友好，避免歧义
5. **人类可写**：纯Markdown，无需工具，15分钟可完成初版

---

## 敏感级别定义

| 级别 | 含义 | 可给谁 |
|------|------|--------|
| L0 | 公开 | 任意模型，任意场景 |
| L1 | 工作级 | 日常工作协作模型 |
| L2 | 信任级 | 长期主力模型，脱敏后 |
| L3 | 私密 | 仅本地存储，不外发 |

---

## 维度 1 · 叙事身份 Narrative Identity

> 更新频率：极低（年级）
> 敏感级别：L0-L1

我是谁——不是简历，是你对自己故事的理解。

```yaml
narrative_identity:
  tagline: string           # L0 · 一句话自我定义，给模型用
  origin_story: string      # L1 · 我怎么走到现在（3-5句话叙事）
  defining_moments: list    # L1 · 塑造现在的你的2-3个关键节点
  self_perception: string   # L1 · 我认为自己是什么样的人
  public_roles: list        # L0 · 对外身份标签（创业者/产品人/独立开发者等）
```

**示例**
```yaml
narrative_identity:
  tagline: "在游戏公司做AI管线的产品人，同时跑几个个人产品。"
  origin_story: "从内容/运营背景转产品，在游戏行业做了多年，2024年开始all-in AI工具方向。"
  defining_moments:
    - "第一次用Claude完整搭出一个产品原型，发现AI可以替代很多以前必须找人的环节"
    - "AI游戏管线第一个外部客户意向达成，从内部项目变成可能的商业产品"
  self_perception: "执行力强，偏保守但能快速学习，对形式主义有清醒认知。"
  public_roles: ["产品负责人", "独立开发者", "技术博主"]
```

---

## 维度 2 · 认知操作系统 Cognitive OS

> 更新频率：低（季度级）
> 敏感级别：L0-L1

我怎么思考、怎么判断、对AI有什么强制要求。

```yaml
cognitive_os:
  thinking_style: string        # L0 · 思维风格（直觉/分析/系统等）
  decision_pattern: string      # L1 · 决策偏好（快速迭代/谨慎验证等）
  communication_style: string   # L0 · 沟通偏好（直接/结构化/克制等）
  
  ai_hard_rules:                # L0 · 对所有AI的强制约束，不可违反
    forbidden: list             # 禁止行为列表
    required: list              # 必须行为列表
    
  ai_workflow_modes: list       # L1 · 特定工作流触发规则（如/office-hours）
  output_preferences:           # L0 · 输出格式偏好
    format: string              # 默认格式（md/prose/list等）
    length: string              # 偏好长度（简洁/详细/按需）
    language: string            # 主要语言
```

**示例**
```yaml
cognitive_os:
  thinking_style: "系统性，但不喜欢过度抽象；偏好有具体锚点的讨论"
  decision_pattern: "先做最小验证，不喜欢大而全的方案；有外部数据前保守"
  communication_style: "直接，不套话，用括号写内心话，反公式化结尾"
  
  ai_hard_rules:
    forbidden:
      - "不说'很有意思''有很多方式思考''可能值得考虑'等套话"
      - "不主动生成docx/pptx，默认md"
      - "涉及商业化触发词时不可跳过/office-hours流程"
      - "不把兴趣/等候名单当需求，付钱才算需求"
    required:
      - "必须表态：这能不能成立，依据是什么"
      - "方案给出2-3个不同路径并明确推荐"
      - "收到导出/记忆指令时主动触发历史搜索"
      
  ai_workflow_modes:
    - trigger: "涉及商业化/融资/定价/合作/客户"
      mode: "/office-hours → /plan-ceo-review"
      description: "逼迫性审查流程，不可软化"
      
  output_preferences:
    format: "markdown"
    length: "简洁优先，节省tokens"
    language: "中文为主，技术/英文内容保持英文"
```

---

## 维度 3 · 具身状态 Embodied State

> 更新频率：高（月级）
> 敏感级别：L2-L3

身体是工作的载体，健康状态影响认知和判断。

```yaml
embodied_state:
  health_conditions: list       # L3 · 慢性/长期健康问题
  current_issues: list          # L2 · 当前活跃的健康问题
  energy_pattern: string        # L2 · 能量节律（早鸟/夜猫/高峰时段）
  physical_constraints: list    # L2 · 影响工作的身体限制
  sensory_preferences: dict     # L1 · 感官偏好（工作环境、噪音容忍度等）
  last_updated: date
```

**示例**
```yaml
embodied_state:
  health_conditions: []
  current_issues:
    - condition: "左肩冈上肌部分撕裂+盂唇损伤"
      status: "保守治疗中，待复诊"
      impact: "避免过头举重、单肩背包"
      since: "2026-05"
  energy_pattern: "上午效率最高，下午容易松散"
  physical_constraints:
    - "久坐为主，缺乏运动习惯"
  sensory_preferences:
    noise_tolerance: "低，需要安静工作环境"
    co2_awareness: "关注办公室CO2浓度对专注力的影响"
  last_updated: "2026-05-25"
```

---

## 维度 4 · 情绪与心理 Emotional & Psychological State

> 更新频率：高（月级）
> 敏感级别：L3
> **可选维度**：不强制填写。有意愿时填，整个维度可以为空。导出时仅包含在L2+，L1不包含。

```yaml
emotional_state:
  current_mood_baseline: string  # L3 · 近期整体情绪基调
  stress_sources: list           # L3 · 当前主要压力来源
  emotional_triggers: list       # L3 · 容易触发负面情绪的模式
  coping_patterns: list          # L3 · 惯用的应对方式
  psychological_needs: list      # L3 · 当前需要被满足的心理需求
  
  ai_interaction_notes: string   # L2 · 对AI互动的情绪偏好（如：需要直接不需要安慰）
  last_updated: date
```

---

## 维度 5 · 能力与专长 Capabilities & Expertise

> 更新频率：低（季度级）
> 敏感级别：L0-L1

```yaml
capabilities:
  domains: list                  # L0 · 专业领域列表
  depth_map: dict                # L1 · 各领域深度（入门/熟练/专家）
  
  technical_stack: dict          # L1 · 技术栈
    languages: list
    tools: list
    frameworks: list
    
  methodology: list              # L0 · 工作方法论（如document-driven development）
  
  terminology: list              # L1 · 专属术语表
    - term: string
      meaning: string
      
  known_blind_spots: list        # L2 · 自知的能力盲区
```

---

## 维度 6 · 资产图谱 Asset Map

> 更新频率：中（季度级）
> 敏感级别：L1-L3

```yaml
asset_map:
  physical_assets:               # L1 · 物理设备和基础设施
    devices: list
    infrastructure: list
    
  digital_assets:                # L1 · 数字产品和资产
    products: list               # 在运营的产品
      - name: string
        url: string
        status: string           # active/maintenance/dormant
        metrics: dict            # L2 · 关键指标
        
    domains: list                # L1 · 持有域名
    repositories: list           # L1 · 代码库
    accounts: list               # L2 · 重要账号（脱敏）
    
  financial_snapshot:            # L3 · 财务快照（高度脱敏）
    income_streams: list         # 收入来源类型（不含金额）
    burn_rate_level: string      # 高/中/低（不含具体数字）
    runway_months: int           # L3
    last_updated: date
```

---

## 维度 7 · 关系网络 Relationship Network

> 更新频率：中（季度级）
> 敏感级别：L1-L2
> **人名策略**：用户自主决定。默认建议：L1只写角色/代称，L2+写昵称或真名，L3写完整信息。不做强制，用户自行评估隐私风险。

```yaml
relationship_network:
  work_relationships:            # L1 · 工作关系
    - name: string               # 姓名/称呼/代称（用户自定义）
      role: string               # 在你工作中的角色
      organization: string       # 所属组织
      relationship_type: string  # 上级/下属/同级/外部合作方/客户
      current_status: string     # 活跃/维护中/暂停
      notes: string              # L2 · 关系备注
      
  social_relationships:          # L2 · 社交关系（非工作）
    - name: string
      type: string               # 朋友/mentor/社群成员等
      context: string            # 认识的背景
      
  family: list                   # L3 · 家庭关系（仅在必要时填写）
  
  network_gaps: list             # L2 · 当前缺少的关键连接（如：缺少某领域mentor）
```

---

## 维度 8 · 项目与任务快照 Project Snapshot

> 更新频率：极高（月级触发，窗口3-12个月）
> 敏感级别：L1-L2
> **时间窗口**：默认3个月，用户可延长至12个月。快节奏项目用3个月，慢节奏（如游戏开发大周期）可用6-12个月。窗口到期时，内容不删除，降级为`completed_recently`保留背景。
> **与平台记忆叠加**：如果使用支持持久记忆的平台（如Claude Projects），PCA作为底层文档，平台记忆作为增量层。两者叠加覆盖：PCA提供结构化基线，平台记忆提供最近对话细节。

```yaml
project_snapshot:
  snapshot_period: string        # 快照覆盖的时间段（如：2026-03 至 2026-05）
  
  active_projects:               # L1 · 活跃项目
    - name: string
      type: string               # 公司项目/个人产品/研究/其他
      status: string             # 进行中/暂停/收尾
      priority: int              # 1-5，1最高
      current_focus: string      # 当前最重要的事
      blockers: list             # L2 · 当前阻塞点
      next_milestone: string     # 下一个里程碑
      
  active_decisions: list         # L2 · 当前悬而未决的重要决策
  
  completed_recently: list       # L1 · 近期完成的重要事项（给模型提供背景）
  
  on_hold: list                  # L1 · 暂停的项目（保留上下文）
```

---

## 维度 9 · 兴趣与审美 Interests & Aesthetics

> 更新频率：极低（年级）
> 敏感级别：L0-L1

```yaml
interests_aesthetics:
  long_term_interests: list      # L0 · 长期兴趣领域（不随项目变化）
  
  aesthetic_principles: list    # L0 · 审美偏好（适用于设计/写作/产品）
  
  consumption_habits: dict       # L1 · 内容消费偏好
    reading: list                # 常看的类型/平台
    media: list                  # 影视/播客等偏好
    
  dislike_patterns: list         # L1 · 明确反感的风格或模式
  
  creative_sensibility: string   # L0 · 创作/审美的核心倾向
```

**示例**
```yaml
interests_aesthetics:
  long_term_interests:
    - "工业设计史（特别是20世纪功能主义）"
    - "传统中国美学（留白、意境）"
    - "哲学（实用主义、认识论）"
    - "AI基础设施和agent架构"
    
  aesthetic_principles:
    - "极简克制，反装饰"
    - "功能先于形式，但形式不能丑"
    - "留白是设计的一部分"
    
  dislike_patterns:
    - "过度包装和形式主义"
    - "大而全的方案"
    - "套话和公式化表达"
    
  creative_sensibility: "性冷淡克制风格，用最少的元素传达最多的信息"
```

---

## 维度 10 · 世界观与志向 Worldview & Aspirations

> 更新频率：极低（年级）
> 敏感级别：L0-L1

```yaml
worldview_aspirations:
  core_values: list              # L0 · 核心价值观（3-5条，真实的，不是口号）
  
  mental_models: list            # L1 · 常用思维模型或框架
  
  long_term_vision: string       # L1 · 3-5年后想成为什么样的人/做什么事
  
  non_negotiables: list          # L1 · 底线和不可妥协的事
  
  current_philosophy: string     # L1 · 当前人生阶段的指导原则（可以变化）
  
  relationship_with_ai: string   # L0 · 你如何看待自己与AI的关系
```

---

## 文件结构

```
selfctx/
├── README.md              # 使用说明和导出指南
├── schema.md              # 本文件，数据模型定义
│
├── core/                  # 慢变量（年级更新）
│   ├── d1_narrative.md    # 维度1：叙事身份
│   ├── d2_cognitive_os.md # 维度2：认知操作系统
│   ├── d5_capabilities.md # 维度5：能力与专长
│   ├── d9_interests.md    # 维度9：兴趣与审美
│   └── d10_worldview.md   # 维度10：世界观与志向
│
├── dynamic/               # 快变量（月级更新）
│   ├── d3_embodied.md     # 维度3：具身状态
│   ├── d4_emotional.md    # 维度4：情绪与心理
│   ├── d6_assets.md       # 维度6：资产图谱
│   ├── d7_relationships.md# 维度7：关系网络
│   └── d8_projects.md     # 维度8：项目快照
│
└── exports/               # 按级别生成的导出文件
    ├── L0_public.md       # 公开版
    ├── L1_work.md         # 工作版
    ├── L2_trusted.md      # 信任版
    └── L3_full.md         # 全量版（不外发）
```

---

## 字段更新频率汇总

| 维度 | 更新频率 | 触发条件 |
|------|---------|---------|
| D1 叙事身份 | 年级 | 重大人生转折 |
| D2 认知OS | 季度 | 工作方式有意识改变 |
| D3 具身状态 | 月级 | 健康状况变化 |
| D4 情绪心理 | 月级 | 主动检视 |
| D5 能力专长 | 季度 | 新技能/领域 |
| D6 资产图谱 | 季度 | 资产增减 |
| D7 关系网络 | 季度 | 关系变化 |
| D8 项目快照 | 月级触发，3-12个月窗口 | 项目状态变更 |
| D9 兴趣审美 | 年级 | 兴趣演变 |
| D10 世界观 | 年级 | 价值观更新 |
