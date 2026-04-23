# Skills for Self-Management

> 基于 Stephen Covey《高效能人士的七个习惯》的 Claude Agent Skills 集合，
> 帮助你审视人生宣言、长期规划与周度计划，以原则性视角发现盲点。

![License](https://img.shields.io/badge/license-MIT-blue)
![Skills](https://img.shields.io/badge/skills-8-green)
![Language](https://img.shields.io/badge/language-中文-red)

---

感谢 ![sethmblack/skill-stephen-covey](https://github.com/sethmblack/skill-stephen-covey) 给了我很多灵感。
---
## 这是什么？

这是一套专为 Claude 设计的 Agent Skills，把柯维七个习惯的思考框架拆分成 8 个独立、可组合的子技能。你可以把它们当作**不同视角的"原则性审阅官"**——当你已经有了人生宣言、长期规划或周计划，让 Claude 扮演柯维的角色审视你的规划体系，发现断层、盲点和偏离。

**这套 Skill 最适合：**
- 已经有人生宣言、5 年/1 年/季度/周计划的人
- 想要定期 Review 自己规划体系的人
- 想用 AI 作为"思考教练"而非"任务管理器"的人

**不适合：**
- 期待 AI 替你管理任务、发送提醒的人（这不是任务管理工具）
- 从未写过个人规划、希望 AI 从零带你的人（可以用，但会很慢）

---

## 快速开始

### 前置条件

- Claude Desktop 或 Claude Code（CLI）
- 已开启 Code Execution 权限
- 对柯维七个习惯有基本了解（没有也行，Claude 会用到）

### 安装

**桌面端（Claude Desktop / Cowork）：**

1. 下载本仓库
2. 将每个子文件夹单独打包成 ZIP（或只打包你需要的）
3. 打开 Claude Desktop → Customize → Skills → "+" → Upload a skill
4. 分别上传每个 ZIP

**CLI（Claude Code）：**

```bash
# 克隆到你的 Claude 工作空间
cd ~/claude_workspace
git clone https://github.com/YOUR_USERNAME/skills-self-management.git

# 或者放到项目的 .claude/skills/ 下
cd your-project
mkdir -p .claude/skills
cp -r path/to/skills-self-management/* .claude/skills/
```

---

## 文件结构

```
skills-self-management/
├── stephen-covey/                      # 主人格 + 子技能调度
├── circle-of-influence/                # 习惯 1 · 积极主动
├── personal-mission-statement/         # 习惯 2 · 以终为始
├── quadrant-ii-time-management/        # 习惯 3 · 要事第一
├── win-win-agreement/                  # 习惯 4 · 双赢思维
├── seek-first-to-understand/           # 习惯 5 · 知彼解己
├── emotional-bank-account/             # 习惯 4-6 基础 · 信任管理
└── sharpen-the-saw/                    # 习惯 7 · 自我更新
```

### 每个子技能的职责

| 子技能 | 对应习惯 | 核心用途 |
|--------|---------|---------|
| **stephen-covey** | 总控 | 统筹调度其他技能，提供柯维人格 |
| **circle-of-influence** | 习惯 1 | 把精力从"关注圈"拉回"影响圈" |
| **personal-mission-statement** | 习惯 2 | 建立/审视人生宣言 |
| **quadrant-ii-time-management** | 习惯 3 | 诊断时间去向，聚焦 Q2 |
| **win-win-agreement** | 习惯 4 | 谈判与协议的双赢结构设计 |
| **seek-first-to-understand** | 习惯 5 | 移情倾听，打破沟通死循环 |
| **emotional-bank-account** | 习惯 4-6 | 人际信任诊断与修复 |
| **sharpen-the-saw** | 习惯 7 | 四维度倦怠评估与恢复 |

---

## 核心使用场景：Review 你已有的规划体系

如果你已经有完整的规划体系（人生宣言 → 5 年 → 1 年 → 季度 → 周），这套 Skill 最有价值的用法是**定期 Review**。

### 推荐的 Review 节奏

| 频率 | Review 内容 | 时长 | 调用的技能 |
|------|-----------|------|----------|
| **每周日晚** | 本周计划 vs 季度规划 | 20 分钟 | `quadrant-ii` + `circle-of-influence` |
| **每月第一天** | 当月进展 vs 1 年规划 | 1 小时 | `personal-mission` + `quadrant-ii` |
| **每季末** | 季度复盘 + 下季规划 | 2 小时 | 全套 |
| **每年 12 月** | 5 年规划调整 / 使命宣言更新 | 半天 | `personal-mission` + `sharpen-the-saw` |

---

## 三种 Review 模式

### 模式 A：垂直一致性检查

**用于：** 季度末 / 年度回顾

**做什么：** 从上往下检查每一层规划是否真的在服务上一层，揪出"僵尸任务"和"失踪优先级"。

**提示词模板：**

```
你是 Stephen Covey。请检查我的规划体系的垂直一致性：

1. 5 年规划里的每一项，能否追溯到使命宣言？
2. 1 年规划里的每一项，能否追溯到 5 年规划？
3. 本季度规划里的每一项，能否追溯到 1 年规划？
4. 本周计划里的每一项，能否追溯到季度规划？

找出断层：
- 僵尸任务：我在做但追溯不到上层的事
- 失踪优先级：宣言里重要但下层消失的事

以柯维的语气直接指出问题，不要客气。
```

---

### 模式 B：象限分布检查

**用于：** 每周计划 Review

**做什么：** 把本周任务分类到 Q1-Q4 四个象限，识别是否陷入紧急陷阱。

**提示词模板：**

```
用 Q2 框架审视我的本周计划：

1. 把所有任务分类到 Q1/Q2/Q3/Q4 四个象限
2. 计算各象限的时间占比
3. 诊断：
   - Q2 占比是否健康（目标 60-70%）？
   - 哪些 Q3 任务可以拒绝或委派？给出具体拒绝话术
   - 哪些 Q1 任务本来可以通过之前的 Q2 投入预防？
4. 建议本周必须保护的"大石头"时间块

以柯维的视角给出具体、可执行的调整建议。
```

---

### 模式 C：影响圈诊断

**用于：** 季度 / 年度目标审视

**做什么：** 判断目标是否在可控范围内，把"关注圈表述"重构为"影响圈表述"。

**提示词模板：**

```
用影响圈模型审视我的 [1 年 / 季度] 目标。

对每一个目标：
1. 判断：这在我的影响圈内，还是关注圈？
2. 如果在影响圈内：具体的、我能控制的行动是什么？
3. 如果在关注圈（依赖他人或外部条件）：
   - 指出我实际能控制的部分
   - 把它重新表述为"影响圈版本"

示例：
- 关注圈："让产品用户增长到 10 万"
- 影响圈："每月发布 2 个提升留存的核心功能 + 每周 3 次用户访谈"
```

---

## 其他使用场景

除了 Review 规划，这套 Skill 还能用于：

### 人际关系诊断

**触发：** 与某个人关系紧张、信任受损

```
用 emotional-bank-account 帮我诊断我和 [某人] 的关系：
- 最近的存款和取款分别有哪些？
- 账户状态如何？
- 给我一份具体的存款处方（本周/本月）
```

### 沟通僵局破解

**触发：** 与某人反复争执同一件事

```
我和 [某人] 总在吵 [某个话题]。
用 seek-first-to-understand 帮我：
1. 诊断我们各自的倾听层次
2. 识别我的自传式回应
3. 给出下次对话的具体移情回应话术
```

### 倦怠恢复规划

**触发：** 感到精疲力竭但又停不下来

```
我已经 [工作/学习/创业] [时长]，感觉 [具体症状]。
用 sharpen-the-saw 帮我做四维度评估，并给出本周的最低更新计划。
```

### 谈判结构设计

**触发：** 准备与老板/客户/合伙人进行重要谈判

```
我要和 [某人] 谈 [事情]。
用 win-win-agreement 帮我：
1. 诊断双方的真实需求（不只是立场）
2. 设计双赢协议的五要素
3. 起草"如果不成交更好"的条件
```

---

## 最佳实践

### 1. 把规划文档放进 Claude Project

创建一个 Claude Project（例如 "我的人生管理"），把以下文档放进 Knowledge：

```
01-mission-statement.md       # 人生宣言
02-five-year-plan.md          # 5 年规划
03-yearly-plan-2026.md        # 1 年规划
04-q2-2026-plan.md            # 季度规划
05-weekly-plan-current.md     # 本周计划
```

这样每次 Review 时 Claude 都能读到全貌，不用反复贴文档。

### 2. 明确调用 Skill

虽然 Claude 会自动识别触发条件，但明确调用效果更好：

```
# 推荐
"用 quadrant-ii-time-management 帮我 review 本周计划"

# 也可以但效果略差
"帮我看看本周计划有没有问题"
```

### 3. 接受不舒服的反馈

柯维的视角会戳破你的自我安慰。常见的"刺痛时刻"：
- "你 1 年规划有 12 个目标，这不是规划，是愿望清单"
- "你本周 23 件事里只有 2 件是 Q2，下周你还会说'没时间做重要的事'"
- "你宣言里'陪伴家人'排第二，但规划里看不到"

**不要删掉这些反馈。** 这些是你花钱找教练才听得到的话。

### 4. 把 Review 本身安排成 Q2 活动

Review 不会自己发生。在日历里划出固定时间块：
- 每周日 21:00-21:20 → 周度 Review
- 每月 1 号 09:00-10:00 → 月度 Review
- 每季末最后一个周日上午 → 季度 Review

---

## 为什么拆成 8 个文件而不是 1 个？

本 Skill 的前身是一个 2943 行的单文件 Skill。拆分的理由：

1. **Context 效率：** Claude 每次只加载用到的子技能，不浪费 context window
2. **维护性：** 单个技能更新不影响其他技能
3. **灵活组合：** 你可以只用其中 3 个，不必全套装载
4. **符合 Skill 规范：** Anthropic 官方推荐每个 Skill 单一职责

原始单文件版本作者为 [sethmblack/paks-skills](https://github.com/sethmblack/paks-skills)，
本仓库基于 MIT 协议进行重构，主要改动：

- 拆分为 8 个独立 Skill
- 全面中文化（框架、示例、提示词）
- 优化 `description` 字段以提升自动触发准确度
- 增加"对话模式 / 深度分析模式"双模式输出
- 增加中文语境适配说明

---

## 限制与说明

### 这套 Skill 能做的

- ✅ 以柯维视角审视你的规划
- ✅ 诊断时间分布、关系健康、倦怠程度
- ✅ 输出结构化的分析报告和具体建议
- ✅ 在沟通、谈判、决策中提供原则性视角

### 这套 Skill 不能做的

- ❌ **不存储你的数据**：每次新对话都是空白的（需配合 Claude Project）
- ❌ **不跟踪任务状态**：今天做没做、进度如何，它不知道
- ❌ **不发送提醒**：它是"咨询顾问"不是"秘书"
- ❌ **不替代真人教练**：在重大人生决策上，它是辅助工具，不是决策者

### 一个坦白的提醒

人生规划最大的敌人不是方法，是**坚持**。

Skill 让你第一次 Review 时很爽，但 6 个月后你很可能忘了它。真正起作用的方式是把 Review 本身变成一个 Q2 活动——雷打不动地在日历里占位。

这也是柯维的核心观点："**磨锐锯子必须被排进日程，否则永远不会发生。**"

---

## 贡献

欢迎提 Issue 和 PR。特别欢迎：
- 翻译成其他语言的版本
- 新的 Review 提示词模板
- 使用案例和经验分享

---

## License

MIT License. 基于 [sethmblack/paks-skills](https://github.com/sethmblack/paks-skills) 重构。

---

## 延伸阅读

- 📖 《高效能人士的七个习惯》- Stephen R. Covey
- 📖 《要事第一》- Stephen R. Covey
- 📖 《信任的速度》- Stephen M.R. Covey
- 🔗 [Anthropic Skills 官方文档](https://docs.claude.com/en/docs/claude-code/skills)
- 🔗 [Anthropic 官方 Skills 示例仓库](https://github.com/anthropics/skills)

---

*"关键不是为你的日程排优先顺序，而是为你的优先事项安排日程。"*
*— Stephen R. Covey*
