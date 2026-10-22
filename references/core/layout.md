# Layout JSON（实验性，默认不用）

> **v1 立场**：当前版本 Layout 稳定性不足（坐标要换算成中心原点、跨分辨率易错位、多框互相挤占），默认交付 caption；只有文字必须精确落位时才用，并接受需要重试。

## 1. 结构

```json
{
  "summary": {"meta": ["poster"], "canvas": "single", "caption": "A minimalist travel poster with a cream background, a blue mountain illustration, and the title EXPLORE at the top."},
  "items": [
    {"label": "text", "caption": "Large dark-blue uppercase title centered at the top.", "text": "EXPLORE", "bbox": [-416, -384, -288, 384]},
    {"label": "object", "caption": "A flat blue mountain illustration in the lower center.", "bbox": [-192, -288, 384, 288]}
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
| `items[].tags`、`items[].palette`、`summary.palette` | 字符串数组，可选 | 仅见于上游 enhancer 的编译脚本，`USERGUIDE` 未记载；有用才加，效果【未验证】 |
| `bbox_coord_space` | 固定 `"abs_centralized"` | 以画布中心为原点 |
| `bbox_format` | 固定 `"yxyx"` | `[y_min, x_min, y_max, x_max]` |

不要加 `children`、`parent`、`id`、`elements` 等字段——公开 schema 里没有，加了也不会被理解（上游编译脚本遇到未知字段会直接报错）。

## 2. 坐标换算

**优先用上游脚本，不要手算。** 上游仓库自带 `skills/moss-image-prompt-enhancer/scripts/compile_prompt.py`：先写像素草稿（左上角原点、`[x_min,y_min,x_max,y_max]`、`bbox_coord_space:"abs"`、`bbox_format:"xyxy"`，外加顶层 `width`/`height`），脚本转成下面的中心原点 `yxyx` 整数坐标，并拒绝越界或非法框，不会静默裁剪。草稿格式是上游 skill 的内部约定，**不是**模型吃的格式，模型只吃编译后的那一行。

```bash
python compile_prompt.py draft.json --output prompt.txt
```

宽高必须是 16 的正整数倍；`width`/`height` 不进入编译结果，生成时要在提示词外单独填同样的尺寸。文字框用全局画布坐标，叠在物体上的文字也一样；框只是位置标注，不是要画出来的边框。

没有脚本环境时才手算（本 skill 不附带脚本），以画布中心为原点，x 向右、y 向下递增；把常规左上角原点的坐标分别减去 `W/2` 与 `H/2`：

```text
yxyx_centered = [y1 - H/2, x1 - W/2, y2 - H/2, x2 - W/2]
```

分数边缘：左上坐标向下取整（floor），右下坐标向上取整（ceil），保证宽高为正整数。按官方示例（1024×1024，`W/2 = H/2 = 512`）反推：

| | 官方 centered `yxyx` | 减回去得到左上原点 `xyxy` |
| :--- | :--- | :--- |
| 标题 | `[-416, -384, -288, 384]` | x 128→896，y 96→224 |
| 山 | `[-192, -288, 384, 288]` | x 128→800，y 320→896 |

## 3. 交付前校验

1. 宽高是 16 的正整数倍，且与生成时实际用的尺寸**一致**（尺寸写在提示词外面，生成参数里单独设）。
2. 每个框 `x1 < x2`、`y1 < y2`，且都在画布范围内。
3. 顺序是 `yxyx` 不是 `xyxy`，原点在中心不是左上角。
4. 一条提示词 = 一行 JSON（`json.dumps` 压缩后）；Gradio 里直接粘贴，Python API 里作为字符串传入。
5. `label: "text"` 的项都有 `text` 字段，内容逐字正确、换行用 `\n`。
6. `caption` 里没有 bbox、坐标、字段名这类工具说明。

## 4. 何时值得试

| 值得 | 不值得 |
| :--- | :--- |
| 海报、封面、图内表格、UI 版面 | 普通人物图、风景、氛围图 |
| 多分镜漫画页（要格子边界） | 「画面很复杂」但并不需要控位 |
| 需要同类图批量复用同一版面 | 一张图里元素关系松散 |

常见失败模式与改法见 `diagnostics/troubleshooting.md`。
