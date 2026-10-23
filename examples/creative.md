# 创意走查三例

三例都按 `references/creative/concept.md` 的流程写：判模式 → 固化约束 → 定主题三角 → 选一条机制 → 过淘汰判据 → 计价执行预算 → 编译成 caption。

例 1、例 2 的提示词**未出图**；例 3 的「改前」是你实际跑过的版本，「改后」未出图。三例都不构成效果保证。

---

## 例 1：需求粗略 → 增强模式

**需求**：「一个女孩在图书馆看书。」

**判据**：给了主体和场景类型，画面其余全空 → 增强模式；写实通道（默认真人题材）。可改场景关系与光，不可改「图书馆」「看书」这两个核心。

**主题三角**：用途偏叙事插画 / 公众号配图；情绪是安静但不温馨；第一眼要记住「光只存在于一圈里」。

**机制**：时间凝固——翻页的手停在半页，光圈边缘把书架竖线切断。支撑细节只取两件：尘埃穿过光束、光圈外的黑。

```text
【正面提示词】
A single handheld phone torch is the only light in a closed university library at night, its hard circular pool cutting the vertical lines of the book stacks off at the edge, 35mm at eye level from a low seated position, the nearest shelf edge black and out of focus.
A 21-year-old woman sits on the floor with her back against a shelf, a hardback open across her knees, one finger stopped on the corner of a page she has not turned yet, her face lit from below by the torch in her other hand.
Beyond the pool the aisles fall into complete darkness, a few dust motes drifting through the beam; the floor shows scuffed linoleum and a dropped pencil just inside the light.
Real shadow falloff, faint sensor noise in the blacks, zero fill light.

【负面提示词】
worst quality, bad anatomy, watermark, jpeg artifact, blurry, out of focus, lowres, bad hands, extra fingers, fused fingers, deformed hands, distorted face, anime, 2d, illustration, cel shading, 3d render, cgi, doll, plastic skin, cosplay, wig, flat front lighting, evenly lit skin, overexposed skin, studio fill light, second light source, evenly lit background, lens flare, light leak

【采样参数】
1024×1536 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

**为什么这么写**

| 处理 | 依据 |
| :--- | :--- |
| 把「看书」升级成「停在半页」的瞬间，而不是加更多道具 | 改关系而非加装饰（`concept.md` §6） |
| 光源只有一个，且写明它切断了什么 | 光圈边缘才是这张图的边界（`concept.md` §5 时间凝固） |
| 只留两件支撑细节：尘埃、铅笔 | 主焦点之外的一切都在解释「光圈之外什么都没有」 |
| 负面追加 `second light source` | 双光源会把黑吃成灰（`concept.md` §8 落地三件套） |
| 不写「孤独」「安静」 | 抽象词不进 caption（`craft/aesthetics.md` §9） |

**自检**：一句话说得出（「只有一圈光存在，其余书库退回黑暗」）✓；主焦点一个（她 + 光圈）✓；不可能元素无（这套是现实光线，不需要落地三件套）✓。

---

## 例 2：需求详细 → 忠实模式

**需求**：「黄昏，一个少女站在城堡前的石桥上，穿深蓝斗篷，风把斗篷吹起来，背后是城堡和山，要写实。」

**判据**：主体、服装、场景、时间都点了名 → 忠实模式。只做三件事：定光向、定机位、把「风吹起来」写成具体的布料状态。**不新增主体、不换场景、不加奇观。**

**主题三角**：剧照感；情绪是临行前的一刻；第一眼落在斗篷边缘的逆光上。

```text
【正面提示词】
Late golden-hour sun sits low behind the castle, backlighting the girl on the stone bridge with a thin warm rim along her shoulders and the wind-lifted edge of her deep-blue woollen cloak.
Medium-wide shot at eye level from slightly behind and to her left, 50mm, the bridge running from the lower-right corner toward her, castle and ridge compressed behind her.
A slender 19-year-old woman stands three-quarters away from the camera, hood down, both hands holding the cloak closed at the chest, the hem pulled taut toward the right by the wind and its shadow falling across uneven stone slabs at her feet.
The keep and a dark ridge line sit directly behind her as simple silhouettes, cold blue shadow filling the foreground stone while the upper sky stays warm.
Real shadow falloff, wind-tension in the fabric, zero fill light on her front.

【负面提示词】
worst quality, bad anatomy, watermark, jpeg artifact, blurry, out of focus, lowres, bad hands, extra fingers, fused fingers, deformed hands, distorted face, anime, 2d, illustration, cel shading, 3d render, cgi, doll, plastic skin, cosplay, wig, flat front lighting, evenly lit skin, overexposed skin, studio fill light, floating fabric, cape clipping through body

【采样参数】
1248×1664 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

**改动清单**

| 用户给了 | 处理 |
| :--- | :--- |
| 黄昏、城堡、山、石桥、少女、深蓝斗篷 | 全部保留，不替换 |
| 「风把斗篷吹起来」 | 写成 `hem pulled taut toward the right` + 影子落在石板上，可指认 |
| 未指定光向 | 补「太阳在城堡后」→ 逆光，正面留给冷调阴影 |
| 未指定机位 | 补斜后方中远景，桥面作引导线 |
| 未指定 | **没有**新增人物、飞鸟、旗帜、火焰或奇观元素 |

**自检**：一句话说得出（「逆光下斗篷被风拉直，影子铺在石板上」）✓；主焦点一个 ✓；无不可能元素 ✓；约束未被动 ✓。

---

## 例 3：海报 · 编译合格但平淡 → 换钩子

**需求**：方形极简茶海报，标题 `TEA TIME`，右下小字 `BREATHE`，一杯茶。你已经跑过两版（`imgs/moss_image_t2i_00014_.png`、`00015_.png`，均为 prompt upsampler 开启，Steps 25 / CFG 3）。

**改前**（你实际用的 caption）：

```text
A square minimalist tea poster on warm cream paper, using a restrained forest-green and muted ochre screen-printed palette. A pale ceramic teacup on a saucer sits in the lower center with three simple steam curls. Clean generous margins, subtle paper grain, title in the upper band and a small accent word near the lower-right.
```

**诊断**

| 症状 | 表现 |
| :--- | :--- |
| 没有主题三角 | 只有品类，说不出情绪与第一眼 |
| 是「摆放」不是「发生」 | `a teacup sits in the lower center`，陈列，无事件 |
| 通用模板 | 杯 + 蒸汽 + 衬线大标题 + 小字，任何茶品牌都能用 |
| 潜力被写成属性 | `screen-printed palette`、`paper grain` 只是质感词，没有变成行为 |
| 文字与图无关系 | 两条文字各自待在角落，不参与构图 |

**模式与机制**：自由模式（用户只要了品类）；机制取**媒介转化**——两版色套印刻意错位，让印刷行为本身成为钩子。平面类不需要不可能元素（`concept.md` §8 平面类分支）。

```text
【正面提示词】
A square tea poster screen-printed on warm cream stock in two ink passes, forest green and muted ochre, the two deliberately a few millimetres out of register: the ochre shadow of the cup slips sideways beyond its green outline, and the small word BREATHE doubles faintly where the inks overlap. The cup is drawn in one continuous line with three loose ochre steam curls rising from it. Heavy serif TEA TIME holds the upper band, its edges slightly bitten by paper grain, wide clean margins and nothing else on the sheet.

【负面提示词】
worst quality, jpeg artifact, blurry, lowres, anime, 2d character, illustration with outlines, 3d render, cgi, photograph of a real cup, glossy ceramic, drop shadow, gradient background, extra text, misspelled letters, watermark, sticker edge

【采样参数】
1008×1008 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

**为什么这么写**

| 处理 | 依据 |
| :--- | :--- |
| 把 `palette` 变成「两版套印错位」 | 质感词升级成可见行为（`concept.md` §5 媒介转化） |
| 让 `BREATHE` 在套印重叠处重影 | 文字参与构图，而不是贴在角落（`concept.md` §8 平面类） |
| 保留原文字、原层级、原留白 | 用户已指定的内容不动（`concept.md` §3） |
| 负面封 `drop shadow` / `glossy ceramic` | 立体感会把这套平面印刷拉回商品图 |

**限制**：图内文字与套印重影会互相干扰，重影太重时 `BREATHE` 可能读不出。要上 Layout 精确控位时，先按 `core/layout.md` 写草稿并跑 `scripts/vendor/openmoss/compile_prompt.py`；盒位沿用原草稿也要重跑一次编译器确认。

**自检**：一句话说得出（「两版色套印错开，小字在重叠处重影」）✓；主焦点一个（杯 + 错位轮廓）✓；平面类无需落地三件套，但光向已由「平面印刷」统一 ✓。

**出图状态**：改前两版已跑（upsampler 开启）；改后**未出图**。要判断这个钩子是否真的更抓眼，需同参数、关掉 upsampler 各跑一版再比。
