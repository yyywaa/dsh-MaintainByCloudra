---
name: office-layout-fix
description: "Use when a finished Word or PowerPoint deliverable looks wrong: title wraps to two lines, a large blank band at the bottom of a page, an extra blank page appears, page numbers start or restart wrongly, a replaced image stretches, or the layout \"doesn't match the official template\"."
whenToUse: 用户说排版不对、不对齐、下面空一大块、多出空页、页码不对、图和题注对不上、和模板不一样，或在替换文档内嵌图片之后。
---

# 修 Office 成品的排版问题

先量，再改；改完必须重新渲染验证。观感判断不可靠。

## 三条铁律

1. **先渲染再看**：`office-export-pdf` + `office-render`，不要凭 XML 或观感下结论。
2. **改完必须复测同一指标**（页底空白、页数、折行），不要"改完就宣称好了"。
3. **一次只动一个变量**：同时缩图 + 压行距，出了问题分不清是谁导致的。

## 症状 → 根因 → 修法

| 症状 | 根因 | 修法 |
| --- | --- | --- |
| 页底空一大块（20%+） | 后面那张内嵌图 + 题注塞不进剩余高度，整块跳到下一页 | 按版心剩余高度把这张图等比缩小（改 `wp:extent` 或 inline shape 的宽高）；不要压行距 |
| 压了行距反而更多页、更多空洞 | 文字缩短后图重新挪位，制造新的空洞 | 回退行距改动，只缩图 |
| 多出空白页 | 表格后面挂着的空段落（LibreOffice 不占位，Word 会挤出一页） | 把尾部空段落设成 1pt 字号 + 固定 1pt 行距 + 段前段后 0 |
| 标题被挤成两行 | 标题框宽度不够；`wrap=none` + `SHAPE_TO_FIT_TEXT` 在 LibreOffice 下照样折行 | 统一把页眉标题框加宽（如 14.2in）、`word_wrap=False`、`auto_size=NONE` |
| 页码从头接着算 / 提取正文后序号乱 | 多节文档共用连续页码 | 在目标节的 `sectPr` 里加 `<w:pgNumType w:start="1"/>`；提取正文时先删掉前置内容再设 |
| 换进去的图被拉伸 | 直接把新图塞进 `word/media/`，没按显示框比例裁 | 按 `wp:extent` 的 cx/cy 裁图（截图一般裁顶部白边），再替换部件 |
| 参考文献出现巨大字距洞 | 段落两端对齐 + 长 URL | 参考文献段落改左对齐 |
| 某段正文把整页顶出空洞 | 正文误用了标题样式（长文本 + keep_with_next） | 改回正文样式，清掉直接格式 |

## 工具

仓库 `dsh-MaintainByCloudra/scripts/office_patch.py`：`swap-docx-image`（按比例换图）、`fit-pptx-titles`（批量加宽标题框）。两个都支持 `--dry-run`。

## 量页底空白（验证用）

```python
from PIL import Image
import numpy as np
TEXT_BOTTOM = 1518          # 版心下边界像素，按渲染 DPI 换算
a = np.array(Image.open(png).convert("L"))[:1500, :]   # 排除页脚
rows = np.where((a < 200).sum(axis=1) > 2)[0]
print(TEXT_BOTTOM - (rows.max() if len(rows) else 0))
```

## 两个会静默咬人的坑

- **LibreOffice Kit `convert` 不会覆盖已存在的输出**：目标存在时报 `EEXIST` 且不写文件，后面的渲染会读到旧 PDF。每次先删输出，再检查文件是否真的生成。
- **字体缺失**：`missingFonts` 非空时 PDF 用的是替代字体（如 `仿宋_GB2312`、`方正小标宋简体`、`楷体_GB2312`）。正式打印要在装了这些字体的 Windows 上重导，或明确告诉用户后果。

## 对齐"官方模板"时

不要凭观感。直接读模板里目标段落的属性：`w:rFonts` 的 `eastAsia`、字号、`w:b`、`first_line_indent`（通常 2 字 = 2×字号）、`line_spacing`（多为固定 `31pt`）、对齐方式。再把同属性套到你的段落上，逐项核对后渲染比对。
