# 美学词汇：光、色、技法、流派、材质
要指定**光位、色彩关系、画种技法、风格流派、材质氛围**时读本文件；只缺镜头或版式时读 `camera.md` / `composition.md`。官方 caption 规范要求逐项描述 `colors`、`lighting`、`artistic style` 三个维度且只写图上可见信息，落在这三个维度里的词（`loop lighting`、`teal-and-orange`、`cel shading`）像素对应稳定；作者名、品牌名、软件名、渲染引擎名单写无效。
「可抄英文短语」是起始写法，替换主体与方位即可。通道列：`写实` 走 `styles/photo.md`，`二次元` 走 `styles/anime.md`，`通用` 两条通道都成立；混合画面先读 `styles/hybrid.md` 的三问再回来挑行。
## 1. 光位分工
一条光只写一个主控。同句出现两个方向相反的主光（`window light from the left` + `hard spotlight from behind`）会被平均成平光；要多层就写明每层负责哪个部位。
| 中文 | English | 可抄英文短语 | 可见结果 | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 主光 | key light | `a single strong key light from the upper left` | 定投影方向与暗部位置，其余光只提亮不改几何 | 通用 |
| 辅光 | fill light | `a weak fill light lifting the shadow side without erasing it` | 暗部有细节但不消失，明暗比被压缩 | 通用 |
| 轮廓光 | rim light | `a thin bright rim light along the hair and shoulder edge` | 边缘一圈窄亮线，主体从背景里被切出来 | 通用 |
| 发丝光 | hair light | `a top-back hair light picking out individual stray strands` | 发梢分离、细发丝发亮 | 写实 |
| 负补光 | negative fill | `negative fill on the shadow side, the shadow side crushed to near black` | 暗侧更黑、边缘更利，明暗比被动拉大 | 写实 |
| 实用光 | practical light | `a practical table lamp visible in frame lighting her from below-left` | 光源本体入画，光向与灯位严格一致 | 通用 |
| 顶光 | top light | `a single overhead ceiling tube, eye sockets in shadow` | 眼窝、鼻下、颌下三处暗区 | 通用 |
| 底光 | underlight | `harsh uplight from a fire below, shadows climbing upward on the wall` | 投影向上、面部结构反转，与顶光记忆相反 | 通用 |
| 眼神光 | catchlight | `a small square catchlight in each pupil` | 瞳孔内一小块亮斑，形状即光源形状 | 写实 |
| 接触阴影 | contact shadow | `a tight dark contact shadow where the cup meets the table` | 物体与承托面之间一条深色窄影，缺它像贴纸 | 通用 |
| 剪影 | silhouette / contre-jour | `full silhouette against a blown-out window, no detail on the body` | 主体全黑、背景过曝，只剩外形 | 通用 |
| 硬光 | hard light | `hard direct sunlight, crisp-edged shadows with a sharp boundary` | 投影边缘锐利、明暗交界线清楚 | 通用 |
| 柔光 | soft light | `large soft source, shadow edges fully diffused, no hard terminator` | 明暗过渡宽，找不到交界线 | 通用 |

## 2. 六式人像布光
二次元通道里光位词收益有限，更吃「色片 + 硬软过渡」，要写成可见形状：`a hard-edged shadow dividing the face in half`。【需核】宽光显宽、窄光显窄的复现稳定性取决于训练图分布，长期使用前同 seed 做一次 A/B。
| 中文 | English | 可抄英文短语 | 可见结果 | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 伦勃朗光 | Rembrandt lighting | `Rembrandt lighting, a small triangle of light on the shadow-side cheek below the eye` | 暗侧脸颊一块倒三角亮区，鼻影与颊影相连 | 写实 |
| 分割光 | split lighting | `split lighting, exactly half the face in shadow, dividing line down the nose bridge` | 脸沿鼻梁一分为二，暗侧几乎无细节 | 写实 |
| 蝴蝶光 | butterfly lighting | `butterfly lighting from directly above the lens, a small butterfly shadow under the nose` | 鼻下一小片蝶形影，两颊对称微影，下颌线清晰 | 写实 |
| 环形光 | loop lighting | `loop lighting, a small shadow loop beside the nose that does not touch the upper lip` | 鼻侧一小段弧形影，不连到上唇 | 写实 |
| 宽光 | broad lighting | `broad lighting, the side of the face turned to camera is the lit side` | 脸显宽、显亲和，受光面积占面部比例更大 | 写实 |
| 窄光 | narrow lighting | `narrow lighting, only the far cheek is lit, the near cheek in shadow` | 脸显窄、下颌线更利，暗部压缩轮廓 | 写实 |

## 3. 明暗比与风格化光影
`high-key` 与 `low-key`、`chiaroscuro` 与 `flat overcast daylight` 不能同框，同时出现会被平均成中间调。写 `low-key` 时就删掉一切提亮词（`bright`、`luminous`、`glowing`、`fair porcelain skin`、`daylight`）——删冲突词比补 `very dark` 有效。
| 中文 | English | 可抄英文短语 | 可见结果 | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 高调 | high-key | `high-key lighting, near-white background, almost no shadow on the face, milky lifted blacks` | 全图明亮、暗部极浅、对比低 | 通用 |
| 低调 | low-key | `low-key lighting, one narrow pool of light, most of the frame near black` | 大面积近黑、单一光池，暗部占比远大于亮部 | 通用 |
| 明暗对照 | chiaroscuro | `chiaroscuro, forms modeled only by a slow falloff from light into deep shadow` | 体积靠长渐变塑造，无硬边 | 通用 |
| 暗黑主义 | tenebrism | `tenebrism, a single raking spotlight out of total darkness, everything else swallowed in black` | 光像切进来，背景明度归零 | 通用 |
| 晕涂 | sfumato | `sfumato, every edge dissolving in a smoky haze, no contour anywhere` | 无清晰轮廓线，边界糊成雾 | 通用 |
| 环境遮蔽 | ambient occlusion | `soft ambient occlusion in every corner and fold, grounded shadows` | 角落、褶皱、缝隙自然变暗，物体不再浮在环境里 | 写实 |
| 光线衰减 | light falloff | `steep light falloff, the far wall already fallen into black` | 离光源越远越暗，衰减幅度一眼可见 | 通用 |

## 4. 时间、色温与光源性质
体积光**必须配介质**：只写 `volumetric lighting` 不写 `dust / fog / smoke / steam`，多半得到均匀柔光而不是光柱。双色色片必须写左右或前后（`left cheek` / `right cheek`），写成 `pink and blue light` 会随机分配甚至混成紫色。
| 中文 | English | 可抄英文短语 | 可见结果 | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 棚拍闪光 | studio strobe | `bare studio strobe, hard specular hotspot on the forehead, sharp shadow on the backdrop` | 高光点小而亮、投影边缘硬 | 写实 |
| 窗光 | window light | `soft directional window light from camera left, gradual falloff into the room` | 单侧柔光、缓慢衰减、暗部大 | 通用 |
| 阴天光 | overcast daylight | `flat overcast daylight, no cast shadows anywhere, cool grey cast` | 几乎无投影、低对比、整体偏冷灰 | 写实 |
| 黄金时刻 | golden hour | `golden hour backlight, long shadows raking across the ground, warm amber rim on the hair` | 暖橙光、影子极长、发丝金边 | 通用 |
| 蓝调时刻 | blue hour | `blue hour, deep cobalt ambient sky against warm tungsten windows` | 环境深蓝、人造光暖橙，冷暗暖亮 | 通用 |
| 钨丝灯 | tungsten | `tungsten interior light, warm orange cast on skin and walls` | 整体橙黄，肤色偏暖 | 通用 |
| 荧光灯 | fluorescent | `greenish fluorescent ceiling tubes, uneven top light, sickly green cast` | 偏绿、顶光不均 | 通用 |
| 双色色片 | two-tone gel lighting | `split gel lighting, electric cyan on the left cheek, hot magenta on the right cheek` | 脸左右各一色，交界落在面部中线 | 通用 |
| 单色色片 | gel wash | `the whole scene washed in one deep red gel, monochrome red lighting` | 全图单一色相，结构只靠明度分辨 | 通用 |
| 体积光 | volumetric light | `volumetric god rays cutting through a dusty room, visible light shafts with soft edges` | 光束本体可见，带柔边与明暗条纹 | 通用 |
| 反弹光 | bounce light | `warm bounce light off the wooden floor filling the underside of the jaw` | 暗部带上反弹面的颜色与方向 | 写实 |
| 空气尘雾 | haze / dust in the air | `thin dust haze in the air, the background losing contrast behind it` | 远处对比下降、亮部发灰、黑位抬高 | 通用 |

## 5. 色彩
饱和度和明度必须成对写（只写 `pastel` 可能得到高明度高饱和的糖果色，只写 `desaturated` 可能得到脏灰），稳定式是 `high value, low chroma`；二次元肤色写 `skin tone variation` 会退化成脏斑，改用 `a soft cool tint along the shadow edge of the face`。
| 中文 | English | 可抄英文短语 | 可见结果 | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 明度分层 | value structure | `a clear three-value structure: bright highlights, mid-tone skin, near-black background` | 缩略图状态也能认出主体轮廓 | 通用 |
| 低对比 | low contrast | `compressed tonal range, milky shadows, no true black anywhere` | 全图发灰，明度直方图两端被裁掉 | 通用 |
| 高对比 | high contrast | `high contrast, crushed blacks against clipped white highlights` | 黑白各自成块，中间调很少 | 通用 |
| 明暗节奏 | tonal rhythm | `repeating pattern of bright windows against dark walls` | 明暗交替形成视觉节拍 | 通用 |
| 邻近色 | analogous palette | `analogous palette of teal, sage green and pale blue-green` | 全图和顺、对比弱，色相环上相邻无冲突面积 | 通用 |
| 互补色 | complementary palette | `complementary palette, warm amber subject against a cold blue ground` | 主体与背景互撞，主体跳出来 | 通用 |
| 分裂互补 | split-complementary | `split-complementary scheme, warm terracotta against blue-green and violet` | 有对比但不刺眼，冲突被摊薄 | 通用 |
| 三角配色 | triadic palette | `triadic palette of mustard yellow, teal and muted red` | 三色均势，无主从 | 通用 |
| 单色 | monochrome | `monochrome in a single deep indigo, structure read only by brightness` | 只有一个色相，色相通道被锁死 | 通用 |
| 双色调 | duotone | `two-ink duotone print, black and burnt orange only` | 所有像素只落在两色连线上 | 通用 |
| 冷暖分离 | warm/cool separation | `warm skin against a cool blue-grey environment` | 主体与背景分属冷暖两侧，最省力的主体分离 | 通用 |
| 主色占比 | dominant color ratio | `the frame dominated by desaturated concrete grey, one small red accent` | 大面积底色加小面积强调，面积差制造重心 | 通用 |
| 青橙调 | teal-and-orange | `teal-and-orange grade, deep teal shadows, warm amber skin tones` | 暗部青、肤色橙，互补色对固定在两个位置 | 写实 |
| 灰调 | desaturated | `desaturated muted palette, everything pulled toward grey, low chroma throughout` | 全图发灰，色相保留但彩度整体压低 | 通用 |
| 漂白留银 | bleach bypass | `bleach-bypass look, silver retained in the highlights, crushed shadows, near-monochrome` | 高光发银白、饱和极低、反差大 | 写实 |
| 粉彩 | pastel | `pastel palette, high value low chroma, pale mint cream and powder pink` | 明亮寡淡、粉感，明度高彩度低 | 通用 |
| 高彩度 | high-chroma | `high-chroma saturated poster colors, pure cadmium red and ultramarine` | 颜色纯、边界硬，接近颜料原色 | 二次元 |
| 大地色 | earth tone | `earth tone palette of ochre, burnt sienna, olive and umber` | 暖褐稳定，彩度中等明度偏低 | 通用 |
| 霓虹双色 | neon bimodal | `electric cyan and hot magenta neon only, no other hue in frame` | 只有两个饱和色，其余归黑，中间色相缺失 | 通用 |
| 褪色旧照 | faded / sun-bleached | `faded sun-bleached color, cyan shift in the shadows, yellowed highlights` | 高光偏黄、暗部偏青，整体失饱和 | 写实 |
| 限色 | limited palette | `strictly limited to four colors: cream, rust, charcoal, forest green` | 颜色极简、画面干净，去掉随机配色 | 通用 |
| 冷环境暖肤色 | warm skin in a cool environment | `warm sunlit skin against a cold blue-grey interior, temperature contrast kept clean` | 皮肤是画面唯一暖区，人自动成为焦点 | 通用 |
| 环境染色 | color contamination | `the green wall casting a green tint onto the shadow side of her face` | 暗部带环境色，皮肤不再塑料白 | 写实 |
| 肤色分区 | skin tone variation | `warmer red at the nose and ears, cooler olive on the jaw, faint blue in the beard shadow` | 一张脸上多个色相，来自血管密度与角质厚度不均 | 写实 |
| 白平衡错配 | white balance mismatch | `uncorrected white balance, warm tungsten skin against a daylight-blue window` | 同图两种色温并存 | 写实 |

## 6. 绘画与平面技法
技法词的冲突：`impasto` / `gouache` / `watercolor` 与 `black outlines`、`lineart` 天然对立，同框退化成不存在的画种；`cel shading` 与 `soft shading` 必须二选一，同写得到半硬半软的糊面；`screentone` 只配 `monochrome / greyscale`，带彩色会局部留色。写实通道里出现任何颜料词都会把照片拉成画，要质感改用 §8。
| 中文 | English | 可抄英文短语 | 可见结果 | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 厚涂 | impasto | `heavy impasto, thick ridges of oil paint catching the light, visible bristle marks` | 颜料有立体凹凸，脊线带真实高光与投影 | 二次元 |
| 刮刀 | palette knife | `palette knife work, flat scraped planes with sharp straight ridges` | 平直刮痕、块面锋利 | 二次元 |
| 水粉 | gouache | `opaque matte gouache, flat even coverage, chalky dry surface` | 哑光、覆盖力强、无透明叠色 | 二次元 |
| 水彩渲染 | watercolor wash | `transparent watercolor washes, pigment pooling at the edges, rough cold-press paper grain showing through` | 透明叠色、边缘积色、纸纹透出 | 二次元 |
| 水墨晕染 | ink wash | `sumi ink wash, graded dilution from black to pale grey, soft bleeding into damp paper` | 单一墨色的浓淡梯度，边缘洇开 | 二次元 |
| 飞白 | dry brush | `dry-brush strokes with broken flying-white gaps, the paper showing through the ink` | 笔迹中间露白、毛糙断续 | 二次元 |
| 喷枪 | airbrush | `airbrushed gradients, perfectly smooth transitions, zero brush texture` | 无笔触、渐变极顺滑 | 二次元 |
| 数字厚涂 | painterly digital painting | `painterly digital painting, soft blended strokes, color picked from the neighbors` | 有笔触但边缘被吸色软化 | 二次元 |
| 赛璐璐上色 | cel shading | `cel shading, two flat tones per surface, a hard-edged shadow boundary` | 只有亮暗两块平涂，交界锋利，明度被量化成档位 | 二次元 |
| 柔和上色 | soft shading | `soft airbrushed shading, the shadow terminator fully blurred` | 明暗交界糊开，明度连续过渡 | 二次元 |
| 色块硬边 | hard-edge | `hard-edge color fields, crisp boundaries between flat shapes` | 色块直接相邻，无过渡带 | 二次元 |
| 无描边 | lineless | `lineless illustration, forms separated only by value and color blocks` | 没有轮廓线，结构由明度差承担 | 二次元 |
| 发型高光块 | anime specular | `cel shading with one crisp white specular patch on the hair` | 头发上一块边缘锐利的白高光，高光被当图形处理 | 二次元 |
| 渐层 | gradient ramp | `two-tone gradient ramp from warm cream to cool lavender` | 单方向平滑过渡，只有两个端点色 | 二次元 |
| 线宽变化 | lineart weight | `variable lineart weight, thick where forms overlap, thin at the fingertips and hair tips` | 线宽承载重量与前后关系 | 二次元 |
| 排线 | cross-hatching | `pen cross-hatching, dense crossed strokes building darker values` | 线的覆盖面积决定明度，暗部是交叉网 | 二次元 |
| 网点 | screentone | `manga screentone, halftone dot patterns graded from dense to sparse` | 灰阶由点阵密度表现 | 二次元 |
| 墨线轮廓 | inked contour | `bold black ink outlines of even width around every shape` | 每个形状都有等宽黑边 | 二次元 |
| 铅笔草稿 | pencil sketch | `rough graphite sketch, visible construction lines and eraser smudges` | 辅助线、灰污、未擦线都被保留 | 二次元 |

## 7. 风格与流派
| 中文 | English | 可抄英文短语 | 可见结果（三个特征） | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 巴洛克 | Baroque | `Baroque oil painting, dramatic single-source light, diagonal composition, heavy warm brown shadows` | ①大面积深褐暗部加一束强侧光 ②对角线或旋涡构图 ③厚重织物与肉体的暖褐调 | 写实 |
| 新艺术 | Art Nouveau | `Art Nouveau poster, whiplash curves, flat ornamental border, muted sage and gold` | ①鞭形曲线 ②花卉母题与装饰边框 ③平涂色块加均匀轮廓线 | 通用 |
| 包豪斯 | Bauhaus | `Bauhaus design, primary colors on white, circle square triangle only, asymmetric balance` | ①只有基本几何形 ②红黄蓝加黑白灰 ③非对称平衡、无衬线大字 | 通用 |
| 浮世绘 | ukiyo-e | `ukiyo-e woodblock print, flat color areas, bold keyblock outlines, stylized wave patterns` | ①完全平涂无渐变 ②墨线轮廓清晰 ③平面化构图加装饰性波纹云纹 | 通用 |
| 日本画 | nihonga | `nihonga, mineral pigment texture, gold leaf ground, generous empty space` | ①矿物颜料颗粒感 ②和纸或绢纤维底 ③大量留白加金箔或群青 | 二次元 |
| 孔版印刷 | risograph | `risograph print, two spot inks with visible misregistration, coarse halftone dots` | ①有限专色叠印 ②套色错位偏移 ③油墨不匀的斑驳颗粒 | 通用 |
| 瑞士国际主义 | Swiss Style | `Swiss International Typographic Style poster, strict grid, flush-left sans-serif, vast white space` | ①严格网格对齐 ②左对齐无衬线大标题 ③大面积留白加黑白摄影 | 通用 |
| 粗野主义平面 | brutalist graphic design | `brutalist graphic design, raw default typeface, unrounded black blocks, exposed structural rules` | ①裸露系统默认字体 ②生硬高对比色块、无圆角 ③可见边框下划线与编号 | 通用 |
| 蒸汽波 | vaporwave | `vaporwave aesthetic, pink-to-cyan gradient, wireframe grid horizon, marble statue, VHS scanlines` | ①粉紫到青的渐变 ②网格地平线加古典雕像 ③文字与扫描线 | 二次元 |
| 太阳朋克 | solarpunk | `solarpunk, dense greenery growing over white architecture, bright high-key daylight, stained-glass mosaic panels` | ①建筑与植物共生 ②高调明亮日光 ③白与浅木加彩色玻璃拼贴 | 通用 |
| 中世纪现代 | mid-century modern | `mid-century modern illustration, flat geometric shapes, mustard teal and brick red, slight paper grain` | ①扁平几何加有机形 ②有限复古配色 ③轻微纸纹与套色偏移 | 二次元 |
| 黑色电影 | film noir | `film noir still, high-contrast black and white, venetian blind shadows across the wall, low camera angle` | ①高反差黑白 ②百叶窗格栅硬投影 ③低机位与倾斜构图 | 写实 |
### 7.1 流派名与可见特征：两者都成立，判据在词锁定了什么
- 锁定**工艺与材料**的词——`gouache`、`ukiyo-e`、`risograph`、`cel shading`、`impasto`——放在提示词开头就能切换整图美术方向，它在 `artistic style` 维度里对应唯一的像素工艺（纸纹、网点、平涂、笔触厚度），单写有效，仍建议补一条可见证据；锁定**时代、题材与构图习惯**的词——`Baroque`、`Bauhaus`、`Art Nouveau`、`vaporwave`——名字指向作品集合的模糊中心，展开后可以差出教堂、海报、家具，必须配三个可见特征，否则交回的是集合的平均值。
- 流派名会带出无关经典元素：`film noir` 自带雨夜街道与烟，`Bauhaus` 可能交一张海报而不是场景；只借其中一项时直接写那一项。两个流派名并列还会互相稀释，两组特征才能按比例叠加。
- 推荐式：**流派名（一个）+ 三个可见特征 + 一个排除句**，例 `Art Nouveau poster, whiplash curves, flat muted sage and gold color fields, even-weight outlines, no photographic texture.`
- 【需核】`brutalist`、`vaporwave`、`solarpunk`、`mid-century modern` 多义或跨媒介（建筑、平面、网页；音乐、视觉；文学运动、视觉风格），在 MOSS-Image 上的绑定强弱未实测。

## 8. 材质与质感
两条实用规则：**高光形状等于光源形状**，写了 `a window reflected in the tabletop` 就意味着环境里必须有窗，否则自造矛盾光源；**写实的真实感主要靠不均匀**，`slight oil sheen on the forehead`、`uneven texture`、`a few water spots` 比 `ultra detailed texture` 有效得多。
| 中文 | English | 可抄英文短语 | 可见结果 | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 次表面散射 | subsurface scattering | `subsurface scattering in the ears and fingertips, a warm red glow through the thin edges` | 耳廓、鼻翼、指缝透出红色半透明 | 写实 |
| 镜面高光 | specular highlight | `a small hard specular highlight on the lip and the tip of the nose` | 小而亮的反射点，形状随光源 | 通用 |
| 粗糙度 | roughness | `low roughness, mirror-like reflection of the window in the tabletop` | 低粗糙映出环境倒影，高粗糙只剩模糊亮斑 | 写实 |
| 哑光 | matte | `completely matte surface, no reflection at all, light absorbed into the color` | 无高光、颜色实 | 通用 |
| 缎面 | satin | `satin sheen, a soft elongated highlight that slides along the fold` | 高光被拉长成带，随形变移动 | 通用 |
| 薄纱 | sheer lace | `sheer lace over skin, the pattern visible as a fine mesh, the background shifting through it` | 透过织物看见下层，纹样是细网 | 通用 |
| 天鹅绒 | velvet | `crushed velvet, deep light-absorbing core with a bright sheen only at grazing angles` | 正对镜头极暗，掠射角发亮 | 通用 |
| 拉丝金属 | brushed metal | `brushed aluminum with fine parallel streaks, an anisotropic highlight stretched vertically` | 高光沿一个方向拉长，表面有细平行纹 | 写实 |
| 铜绿包浆 | patina | `green verdigris patina settled in the crevices of the bronze` | 凹处积绿、凸处磨亮 | 写实 |
| 凝露 | condensation | `cold condensation beading on the glass, tiny droplets refracting the light behind` | 密布小水珠，每颗都带倒影 | 写实 |
| 湿沥青 | wet asphalt | `rain-soaked asphalt mirroring the neon signs above, broken reflections in the puddles` | 地面成为第二块镜面，倒影被水洼切断 | 通用 |
| 大气透视 | atmospheric perspective | `strong atmospheric perspective, distant hills washed out to pale blue-grey and low contrast` | 越远越淡、越蓝、越少细节 | 通用 |
| 湿发 | wet hair | `wet hair clumped into separate dark strands with sharp highlights` | 头发成缕、发暗、反光锐利 | 通用 |
| 磨损 | worn and scratched | `scratched paint with the metal showing through at the edges, chipped corners` | 掉漆露底材，磨损集中在受摩擦处 | 通用 |
| 半透明 | translucency | `translucent rice paper glowing from behind, the silhouette of the hand visible through it` | 背光透出后方形状 | 通用 |

## 9. 情绪词拆成可见描述
| 中文 | English | 可抄英文短语 | 可见结果（四个旋钮） | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 治愈 | healing | `soft high-key morning light, pale cream and mint palette, generous empty space around her, nothing sharp in frame` | 高调近乎无影；暖白加淡青绿、高明度低彩度；中等密度；四周留呼吸空间、无锐角 | 通用 |
| 温柔亲密 | intimate | `soft window light from the left, warm cream palette, she fills most of the frame, background dissolved into blur` | 单侧窗光、明暗比小；暖肤色加奶油白；主体占画面大部分；浅景深 | 通用 |
| 孤独 | lonely | `one small distant light source, the figure tiny in a vast empty concrete space, everything else cold blue-grey` | 单一小光源、暗部占多数；冷青灰、几乎无暖色；主体极小；大面积空场 | 通用 |
| 压抑 | oppressive | `harsh overhead fluorescent light, heavy vignette, the low ceiling pressing down, walls closing in` | 硬顶光、投影压向人物；钠黄或病态绿、低明度；天花板入画；无留白 | 通用 |
| 危险 | dangerous | `hard side light, deep black surroundings, a red practical glowing behind, foreground bars crossing the frame` | 硬侧光、大面积深黑；深红或琥珀点光配冷背景；主体被遮挡；前景横插物 | 通用 |
| 神圣 | sacred | `a shaft of light from above through dust, gold and cold white, symmetrical composition, vast empty air above` | 顶光加体积光；金色配冷白；居中对称；上方大量留白 | 通用 |
| 怀旧 | nostalgic | `faded low-contrast color, yellowed highlights and cyan shadows, slight softness, fine visible grain` | 低对比、黑位抬升；高光偏黄、暗部偏青、低饱和；轻微失焦；可见颗粒 | 通用 |
| 恐怖 | horror | `a single hard light from below, the rest of the frame pitch black, desaturated cold green, a dark shape at the frame edge` | 单点硬光、其余全黑；冷绿去饱和；主体贴边；前景遮挡、暗角重 | 通用 |

别写 `healing`、`lonely`、`oppressive`、`emotional atmosphere` 当画面描述——它们不在标注规范要求的可见信息里，只会被当成风格词借用某个常见模板。上表的 English 列只是索引，抄短语列才是内容。

## 10. 空转词与替代写法
| 中文 | English | 可抄英文短语 | 可见结果 | 通道 |
| :--- | :--- | :--- | :--- | :--- |
| 电影感 | cinematic | `anamorphic widescreen framing, teal-and-orange grade, oval bokeh, horizontal flare streak` | 从「像电影」落到画幅、调色、散景形状与眩光方向 | 写实 |
| 氛围感 | aesthetic | `dusty blue and warm cream, matte paper texture, one soft window on the left` | 从评价词落到色盘加材质加光位三件 | 通用 |
| 艺术品级 | masterpiece / best quality | （删掉，词位让给皮肤与材质细节） | 无；来源是评分站排序标签，不对应任何像素 | 通用 |
| 8k / 4k | 8k, ultra HD | `visible microscopic pores, individual eyelashes, fine fabric weave` | 从输出参数落到具体部位的细节证据 | 通用 |
| 超高细节 | ultra detailed | `detailed only on the face and hands, clothing left loose and painterly` | 指定细化部位，避免全图均匀锐化发硬 | 通用 |
| 超写实 | hyperrealistic | `uneven skin tone, slight oil sheen, real shadow falloff` | 从 CG 塑料感回到实拍证据 | 写实 |
| 平台背书 | trending on artstation | `painterly digital illustration, muted palette, selective focus` | 从平台名落到画风特征 | 二次元 |
| 渲染器名 | 4k octane render / UE5 | `hard contact shadows, physically consistent reflections` | 从软件名落到它造成的可见结果 | 通用 |
| 体积光单写 | volumetric lighting | `dusty air, visible shafts from a window with slats` | 缺介质只剩柔光，补介质才有光柱 | 通用 |
| 戏剧光 | dramatic lighting | `a single hard key from the upper right, the left side of the face near black` | 从笼统形容落到方向与明暗比 | 通用 |
| 有情绪 | moody | `low-key, desaturated cool palette, crushed shadows` | 从平均值落到明暗比与色盘 | 通用 |
| 色彩鲜艳 | vibrant colors | `high chroma, dominated by cobalt and vermilion, one small pale accent` | 从程度词落到三四个色名加占比 | 通用 |
| 专业摄影 | professional photography | `three-point lighting, softbox above camera left, 85mm at eye level` | 从器材身份落到布光结构 | 写实 |
| 作者风格 | by [artist name] | 该作者的三个可见特征：笔触、配色、构图 | 作者名不在可见信息内，且会把多种风格混成一锅 | 二次元 |

## 11. 美学组合配方
- **写实 · 低调 + 冷暖分离 + 湿面反射**：`low-key window light from camera left, deep teal shadows against warm amber skin, one narrow shaft of dusty air catching the light, the lacquered tabletop mirroring the window with a thin specular edge along the cup, real shadow falloff and no flat front fill.` → 夜景室内人像、静物、产品近景。
- **写实 · 黄金时刻逆光 + 大气透视**：`golden hour backlight with long shadows raking across the ground, warm amber rim on the hair, distant hills washed out to pale blue-grey, thin dust haze softening the light sources.` → 户外黄昏、公路、田野、背影。
- **二次元 · 水粉厚涂 + 限色 + 疏密分级**：`opaque matte gouache on rough cold-press paper, chalky dry surface with visible brush ridges, palette strictly limited to dusty blue, warm cream, sage and rust, even-weight contours, fine detail reserved for the face and left loose elsewhere, no photographic texture.` → 轻小说封面、角色半身、插画海报。
- **二次元 · 赛璐璐截帧 + 硬投影**：`cel shading with two flat tones per surface, crisp lineart, hard-edged shadows dividing the face in half, late afternoon sunlight through window slats casting parallel bands across the corridor.` → TV 动画截帧、Galgame CG、分镜试稿。
- **通用 · 高调治愈 + 粉彩 + 大留白**：`high-key overcast daylight with no cast shadows, pale cream and mint at high value and low chroma, the figure small in a wide empty room, generous negative space at the top of the frame.` → 生活方式、母婴、治愈系配图。
- **通用 · 单色片 + 体积光 + 材质反差**：`the whole scene washed in one deep red gel, volumetric god rays through smoke, velvet absorbing light next to a polished metal edge catching one hard streak.` → 概念图、舞台、悬疑海报。
