# 镜头：焦距、景别、机位、景深、画幅

想指定镜头感觉、焦距长短、景别与切点、机位高度与角度、谁站在谁的视角里、景深与焦外形状、画幅比例，或某种拍摄器材自带的画面痕迹时，查这里。与风格文件并列使用：写实通道见 `styles/photo.md`，二次元通道同样只挑需要的行。

总规则：**术语必须先翻译成可指认的可见事实**才写进提示词。`85mm`、`f/1.4`、机身型号都是画面外信息，模型在 caption 里见不到它们；`her face sharp while the string lights behind her melt into soft round orbs` 是画面内信息。判断标准只有一句：写完这个镜头词，能不能指出「画面哪一块区域发生了什么变化」——指不出来就删掉，换成结果句。型号与数字不是禁用，但必须同句配至少三个可见结果，否则删型号、留结果。

## 1. 焦距与透视压缩

焦距要成立必须写全三件事：主体占画幅多少、背景被拉近还是推远、背景清不清晰。只给数字，模型给回一张普通浅景深人像。

| 中文 | English | 可直接抄进提示词的英文短语 | 它改变画面的哪一部分 |
| :--- | :--- | :--- | :--- |
| 超广角 | ultra-wide | `ultra-wide view, the walls bowing outward at the frame edges, the near corner of the table huge and the far wall tiny` | 四角拉伸、直线外凸、近物暴涨 |
| 广角近摄 | wide angle, close in | `wide angle close to the subject, her outstretched arm and the cup loom oversized in the near foreground, the street behind shrinking and tilting away` | 近大远小被夸大、纵深被拉长 |
| 小广角 | slightly wide | `slightly wide framing, subject and background both readable, the ceiling lines converging only mildly` | 轻纵深、轻透视收敛 |
| 环境人像 | environmental portrait | `35mm environmental portrait, the subject occupying about a third of the frame, the whole workshop legible around her, everything from her hands to the far wall in focus` | 主体与环境同时成立、背景整块可读 |
| 标准视角 | normal lens | `neutral normal-lens perspective, natural body proportions, no perspective exaggeration` | 比例最接近肉眼、无夸张 |
| 中长焦人像 | short telephoto portrait | `her head and shoulders sharp against a background flattened and dissolved into soft round orbs, the far street compressed right behind her shoulders` | 背景压缩 + 背景虚化 + 五官不变形 |
| 长焦压缩 | telephoto compression | `telephoto compression, the distant buildings stacked flat and tight behind her, crowd layers pressed into a single plane` | 纵深被压成平面、远物相对放大、背景贴住主体 |
| 超长焦 | long telephoto | `long telephoto compression, background elements overlapping in flat stacked planes, heat shimmer, a tight crop on the face` | 极强压缩、背景填满画幅、空气感发颤 |
| 广角近大远小的证据 | near-object exaggeration | `shot from very close with a wide lens, the near hand and the bottle dominate the lower frame at twice their true size, her body falling away small behind them` | 下方画幅被近物吃掉、主体被推远缩小 |
| 长焦压缩的证据 | background stacking | `the row of parked cars behind her stacked flat and overlapping instead of receding, the far mountain sitting right on her shoulder` | 远物层叠、远近关系被消除 |
| 仰角广角汇聚 | keystone | `wide lens tilted up, the building's vertical lines converging sharply toward the top of the frame` | 竖向线条向顶部汇聚、上部收窄 |

**机制**：近大远小是**机位距离**造成的，广角只是把它装进画幅；压缩是**远物在画幅中相对变大**造成的。所以两种焦距的证据都写在「近物尺寸比」和「远物是否层叠」上，不在镜头名上。一条提示词只留一个焦距数字，且紧跟它的可见结果。

## 2. 景别与切点

景别真正控制的是**画幅里能容纳几个信息单元**，模型靠占比决定细化哪一层（脸 / 手 / 布料 / 环境）。切点是可见事实，景别名只是行业缩写，两个都写才稳。

| 中文 | English | 可直接抄进提示词的英文短语 | 它改变画面的哪一部分 |
| :--- | :--- | :--- | :--- |
| 大远景 | extreme wide shot | `extreme wide shot, the figure reduced to a small dark silhouette in the lower third, the landscape dominating the frame` | 环境占满画幅、人退成剪影 |
| 远景 | wide shot | `wide shot, the full figure visible with generous space above and around, the location readable` | 空间关系与站位 |
| 全身 | full body shot | `full body shot from head to shoes, both feet planted flat on the wet asphalt, clear floor space around the feet` | 体型、廓形、脚与地面的接触 |
| 七分身 | cowboy shot | `cowboy shot framed from mid-thigh up, hands resting near the holsters` | 腰间道具、手势、站姿 |
| 膝上 | knee-up shot | `knee-up framing, cut just below the knees` | 步伐、裙摆、腿部动作 |
| 半身 / 腰以上 | waist-up shot | `waist-up shot, framed from the waist up, hands visible at the bottom edge` | 上半身动作、服装、手势 |
| 胸像 | bust shot | `bust shot, framed from the chest up` | 面部 + 肩线 + 领口 |
| 头肩 | head-and-shoulders | `head-and-shoulders portrait, shoulders cropped at the frame bottom` | 表情、发质、妆造 |
| 中景 | medium shot | `medium shot, framed from the waist up, the room's key props visible behind` | 动作 + 人物关系 + 少量环境 |
| 中近景 | medium close-up | `medium close-up, from the chest up, the background falling softly out of focus` | 表情 + 一点环境 |
| 特写 | close-up | `close-up on her face filling most of the frame, the background reduced to soft color` | 表情、皮肤、眼神 |
| 大特写 | extreme close-up | `extreme close-up on one eye and the lashes, skin texture and pores visible` | 材质、细节、情绪张力 |
| 局部 / 插入镜 | insert shot | `insert shot of her fingers gripping the chipped enamel mug` | 单一物件、手、材质 |

**跨景别冲突**：`close-up` + `both hands visible` + `full outfit` 同现会被拉成中景、脸变最小。删到只剩一个景别主体。

## 3. 机位高度与角度

角度名信息量低，可靠的是**地平线落在画幅哪里 + 谁的头顶更高 + 关节位置**。

| 中文 | English | 可直接抄进提示词的英文短语 | 它改变画面的哪一部分 |
| :--- | :--- | :--- | :--- |
| 平视 | eye level | `camera at the subject's eye level, the horizon line crossing at her eyes` | 地平线穿眼、比例无变形 |
| 略低 | slightly below eye level | `camera slightly below her eye level, looking marginally up` | 地平线略低于眼、轻微抬高主体 |
| 仰拍 | low angle | `low angle from knee height looking up, her figure towering over the camera, the ceiling and sky behind her` | 地平线压到画幅底部、下巴与鼻孔暴露、背景换成顶面 |
| 极低 / 虫视 | worm's-eye view | `worm's-eye view from ground level, the soles of her shoes in the foreground, her body converging upward` | 脚掌占据前景、身体向上收窄 |
| 俯拍 | high angle | `high angle looking down at her, the floor spreading around her feet, the top of her head toward the camera` | 地平线抬高、头顶变大、腿变短 |
| 顶视 | overhead / top-down | `directly overhead top-down view, her body and the table laid out flat like a diagram, no horizon line` | 画幅变成平面图、脸只剩额头与鼻尖 |
| 鸟瞰 | bird's-eye view | `bird's-eye view from high above, streets and rooftops forming a grid, tiny figures casting long shadows` | 人物成点、阴影拉长、地面成网格 |
| 荷兰角 | dutch angle | `dutch angle, the horizon tilted about fifteen degrees, the vertical lines of the doorway leaning` | 全部竖线倾斜、地平线切过画面 |
| 地平线定位 | horizon placement | `the horizon line sits at her chest, she fills the upper two thirds` | 主体与环境的面积分配 |

**坐姿 / 蹲姿配高角度**会把大腿压到消失，得到上半身直接接脚。补丁：写明关节 `both knees bent sharply, thighs horizontal, calves vertical, feet flat`，负面加 `missing thighs, fused legs`。

## 4. 机位关系（观众与人物、人物与人物）

模型对「谁在看谁」的理解来自**视线方向 + 谁被遮挡**。关系镜头的可见证据就是画幅边缘的前景遮挡物。

| 中文 | English | 可直接抄进提示词的英文短语 | 它改变画面的哪一部分 |
| :--- | :--- | :--- | :--- |
| 过肩 | over-the-shoulder | `over-the-shoulder shot, the out-of-focus back of a man's head and shoulder filling the left foreground, her face sharp beyond it` | 左／右下角被前景头肩占住并虚化 |
| 双人镜 | two-shot | `two-shot, both figures in profile facing each other, equal space on both sides` | 画幅左右对称分配、两人侧脸相对 |
| 反向视角 | reverse angle | `reverse angle on the other person, now facing the opposite direction, same room and same light direction flipped` | 朝向翻转、光源落到另一侧脸 |
| 主观镜头 | POV / first person | `first-person POV, looking down at her own hands on the steering wheel` | 视点降到眼位、自己的脸不入画 |
| 画外第一人称 | off-screen first person | `camera-as-eyes: a bare hand enters from the bottom right edge, slightly out of focus, no face and no body visible in frame` | 画幅边角多出一只手、无自身身体 |
| 越肩背影 | behind-the-back framing | `from behind her back, her hair and shoulder in the near foreground, the lit doorway small and far ahead` | 前景被后脑与肩占满、目标物变小 |
| 背影 | back view | `back view, her face not visible, only the nape of her neck and the coat's back seam` | 五官消失、只剩后颈与衣物背面 |
| 侧面 | strict profile | `strict side profile, the nose line and jaw silhouette against the bright window` | 骨相变剪影、双眼只剩一只 |
| 四分之三 | three-quarter view | `three-quarter view turned about forty degrees from the camera` | 兼顾双眼与面部体积 |
| 越轴提示 | screen direction | `she faces frame right, he faces frame left` | 视线与身体朝向固定在画幅一侧 |

**写法要点**：OTS 不写「虚化」会得到两个清晰后脑勺；不写左右会随机；`reverse shot` 在单图里只能写成「同一空间的反向视角」，写「剪辑」无意义。

## 5. 景深、焦平面与光斑形状

`bokeh` 单独出现时模型常把整图糊掉。有效写法永远是「A 锐 + B 虚」——虚实边界本身是可见信息，模型必须解出一个焦平面。光斑形状同理：写形状，不写叶片数字。

| 中文 | English | 可直接抄进提示词的英文短语 | 它改变画面的哪一部分 |
| :--- | :--- | :--- | :--- |
| 浅景深 | shallow depth of field | `shallow depth of field, only her eyes and lashes are sharp, her ear and the wall behind already soft` | 锐度收窄到一小块、前后同时化开 |
| 极浅焦平面 | razor-thin focus | `razor-thin focus plane on the near eye only, the far eye just beginning to soften` | 单一平面锐、同一张脸内虚实切换 |
| 深景深 | deep focus | `deep focus, the near mug, her face and the far doorway all equally sharp` | 全画面锐、纵深被摊平 |
| 指定焦平面 | focal plane on X | `the focal plane sits on her cheek, her shoulder in front already blurred, the shelf behind softly dissolved` | 虚实分界精确落在某个物件的某一个面 |
| 前景虚化层 | foreground blur layer | `in the near foreground, an out-of-focus sprig of leaves crosses the lower left corner, softening that edge into green haze` | 边角糊成一片色块、画面多一层纵深 |
| 主体分离 | subject separation | `subject clearly separated from the background by a blurred halo of light` | 主体轮廓外缘出现亮边 |
| 焦外光斑 | bokeh orbs | `out-of-focus string lights forming overlapping soft round discs in the background` | 背景亮点变成一片圆盘 |
| 圆形光斑 | round bokeh | `round bokeh orbs with soft edges, no bright rim` | 光斑内部均匀、边缘渐隐 |
| 椭圆光斑 | oval / anamorphic bokeh | `vertically stretched oval bokeh orbs` | 光斑竖向拉长、宽银幕观感 |
| 多边形光斑 | polygonal bokeh | `hexagonal bokeh highlights with visible straight edges` | 光斑有棱角、显硬 |
| 二线性焦外 | soap-bubble bokeh | `nervous soap-bubble bokeh with bright rings around each disc` | 光斑带亮环、背景躁动 |
| 柔和落差 | smooth focus falloff | `smooth focus falloff, no hard transition between sharp and blurred` | 虚实过渡拉长、无明显分界线 |
| 分裂屈光度 | split diopter | `split-diopter shot: the near profile on the left and the far figure on the right both sharp, the middle of the frame blurred` | 两个不连续焦平面共存、画幅中部糊【需核：可能被解成糊块】 |

**互斥**：`shallow depth of field` 与 `environment everywhere readable` 互斥；`deep focus` 与 `creamy bokeh` 互斥。两者同写会得到「人脸清楚、背景半糊」的中间态。

## 6. 镜头缺陷

缺陷是光学不完美的可见痕迹，**必须与拍摄条件配对**：没有强光源却写眩光，模型会凭空造一个光源，构图被破坏。

| 中文 | English | 可直接抄进提示词的英文短语 | 它改变画面的哪一部分 |
| :--- | :--- | :--- | :--- |
| 暗角 | vignette | `dark corner vignette, the four corners falling off into black` | 四角压暗、中心相对变亮 |
| 面纱眩光 | veiling flare | `veiling flare washing the lower right corner into milky haze, contrast dropping there` | 局部对比下降、出现乳白雾层 |
| 鬼影 | ghosting flare | `a chain of small green-blue ghost reflections running diagonally across the frame` | 一排彩色小亮点斜穿画面 |
| 红色光晕 | halation | `red-orange halation blooming around the window highlights, bleeding into the surrounding shadow` | 高光外圈发红、边缘扩散 |
| 色散 | chromatic aberration | `purple and green fringing along the high-contrast edge of the window frame` | 高反差边缘描彩边 |
| 边角软 | edge softness | `corners noticeably softer than the center, the outer third of the frame slightly smeared` | 画面外圈失焦、中心独占锐度 |
| 桶形畸变 | barrel distortion | `barrel distortion, the doorframe and shelf lines bowing outward near the edges` | 直线向外鼓、画面像被撑圆 |
| 枕形畸变 | pincushion distortion | `pincushion distortion, straight lines bending slightly inward toward the frame center` | 直线向内收、四角向外拉 |
| 变形拉丝 | anamorphic streak | `horizontal blue lens flare streak cutting across the frame at highlight height` | 一条水平亮线横穿画面 |
| 彗差 | coma | `stars near the corners smeared into small comet tails` | 四角亮点拖出尾巴 |
| 柔焦 / 黑雾 | diffusion filter | `black-mist diffusion: highlights blooming softly, blacks slightly lifted, micro-contrast reduced` | 高光溢出、暗部提亮、细节变糊 |
| 星芒 | star filter | `four-point star streaks radiating from each point light` | 每个点光源长出放射尖角 |
| 摩尔纹 | moiré | `fine rainbow moiré pattern across the screen's pixel grid` | 屏面出现彩条网纹 |
| 扫描线 | CRT scanlines | `visible horizontal CRT scanlines and slight barrel curvature of the glass` | 横向条纹 + 屏面外鼓 |
| 噪点 | luminance / chroma noise | `fine luminance grain with almost no color blotches` | 暗部出现单色颗粒、无彩色斑块 |

**注意**：`heavy vignette` 会整图压黑；`strong chromatic aberration` 会给整张脸描紫边；`noise` 单词单写常变成全图脏。缺陷词一条只留一个，且写清落点。

## 7. 画幅比例与画幅感

画幅首先由输出分辨率（`core/params.md` 的 W×H）决定，正文里的比例词只是加固。文字真正能影响的是**构图分配**：主体靠哪一侧、留白在哪、环境在上还是在下。

| 中文 | English | 可直接抄进提示词的英文短语 | 它改变画面的哪一部分 |
| :--- | :--- | :--- | :--- |
| 1:1 方幅 | square | `square composition, subject centered with equal margins` | 横向空间被砍掉、四周留白均等 |
| 3:2 | 3:2 photographic frame | `3:2 photographic frame` | 默认摄影比例、横竖都自然 |
| 16:9 | widescreen | `16:9 widescreen framing, a wide horizontal band of environment above the subject` | 横向环境带加宽、上下压缩 |
| 2.39:1 | scope / cinemascope | `2.39:1 anamorphic scope frame, the subject's head near the top edge, wide empty space to one side` | 上下裁切极狠、单侧留大片空白 |
| 9:16 竖幅 | vertical | `9:16 vertical composition, the figure stacked vertically, ceiling and floor implied` | 环境只能上下延伸、并排两人变挤 |
| 4:5 / 5:4 | portrait crop | `4:5 portrait crop, head near the top third` | 头位固定在上三分之一、下方留身 |
| 65:24 全景 | panoramic strip | `65:24 panoramic strip, a thin horizontal band of street` | 变成狭长横带、人物必小 |
| 中画幅平整感 | medium-format rendering | `medium-format rendering: even corner sharpness, gentle highlight rolloff, no perspective distortion` | 四角与中心一样锐、高光过渡变缓【需核：成因混杂，只作风格锚点】 |
| 移轴模型感 | tilt-shift miniature | `tilt-shift: a narrow horizontal band of sharpness across the middle, the top and bottom heavily blurred, shot from a high vantage point` | 中部一条清晰带，上下整片虚 |

**反例**：9:16 里写「横向环境带」会得到上下大片空白；`tilt-shift` 必须配高机位，平视写移轴只得到普通虚化；`2.39:1` 与竖排文字、竖屏裁切不兼容。

## 8. 特殊机位

这类机位自带可信度，因为把**拍摄条件的物理限制**画进了画面：固定支架 → 固定俯角，广角 → 畸变，廉价传感器 → 噪点与压缩痕，玻璃 → 反光。每条至少写两个限制痕迹，否则只得到一张普通照片。

| 中文 | English | 可直接抄进提示词的英文短语 | 它改变画面的哪一部分 |
| :--- | :--- | :--- | :--- |
| 行车记录仪 | dashcam | `dashcam POV through the windshield, the dark dashboard and wiper blades along the bottom edge, slight wide-angle warp, low-light sensor noise` | 画幅下缘被仪表台与雨刮占住、两侧轻微外鼓 |
| 监控 | CCTV | `CCTV still from a high ceiling corner, extreme wide angle looking down, fisheye curvature at the edges, washed-out exposure, timestamp in the corner` | 俯角固定、边缘弯成弧、曝光发灰 |
| 门镜 | door peephole | `peephole view: a circular image surrounded by black, strong fisheye bulge, the visitor's face distorted at the center` | 画面变成黑框中的圆、脸部中央鼓出 |
| 显微镜 | microscope | `microscope view, a circular field, shallow depth with only one plane in focus, a scale bar at the bottom` | 圆形视场、只有一层焦平面 |
| 航拍 | aerial / drone | `aerial drone shot from directly above, long shadows, roofs and roads forming flat geometry` | 地面成几何图形、阴影拉长 |
| 卫星图 | satellite | `satellite view, orthographic top-down, no atmosphere or shadows, terrain in muted false color` | 无透视无阴影、色相失真 |
| 翻拍屏幕 | screen photo | `photograph of a laptop screen: visible pixel grid, faint moiré rainbow bands, a soft reflection of the room across the glass, dark bezel along the edges` | 屏面出现网格与彩纹、玻璃上叠环境反光、四周留黑边 |
| 网络摄像头 | webcam | `laptop webcam framing, wide lens close to the face, slightly low angle, flat screen light on the skin, mild compression artifacts` | 脸部近距广角变宽、平光、边缘块状失真 |
| 执法记录仪 | bodycam | `bodycam view from chest height, very wide angle, the wearer's hands entering the bottom of the frame` | 视点降到胸口、画幅下缘多出自己的手 |
| 平板扫描 | flatbed scan | `flatbed scan, perfectly even light, zero perspective, object pressed flat against glass` | 零透视零阴影、物体被压平贴画幅 |

**写法要点**：翻拍屏幕的三件套（像素网格 + 摩尔纹 + 反光）缺一个，就退化成「屏幕内容截图」；CCTV 的时间戳属于图内文字，能不能渲染先按 `core/text-in-image.md` 判断。

## 9. 常见误用

| 别写 | 为什么掉质量 | 改成 |
| :--- | :--- | :--- |
| `cinematic` | 只把图拉向「青橙 + 宽画幅 + 压黑」的均值脸，常伴过饱和 | `teal shadows and warm amber skin, 2.39:1 scope framing, crushed blacks` |
| `professional photography`、`award-winning photo` | 空转词，不在可见信息分布里 | 写布光与镜头结果 |
| `8k`、`ultra detailed`、`masterpiece` | 空转，与解码能力无关 | `visible pores, frayed cotton fibers` |
| `DSLR`、`shot on Contax T2, 38mm` 单写 | 型号税未付：型号不带三个可见结果就是噪声 | 型号 + ≥3 个可见结果，或删型号留结果 |
| `bokeh` 单写 | 不指定虚实边界 → 整图糊 | `only her eyes sharp, the street behind dissolved into soft round discs` |
| `wide angle` + `shallow depth of field` | 物理相反，模型折中 | 二选一，或 `wide but stopped down, everything from hand to far wall sharp` |
| `macro` + `full body` | 画幅尺度相反 | 拆成两张需求 |
| `fisheye` + `straight architectural lines` | 相反 | `wide angle with mild barrel distortion` |
| `telephoto` + `environment fully readable` | 相反 | `35mm environmental portrait, deep focus` |
| `low angle` + `full body` + `long legs` | 三者叠加常出畸形腿长与巨大脚掌【需核：腿变长只在姿势配合时成立】 | 删 `long legs`，写 `both feet flat on the ground` |
| `high angle` + `full body` | 头大身短，缩成四头身 | `high angle but the full figure still readable, camera only slightly above eye level` |
| `dutch angle` + 建筑直线 / 图内文字 | 直线与文字全歪，文字渲染失败率上升 | 有文字时去掉 dutch |
| `lens flare` 无强光源 | 模型凭空造灯，构图崩 | 先写光源位置，再写眩光 |
| `extreme close-up` + `both hands doing X` | 画幅里没有手的容身位置 | `insert shot of the hands` |
| `full body` 不写脚与地面 | 五头身 | `both feet planted on the wet asphalt, full body from head to shoes` |
| 一条里两个以上焦距数字 | token 内耗 + 描述互相打架 | 只留一个，紧跟结果 |
| `F1.4`、`f/1.4` 单写 | 光圈值是画面外信息 | `only the near eye sharp, everything behind dissolved` |
| `HDR`、`ray tracing`、`Unreal Engine` | 拉向 CG 塑料感 | 走胶片与皮肤纹理 |

## 10. 可直接抄的镜头句配方

1. `35mm environmental portrait, she occupies about a third of the frame, the whole workshop legible around her, deep focus from the near bench to the far door.` —— 要交代环境又要看清人时用。
2. `telephoto compression, the crowd behind her stacked into flat overlapping layers pressing against her shoulders, only her face sharp.` —— 人群里孤立一个人、要挤压感时用。
3. `wide angle close in, her outstretched hand and the glass oversized in the lower frame, the alley receding small and steep behind.` —— 强调纵深与动势时用。
4. `over-the-shoulder shot, the out-of-focus back of his head and shoulder filling the left foreground, her face sharp in the right third at eye level.` —— 对话与在场感。
5. `CCTV still from a high ceiling corner, wide angle looking down, washed-out exposure, faint fisheye curvature, timestamp in the corner.` —— 需要「记录感」而非摆拍时用。
6. `directly overhead top-down view, the hands and the scattered papers laid out flat, no horizon line, even soft light from above.` —— 桌面动作、图形化构图时用。
