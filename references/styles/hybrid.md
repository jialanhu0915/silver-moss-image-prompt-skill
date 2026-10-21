# 通道 C：混合风格

混合不是「写实和二次元各写一半」，那样只会得到两套光照打架的中间态；融合手段没写，模型就自己选最省事的那种：剪贴画白边、正中一条分镜线，或整图退化成厚涂。必须先回答三个问题：
1. **谁是主体**——决定语言主干用哪种描述习惯、负面词封杀哪一边。
2. **靠什么融合**——光影合成、描边统一、调色统一、介质叠加、还是硬分屏线。
3. **边界在哪**——转换点必须写出来（哪一侧是 2D、哪一层是实拍、分界线在画面什么位置）。

## 1. 四类混合
| 类型 | 构成 | 融合手段 | 失败时会变成 |
| :--- | :--- | :--- | :--- |
| **跨次元合成** | 2D 动漫角色 + 实拍 3D 场景 | 光影合成（角色接受环境光、投影落在实景上） | 贴纸感 / 白边剪贴 / 角色被画成真人 |
| **三渲二** | 3D 结构 + 2D 描边与平涂 | toon 着色 + 描边 pass + 单一硬光源 | 塑料 PBR 人偶 / 廉价游戏建模 |
| **媒介叠合** | 照片底 + 手绘/印刷/拼贴层 | 介质顺序 + 叠加痕迹（纸边、网点、胶带、马克笔） | 只是「加了脏点的照片」 |
| **同图双画风** | 同一画面里两种画种 | 明确的硬分界线 + 两侧各自锁死 | 两风格互相渗透、中间长出渐变带 |

## 2. 跨次元：2D 角色进实景
写作顺序固定，**不要分块**（分成两个 `<|...|>` 块会让模型在画面正中切一条分镜线）：
```text
1. 先写实景：光线方向与色温、镜头与景深、景深落点
2. 再写角色：2D 画风与上色方式、线条、比例
3. 最后一句写合成关系：谁接受谁的光、投影落在哪
```
### 2.1 三种上色浓度
| 档 | 关键句 | 效果 |
| :--- | :--- | :--- |
| 清透淡彩（主力） | `flat 2D cel-shaded anime character with crisp ink outlines and minimal single-layer shading, warm sunlight rim-lighting and ambient color bleed across her lines` | 角色保持 2D，但被真实环境光浸染，最不突兀 |
| 纯白描速写 | `minimal pencil lineart, single-layer shadow only, no color fill, real sunset rim light catching the line edges` | 白描人站在真实场景里，靠光线缝合 |
| 暖金浸染 | `simple sketched lines flooded by warm golden hour ambient color, the drawing's paper tone shifting to the scene's palette` | 强风格化，适合氛围图 |

### 2.2 四个高频事故
| 事故 | 原因 | 改法 |
| :--- | :--- | :--- |
| 白边剪贴感 | 没有接触阴影与投影，角色像后贴上去的 | 写 `a soft shadow cast by her feet onto the real ground`；负面加 `white outline, sticker, cut-out edge` |
| 角色被画成真人 | 近景时写实词先出现，注意力把角色推向照片 | 句首明写 `2D anime girl composited into a photoreal scene`，并写 `clear 2D profile line and bright anime eyes`；删掉全身/远机位词，防镜头被拉远 |
| 腿部被拉成超模比例 | 写实镜头词默认写真人身高 | 写 `chibi-ish 6-head-tall proportions` 或 `petite 150cm proportions, short limbs`，负面加 `long legs, fashion model proportions` |
| 角色自带一套光源 | 只写角色光、没写场景光 | 只写一套光，然后写 `her shading follows the same light direction as the room` |

### 2.3 母版（跨次元）
```text
Warm late-afternoon sunlight rakes through a cafe window from the left, 35mm look, shallow depth of field on the foreground table.
A flat 2D cel-shaded anime girl with crisp black ink outlines, minimal single-layer shading and a simple round face sits at the real wooden table, holding a real ceramic cup with both sketched hands.
The room's warm light falls across her flat-color skin, a soft shadow from her sketched body lands on the real tabletop, and the ambient amber tone bleeds into her line edges so she settles into the scene.
Photoreal wooden grain and ceramic glaze in the same frame, no white outline around her.
```
## 3. 三渲二：3D 结构 + 2D 表现
把两件事分开：结构交给 3D 语言，表面交给 2D 语言；写 `3D render` + `realistic materials` 会得到手游广告里的塑料人偶，核心是**拒绝 PBR**。

| 要写 | 别写 |
| :--- | :--- |
| `3D base geometry with a toon shader, two flat tones per surface, hard-edged shadow terminator` | `subsurface scattering`、`ray tracing`、`physically based rendering` |
| `crisp outline pass on the silhouette only, no internal outlines` | `thick black outlines everywhere`（会糊成漫画） |
| `single hard key light from the upper left, ambient occlusion only at contact points` | 多光源布置（toon 着色下会出脏块） |
| `matte flat colors, no specular highlights on the skin` | `glossy skin, specular sheen`（立刻变塑料人偶） |
母版：
```text
3D base geometry rendered with a toon shader, two flat tones per surface, hard shadow terminator, crisp outline pass on the silhouette only.
A young woman stands in a rain-soaked alley, single hard key light from the upper left, matte flat colors with no specular highlights on her skin, ambient occlusion only where her boots meet the wet ground.
Rain rendered as simple white streaks, puddle reflections flattened into solid light shapes.
```

## 4. 媒介叠合：照片底 + 手绘/印刷层
写清**介质顺序与叠加痕迹**：先写底（照片或印刷品），再写叠加层，最后写它们之间的物理关系（在表面、有厚度、压出阴影）；只写「拼贴」会得到一张普通照片。

| 手法 | 可抄短语 | 痕迹要点 |
| :--- | :--- | :--- |
| 撕纸拼贴 | `torn magazine cut-outs collaged over a photograph, visible white paper fibers along the torn edges, small pieces of yellowed tape at the corners` | 纸边纤维、胶带、轻微翘起的投影 |
| 照片上手绘 | `hand-drawn marker scribbles and arrows drawn directly over the photo, the ink sitting on the glossy surface with a faint sheen` | 墨在表面上而非融进画面 |
| 网点/半调叠印 | `a coarse halftone dot pattern printed over the photograph, slight misregistration of cyan and magenta` | 网点可见、套印错位 |
| 版画 + 照片 | `risograph-style duotone print of the scene, grain and roller marks, two-color overprint` | 双色、滚筒痕、颗粒 |
| 屏幕翻拍 + 涂鸦 | `a photo of a screen with marker annotations, moiré bands and a soft room reflection across the glass` | 摩尔纹、反光、像素网格 |
## 5. 同图双画风
这是**唯一鼓励分块**的场景。
- 分界线要写形状与位置：`a hard vertical split exactly at the center line`、`a diagonal tear from bottom-left to top-right`；两侧各自锁死画种：`the left half strictly a monochrome screentone manga panel` / `the right half strictly a full-color oil painting`。
- 主体跨线时明确哪一半用哪种处理：`her face crosses the line, the left half of her face drawn in ink screentone, the right half in oil color`；负面必须封渗透：`style bleeding, gradient between styles, blended styles, half-colored`；**不要**在跨次元合成里用这套分块——那会切出分镜线（见 §2）。

## 6. 混合通道的负面词
混合时**不能把两套 L2 封杀组都打开**：写实的 `anime, 2d, illustration` 会杀掉你要的 2D 角色，二次元的 `photorealistic, photograph, film grain` 会杀掉你要的实景。只封杀你不想要的**第三态**：
```text
nsfw, worst quality, bad anatomy, watermark, jpeg artifact,
white outline, sticker edge, cut-out edge, pasted-on look,
style bleeding, gradient between styles, blended styles,
plastic skin, 3d render, cgi, doll,
blurry, out of focus, lowres, bad hands, extra fingers, fused fingers
```
三渲二额外封：`photorealistic skin, subsurface scattering, glossy plastic, toy figure`；同图双画风额外封：`half-colored, smeared transition, airbrushed blend`。

## 7. 混合通道的自检
1. 三问都答了吗——谁主体、靠什么融合、边界在哪？是否只写了一套光？两套方向不同的主光会互相抵消。
2. 跨次元里有没有写「接触阴影」和「环境光溢色」？缺这两个必出贴纸感。
3. 负面是不是只封杀了第三态？同图双画风以外，是否误用了分块标签？
