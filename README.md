# webnovel-writer-craft

**给 AI 写作 Agent 注入 125 位人类作家的集体智慧。**

基于 [lingfengQAQ/webnovel-writer](https://github.com/lingfengQAQ/webnovel-writer)（5.3k⭐，v6.2.0）扩展的 Claude Code 插件。原项目解决了长篇连载的"遗忘"和"幻觉"问题，本项目在此基础上注入了叙事学理论和 125 位作者风格库。

---

## 与上游的关系

| 维度 | 上游 webnovel-writer | 本项目 webnovel-writer-craft |
|------|---------------------|------------------------------|
| 核心能力 | 长篇一致性系统（设定/伏笔/时间线） | + 叙事理论 + 风格选型 + 质量评分 |
| 风格系统 | 无 | 12 流派 × 125 位作者 × 625+ 作品 |
| 叙事理论 | 无 | McKee/Campbell/Snyder/Propp 注入 |
| 质量审查 | 一致性/爽点/节奏 | + 五维度叙事质量评分 |
| 题材模板 | 37 个 | 37 个 + 每个附带风格推荐 |
| 上游版本 | v6.2.0 | 完全兼容，所有上游能力保留 |

**所有上游功能完全保留**：断点续跑、上下文瘦身、作者友好报告、webnovel-doctor、Story System 等。

---

## 本项目的增量

### 风格选型系统

init 时基于题材自动推荐写作风格，写入"风格圣经"，全链路参数化输出：

```
/init: 选题材 → genre-style-bridge 推荐风格 → 用户选定 → 生成风格圣经
/plan: 每章标注价值转变 + 冲突类型 + 风格
/write: context-agent 携带风格参数 → 按风格输出
/review: 五维度叙事质量评分（A/B+/B/C/D）
```

### 12 大风格流派

| 流派 | 代表作者 | 一句话 |
|------|---------|--------|
| 白描爽文流 | 天蚕土豆/血红/蝴蝶蓝 | 短句快推 |
| 意境渲染流 | 辰东/烟雨江南/金庸 | 以景写境 |
| 文青叙事流 | 猫腻/古龙/三天两觉 | 人物驱动 |
| 情感驱动流 | 耳根/萧鼎/沈从文 | 执念叙事 |
| 写实逻辑流 | 忘语/紫金陈/马伯庸 | 严谨体系 |
| 零度白描流 | 鲁迅/余华 | 每个词都有用 |
| 感官渲染流 | 张爱玲/莫言/南派三叔 | 感官轰炸 |
| 荒诞幽默流 | 王小波/会说话的肘子 | 黑色幽默 |
| 华丽史诗派(♀) | 天下归元/希行 | 大格局权谋 |
| 细腻虐恋派(♀) | 桐华/意千重 | 意难平 |
| 轻甜治愈派(♀) | 顾漫/墨宝非宝 | 甜到齁 |
| 硬核智识派(♀) | 丁墨/Priest | 高智商恋爱 |

### 叙事质量五维度审查

每章量化评分，趋势追踪：

- 价值转变（McKee）— 场景开始→结束是否有变化
- 冲突有效性 — 是否产生"期望鸿沟"
- 角色弧光一致性 — 主角行为是否匹配弧光类型
- 风格一致性 — 文字风格是否与选定流派一致
- 伏笔张力 — 活跃伏笔是否在制造悬念

### 37 题材模板 + 风格推荐

选"修仙"→推荐意境渲染流·仙侠美学型；选"悬疑推理"→推荐硬核智识派·考据推理型。

---

## 安装

```bash
# Claude Code Marketplace
claude plugin marketplace add Yuwen-1577/webnovel-writer-craft --scope user
claude plugin install webnovel-writer-craft@webnovel-writer-craft-marketplace --scope user

# 或手动安装
git clone https://github.com/Yuwen-1577/webnovel-writer-craft.git ~/.claude/skills/webnovel-writer-craft
```

---

## 快速开始

```bash
/webnovel-init      # 选题材、选风格、建项目
/webnovel-plan 1    # 拆卷纲、写章纲（含价值转变+风格字段）
/webnovel-write 1   # 按风格圣经写章
/webnovel-review 1  # 五维度叙事质量评分
```

---

## 文件结构

```
webnovel-writer/
├── skills/                          # 8 个 Skill 命令
├── references/
│   ├── shared/
│   │   ├── style-system.md          ← 12流派+8维度+场景映射（必读）
│   │   ├── style-authors.md         ← 125位作者详细档案（按需）
│   │   ├── narrative-structures.md  ← 六大叙事框架
│   │   ├── character-psychology.md  ← 角色心理学
│   │   ├── scene-value-change.md    ← 场景价值转变
│   │   ├── writing-craft.md         ← 写作技法
│   │   ├── genre-style-bridge.md    ← 题材→风格桥接
│   │   ├── style-bible-template.md  ← 风格圣经模板
│   │   └── ...（上游原有文件）
│   └── ...
├── templates/genres/                ← 37 题材模板（含风格推荐）
└── scripts/                         ← Python 工具脚本
```

---

## 风格库

125 位作者覆盖中文网文（男频+女频+细分类型）、中国传统文学、西方类型小说、日本文学、韩国网文。

按功能索引（需要什么效果，参考谁）：

| 需求 | 参考作者 |
|------|---------|
| 对话驱动 | 王朔/东野圭吾/刘震云/顾漫 |
| 氛围营造 | 苏童/村上春树/烟雨江南 |
| 恐怖氛围 | King/我会修空调/Shirley Jackson |
| 悬疑推理 | Christie/东野圭吾/紫金陈 |
| 甜蜜互动 | 顾漫/墨宝非宝 |
| 女强权谋 | 天下归元/希行/Priest |

完整档案详见 `references/shared/style-authors.md`。

---

## 贡献

### 添加新作者

在 `references/shared/style-authors.md` 中按格式添加。

### 添加新题材

在 `templates/genres/` 中创建新文件，参照已有模板格式，必须包含"写作风格推荐"区块。

### 添加新流派

在 `references/shared/style-system.md` 的流派总览表中添加行，同时在参数值表中添加对应参数。

---

## 致谢

基于 [lingfengQAQ/webnovel-writer](https://github.com/lingfengQAQ/webnovel-writer)（5.3k⭐）扩展。原项目提供了完整的长篇网文创作工作流，本项目在此基础上注入了叙事学理论和 125 位作者风格库。

---

## License

[GPL-3.0](LICENSE) — 与上游保持一致。
