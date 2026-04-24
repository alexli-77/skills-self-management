---
name: lark-workflow-weekly-review
version: 1.0.0
description: "Weekly Review 工作流：读取飞书 Weekly 文档中的 Q2 表格 → 用柯维四象限分析本周计划 → 将新一周计划写回表格。当用户说'帮我做 Weekly Review'、'写本周计划'、'更新 Weekly 表格'、'做 weekly'时使用。"
metadata:
  requires:
    bins: ["lark-cli"]
---

# Weekly Review 工作流

**CRITICAL — 开始前 MUST 先用 Read 工具读取 [`~/.agents/skills/lark-shared/SKILL.md`](~/.agents/skills/lark-shared/SKILL.md)，其中包含认证、权限处理**

## 适用场景

- "帮我做本周的 Weekly Review"
- "把本周计划写入飞书表格"
- "更新 Q2 🐶 表格，加入这周的计划"
- "帮我做 weekly"

## 用户信息

| 字段 | 值 |
|------|-----|
| 文档 token | `MDladM2GtotiM6xwEKecTMOinph` |
| Q2 🐶 表格 block_id | `GkpXdEoafoGmABxeDMYcGWaMnmg` |
| 时区 | America/Toronto（蒙特利尔，UTC-4/UTC-5） |
| 工作时间 | 08:30 - 23:00 |

## 工作流总览

```
Step 1: 读取文档结构
        ↓
Step 2: 获取表格 block 结构（已有列数/列宽/单元格 ID）
        ↓
Step 3: 与用户确认本周计划内容（如未提供）
        ↓
Step 4: 插入新列（要务列 + retro 列）
        ↓
Step 5: 逐单元格写入内容（block API，保留格式）
        ↓
Step 6: 可选：柯维四象限分析 + 建议
```

## Step 1 & 2：读取表格结构

```bash
# 读取文档大纲，找到 Q2 🐶 表格位置
lark-cli docs +fetch --doc MDladM2GtotiM6xwEKecTMOinph \
  --scope outline --max-depth 3

# 获取表格 block 详情，拿到 cells 数组和当前列数
lark-cli api GET "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/GkpXdEoafoGmABxeDMYcGWaMnmg" \
  --as user
```

**单元格定位规则：**
- `cells` 数组按 `row * col_count + col` 索引
- 第 0 行是表头行（🐶、任务内容、MIT、W1 要务、W1 retro ...）
- 每个新周期占 2 列：`{日期范围} 要务` 和 `retro`

## Step 3：确认内容

**若用户未提供本周计划，必须先问清楚：**

```
你好，请告诉我本周（{日期范围}）的要务内容：
1. 每条要务是一个有序列表项
2. MIT（最重要的事）用红色标注
3. 示例格式：
   - KR1: 完成 XXX 设计方案 [MIT]
   - KR2: 与 YYY 对齐需求
```

## Step 4：插入新列

⚠️ **写入操作前必须与用户确认列插入位置**

```bash
# 在最后一列之前插入"要务"列（column_index = 当前列数 - 1，即倒数第二位置）
# 通常 retro 和 要务 成对插入
lark-cli api PATCH "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/GkpXdEoafoGmABxeDMYcGWaMnmg" \
  --as user \
  --data '{"insert_table_column": {"column_index": N}}'

# 连续插入两列（先插 retro，再插 要务，保证顺序正确）
# 第一次：插入 retro 列（index N）
# 第二次：插入 要务 列（index N，retro 自动后移）
```

详见 [`references/weekly-table-api.md`](references/weekly-table-api.md) 中的完整 API 示例。

## Step 5：写入单元格内容

⚠️ **核心原则：必须用 block API 直接写入，禁止用 Markdown 模式写表格单元格（会丢失 callout、列表、颜色格式）**

```bash
# 写入表头（纯文本）
lark-cli api POST "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/{header_cell_id}/children" \
  --as user \
  --data '{"children": [{"block_type": 2, "text": {"elements": [{"text_run": {"content": "4.21-4.27 要务"}}], "style": {}}}], "index": 0}'

# 写入有序列表（KR 条目）
lark-cli api POST "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/{cell_id}/children" \
  --as user \
  --data '{
    "children": [
      {
        "block_type": 13,
        "ordered": {
          "elements": [
            {"text_run": {"content": "KR1: 任务内容"}},
            {"text_run": {"content": " MIT", "text_element_style": {"bold": true, "text_color": 1}}}
          ],
          "style": {}
        }
      }
    ],
    "index": 0
  }'
```

**block_type 对照：**
| 值 | 类型 |
|----|------|
| 2 | 普通文本段落 |
| 12 | 无序列表 |
| 13 | 有序列表 |
| 19 | Callout 高亮框 |
| 31 | 表格 |
| 32 | 表格单元格 |

**text_color 对照：**
| 值 | 颜色 |
|----|------|
| 1 | 红色（MIT 标注用） |
| 2 | 橙色 |
| 4 | 绿色 |
| 5 | 蓝色 |

## Step 6（可选）：柯维四象限分析

写入完成后，可调用 `quadrant-ii-time-management` Skill 对本周计划做象限诊断：

- Q1（重要+紧急）：当周必完成，MIT 候选
- Q2（重要+不紧急）：重点保护，不被 Q1 挤压
- Q3（紧急+不重要）：警惕；可否委托或拒绝？
- Q4（不重要+不紧急）：削减

输出建议格式：
```
## 四象限诊断（{日期范围}）

| 象限 | 任务 | 建议 |
|------|------|------|
| Q1 紧急+重要 | KR2: XXX | 本周必做 |
| Q2 重要不紧急 | KR1: YYY | 保护时间块 |
| Q3 紧急不重要 | 会议 ZZZ | 考虑委托 |

> 本周 Q2 占比：{N}%（建议 ≥ 60%）
```

## 权限表

| 操作 | 所需 scope |
|------|-----------|
| 读取文档 | `docx:document:readonly` |
| 写入文档（block API） | `docx:document` |

```bash
# 授权（如遇 Permission denied）
lark-cli auth login --scope "docx:document docx:document:readonly"
```

## 参考

- [weekly-table-api.md](references/weekly-table-api.md) — 表格 block API 完整示例
- [lark-shared](~/.agents/skills/lark-shared/SKILL.md) — 认证、权限
- [lark-doc](~/.agents/skills/lark-doc/SKILL.md) — 文档读写通用 skill
