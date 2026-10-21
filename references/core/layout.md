# Layout JSON（实验性，默认不用）

> **v1 立场**：当前版本 Layout 稳定性不足（坐标要手工换算、跨分辨率易错位、多框互相挤占），默认交付 caption。只有在「文字必须精确落位」时才考虑本节，并接受需要重试。

## 1. 结构

```json
{
  "summary": {
    "meta": ["poster"],
    "canvas": "single",
    "caption": "A minimalist travel poster with a cream background, a blue mountain illustration, and the title EXPLORE at the top."
  },
  "items": [
    {
      "label": "text",
      "caption": "Large dark-blue uppercase title centered at the top.",
      "text": "EXPLORE",
      "bbox": [-416, -384, -288, 384]
    },
    {
      "label": "object",
      "caption": "A flat blue mountain illustration in the lower center.",
      "bbox": [-192, -288, 384, 288]
    }
  ],
  "bbox_coord_space": "abs_centralized",
  "bbox_format": "yxyx"
}
```

| 字段 | 取值 | 说明 |
| :--- | :--- | :--- |
| `summary.caption` | 非空字符串 | 整体场景与风格。风格句、光线句写在这里 |
| `summary.meta` | 字符串数组 | 类型标签，如 `poster`、`screenshot` |
| `summary.canvas` | `single` / `multi_panel` / `collage` | 单画面 / 多分镜 / 拼贴 |
| `items[].label` | `object` / `character` / `text` | 只有这三种 |
| `items[].caption` | 非空字符串 | 该元素的外观；**不要写坐标与 JSON 说明** |
| `items[].text` | 字符串 | `label: "text"` 必填，要渲染的原文 |
| `items[].bbox` | 4 个数字 | `abs_centralized` + `yxyx` |
| `bbox_coord_space` | 固定 `"abs_centralized"` | 以画布中心为原点 |
| `bbox_format` | 固定 `"yxyx"` | `[y_min, x_min, y_max, x_max]` |

不要加 `children`、`parent`、`id`、`elements` 等字段——公开 schema 里没有，加了也不会被理解。

## 2. 坐标换算（没有脚本，只能手算）

官方规则：以画布中心为原点，x 向右、y 向下递增；把常规左上角原点的坐标分别减去 `W/2` 与 `H/2`。

```text
yxyx_centered = [y1 - H/2, x1 - W/2, y2 - H/2, x2 - W/2]
```

分数边缘：左上坐标向下取整（floor），右下坐标向上取整（ceil），保证宽高为正整数。

**看着官方示例反推一遍**（1024×1024，`W/2 = H/2 = 512`）：

| | 官方 centered `yxyx` | 减回去得到左上原点 `xyxy` |
| :--- | :--- | :--- |
| 标题 | `[-416, -384, -288, 384]` | x 128→896，y 96→224 |
| 山 | `[-192, -288, 384, 288]` | x 128→800，y 320→896 |

自己写的时候**先在纸上按左上原点画**，再套上面公式换算，不要边想边换——两套坐标系来回切是最常见的错。

## 3. 交付前校验

1. 宽高是 16 的正整数倍，且与生成时实际用的尺寸**一致**（尺寸写在提示词外面，生成参数里单独设）。
2. 每个框 `x1 < x2`、`y1 < y2`，且都在画布范围内。
3. 顺序是 `yxyx` 不是 `xyxy`，原点在中心不是左上角。
4. 一条提示词 = 一行 JSON（`json.dumps` 压缩后），Gradio 里直接粘贴、Python API 里作为字符串传入。
5. `label: "text"` 的项都有 `text` 字段，内容逐字正确、换行用 `\n`。
6. `caption` 里没有 bbox、坐标、字段名这类工具说明。

## 4. 何时值得试

| 值得 | 不值得 |
| :--- | :--- |
| 海报、封面、图内表格、UI 版面 | 普通人物图、风景、氛围图 |
| 多分镜漫画页（要格子边界） | 「画面很复杂」但并不需要控位 |
| 需要同类图批量复用同一版面 | 一张图里元素关系松散 |

常见失败模式与改法见 `diagnostics/troubleshooting.md`。
