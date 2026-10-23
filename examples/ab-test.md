# 同 seed A/B 记录

三组对照，2026-10-23，本机 ComfyUI。**结论是方向性的：单 seed、单一权重，不外推为统计结论。**

## 固定项

```text
分辨率 1360×752（16:9 / 1MP）
Steps 25 / CFG 3.0 / Euler / simple / SLG 关闭
每组两张同 seed，只改正面 caption；A 组另改 upsampler 开关
改写器 = 工作流内的 Qwen3.5-9B 文本节点（ComfySwitchNode 控制，开/关）
```

**四组共用负面**

```text
worst quality, lowres, bad anatomy, bad hands, extra fingers, extra limbs, watermark, signature, jpeg artifact, blurry, oversaturated, flat front lighting, evenly lit skin, studio fill light, anime, 2d, illustration, cel shading, cartoon, 3d render, cgi, doll, plastic skin
```

---

## A 组：写实语序（2×2）

seed `738835547678523`。目的是把「写法的净效果」与「改写器的效果」分开。

|  | 基线 | skill 写法 |
| :--- | :--- | :--- |
| upsampler 关 | `a_base_off.png` | `a_skill_off.png` |
| upsampler 开 | `a_base_up.png` | `a_skill_up.png` |

**基线**

```text
A young woman in a beige coat buying a hot coffee from a convenience store counter on a rainy night, realistic photography, cinematic lighting, high detail, shallow depth of field.
```

**skill 写法**

```text
Saturated green fluorescent light from the store canopy is the only light on her, cut off at the awning edge so the rainy street beyond falls into blue darkness, 35mm at chest height from across the wet pavement.
A 24-year-old woman in a damp beige wool coat stands at the counter in the right third, both hands around a paper cup, steam rising across her chin, a thin warm amber band from the interior shelf lights the left side of her face.
The counter glass carries green reflection and fingerprint smears; behind her the empty street recedes as small blurred puddles, and the wet asphalt in the foreground reflects the canopy edge as one broken green stripe.
Visible skin pores, fine damp hair strands stuck to her temple, light film grain, hard shadow falloff on the right side of her face.
```

**观察**

- 关改写器：skill 版的绿檐灯、路面绿反射、街道蓝黑、右侧暖货架、蒸汽受光全部出现；基线版是暖白平光、没有绿、没有雨、招牌还长出了乱码中文。差异可归因到 caption。
- 开改写器：基线被补成一张合格的温馨便利店图，两组差距明显变小，skill 版的脸也被改写器推向整体暖调。
- 没能完全落地的：`both hands around a paper cup` 变成了单手持杯，`fingerprint smears` 没有出现。

## B 组：创意层 + 导演层

seed `197301879477886`，两组都开 upsampler。

**基线** → `b_base_up.png`

```text
A giant moon hanging above an old library at night, surreal concept art, epic composition, highly detailed, dramatic lighting.
```

**skill 写法** → `b_skill_up.png`

```text
Cold blue moonlight floods through a giant arched window that the moon itself fills, its pale disc so large that the window mullions cut it into rectangular panes, seen from a low seat inside an old reading room.
An old man in a dark coat sits at a long wooden table in the lower-left third, small against the window, a single amber desk lamp lighting his newspaper and the near edge of the table while his back stays in silhouette.
Rows of empty reading desks and green-shaded lamps recede to the right, dust drifting in the moon beam, the floorboards cold grey with a single dropped glove beside his chair.
```

**观察**

- 基线把「图书馆」漂成哥特庄园：月亮居中、无人、无尺度参照、整张图退化成通用奇幻海报。
- skill 版逐条落地：窗棂把月亮切成格、冷蓝月光、琥珀台灯只照桌面、右侧绿罩台灯阵列纵深、地上那只手套。这一组即使在改写器干扰下差异也没被抹平。
- 瑕疵：老人背后的光束从右侧入画，和正后方月亮的方向矛盾；报纸内容不可辨。

## C 组：导演层最小改动

seed `551418087126216`，两组都关 upsampler。

**基线** → `c_base_off.png`

```text
An old man reading a newspaper by the window on the second floor of a teahouse, rainy day outside, warm interior light, realistic photo, detailed.
```

**skill 写法（修正版）** → `c_skill_off.png`

```text
Cold rainy daylight stays the main light on him, while a single warm ceiling lamp pools over the corner of the table, the rest of the teahouse sinking into brown shadow, 40mm from a seat at the same level.
Seen past a narrow blurred strip of wooden railing that occupies only the bottom sixth of the frame, a thin 70-year-old man fills the left third, a folded newspaper open at chest height and lit well enough to read the column edges, a lidded tea cup at his elbow, his shoulder edged by the grey window light.
Rain runs down the glass in long streaks and the street below is a soft grey blur with one red tail light; the empty chairs behind him are stacked.
```

**观察**

- 前一版（未留存）写的是「落进褐色阴影 + 前景虚焦栏杆」，结果整体欠曝、报纸不可读、人脸沉暗、栏杆吃掉约四分之一画幅——绝对句被执行到了失效。
- 修正版补上三条下限后，盖碗茶、可读报纸、窗外红尾灯、底部一条栏杆、身后堆叠椅子同时出现。基线版本身也不难看，只是没有这些指定细节。
- 因此这一条记为「修正版有效」，**不是**「skill 版比基线版更好看」。

## 这组测试没能证明什么

- 不能说 skill 让画面更美：`a_base_off.png` 干净但平庸，`c_base_off.png` 本身成立。
- 不能外推到其他 seed、分辨率、权重或参数档。
- B 组仍开着 upsampler，写法与改写器的贡献混在一起。
