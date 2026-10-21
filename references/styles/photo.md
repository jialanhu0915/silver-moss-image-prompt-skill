# 通道 A：三次元写实

## 1. 何时走这条
真人、纪实摄影、电影剧照、时尚大片、商品与空间写实，需要「像拍出来的」而不是「像画出来的」。反例（该走 `anime.md`）：插画、动画截帧、漫画、赛璐璐、明显笔触。

## 2. 机制前提：写「看得见的结果」，不写「器材的名字」
官方 caption 规范只描述 `composition / key subjects / actions / setting / colors / lighting / artistic style`，且 `Include only information visible in the image`；型号与引擎是画面上看不见的推断信息。一个型号配至少三个可见结果，否则删掉型号留结果。

| 无效（单写不值钱） | 有效（写它造成的可见结果） |
| :--- | :--- |
| `Contax T2` | `harsh direct on-camera flash, hard black drop shadow on the wall, dark corner vignette` |
| `Polaroid SX-70` | `faded milky low-contrast color, soft bluish shadows, slight edge falloff` |
| `Unreal Engine 5` | 别写；写实渲染人物不是这条通道的能力范围，见 §9 |
| `film grain` 单独写 | 加重量级：`coarse visible 35mm grain in the shadows` |

## 3. 开场模组库
第一条句子定整图的光学与显影基调。选一组整句照抄再改细节，不要拆成单词混搭；`[Q,R]` 两档都成立。

| # | 风格 | 开场句（可直接抄） | 必须同时出现的可见要素 |
| :--- | :--- | :--- | :--- |
| 1 | 90s 一次性胶片直闪 | `raw 1990s disposable 35mm film snapshot, harsh direct on-camera flash, hard black drop shadow cast on the wall behind the subject, dark corner vignette, coarse analog grain` | 墙面硬投影、四角暗角、皮肤油光 |
| 2 | 暗室单束光 | `low-key chiaroscuro photograph in a pitch-black room, lit only by one narrow warm beam from the side, half the face and body sunk in deep shadow, zero front fill light` | 半脸入暗、明确的暗部位置 |
| 3 | 港片霓虹慢门 | `1990s Hong Kong arthouse film still, saturated emerald-green and warm amber tungsten neon, slow-shutter motion blur trailing behind the subject, red halation blooming on highlights` | 翠绿+暖黄、拖影、红色光晕 |
| 4 | 银盐黑白 | `monochrome black-and-white silver gelatin print, high-contrast grayscale lighting, crushed blacks and crisp silver highlights, coarse HP5-style grain` | 删掉正文所有颜色词 |
| 5 | 落日逆光 | `golden hour backlit portrait, low sun directly behind the subject, glowing rim light along stray hair strands, natural optical lens flare` | 发丝金边、真实眩光 |
| 6 | 冷峻漂白 | `desaturated bleach-bypass cinema still, crushed shadows, cold silver-teal grading, harsh overcast window light, raw micro skin texture` | 低饱和金属银青、深黑暗部 |
| 7 | 双色色片 | `nighttime neon portrait, split two-tone gel lighting, electric cyan on the left side of the face, hot magenta on the right, wet glass reflections` | **写清左右两侧各自的颜色** |
| 8 | 湿版老照片 | `1880s sepia wet-plate albumen print, faded brown-yellow monochrome, chemical edge staining, dust scratches and paper creases, soft swirly Petzval vignette` | 药水边缘腐蚀、折痕 |
| 9 | 家用 VHS | `1994 lo-fi home VHS tape still, horizontal CRT scanlines, RGB chroma bleed, magnetic tape noise, glowing green OSD text reading "PLAY  1994.10.17"` | 扫描线、色散、OSD 时间戳 |
| 10 | 红外监控 | `green monochrome night-vision CCTV footage, high corner camera angle, phosphor-green IR illumination, glowing white infrared eyes, digital compression noise, timestamp "CAM-04 02:14:09"` | 荧光绿、反光白瞳、俯拍时间戳 |
| 11 | 日系高调过曝 | `airy overexposed pastel film photograph, high-key diffused window daylight, milky lifted shadows, pale cyan-mint and warm cream cast, dreamy summer haze` | 提亮暗部、薄荷奶油调 |
| 12 | 青橙宽银幕 | `cinematic anamorphic widescreen movie still, teal-and-orange grading, deep teal shadows and warm amber skin, oval vertical bokeh orbs, horizontal blue flare streak` | 椭圆焦外光斑、水平拉丝 |

## 4. 暗部与逆光（最容易翻车的地方）
只写「夜晚」「暗室」不够：肖像训练图以正面平光为主，模型会自行给正面补光；`[R,Q]` 顺光主导的画面不需要这套。
1. **正面提示词删掉**：`fair skin, porcelain skin, bright, glowing, luminous skin, daylight`。
2. **正文直接写暗部位置**：`the front of her face, chest and stomach are sunk in deep shadow, only a thin rim light traces the edge of her silhouette`。
3. **结尾锁一句**：`realistic shadow falloff, zero flat front fill light`。
4. **负面追加**：`flat front lighting, evenly lit skin, overexposed skin, pale white skin, studio fill light, whiteout`。

## 5. 主体：年龄、骨相、身材
### 5.1 双向排除
防老与防幼的默认偏移方向相反，两边都要写否定：
```text
a slender 15-to-16-year-old girl with true adolescent proportions — neither a big-headed 10-year-old child nor a mature 25-year-old woman — with a softly tapered chin and a long graceful neck.
```

- 防老/防胖不写 `woman, gorgeous, mature, curvy, wide hips, bone structure, deep-set eyes, defined nose bridge`；防幼不写 `very young, babyface, chubby cheeks, button nose, petite, budding`。
- 年龄感来自骨相，不来自数字：`softly tapered chin` + `long neck` 比 `15 years old` 有用。

### 5.2 全身镜头必须交代脚与地面
删掉脚下关系，头身比会缩成五头身。写 `both feet planted on the wet asphalt, full body from head to shoes visible`，或明确悬空 `legs hang freely in mid-air well above the floor`（负面加 `feet on floor, standing`）。

### 5.3 皮肤与毛发
- 真实感来自**不均匀**：`visible microscopic pores, faint uneven skin tone, a few tiny moles, slight oil sheen on the forehead`；毛发写「细+乱」：`natural fine real hair with thin wispy bangs and loose flyaway strands`，只写 `blonde hair` 会得到假发。
- 双色发分清主体与发梢：`blonde hair with pastel-pink tips`，不要反写；脸红只写 `faint pink blush`，不写 `deeply flushed / burning red`。

### 5.4 眼睛与表情
遮眼、闭眼、熟睡时**删掉所有眼神动词**（`looking, gazing, staring, wide-eyed`），改写 `eyes completely closed, unaware of the camera`，负面加 `visible eyes, open eyes, looking at viewer`。

## 6. 动作写成静态结果
`[R,Q]` 涉及衣物、道具、肢体的动作，写成「已经处于什么状态」（进行时动词会多画一只手）：

| 别写 | 改成 |
| :--- | :--- |
| `pulling up her shirt` | `shirt already pushed up above the waist` |
| `taking off her jacket` | `jacket already slipped off one shoulder` |
| `holding up two cups` | `one cup in each hand` |

## 7. 多人同框
- 按位置分块写，不按部位分块；每个人写全自己的发色、肤色、是否戴眼镜、有无雀斑。
- 第二人起句首切断继承：`In sharp contrast, the woman on the right wears NO glasses and has spotless skin with zero freckles`；群像开头可写计量句：`Featuring exactly 4 distinct people, each appearing once, arranged asymmetrically rather than in a grid.`（官方公开示例，增益未独立对照，`[社区]`）；负面加 `twins, identical faces, same hair color, cloned faces`；两人身体重叠时不要用纯侧机位（`from side`），改斜侧 3/4 角。

## 8. 剧照感：让它不像证件照
真实电影截图很少是单人孤立居中。五件事任选三件：
1. **特殊机位与遮挡**：`first-person dashcam POV through the windshield with the dark dashboard and wiper blades along the bottom edge`。
2. **前景虚化层**：`in the left foreground, the out-of-focus back of a man's head and shoulder in an over-the-shoulder frame`。
3. **灯具形态与受光位置**：`two harsh emerald fluorescent tubes diagonal across the upper-left ceiling, catching her nose tip and forehead while the rest of her face stays in shadow`。
4. **年代与颗粒**：`1950s black-and-white 35mm Hollywood still`、`warm tungsten-lit 1990s period drama close-up`。
5. **破精致感的小道具**：`a toothpick at the corner of his mouth`、`a chipped enamel mug`、`a printed notice taped to the wall with a curled corner`。

## 9. 这条通道的专有坑
- **正文里残留二次元词会把整图拉回 2D**：`anime, cel shading, waifu, 2.5D` 一个都不能留；**黑背景 + 白皙皮肤**是最容易过曝的组合，必须按 §4 写暗部。
- **不要指望写出写实 3A 游戏角色**：`Unreal Engine 5`、`CGI character`、`3D render` 会退化成塑料人偶或厚涂；要写实游戏角色，用真拍写法（胶片、直闪、毛孔），不要提引擎。
- **档 R**：手、眼、文字、图案最先崩，`[R]` 标记的防崩词（`five distinct natural fingers clearly visible`、`crisp symmetrical eyes`）不能省；**`[Q]`**：开着 SLG 时不要继续堆防崩词，会把边缘压得过硬。

## 10. 母版
### 母版 A：胶片直闪（默认主力，档 R 或 Q）
```text
raw 1990s disposable 35mm film snapshot, harsh direct on-camera flash, hard black drop shadow on the wall behind her, dark corner vignette, coarse analog grain, deep depth of field.
[主体：a slender 20-year-old woman with natural fine dark-brown hair, loose flyaway strands, faint pink blush, no makeup].
[姿态与服饰：static, already-seated pose, oversized white shirt slipping off one shoulder, bare feet on a wooden floor].
[场景：a cramped apartment kitchen at night, one fluorescent tube overhead, a kettle and two mismatched mugs on the counter].
Unretouched skin with microscopic pores and a slight sheen under the flash, realistic shadow falloff, zero flat front fill light.
```
负面：L0 + L1 + 写实 L2 + `flat front lighting, evenly lit skin, overexposed skin, studio fill light`。

### 母版 B：日系柔光（交付级，档 Q）
```text
soft diffused window daylight from the left, warm skin-tone shadow contrast, shallow depth of field with a calm background.
[主体：a slender 18-year-old woman with natural fine black hair, airy wispy bangs, a shy sideways glance].
[服饰与动作：a cream knit cardigan over a white cotton dress, sitting sideways on a windowsill, knees drawn up].
[场景：a quiet tatami room with a low table, a glass of iced tea catching the light].
Smooth supple real skin with a soft luminous finish, gentle falloff into shadow, fine natural film grain.
```
负面：L0 + L1 + 写实 L2（**去掉 `airbrushed`**，柔光档要留一点柔）+ `harsh pores, rough skin, acne, overexposed, washed out, whiteout`。

### 母版 C：黑白纪实（档 Q）
```text
monochrome black-and-white silver gelatin print, high-contrast lighting, crushed blacks, crisp silver highlights, coarse grain.
[主体：a lean 30-year-old man with close-cropped hair, deep-set eyes, a scar above one eyebrow].
[动作与服饰：leaning against a concrete pillar, a worn wool coat, both hands in his pockets].
[场景：a rain-soaked alley at night, one bare bulb overhead].
```
**正文必须删掉所有颜色词**，只留明暗关系（`deep shadow`, `bright highlight`）。负面追加 `color, colorful, saturated`。
