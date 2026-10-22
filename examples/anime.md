# 二次元通道示例

两例均为**示意稿**，按本 skill 规则编写，参数为档 Q 默认值。示例证明写法结构，不证明出图质量。

---

## 例 1：厚涂半身像（交付级）

**需求**：一张轻小说封面感的少女半身，冷色调，别画成塑料页游立绘。

**判据**：插画 → 二次元通道；要「完成度」→ 必须做主次分级（`styles/anime.md` §5）；冷色 → 色盘写 3 个色名并删正文冲突色词。

```text
【正面提示词】
High-taste 2D digital painting with selective focus: finely rendered luminous facial features and delicate hair strands, contrasted against expressive breathable painterly gouache brushwork on the clothing and a softly blurred background. Muted low-saturation palette of dusty blue, warm cream and desaturated terracotta. Zero rough sketch lines.
Medium close-up of a slender 17-year-old girl with balanced facial proportions — neither a big-headed child nor a mature adult — a softly tapered chin and a slender neck. Tilting her head slightly at a three-quarter angle, she gazes through half-lidded, languid grey eyes with quiet teenage aloofness. Soft blush on the nose tip, glossy pale lips.
Her silky ash-grey hair is pulled into slightly loose low twin buns with airy translucent wisps of bangs across her forehead; one hand rests on the collar of her coat, five distinct fingers visible.
She wears a plain matte navy wool coat with clean fabric blocks and no gaudy patterns, against a softly out-of-focus snow-covered courtyard at dusk.

【负面提示词】
worst quality, bad anatomy, watermark, jpeg artifact, blurry, out of focus, lowres, bad hands, extra fingers, fused fingers, deformed hands, distorted face, photorealistic, real human, photograph, camera flash, film grain, microscopic pores, 3d render, cgi, sketch, rough sketch, uncolored patches, thick black outlines, vector art, plastic skin, oversaturated neon colors, gaudy gold embroidery, oversized head, big round babyface, short stubby neck, wide-open staring eyes, flat chest

【采样参数】
1248×1248 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

**为什么这么写**

| 处理 | 依据 |
| :--- | :--- |
| 首句就做 `selective focus` 分级 | 笔触松紧若不限定部位会蔓延到脸（`styles/anime.md` §5） |
| 写 3 个色名 + `low-saturation` | 自然语言色盘替代 HEX（`styles/anime.md` §4） |
| `Zero rough sketch lines` | 防半成品草稿感 |
| 年龄双向排除，不写 `petite / loli` | 防成人化与幼化（`styles/photo.md` §5.1、`anime.md` §6） |
| 发髻写 `slightly loose` + 空气感碎发 | 避免两个黑球（`styles/anime.md` §5 规则 2） |
| 眼睛不写 `jewel-like, sparkling` | 防触发大头大眼幼态脸 |
| 衣服显式禁止刺绣 | 复杂花纹会抢注意力（`styles/anime.md` §5 规则 1） |
| 负面用二次元封杀组 | 含 `photorealistic, photograph, film grain, camera flash` |

**自检**：正文无毛孔/闪光灯/胶片词 ✓；负面无 `anime` ✓；色盘与正文无冲突色词 ✓；手部写明五指 ✓。

---

## 例 2：TV 动画截帧（快档）

**需求**：一张番剧正片截图，教室走廊，回头，底部有黄色字幕。

**判据**：要「播出截帧」不是「插画」→ 用版式容器反推画风（`styles/anime.md` §3）；有字幕 → 走 `core/text-in-image.md`，中文字数少、字幕区高度足够。

```text
【正面提示词】
anime screencap, TV anime broadcast screenshot, cel shading, flat anime coloring, crisp lineart, two flat tones per surface.
Medium shot of a 16-year-old girl in a navy school uniform standing in a classroom corridor, one hand on the door frame, looking back over her shoulder with a surprised expression, her mouth slightly open.
Late afternoon sunlight through the corridor windows casting parallel light bands across the floor, dust in the air, the far staircase softly out of focus.
At the bottom center, crisp yellow Chinese subtitle text with a black outline reading "等等！"

【负面提示词】
worst quality, bad anatomy, jpeg artifact, blurry, out of focus, lowres, bad hands, extra fingers, fused fingers, distorted face, photorealistic, real human, photograph, camera flash, film grain, microscopic pores, 3d render, cgi, sketch, rough sketch, uncolored patches, thick black outlines, vector art, plastic skin, oversaturated neon colors, oversized head, big round babyface, wide-open staring eyes

【采样参数】
1024×1024 / Steps 30 / CFG 3.0 / Shift 5.0 / Euler / SLG 关（档 R） / Seed 随机

【换算】
屏幕字幕属于「中等字号」：1024×1024 下字幕区高约 80px、单行 3 个汉字 → 字高约 60px，远高于 24px 阈值，档 R 也能读。
```

**为什么这么写**

| 处理 | 依据 |
| :--- | :--- |
| 开头 `anime screencap + cel shading + flat coloring` | 画种词整组替换，不零散混搭（`styles/anime.md` §2） |
| 不写「插画感」相关词 | 版式容器与画种词必须同向 |
| 字幕用引号 + 明确方位 | 图内文字基本写法（`core/text-in-image.md` §1） |
| 字幕只 3 个字 | 短文案正确率最高 |
| 负面去掉 `text` 与 `watermark` | 这两个词会把字幕一起压掉（`core/negative.md` §2） |
| 档 R 但保留 `five distinct fingers` 类防崩 | 低步数下手最先崩（`styles/anime.md` §9） |

**自检**：画种词与负面互斥 ✓；字幕字高 ≥ 40px ✓；负面未含 `text / watermark / speech bubble` ✓；档位与规则档匹配（未堆 Q 档精修词）✓。

---
