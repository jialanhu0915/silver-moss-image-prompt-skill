# 写实通道示例

两例都是**未实拍**的示意稿：提示词按本 skill 规则编写，参数为档 Q 默认值。示例只证明写法结构，不证明出图质量——后者需要你自己跑。

---

## 例 1：夜雨便利店门口

**需求**：一个在便利店门口避雨的女生，夜雨，别太亮。

**判据**：真人 + 夜间 + 强光源 → 写实通道；光源复杂 → 光线句必须最前置；有湿发与反光材质 → 特写层级；无文字 → 不需要 SLG 也稳定，但保留默认档 Q。

```text
【正面提示词】
Cool blue-white fluorescent light from the store window spilling onto wet asphalt, 35mm at eye level, deep focus from the near puddle to the far street.
A slender 20-year-old East Asian woman in a soaked oversized grey hoodie and black shorts stands under the awning just outside the glass door, wet hair clumped into separate dark strands stuck to her cheek, both hands hugging a paper bag to her chest, looking off to her left with an exhausted half-smile.
Behind her the glass door reflects rows of shelves and a green price tag; in the near foreground at the bottom-left corner a wet plastic bag drifts in a puddle, out of focus.
Rain droplets caught in the harsh fluorescent light, realistic wet skin highlights, real shadow falloff, zero flat front fill light.

【负面提示词】
nsfw, worst quality, bad anatomy, watermark, jpeg artifact, blurry, out of focus, lowres, bad hands, extra fingers, fused fingers, deformed hands, distorted face, anime, 2d, illustration, cel shading, 3d render, cgi, doll, plastic skin, cosplay, wig, flat front lighting, evenly lit skin, overexposed skin, studio fill light

【采样参数】
1024×1536 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

**为什么这么写**

| 处理 | 依据 |
| :--- | :--- |
| 第一句就是光源与镜头 | 前置光线给全图定色温（`core/caption.md` §1） |
| 写「湿发成缕」而不是 `wet hair` | 可见结果是「成缕、发暗、反光锐利」（`craft/aesthetics.md` §8） |
| 前景塑料袋虚化，占左下角 | 三层空间各给一个角色（`craft/composition.md` §3） |
| 「双手抱纸袋」写成静态结果 | 避免进行时动词多吃一只手（`styles/photo.md` §6） |
| 结尾 `zero flat front fill light` | 夜间强光源场景防正面补白（`styles/photo.md` §4） |
| 负面用写实封杀组 | 与通道一致（`core/negative.md` §2） |

**自检**：主体 1 人 ✓；光线在主体前 ✓；无图内文字，跳过字号检查 ✓；负面无二次元通道词 ✓；未写相机型号 ✓。

---

## 例 2：暗房单束光的人像

**需求**：像王家卫电影里的一帧，绿色霓虹，人在暗处。

**判据**：要「电影剧照」不是「电影感」这个词；先写模具组（港片霓虹），再写主体；暗部必须明写。

```text
【正面提示词】
1990s Hong Kong arthouse film still, saturated emerald-green and warm amber tungsten neon, slow-shutter motion blur trailing behind her shoulder, red halation blooming on the wet highlights, coarse 35mm grain.
A 28-year-old woman with a sharp jawline and short bleached hair sits sideways in a narrow booth in a dim noodle shop, one elbow on the chipped formica table, a cigarette held between two fingers, her face turned toward a green neon sign off-frame.
The room is dark, lit only by that sign through a beaded curtain; the front of her face, chest and hands fall into deep, moody shadow while a thin rim of green traces her jaw and shoulder, and the beaded curtain casts broken light bands across the table.
Realistic shadow falloff, zero flat front fill light, organic 35mm analog grain.

【负面提示词】
nsfw, worst quality, bad anatomy, watermark, jpeg artifact, blurry, out of focus, lowres, bad hands, extra fingers, fused fingers, deformed hands, distorted face, anime, 2d, illustration, cel shading, 3d render, cgi, doll, plastic skin, cosplay, wig, flat front lighting, evenly lit skin, overexposed skin, pale white skin, studio fill light, whiteout

【采样参数】
1456×1456 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 固定后做变体

【可选】
想更贴「抽帧」感：`Steps 28` + `SLG=""`（档 R），并保留上面全部防崩词。
```

**为什么这么写**

| 处理 | 依据 |
| :--- | :--- |
| 不写 `cinematic`，写「绿霓虹 + 暖钨丝 + 红色光晕 + 颗粒」 | 空转词换成四个可见结果（`craft/camera.md` §9） |
| 明写正面暗部与边缘光 | 只写「暗房」会被补成平光（`styles/photo.md` §4） |
| 抽出 `fair skin` 类词 | 提亮肤色的词会毁掉低调光 |
| 手部写「夹烟、两指」而不是动作进行时 | 静态结果（`styles/photo.md` §6） |
| 湿高光 + halation 挂在光源条件之后 | 缺陷必须与拍摄条件配对（`craft/camera.md` §6） |
| 年龄不写 `gorgeous / curvy` | 避免被画成「平均美女」（`styles/photo.md` §5.1） |

**自检**：光源在主体前 ✓；暗部三处（脸/胸/手）写明 ✓；负面含 `pale white skin, studio fill light` ✓；无 `cinematic` ✓；档位标注清楚 ✓。

---
