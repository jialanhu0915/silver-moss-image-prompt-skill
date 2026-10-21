# 症状排查

按症状查。每条给：最可能的原因 → 改哪个文件的哪一节。**先改正面提示词，最后才动负面词**——负面词只能压方向，修不了结构。

## 画面结构

| 症状 | 最可能原因 | 改法 |
| :--- | :--- | :--- |
| 多长一颗头 / 一条胳膊 / 一只手 | 进行时动词占手；多主体混在一段里 | `photo.md` §6 改静态结果；按主体分段 |
| 人物融合、粘连、变成双胞胎 | 多主体没写互斥差异；没写距离 | `photo.md` §7；负面加 `twins, identical faces, cloned faces` |
| 腿糊成一条 / 多条腿 | 身体重叠时用了纯侧机位 | 换 3/4 斜侧；`photo.md` §7 |
| 人物被画成 Q 版、五头身 | 全身镜头删了脚下关系；小分镜写了 `full-body` | `photo.md` §5.2；分镜改 `waist-up medium shot` |
| 人物被画成幼童 | 图内印了年龄/尺寸文字；正文有 `babyface, petite` | `text-in-image.md` §4；改骨相词 |
| 人物被画成成年丰满 | 正文有 `woman, curvy, bone structure`；图内印字带了成熟暗示 | `photo.md` §5.1 双向排除 |
| 左侧人物染上右侧人物的特征/灯光 | 一段写完两人，前后因果串联 | 按人物分段，第二人句首写 `In sharp contrast, NO...` |
| 画面上下出现大片黑边 | 多层景深（前景/中景/远景）挤在一句里 | 按空间层次拆段；`photo.md` §8 |
| 前景道具重复出现并挡脸 | 前景描述与主体描述混写 | 前景单独一段并写 `blurred` |

## 光线与曝光

| 症状 | 最可能原因 | 改法 |
| :--- | :--- | :--- |
| 人脸惨白、暗部消失 | 只写「黑夜/暗室」，正文还留着 `fair skin, bright` | `photo.md` §4 四步法 |
| 整体过曝发白 | 画面有大量白色元素 + `bright background / daylight` 叠写 | 删掉笼统亮度词，改 `warm indoor lighting with rich shadow depth`；负面加 `overexposed, washed out, whiteout` |
| 霓虹/色片灯只画出灯管，人没染色 | 光源写在主体之后 | 光源句挪到最前（`caption.md` §2） |
| 画风切不动 | 正文残留写实词把画风锁死 | 删干净同类词再换开头词组（`anime.md` §2、§9） |

## 文字

| 症状 | 最可能原因 | 改法 |
| :--- | :--- | :--- |
| 字是糊的 / 变成墨块 | 字高 < 24px | 提分辨率 / 扩区域 / 减字数；`text-in-image.md` §2 |
| 有错字、缺笔画 | 单块字太多；档 R 低步数 | 拆块；升档 Q（1.5M + Steps 50 + SLG 22） |
| 竖排数字叠成一坨 | 竖排里用了半角阿拉伯数字 | 改汉字数字，`text-in-image.md` §3 |
| 姓名里出现一个圆圈 `O` | 姓名中间有半角空格 | 连写 |
| 文字位置乱跑 | 只写了「有标题」 | 补方位与版面关系：`centered across the top third` |
| 文字整体消失 | 负面里的 `text, watermark` 把字压掉了 | 改成 `watermark, signature, ui artifacts` |
| 缺行 / 断行不对 | 没有显式换行 | 用 `\n` 或真实换行 |

## 质感与风格

| 症状 | 最可能原因 | 改法 |
| :--- | :--- | :--- |
| 塑料磨皮人偶感 | 负面风格组缺失；写了 `3D render / CGI` | 换写真拍写法；`photo.md` §9 |
| 半成品草稿感（二次元） | 笔触词没有限定作用部位 | `anime.md` §5 主次分级 |
| 页游塑料立绘感（二次元） | 全图堆 `intricate, ultra detailed` | 减精修词，只锁五官与发丝 |
| 假发感 / 衣服像塑料 | 缺真发细节；出现 `cosplay` | `photo.md` §5.3；删 `cosplay, cosplayer` |
| 双色发画反 | 主色与发梢混写 | `blonde hair with pastel-pink tips` |
| 脸红成关公 | 写了 `deeply flushed, burning red` | 改 `faint pink blush` |
| 遮眼却还画出了眼睛 | 正文留了眼神动词 | 删 `looking, staring, wide-eyed`；负面加 `visible eyes, open eyes` |
| 墨块 / 局部留色（黑白漫画） | 正文没删颜色词 | `anime.md` §2 |

## 参数与交付

| 症状 | 最可能原因 | 改法 |
| :--- | :--- | :--- |
| 报错：尺寸非法 | 宽或高不是 16 的倍数 | `params.md` §3 速查表 |
| 换分辨率后人物变小、背景抢戏 | 同一条提示词换了画幅 | 补景别词 |
| 改一句话后整张脸变了 | 固定 seed 下大幅增删前置句 | 只改出错项，控制改动 token（`params.md` §6） |
| 加了一个负面词后全图偏色 | 负面词改变采样方向 | 系列图负面词一字不改 |
| Layout 框错位 / 越界 | 坐标系混用（左上 vs 中心）、宽高与实际生成不一致 | `core/layout.md` §2–§3 |
| 用了 Layout 但 Fritz 出多个人头 | 特写也标了 `character` | 局部特写一律 `object`，caption 写 `Extreme close-up inset showing ONLY...` |

## 排查顺序

1. 先确认参数档位（Q 还是 R）与负面词风格组是否和通道一致。
2. 再确认语序：光源、镜头是否在主体之前。
3. 再确认结构：多主体有没有分段、动作是不是静态结果。
4. 最后才调词表与权重类描述。
5. 每次只改一处，记下档案（`params.md` §6）。

改动超过三处还没好转，**推倒重写**比继续打补丁快。
