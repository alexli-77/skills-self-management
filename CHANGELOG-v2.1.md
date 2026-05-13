# v2.1.0 — 基于原著 OCR 的整体重写

> 本次升级基于《高效能人士的七个习惯》（20 周年纪念版，高新勇译）**全本 380 页 OCR**，
> 把原著中未被上一版 skill 充分利用的核心概念、附录、中文经典案例、导师谈心语气，
> 系统性地注回 9 个子 skill。
>
> **总基调变化：** 从"工具说明书"型 skill，变成带有**原著导师语气**、**诊断式对话流程**、
> **原文引用与经典比喻**的深度思考框架。

---

## 主要变化一览

### 1. 新增 skill · `life-center-diagnosis`

基于**附录一"你是哪种类型的人——生活中心面面观"**，新建独立子技能。

**定位：** 作为 `personal-mission-statement` 的**前置诊断**——不先看清当下被什么锚定，写出来的宣言往往是现状美化版。

**内容：**
- 4 项基本需求诊断（安全感 / 指引 / 智慧 / 力量的来源）
- 10 种生活中心的完整矩阵（附录一原表）
- 4 组对话引导问题（分别指向 4 项需求）
- "原则中心"作为唯一健康中心的完整替代视角
- 迁移路径的三步小实验

---

### 2. 调度逻辑升级 · `stephen-covey`

**旧逻辑：** 识别触发词 → 直接调子技能

**新逻辑：** **先做 2 分钟成熟度 + 生活中心 + 规划体系完整度快诊断 → 再决定路线**

**新诊断三问：**
1. 成熟度锚点：这件事你觉得主责方是外部/自己/双方？ → 对应依赖/独立/互赖期
2. 生活中心锚点：让你难受的是金钱/感情/身份/自尊/别人看法…？
3. 规划体系完整度：有没有宣言 / 年度 / 周计划这一串？

**诊断后给用户明示路线图**——不偷偷调度，告诉用户"我建议按这个顺序谈：(1)…(2)…"。

**组合触发原则明示：**
- 依赖期 + 人际问题 → 不跳互赖，先回 `circle-of-influence`
- 没有宣言 + 要做 Q2 → 先 `personal-mission-statement`
- 极度倦怠 + 任何建议 → 先 `sharpen-the-saw` 恢复产能

---

### 3. 引入贯穿框架 · P/PC 平衡 + 成熟度连续体

这两个在原著中贯穿全书的核心概念，此前 skills 几乎没有展开。本版重新嵌入：

**P/PC 平衡（产出/产能）被注入：**
- `sharpen-the-saw`：作为"为什么要磨锯子"的**底层原理**
- `quadrant-ii-time-management`：作为"为什么 Q2 比 Q1 更重要"的**底层解释**
- `stephen-covey`：作为人格基线

**成熟度连续体（依赖 → 独立 → 互赖）：**
- 作为 `stephen-covey` 的**诊断工具**
- 引用原著 p62-64 完整定义，包括当代对"独立"的过度推崇陷阱

---

### 4. 扩充 · `quadrant-ii-time-management`

基于**附录二"第四代的时间管理——高效能人士的一天"**完整扩写：

**新增内容：**
- **四代时间管理演进**（便条 → 日程表 → 优先级 → 个人管理）+ 每代副作用
- **P/PC 平衡作为 Q2 底层解释**（忽视 Q2 = 杀鹅取卵）
- **帕雷托原则**的原著出处
- **按角色 + 目标的周计划模板**（原著 p171-176 核心方法）
- **附录二一日样板**提炼为可复用模板（列活动→标象限→问 II 前置→设计对策）
- **"用今天的 30 分钟 II，换掉下一周的 3 小时 I"口诀**

---

### 5. 语气整体向原著导师风靠拢

**每个 SKILL.md 都有：**
- **开篇引文**（原著金句）
- **对话引导问题**（指向用户自省而非直接给答案）
- **原著比喻嵌入**（下金蛋的鹅、伐木工与锯子、眼科医生的药方、年轻女子/老妇人、两次创造…）
- **结尾付诸行动**（每章原著"付诸行动"格式的作业）

**去掉：**
- 过于"工具说明书"的措辞
- 英文术语重复（保留必要英文概念如 P/PC、Q2，但说明优先中文）

---

### 6. 每个子 skill 补齐的关键内容

| Skill | 补充的关键内容 |
|---|---|
| `stephen-covey` | 人格语气四条 / 成熟度连续体完整定义 / P/PC 作为地基 / 诊断路线图 / 新调度表 |
| `circle-of-influence` | 三类问题（可直接/间接/无法控制）/ 消极主动语言原著对照表 / 四项天赋 / 30 天测试 / 主管与总裁案例 |
| `life-center-diagnosis` | 全新 skill；4 项需求诊断 + 10 种中心完整矩阵 + 原则中心替代视角 |
| `personal-mission-statement` | 两次创造 / 四种基本需求 / 遗产可视化的四位讲者 / 写作约束 6 条 / 决策测试 |
| `quadrant-ii-time-management` | 四代演进史 / P/PC 层级 / 按角色周计划 / 附录二一日样板 / 说"不"的勇气 |
| `win-win-agreement` | 六种互动范式 / 勇气×体谅矩阵 / 富足 vs 稀缺心态 / 五要素协议 / 统合综效第三条路 / Win-Win or No Deal 的底气 |
| `seek-first-to-understand` | 眼科医生的比喻 / 五个倾听层次 / 四阶段移情回应 / 四种自传式回应 / 心理空气 / 困难对话前置练习 |
| `emotional-bank-account` | 六种存款 + 六种取款 / "爱是动词" / 道歉的四要素结构 / "有些账户无法修复"的坦诚 / 三个原著案例 |
| `sharpen-the-saw` | P/PC 作为底层 / 四个更新维度的原著定义 / 每日私下胜利 / 螺旋式上升 / 伐木工与锯子 |

---

## 文件改动清单

```
skills-self-management/
├── README.md                                     # 更新：9 skill 结构、v2.1 变化说明、模式 D 新增
├── CHANGELOG-v2.1.md                            # 新增（本文档）
└── skills-self-management/
    ├── stephen-covey/SKILL.md                    # 重写（242 行）
    ├── circle-of-influence/SKILL.md              # 重写（313 行）
    ├── life-center-diagnosis/SKILL.md           # 【新建】（243 行）
    ├── personal-mission-statement/SKILL.md       # 重写（301 行）
    ├── quadrant-ii-time-management/SKILL.md      # 重写（320 行）
    ├── win-win-agreement/SKILL.md                # 重写（327 行）
    ├── seek-first-to-understand/SKILL.md         # 重写（294 行）
    ├── emotional-bank-account/SKILL.md           # 重写（287 行）
    └── sharpen-the-saw/SKILL.md                  # 重写（278 行）
```

**总行数：** 从 v2.0 的约 2100 行扩展到 v2.1 的约 2600 行，但信息密度更高（去掉了说明书式的重复表述，补上了原著深度内容）。

---

## 版本兼容性

- 所有 skill 的 `name` 字段保持不变 → 上游调用无需改动
- 所有 skill 的 `description` 保留原来的触发词集 + 新增中文场景词
- frontmatter 统一为 `version: 2.1.0`, `author: sethmblack (restructured) · 基于原著 [章节] 补全`

---

## 建议的升级路径

1. **备份**：如果你在用 v2.0，先把旧的 8 个文件夹存档
2. **替换**：用 v2.1 的 9 个文件夹替换（包括新增 `life-center-diagnosis`）
3. **试用顺序建议：**
   - 第一次打开对话，让 `stephen-covey` 跑一次诊断（它会推荐你先去哪个 skill）
   - 如果在做年度 Review，强烈建议按 `life-center-diagnosis` → `personal-mission-statement` → `quadrant-ii-time-management` 的顺序走一遍
   - 单 skill 调用时，直接喊名字即可（如 "用 sharpen-the-saw 帮我做四维度诊断"）

---

## 已知遗留

- 原项目根目录下有一个空目录 `{stephen-covey,circle-of-influence,...}`（早期 brace expansion 残留），不影响功能，可手动删除
- 附录三"答读者问"（p370-380）里有更多原著作者自陈的背景与补充，本版暂未提炼独立成 skill——可作为下一版补充
- 原著第十一章"再论由内而外造就自己"的跨代际剧本改写（Transition Person）概念，目前仅在 `personal-mission-statement` 略提，未独立展开——如果读者后续感兴趣可以作为第 10 个 skill 考虑

---

## 致谢

- 原版单文件灵感：[sethmblack/skill-stephen-covey](https://github.com/sethmblack/skill-stephen-covey)
- 原著中译本：《高效能人士的七个习惯》（20 周年纪念版，高新勇等译，中国青年出版社）
- OCR 工具：RapidOCR (ONNX) + pdftoppm，380 页中文扫描版 8 批次分块完成
