# 通道 B：二次元插画

## 1. 何时走这条
动漫插画、TV 动画截帧、Galgame CG、漫画、轻小说封面、二次元海报、角色设定图、Q 版。关键前提：**主体描述保持「画风中立」**——不写毛孔、闪光灯、胶片颗粒、真实皮肤；一旦出现写实质感词，后面再怎么写画种词也拉不回来。

## 2. 通道一：画种与技法词
在正面提示词**开头**放一组画种/年代/技法词，能直接切换整张图的美术方向。选一组，不要跨组混搭。

| 风格 | 开头词组 | 必须同时做的删改 |
| :--- | :--- | :--- |
| 90s 复古赛璐璐 OVA | `1990s (style), retro artstyle, anime screencap, cel shading, hand-painted cel animation, VHS color bleed` | 删掉 `painterly, painterly gouache, soft blending` |
| 黑白漫画网点 | `manga page, monochrome, greyscale, screentones, inked lineart, bold black ink outlines, pen crosshatching` | **删掉正文所有具体颜色词**（`red, silver, navy`…），否则会变局部留色漫画 |
| 透明水彩 | `watercolor (medium), traditional media, ink and wash, soft pigment bleed on rough cold-press paper` | 删掉 `flat color, crisp vector` |
| 扁平矢量波普 | `flat color, vector illustration, bold thick colored outlines, hard geometric cel shading, pop palette` | 删掉 `gradient, airbrush, soft shading` |
| 厚涂刮刀 | `impasto, oil painting (medium), heavy visible brushstrokes, thick palette knife texture, painterly lineless` | 删掉 `black outlines, lineart` |
| 动画原画手稿 | `anime genga, production art, rough pencil sketch, uncolored layout sheet, blue and red construction lines on paper` | 删掉所有上色词 |
| Q 版 | `chibi, super deformed, 2-head-tall proportions, oversized head, tiny body, bold outlines` | 删掉写实比例词（`7.5-head-tall` 之类） |
| 浮世绘 / 日本画 | `ukiyo-e, traditional Japanese woodblock print, nihonga, flat mineral pigments on aged washi, sumi ink contours` | — |
| PC-98 像素 | `pixel art, 16-bit PC-98 adventure game graphic, visible square pixel grid, checkerboard dithering, limited palette` | 删掉 `smooth, gradient` |
| 无描边粉彩 | `lineless anime illustration, soft oil pastel on rough paper, no black outlines, grainy chalk texture` | 删掉 `lineart, ink` |
| 水墨重彩 | `Chinese wild ink and wash painting, dry-brush sumi outlines with flying-white texture, splashed ink over mineral cinnabar and indigo on yellowed xuan paper` | — |

`[Q,R]` 画种词属于「开头词组」，两档都生效；但档 R 下笔触类细节（网点、像素格）更容易糊。

## 3. 通道二：用版式容器反推画风
写出容器 + 容器里的文字，带出对应的整体画风。

| 目标画风 | 开头 | 结尾的容器句 |
| :--- | :--- | :--- |
| Galgame / 视觉小说 CG | `visual novel cg, Japanese galgame screenshot, glossy anime coloring` | `At the bottom of the frame, a semi-transparent dark-blue dialogue box with a pink nameplate reading "葵" and crisp white text reading "……你终于来了。"` |
| TV 动画正片截帧 | `anime screencap, TV anime broadcast screenshot, cel shading, flat anime coloring` | `At the bottom center, crisp yellow subtitle text with a black outline reading "别回头。"` |
| 角色设定集 | `anime character reference sheet, official design sheet on clean white background, multiple views` | `full-body front view plus three expression headshots, clean cel-shaded lineart, a row of color swatches at the bottom` |
| 集换式卡牌 | `SSR anime trading card, ornate golden holographic frame border, dazzling illustration` | `a top title bar reading "苍之骑士", five gold stars at the top right, a bottom stat box reading "ATK 2500 / DEF 2100"` |

## 4. 通道三：配色
- 官方支持 `items[].palette` / `summary.palette` 的 HEX 数组，但这属于 Layout 通道，当前版本不稳定（见 `core/layout.md`）。
- **降级做法**：用自然语言写色盘，比给 HEX 更稳——3~4 个色名 + 明度饱和度形容词（`muted, low-saturation, dusty, deep`），**删掉正文里与之冲突的具体颜色词**，收尾留一句 `dominated strictly by this palette`：
```text
Muted, sophisticated low-saturation palette of dusty blue, warm cream and desaturated terracotta.
```

## 5. 完成度：主次分级
二次元最容易出两种废图：**半成品草稿**（笔触松到脸上）和**塑料页游立绘**（全图过度锐化）。把「精修」和「松弛」分配到不同部位，四段骨架可直接抄、替换方括号：
```text
<|artist|>[画师触发词，无则整行删除]<|/artist|>
<|style_and_aesthetic|>High-taste 2D digital painting with selective focus: finely rendered luminous facial features and delicate hair strands, contrasted against expressive breathable painterly gouache brushwork on the clothing and a softly blurred background. Muted low-saturation palette of [2~3 色名]. Zero rough sketch lines.<|/style_and_aesthetic|>
<|teenage_girl_aura|>[景别] of a slender [年龄] girl with balanced facial proportions, a softly tapered chin and a slender neck. [头颈微动态], she gazes with [眼神]. Soft blush on the nose tip and cheeks, glossy pale lips.<|/teenage_girl_aura|>
<|hair_and_pose|>Her silky [发色] hair styled into [发型，加 slightly loose / airy translucent wisps], [手部与道具的简洁动作].<|/hair_and_pose|>
<|outfit_and_background|>She wears [服装，加 clean matte fabric blocks, without gaudy patterns], set against a softly out-of-focus [背景].<|/outfit_and_background|>
```
`<|xxx|>` 闭合标签是**社区写法**，不在官方文档里；用之前自己 A/B 一次，判据：同一 seed 下脸是否更稳、特征是否串味。

四段骨架的三条规则：
1. **不要往衣服上加复杂花纹**：`golden floral embroidery` 会分走注意力，写 `without gaudy embroidery, plain matte borders`，大色块更干净。
2. **发髻/丸子头写「微松」**：`neat round twin buns` → 两个黑球；`slightly loose round buns with airy translucent wisps` → 有层次的头发。
3. **眼睛不写 `jewel-like, sparkling, ultra detailed`**：会触发大头大眼的幼态脸型，写 `luminous, water-clear eyes with soft highlights`。

## 6. 主体控制
- 年龄同样要双向排除（见 `styles/photo.md` §5.1），只是把词换成二次元口径：`neither a big-headed 10-year-old child nor a mature 20-year-old woman`。
- 脸靠**三个锚点**：`softly tapered chin`、`slender neck`、`half-lidded, languid`。
- 头发同理：`slightly loose`、`airy translucent wisps`、`loose flyaway strands` 是这个通道的通用补丁。
- 手：`relaxed hands with five distinct fingers, natural knuckles`；手部是二次元最先崩的部位。

## 7. 画师与 LoRA
- **tag 串形式**里有 Artist 位：`Quality -> Score -> Meta -> Year -> Character -> Series -> Artist -> General`，官方示例用了 `@foo bar` 这种写法。
- **散文形式**里写画师名 / `XXX style` 效果很弱：训练 caption 由 VLM 重新生成，规范只描述可见信息（`[推断]`，见 `diagnostics/sources.md`）。
- 想稳定拿到某个画师的笔触只有两条路：① 用别人训好的 LoRA；② 自己训 LoRA（官方要求：训 LoRA 时**冻结 Text Encoder**）。
- 触发词格式由**该 LoRA 的作者**定义，常见形如 `<|artist|>fkey<|/artist|>`，写在正面提示词第一行、不加空格不加句号；强度按作者建议（常见 0.4~0.8），用之前看模型卡。
- 不用零碎几何词硬凑画师手癖（`四角星高光 + 斜杠腮红 + 贴纸白边`），会机械拼贴出一张拼图脸。

## 8. 母版
### 母版 D：厚涂半身像（交付级，档 Q）
```text
High-taste 2D digital painting with selective focus: finely rendered luminous facial features, delicate hair strands, expressive breathable painterly gouache brushwork on the clothing, softly blurred background. Muted low-saturation palette of dusty blue, warm cream and desaturated terracotta. Zero rough sketch lines.
Medium close-up of a slender 17-year-old girl with balanced facial proportions, a softly tapered chin, a slender neck. Tilting her head slightly at a three-quarter angle, she gazes through half-lidded, languid hazel eyes with quiet teenage aloofness. Soft blush on the nose tip, glossy pale lips.
Her silky dark-chestnut hair is pulled into slightly loose low twin buns with airy translucent wisps of bangs across her forehead; one hand rests on the collar of her coat.
She wears a plain matte navy wool coat with clean fabric blocks and no gaudy patterns, against a softly out-of-focus snow-covered courtyard at dusk.
```
负面用 `negative.md` 的 L0 + L1 + 二次元 L2 + `oversized head, big round babyface, short stubby neck, wide-open staring eyes, flat chest, plastic skin, oversaturated neon colors, gaudy gold embroidery, thick black outlines`。

### 母版 E：TV 动画截帧（快档，档 R 或 Q）
```text
anime screencap, TV anime broadcast screenshot, cel shading, flat anime coloring, crisp lineart.
Medium shot of a 16-year-old girl in a school uniform standing in a classroom corridor, one hand on the door frame, looking back over her shoulder with a surprised expression, two-tone flat shadows.
Late afternoon sunlight through the windows, warm dust in the air.
At the bottom center, crisp yellow subtitle text with a black outline reading "等等！"
```

## 9. 这条通道的专有坑
- **写实词残留**：`microscopic pores, camera flash, film grain, unretouched` 任一残留都会把画面推回照片，必须全删；**黑白漫画不删颜色词** → 局部留色。
- **`cel shading` 单独一个词切不动画风**：正文还挂着 150 词写实毛孔描述时全被压制，要么整套换，要么不换。
- **小分镜里不写 `petite, child, little, 10-year-old`**，哪怕是否定式（`neither a 10-year-old`）也会被抽出来用；换 `slender, tall, teenage`。
- **Q 版通道不混入正常比例的全身描述**，否则会出半 Q 半正常。
- **`[R]` 档**：手指、双眼对称、发丝层次最先崩，务必补 `relaxed hands with five distinct fingers`、`symmetrical eyes`、`delicate hair strands in sharp focus`。
- **`[Q]` 档**：开着 SLG 时不要堆 `ultra detailed, intricate`，会把边缘拉硬。
