# Weekly 表格 Block API 参考

## 文档信息

| 字段 | 值 |
|------|-----|
| 文档 token | `MDladM2GtotiM6xwEKecTMOinph` |
| Q2 🐶 表格 block_id | `GkpXdEoafoGmABxeDMYcGWaMnmg` |

---

## 1. 获取表格结构

```bash
lark-cli api GET "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/GkpXdEoafoGmABxeDMYcGWaMnmg" \
  --as user
```

返回中关键字段：
- `table.cells`：所有单元格 block_id 的平铺数组
- `table.property.column_size`：当前列数
- `table.property.row_size`：当前行数
- 单元格定位：`cells[row * column_size + col]`

---

## 2. 插入新列（成对插入：要务 + retro）

**顺序很重要**：先插 retro，再插 要务。这样最终顺序是：... | 要务 | retro |

```bash
# Step A：插入 retro 列（在当前末尾，index = column_size）
lark-cli api PATCH "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/GkpXdEoafoGmABxeDMYcGWaMnmg" \
  --as user \
  --data '{"insert_table_column": {"column_index": CURRENT_COL_COUNT}}'

# Step B：插入 要务 列（紧接在 retro 前，index = column_size，retro 自动右移）
lark-cli api PATCH "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/GkpXdEoafoGmABxeDMYcGWaMnmg" \
  --as user \
  --data '{"insert_table_column": {"column_index": CURRENT_COL_COUNT}}'
```

插入后重新 GET 表格结构，拿到新的 `cells` 数组。

---

## 3. 写入表头（纯文本）

```bash
# 要务列表头
lark-cli api POST "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/{HEADER_CELL_ID}/children" \
  --as user \
  --data '{
    "children": [
      {
        "block_type": 2,
        "text": {
          "elements": [{"text_run": {"content": "4.21-4.27 要务"}}],
          "style": {}
        }
      }
    ],
    "index": 0
  }'

# retro 列表头
lark-cli api POST "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/{RETRO_HEADER_CELL_ID}/children" \
  --as user \
  --data '{
    "children": [
      {
        "block_type": 2,
        "text": {
          "elements": [{"text_run": {"content": "retro"}}],
          "style": {}
        }
      }
    ],
    "index": 0
  }'
```

---

## 4. 写入有序列表（含 MIT 红色标注）

每个 KR 条目是一个 `block_type: 13`（有序列表）block。MIT 用红色 `text_color: 1` 标注。

```bash
# 单条 KR（无 MIT）
lark-cli api POST "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/{CELL_ID}/children" \
  --as user \
  --data '{
    "children": [
      {
        "block_type": 13,
        "ordered": {
          "elements": [
            {"text_run": {"content": "KR1: 任务内容描述"}}
          ],
          "style": {}
        }
      }
    ],
    "index": 0
  }'

# 含 MIT 红色标注的 KR（text_color: 1 = 红色）
lark-cli api POST "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/{CELL_ID}/children" \
  --as user \
  --data '{
    "children": [
      {
        "block_type": 13,
        "ordered": {
          "elements": [
            {"text_run": {"content": "KR2: 最重要的任务"}},
            {"text_run": {"content": " MIT", "text_element_style": {"bold": true, "text_color": 1}}}
          ],
          "style": {}
        }
      }
    ],
    "index": 0
  }'
```

多条 KR：在同一个 `children` 数组中追加多个 block，或分多次 POST（`index` 递增）。

---

## 5. 写入 Callout（高亮框）

```bash
lark-cli api POST "/open-apis/docx/v1/documents/MDladM2GtotiM6xwEKecTMOinph/blocks/{CELL_ID}/children" \
  --as user \
  --data '{
    "children": [
      {
        "block_type": 19,
        "callout": {
          "callout_background_color": 1,
          "border_color": 1,
          "emoji_id": "dog",
          "children": [
            {
              "block_type": 2,
              "text": {
                "elements": [{"text_run": {"content": "callout 内容"}}],
                "style": {}
              }
            }
          ]
        }
      }
    ],
    "index": 0
  }'
```

---

## 单元格行列索引速查

表格结构（根据实际读取结果更新）：
- 行 0：表头（🐶 | 任务 | MIT | W1 要务 | W1 retro | ...）
- 行 1+：各 KR 行（KR1、KR2、KR3 ...）

```
cell_id = cells[row * column_size + col]
```

例：第 2 行、第 5 列（从 0 开始）：`cells[2 * total_cols + 5]`

---

## 常见错误

| 错误 | 原因 | 解决 |
|------|------|------|
| 单元格内容只显示纯文本，格式丢失 | 用了 Markdown 模式写入 | 改用本文档的 block API |
| `404 block not found` | cell_id 取错 | 重新 GET 表格拿最新 cells 数组 |
| `insert_table_column` 无效 | PATCH 方法用错 | 确认是 PATCH，data 是 JSON object |
| 列插入顺序错误 | 先插了 要务 | 必须先插 retro，再插 要务 |
