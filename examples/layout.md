# Layout 示例（实验性，未验证出图）

本例演示草稿格式与坐标转换，**没有提交给 MOSS-Image 生成图片**，不证明文字渲染或版面质量；验证状态见文末。

## 需求

方形茶品海报：左下放陶壶，上方标题，右下两行副标题。画布 `1024×1024`。

## 可编辑草稿

使用上游编译草稿格式：左上角原点、`xyxy`、顶层宽高。`bbox` 顺序是 `[x_min, y_min, x_max, y_max]`。

```json
{
  "width": 1024,
  "height": 1024,
  "bbox_coord_space": "abs",
  "bbox_format": "xyxy",
  "summary": {
    "meta": ["poster", "product photography"],
    "canvas": "single",
    "caption": "A square minimalist tea poster on warm ivory paper. A handmade ceramic teapot sits in the lower-left area under soft window light; dark-green typography occupies the clear upper band and lower-right corner. Calm editorial styling, tactile glaze and subtle paper grain."
  },
  "items": [
    {
      "label": "object",
      "caption": "A small cream ceramic teapot with a rounded handle, subtle speckled glaze and a soft contact shadow, viewed at a three-quarter angle.",
      "bbox": [96, 280, 584, 896]
    },
    {
      "label": "text",
      "caption": "Large dark-green uppercase sans-serif title, centered in the upper band with generous letter spacing.",
      "text": "MORNING TEA",
      "bbox": [96, 96, 928, 232]
    },
    {
      "label": "text",
      "caption": "Small dark-green subtitle in two short lines, right-aligned in the lower-right corner.",
      "text": "A quiet\nstart",
      "bbox": [650, 800, 930, 930]
    }
  ]
}
```

## 编译

从 MOSS-Image 仓库根目录运行上游脚本；将草稿另存为 `draft.json`：

```powershell
python skills/moss-image-prompt-enhancer/scripts/compile_prompt.py draft.json --output prompt.txt
```

## 编译结果

以下单行 JSON 可粘贴到 MOSS-Image 正向提示词中。生成参数在提示词外设置为 `1024×1024`。

```json
{"summary":{"meta":["poster","product photography"],"canvas":"single","caption":"A square minimalist tea poster on warm ivory paper. A handmade ceramic teapot sits in the lower-left area under soft window light; dark-green typography occupies the clear upper band and lower-right corner. Calm editorial styling, tactile glaze and subtle paper grain."},"items":[{"label":"object","caption":"A small cream ceramic teapot with a rounded handle, subtle speckled glaze and a soft contact shadow, viewed at a three-quarter angle.","bbox":[-232,-416,384,72]},{"label":"text","caption":"Large dark-green uppercase sans-serif title, centered in the upper band with generous letter spacing.","text":"MORNING TEA","bbox":[-416,-416,-280,416]},{"label":"text","caption":"Small dark-green subtitle in two short lines, right-aligned in the lower-right corner.","text":"A quiet\nstart","bbox":[288,138,418,418]}],"bbox_coord_space":"abs_centralized","bbox_format":"yxyx"}
```

## 负面提示词与采样参数

Layout 只替换正向提示词，负面与参数照常交付。有图内文字，所以负面按 `core/negative.md` §2 去掉 `watermark` 和 `text`；中等字号标题，按 `core/params.md` §4 走档 Q。

```text
worst quality, bad anatomy, jpeg artifact, blurry, out of focus, lowres, anime, 2d, illustration, cel shading, painting, 3d render, cgi, digital art
```

```text
1024×1024 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

## 本次验证

- 副标题框原先落在右侧中部（y 340–520），与「右下角」的描述不符，已改为 `[650,800,930,930]`。编译器只检查语法和边界，查不出这类位置与描述的不一致，需要人工对照。
- 当前示例的编译结果由手算得出（`y−H/2`、`x−W/2`，整数边），**尚未用上游脚本编译**。
- MOSS-Image 实际出图：**未测试**。
