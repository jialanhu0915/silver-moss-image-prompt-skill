# Caption：正面提示词

主体是一段散文，不是 tag 堆。模型见的 caption 由 VLM 重写，顺序是**构图 → 主体 → 动作 → 场景 → 颜色 → 光线 → 画风**，且只写可见信息。照此顺序写最省力。

## 1. 语序

`光线与色温 → 媒介与镜头 → 主体 → 动作与关系 → 场景 → 材质收尾`

- 光源写在句尾等于没写：先写「白衬衫」，末尾补「只有顶上绿灯管」，得到的仍是暖白平光。把光源提前，后面的皮肤衣服才被染色。
- 多主体：主角色放第一段定调；次角色句首写反向特征切断继承——`In sharp contrast, the girl on the right wears NO glasses and has spotless skin with zero freckles`。
- 分段用自然换行，一段一话题（光线 / 主体 / 场景 / 文字）。`<|xxx|>` 闭合标签不在官方文档里，要用先自测。

## 2. 长度

| 档 | 词量 | 场景 |
| :--- | :--- | :--- |
| 短 | 20~50 | 单物体、极简需求 |
| 中 | 60~140 | 单人像、单场景（默认） |
| 长 | 150~300 | 多人、复杂空间、大量图内文字 |

不按长度凑词。用户说极简，就写极简；短提示词把 CFG 调高一点。

## 3. 语言

默认英文（训练量最大）。中文适用于：用户要求中文、图内要大段中文、题材本身是中式物件。一条提示词里同一事不要中英各写一遍。

## 4. 骨架

```text
[光照与色温]. [媒介、镜头与构图钩子].
[主体：年龄 + 骨相 + 发色发质 + 表情 + 服饰 + 配饰].
[动作：静态结果，如 shirt already pushed up，不要 pulling up her shirt].
[场景：位置 + 材质 + 背景层次].
[收尾：皮肤 / 材质 / 颗粒].
```

进行时动词要占手，模型会为此多画一只手；静态结果只摆姿势。

### 4.1 润色幅度跟着需求走

先弄清用户想要什么样的图片；不按字数判断需求是否详细，也不重复询问已经说清的内容。若主体 / 题材、媒介 / 画风或主要气质等关键方向仍不明确，先问一两个聚焦问题；若核心想法清楚、只是画面细节少，就直接补全，不让用户填写问卷。

- **描述已足够具体**：保留用户的构图、气质与独特选择；润色语序、主次和可见呈现，只补能强化原意的细节，不另起一套创意方向。
- **描述比较粗略**：依据整体题材和风格补出连贯方案，明确主焦点，再从构图、动作 / 道具、光色、材质中选 2–3 个互相支撑的细节。若不同选择会明显改变画面，就先询问或给少量方向供选。

两种情况都不改变用户指定的主体、数量、关系、动作、风格、文字与排除项；不编造姓名、品牌、事件、年代等真实事实。避免无关形容词堆叠，把选择写成位置、形状、受光和接触关系，而不是只写「电影感」「梦幻」「高级」。用户明确要求忠实翻译、极简或不加戏时，按要求收敛。

例：「雨夜街摊，一个女人拿热饮」——不止写 `A woman at a street stall on a rainy night, holding a hot drink.`，可以定成：

```text
Seen past the rain-beaded awning edge, a woman pauses in the left third with both hands around a paper cup. A narrow amber lamp catches a thread of steam; green fluorescent reflections break across the wet counter and continue as small pools down the empty alley on the right.
```

这里用遮挡、左右留白和绿 / 琥珀色反射组织画面；若用户已经指定了主体位置、光色或其他细节，就应以其选择为准。此例是写法示例，不是效果保证。

## 5. 反模式

| 别写 | 改成 |
| :--- | :--- |
| `masterpiece, best quality, 8k, ultra detailed` | 具体质感与笔触 |
| 相机/引擎/软件型号单独写 | 它造成的可见结果 |
| `beautiful, nice lighting` | `one warm beam from the back-left, deep shadow on the front` |
| `dreamy, cinematic, vivid, detailed` 等互不关联的氛围词 | 一个视觉钩子 + 2–3 个互相支撑的可见细节 |
| `[填入角色名]` 之类占位符 | 写具体内容或删掉该项 |
| caption 里写 bbox、JSON、坐标 | 移到提示词外面 |

## 6. tag 串

官方顺序：`Quality -> Score -> Meta -> Year -> Character -> Series -> Artist -> General`，示例 `best quality, highres, hatsune miku, vocaloid, @foo bar, 1girl, blue hair`。

清洗：留角色名（`lillie (pokemon)`）；删版权大词（`pokemon`、`nintendo`，易出假发感，【社区】未对照）；删 `censored / mosaic censoring / watermark`；纯色背景换具体场景与光向。

禁止：SD 系权重语法 `(masterpiece:1.2)`、`[a:b:0.5]`——本模型没有这个机制。逗号硬串长句会丢关系，需要动作与空间时改散文。

混写：tag 打头做属性清单，散文随后讲空间与光线。

```text
best quality, highres, 1girl, silver hair, red eyes, black coat, city street, night.
Cool blue neon from the shopfronts falls on her left side, 35mm at eye level, shallow depth of field.
She stands with her back to a shuttered storefront, looking toward the camera over one shoulder.
```

## 7. 示例

「便利店门口的女生，夜雨」：

```text
Cool blue-white fluorescent light spilling from a store window onto wet asphalt, 35mm at eye level, shallow depth of field.
A slender 20-year-old East Asian woman in a soaked oversized grey hoodie stands under the awning just outside the glass door, wet hair clumped into dark strands on her cheek, hugging a paper bag with both hands, looking off to her left with an exhausted half-smile.
Behind her the glass door reflects shelves and a green price tag; a wet plastic bag drifts in a puddle in the near foreground.
Rain droplets caught in the fluorescent light, realistic wet skin highlights, muted teal-and-amber palette.
```

第一句锁光线与湿沥青，第二句才给主体，第三句补空间，末句收质感。
