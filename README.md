# webnovel-craft

**给 AI 写作 Agent 注入 125 位人类作家的集体智慧。**

Claude Code 插件，用 `/webnovel-init`、`/webnovel-plan`、`/webnovel-write` 等命令驱动 AI 网文写作全流程。

---

## 安装

```bash
# 全局安装（所有项目可用）
git clone https://github.com/YOUR_USERNAME/webnovel-craft.git ~/.claude/skills/webnovel-craft

# 或项目级安装
git clone https://github.com/YOUR_USERNAME/webnovel-craft.git .claude/skills/webnovel-craft
```

安装后在 Claude Code 中使用 `/webnovel-init` 开始。

---

## 快速开始

```
1. /webnovel-init     → 选题材、选风格、建项目
2. /webnovel-plan     → 拆卷纲、写章纲
3. /webnovel-write    → 逐章写作
4. /webnovel-review   → 质量审查
```

---

## 核心功能

### 风格选型系统

12 大风格流派 × 125 位作者 × 625+ 作品。init 时基于题材自动推荐风格，写入"风格圣经"，全链路参数化输出。

| 流派 | 代表作者 | 一句话标签 |
|------|---------|-----------|
| 白描爽文流 | 天蚕土豆/血红/蝴蝶蓝 | 短句快推，一切服务节奏 |
| 意境渲染流 | 辰东/烟雨江南/金庸 | 以景写境，大气磅礴 |
| 文青叙事流 | 猫腻/烽火戏诸侯/古龙 | 人物驱动，潜台词密 |
| 情感驱动流 | 耳根/萧鼎/沈从文 | 执念叙事，情感爆发 |
| 写实逻辑流 | 忘语/紫金陈/马伯庸 | 严谨体系，策略取胜 |
| 零度白描流 | 鲁迅/余华 | 每个词都有用 |
| 感官渲染流 | 张爱玲/莫言/南派三叔 | 感官轰炸，沉浸感 |
| 荒诞幽默流 | 王小波/三天两觉/会说话的肘子 | 黑色幽默，荒诞并列 |
| 华丽史诗派(♀) | 天下归元/希行 | 女主碾压全场 |
| 细腻虐恋派(♀) | 桐华/意千重 | 所有人都没错但结局错了 |
| 轻甜治愈派(♀) | 顾漫/墨宝非宝 | 甜到齁但停不下来 |
| 硬核智识派(♀) | 丁墨/Priest | 高智商恋爱+严密逻辑 |

### 叙事质量五维度审查

每章量化评分（A/B+/B/C/D），趋势追踪：

- 价值转变（McKee）— 场景开始→结束是否有可识别的变化
- 冲突有效性 — 是否产生"期望鸿沟"
- 角色弧光一致性 — 主角行为是否与弧光类型匹配
- 风格一致性 — 文字风格是否与选定流派一致
- 伏笔张力 — 活跃伏笔是否在制造悬念

### 题材→风格桥接

37 个题材模板自动推荐写作风格。选"修仙"→推荐意境渲染流·仙侠美学型；选"悬疑推理"→推荐硬核智识派·考据推理型。

### 叙事理论注入

- 六大叙事框架（三幕式/英雄之旅/Save the Cat/雪花法/起承转合/Freytag）
- Jung 12 原型 + MBTI 性格生成 + 角色弧光三种类型
- McKee 价值转变 + 六种冲突子类型 + 悬念 vs 惊奇
- 网文模式与叙事理论的映射（打脸=McKee期望鸿沟，废材逆袭=英雄之旅压缩版）

---

## 架构

```
init → plan → write → review → learn
  │       │       │        │       │
  │       │       │        │       └─ 记录成功模式（含风格维度）
  │       │       │        └─ 五维度量化评分 + 趋势追踪
  │       │       └─ 风格圣经参数化输出 + 微变体
  │       └─ 每章标注价值转变/冲突类型/风格
  └─ 题材→风格推荐 → 风格圣经自动生成
```

---

## 文件结构

```
references/shared/
├── style-system.md         ← 核心：12流派+8维度+场景映射（必读）
├── style-authors.md        ← 125位作者详细档案（按需加载）
├── narrative-structures.md ← 六大叙事框架
├── character-psychology.md ← 角色心理学
├── scene-value-change.md   ← 场景价值转变
├── writing-craft.md        ← 写作技法
├── genre-style-bridge.md   ← 题材→风格桥接
├── style-bible-template.md ← 风格圣经模板
├── cool-points-guide.md    ← 爽点工程
└── ...

templates/genres/           ← 37个题材模板（含风格推荐）
```

---

## 风格库

125 位作者覆盖中文网文（男频+女频+细分类型）、中国传统文学、西方类型小说、日本文学、韩国网文。

按功能索引（需要什么效果，参考谁）：

| 需求 | 参考作者 |
|------|---------|
| 对话驱动 | 王朔/东野圭吾/刘震云/顾漫 |
| 氛围营造 | 苏童/村上春树/烟雨江南 |
| 多线叙事 | 格非/伊坂幸太郎/Sing Shong |
| 壮美场面 | Clarke/辰东/金庸 |
| 恐怖氛围 | King/我会修空调/Shirley Jackson |
| 悬疑推理 | Christie/东野圭吾/紫金陈 |
| 甜蜜互动 | 顾漫/墨宝非宝 |
| 女强权谋 | 天下归元/希行/Priest |

完整档案详见 `references/shared/style-authors.md`。

---

## 贡献

### 添加新作者

在 `references/shared/style-authors.md` 中按格式添加：

```
| 作者名 | 流派 | 子变体 | 核心武器 | 句长 | 白描 | 一句话DNA |
```

### 添加新题材

在 `templates/genres/` 中创建新文件，参照已有模板格式，必须包含"写作风格推荐"区块。

### 添加新流派

在 `references/shared/style-system.md` 的流派总览表中添加行，同时在参数值表中添加对应参数。

---

## 致谢

基于 [webnovel-writer](https://github.com/ORIGINAL_PROJECT) 项目扩展。

风格库研究综合了 125 位中外作家的写作风格分析，覆盖 625+ 部作品。

---

## License

MIT
