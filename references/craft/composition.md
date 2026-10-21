# 构图与版面

**何时查本文件**：用户点名版式（三分、对称、对角线、S 线）、要求空间层次（前景／中景／背景、景深）、要求留白或呼吸感、要求多人／群体排布、要求图文版面（海报、封面、图内标题层级）时。

**总规则**：构图术语必须先降维成「谁在画面哪个区域、占多大、周围剩什么」。训练 caption 只记录可见内容，所以 `rule of thirds`、`composition`、`balanced` 这类分析框架词基本不响应（见 §9），只有方位、占比与否定句才落地。

**定式句式**：`[物件] + [方位／占比] + [旁边是什么／不是什么]`。禁写「某处留白」，改写「某处只有什么、没有什么」。写前三问：能用手在图上点出位置吗 → 能换成比例或层数吗 → 这条在防哪种错画面；一问答不上就换写法或删掉。

像素级落位、bbox、多框坐标不在本文件范围，见 `core/layout.md`。

## 1. 基础版式：三分、黄金分割、对称、对角、三角、S 线

| 中文 | English | 可直接抄进提示词的英文短语 | 它解决什么画面问题 |
| :--- | :--- | :--- | :--- |
| 三分法 | rule of thirds | `She stands in the left third of the frame, her eyes one third down from the top; the right two thirds are empty pale sky with nothing in it.` | 主体死居中、背景抢权；有空地可留的单主体画面。画面密度高时退化成「偏一点点」，像手抖【需核】 |
| 黄金分割落点 | golden ratio | `The vase sits just left of center and a little below the middle line, with a long empty wall above it.` | 比三分更稳的中偏置；静物、单栋建筑。写 `0.618` 或 `golden ratio` 不响应，只能靠「略偏左、略低于中线」近似 |
| 中心对称 | center symmetry | `A vertical line splits the frame at the exact middle: identical rows of red pillars left and right, the floor running to one vanishing point at center.` | 庄重、压迫、仪式感；建筑正面、正面人像。人多或有机形状多时对不上，正中人脸左右两半不均 |
| 对角线 | diagonal composition | `The railing enters at the bottom-left corner and runs to the upper-right corner, cutting the frame into two triangles; she leans on its middle.` | 静态画面要张力；坡道、栏杆、楼梯、伸展肢体。对角线穿过脸部即变切线事故，地平线易被带歪 |
| 三角构图 | triangle composition | `Three heads form a triangle in the lower two thirds: the tallest figure centered behind, two shorter figures lower and to either side, each head clear against the sky.` | 三人以上群体的稳定感。直接写 `triangle composition` 偏弱，必须拆成高度差 + 位置差 + 轮廓分离 |
| S 形曲线 | S-curve | `A dirt path enters at the bottom edge, bends left at mid-height, then curves back right and disappears behind the trees at the upper right.` | 引导视线深入、加纵深；小径、河流、飘带、裙摆。只写一个弯就退化成斜线，弯道被主体挡住则消失 |

一整组画面统一用一套坐标（都写方位 + 占比，或都写三分落点）。同一张图混用「交点 + 螺旋 + 三角」三套，模型只挑一套执行，其余变噪声【推断】。

## 2. 引导线与框架构图

| 中文 | English | 可直接抄进提示词的英文短语 | 它解决什么画面问题 |
| :--- | :--- | :--- | :--- |
| 引导线 | leading lines | `Wet tram rails run from the bottom edge of the frame straight up the street toward her back.` | 画面散、视线无落点。必须同时写两点：起点在哪个边、收束到谁身上；线在多处交叉则视线打架 |
| 汇聚／灭点 | vanishing point | `All the floor lines of the corridor meet at a single point on the far wall at the height of her hips.` | 强纵深、隧道感、秩序感。灭点正对头部会变成头后光环，写 `one-point perspective` 无效 |
| 画中画 | frame within frame | `She is seen through a doorway: dark doorjambs fill the left and right edges, the bright kitchen is a rectangle around her.` | 聚焦、窥视感、把杂乱挡在外面。内框过小会被整体忽略只画内景；内外框颜色相近则框消失 |
| 前景压边 | repoussoir | `A dark out-of-focus tree trunk runs along the left edge from top to bottom, covering about one sixth of the frame width.` | 制造「我在现场」的深度感、压住空荡的一侧。写 `repoussoir` 无效，只认「边缘暗块 + 虚化 + 占宽比」；给材质细节会把虚化吃掉，变实心黑块 |
| 镜面二次框 | mirror frame | `A tall mirror on the right wall reflects her back; the wooden frame of the mirror is fully inside the image.` | 同框两个视角、空间复杂度。镜中内容常与本体不一致（衣服、姿势对不上），镜中易多手 |
| 顶部结构 | archway | `A stone arch fills the top third of the frame as a curved band, with the street visible through it below.` | 顶部补结构、避免天空过空。拱门圆心常歪，与柱子组合易粘连 |

## 3. 三层空间：每层只给一个角色

| 中文 | English | 可直接抄进提示词的英文短语 | 它解决什么画面问题 |
| :--- | :--- | :--- | :--- |
| 前景：遮挡 + 尺度参照 + 虚化 | near foreground | `In the near foreground at the bottom-left corner, a blurred cluster of white flowers covers the corner and part of her skirt, out of focus.` | 给尺度与在场感。必须给「位置 + 占比 + 虚化」三件套；写成花瓣细节则虚化被细节吃掉 |
| 中景：主体，全画面最清晰 | midground subject | `She stands at mid-distance, fully sharp from head to feet, about half the frame height.` | 让清晰度有归属。不写 `fully sharp` 与高度占比，模型会把清晰度平铺到全画面 |
| 背景：交代地点 + 亮度对比 | background | `Far behind her the street recedes into soft haze, clearly darker than her face.` | 交代环境并托住主体。给「更暗／更亮」的比较级，不给背景细节清单 |

**景深塌陷的成因【推断】**：层数超过三时模型缺少分层手段，只剩下最省事的「亮度分区」，四层需求被压成上暗／中亮／下暗三条横带，看起来就是画面上下各一条黑边；同时四个层级词争抢同一批条件 token，互相削弱。防塌五条：

1. 只写三层，每层绑一个专有物件（花丛／她／街道），不重复写层级名词。
2. 一层一维：清晰度、亮度、色温、尺度各只用一次，两层不要都用「暗」。
3. 删掉 `middle ground`、`in between` 这类抽象层词，直接写物件方位。
4. 前景占比写数字：`about one sixth of the frame width`。
5. 已出现上下黑边时正负一起补：正面 `evenly lit from edge to edge`，负面 `letterbox, black bars, heavy vignette`。

## 4. 留白与视线余量

| 中文 | English | 可直接抄进提示词的英文短语 | 它解决什么画面问题 |
| :--- | :--- | :--- | :--- |
| 留白 | negative space | `The upper two thirds of the frame contain nothing but flat pale grey sky; no birds, no wires, no clouds.` | 高级感、文字位、情绪压强。留白是「缺席」，必须靠否定句表达；不给「没有什么」就一定会长出杂物 |
| 视线余量 | looking space | `She faces right; the right third of the frame in front of her face is empty wall, and nothing crosses between her nose and the frame edge.` | 人物不憋、有「要去的地方」。主体朝右却放在右三分 → 脸贴边、画面憋死 |
| 主体占比 | subject area | `The subject takes about one third of the frame area; the rest is quiet plain background.` | 控制呼吸感。面积不给数字时模型倾向填满 |
| 满构图 | horror vacui | `Every part of the frame is packed: shelves, jars, hanging herbs, stacked crates, front to back, with no empty area anywhere.` | 集市、复古海报、要「丰盛」。不列举四类以上物件模型会自己留白，且易糊成一团 |
| 边缘留空 | margin | `A clean empty border of about one tenth of the frame width runs around all four sides.` | 印刷、拼贴、装裱感。边框过大会被理解成画框 |
| 视线引导 | eyeline lead | `Her gaze and her raised hand both point to the small bright window at the upper right, and nothing else in the frame is that bright.` | 让观众看对地方。目标不够亮则视线落空；画面有两个同样亮的东西则视线分裂 |

比例速查：极简海报主体占 1/6 ~ 1/3；常规人像 1/3 ~ 1/2；环境人像主体 1/3、环境 2/3；满构图不给比例，只写 `no empty area`。

## 5. 对称与非对称平衡

| 中文 | English | 可直接抄进提示词的英文短语 | 它解决什么画面问题 |
| :--- | :--- | :--- | :--- |
| 对称平衡 | symmetrical balance | `The left and right halves carry the same amount of dark shape, mirrored around the center line.` | 秩序、庄重、产品正面图。对称要求成对物真的成对，模型常少画一侧 |
| 非对称平衡 | asymmetrical balance | `She is small and bright in the left third; the right side is filled by one large dark mass of rock that balances her.` | 生动但有重心；风景人像、街拍。只写 `balanced` 无效，必须写「小亮 vs 大暗」的具体对比 |
| 视觉重量 | visual weight | `A broad black wall takes the right half of the frame; she stands small in the lit gap on the left.` | 控制哪边压得住。两边都写「大面积深色」→ 相互抵消，画面塌 |
| 对角线张力 | diagonal tension | `Her body leans along a strong diagonal from lower left to upper right, off balance, one foot lifted; the horizon stays level.` | 动感、失衡美感、运动。主体一倾斜就必须同时锁地平线，否则整图歪 |
| 三角稳定 | triangular stability | `His wide stance and the two arms braced on the table form a stable triangle at the bottom of the frame.` | 力量感、威慑、静态人物。手撑桌易生多余手指，需配负面 |

平衡是一句**比较**，不是一句**状态**：能写的只有「A 的大小／明度 vs B 的大小／明度」。

## 6. 群体排列：怎么不画成合影

| 中文 | English | 可直接抄进提示词的英文短语 | 它解决什么画面问题 |
| :--- | :--- | :--- | :--- |
| 非网格群像 | asymmetric ensemble | `Five people stand at three different depths: two in the near left, one tall in the center behind them, two further back on the right; no two heads at the same height.` | 打破合影感；乐队、团队、街头群像。人数过多时模型开始复制脸【需核】，深度超过三档又会塌（见 §3） |
| 前后错落 | staggered depth | `Their heads are staggered at different heights, each head fully clear against the background.` | 头重叠、轮廓粘连。只写 `staggered` 不够，必须配合「每颗头都不重叠」 |
| 高低差 | height variation | `The tallest stands at the back, the shortest sits in the near foreground, so their heads sit on three different levels.` | 平视一排的死板。坐着的人易被画成儿童 |
| 遮挡关系 | overlap | `The man in front overlaps the woman behind him at the shoulder, half of her body hidden behind his arm.` | 交代深度、避免并列。遮挡比例不给，两个人溶成一体 |
| 朝向差异 | varied facing | `Two face the camera, one turns to the left in profile, one looks down at the table.` | 全员正脸等于证件照。侧脸与正脸混排时脸型易不一致 |
| 同一人只出现一次 | each appearing once | `Exactly four distinct people, each appearing once, arranged asymmetrically rather than in a grid.` | 人数与个体数对不上、多画半个人 |
| 反合影 | anti-group-photo | 负面：`lined up, standing in a row, evenly spaced, group photo, class photo, symmetrical lineup` | 压掉最强的合影先验。只靠正面描述压不住，正负必须一起写 |

```text
Four people fill the narrow alley at three different depths: a courier in the near right, half out of frame,
a tall woman standing behind him in the center, and a couple further back at the left, partly hidden by a hanging sheet.
Their heads sit at four different heights; a strip of bright sky separates every silhouette.
```

## 7. 构图事故预防

| 中文 | English | 可直接抄进提示词的英文短语 | 它解决什么画面问题 |
| :--- | :--- | :--- | :--- |
| 切线 | tangent | `A clear gap of grey wall separates her shoulder from the doorframe; no edge of the frame touches her outline.` | 轮廓与背景线条相碰，看着「粘住」。只能正面写「有间隙」，写 `no tangent` 无效 |
| 主体贴边 | edge crowding | `Her whole body sits inside the frame with empty floor visible on all four sides.` | 肢体被边缘切断的头号来源 |
| 头顶被切 | cropped head | `The top of her head is well below the top edge, with clear sky above her hair.` | 半身与全身图必写，近景可省 |
| 脚被切 | cut off feet | `Her shoes are fully visible, floor under the soles and space below the toes.` | 全身图必写，负面补 `cut off feet, cropped legs` |
| 地平线穿头 | horizon through head | `The horizon line passes behind her shoulders, well below her chin.` | 头被一条横线切成两段；也可写 `the horizon sits at her waist level` |
| 背景杆子 | pole behind head | `The sky directly above her head is empty; no pole, no wire, no lamp post behind her.` | 头上长杆。最有效的是指名否定，把最常见的三种杆状物逐个否掉 |
| 轮廓粘连 | merged silhouettes | `The two figures are separated by a strip of bright sky between their arms and heads.` | 双人图必写，负面补 `merged bodies, conjoined silhouettes` |
| 手脚多出 | extra limbs | `One hand rests on the table, the other hangs at her side; both arms visible, nothing else.` | 用「数清手脚」预防比堆负面词稳 |
| 文字压脸 | text over face | `The headline sits in the empty band above her hat; no text crosses her face.` | 图文混排必备 |

预防句是**近邻约束**：紧跟主体描述之后、场景描述之前。写在段末时构图已定，改不动。通用兜底句（几乎任何构图都能加）：

```text
Her entire figure is inside the frame, every limb separated from the background by a clear edge.
```

## 8. 图文版面：标题、栏数与留白

| 中文 | English | 可直接抄进提示词的英文短语 | 它解决什么画面问题 |
| :--- | :--- | :--- | :--- |
| 网格与栏数 | grid / columns | `A strict two-column grid with a wide outer margin; the text block sits only inside the left column.` | 版面不散、像「设计过的」。写 `grid` 单独无效，要给栏数与范围 |
| 标题层级 | type hierarchy | `A bold headline in the top fifth, a smaller subtitle directly beneath it, a block of small body text at the lower left.` | 字全一样大等于没有层级。三级字号差没写，模型把三段排成一样大 |
| 字图占比 | text-to-image ratio | `The headline takes the top third; the photo fills the lower two thirds.` | 图被字淹或字被图挤。与留白率冲突时以留白率为准 |
| 版面留白 | white space | `About forty percent of the poster stays blank cream paper.` | 呼吸、杂志感。比例过高时模型把主体一起缩小 |
| 通栏标题 | full-width headline | `A single line of huge black type runs across the entire top of the poster, edge to edge.` | 强冲击、杂志封面。字太长会压缩变形或糊 |
| 角落小字 | corner caption | `Four lines of tiny right-aligned text stacked in the lower-right corner.` | 版权条、规格、文艺感。字太小必糊，先减字再谈版式（字号与分辨率见 `core/text-in-image.md`、`core/params.md`） |
| 竖排 | vertical text | `A narrow vertical column of Chinese characters down the right edge, one character per cell.` | 中式、日式版面。竖排里的阿拉伯数字会挤成一坨 |

一句话说清版面关系，把「谁在哪 + 谁多大 + 剩下什么空着」压进一句：

```text
A full-width headline across the top, the product photo centered in the middle third,
and a small block of text in the lower-right corner, with the rest of the page left blank.
```

像素级落位（bbox、多框坐标、文字的精确位置）不在本文件范围，见 `core/layout.md`。版面描述再准也救不回放不下的字号——先减字，再谈版式。

## 9. 空转词清单

| 空转词 | English | 换成（可直接抄） | 为什么不响应 |
| :--- | :--- | :--- | :--- |
| 三分法术语 | `rule of thirds` | `in the left third, the rest empty sky` | 是分析框架，不对应任何可指认的像素 |
| 黄金比／螺旋术语 | `golden ratio` / `golden spiral` | `just left of center, long empty wall above` | 模型算不出比例，只能近似成「略偏」 |
| 构图 | `composition` / `well-composed` | 直接写方位句 | 抽象评价，无像素对应 |
| 平衡／和谐 | `balanced` / `harmonious` | `small bright figure left, large dark mass right` | 是判断不是描述 |
| 美感词 | `aesthetic` / `beautiful` / `stunning` | 写材质、光线、比例 | 无信息量 |
| 电影感构图 | `cinematic composition` / `dynamic composition` | `railing from bottom-left to upper-right corner` | 风格标签，非空间事实 |
| 摄影光环 | `professional photography` / `award winning` | `single hard key light from the left` | 评价词，不在 caption 分布里 |
| 留白（单写） | `negative space` | `nothing but flat grey sky` | 只学到少细节，学不到少东西 |
| 极简（单写） | `minimalist` | `one chair, bare walls, bare floor` | 同上，且常被读成扁平插画 |
| 分层（单写） | `deep depth of field` / `layered composition` | 逐层写物件 + 清晰／虚化 | 抽象，没有分层指派 |
| 数量玄学 | `rule of odds` / `divine proportion` | `three candles, one taller` | 极小众术语 |
| 中文评价词 | 构图精美／大片感／高级感 | 写具体方位、比例、光比 | 同 `aesthetic` |
| 质量堆料 | `8k` / `ultra detailed` / `masterpiece` | `visible fabric weave, fine grain` | 不在 caption 分布里 |

半有效（可留但必须配「结果」一起写）：`bokeh`、`shallow depth of field`、`wide angle`、`low angle`、`top-down view`、`silhouette`、`symmetry`（名词略强于形容词）、`centered`。

可靠性排序（强 → 弱）【推断】：`in the left third / upper half / lower-right corner` > `behind / in front of / beside / above` > `centered / fills the frame` > `two layers / three rows` > `at a diagonal` > `symmetric` > `rule of thirds` ≈ `composition` ≈ 0。

## 10. 可直接抄的构图句配方

**单人 + 留白 + 视线余量**
```text
She stands in the left third of the frame, fully sharp, about half the frame height, facing right,
with the right third left as empty pale wall and nothing crossing her face.
```

**三层空间（防塌）**
```text
In the blurred near foreground a dark table edge crosses the bottom-left corner.
She stands at mid-distance, sharply focused head to feet, about half the frame height.
Behind her the room recedes into soft grey light, darker than her shirt.
```

**走廊纵深：前景压边 + 引导线 + 灭点**
```text
A dark blurred doorframe runs down the left edge, covering about one sixth of the frame width.
Wet floor tiles run from the bottom edge to a single vanishing point on the far wall, at her waist height.
```

**三人以上非网格群像**
```text
Three people fill the narrow street at three different depths: a courier in the near right, half out of frame,
a tall woman behind him in the center, a man further back at the left.
Their heads sit at three different heights; a strip of bright sky separates every silhouette.
```

**对称建筑正面**
```text
The frame splits at the exact middle: identical rows of columns left and right mirrored around the center line,
the stone floor running to one vanishing point at the center of the far doorway.
```

**海报版面一句话**
```text
A bold headline across the top fifth, a smaller subtitle beneath it, the product centered in the middle third,
a small block of text in the lower-right corner, and the rest of the page left blank cream.
```

自检五条：每层是否只有一个角色；有没有混进 §9 的词；事故预防句是否紧跟主体；留白是否用了否定句；比例、层数、人数是否给了数字。
