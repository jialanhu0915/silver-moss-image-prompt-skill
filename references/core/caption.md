# Caption：正面提示词怎么写

MOSS-Image 的正面提示词主体是一段**散文**，不是 tag 堆。官方支持 tag 串（有固定排序建议），但 tag 串只是另一种输入形式，本 skill 默认用散文，因为散文能承载关系、动作、空间，而 tag 堆不能。

## 1. 数据从哪来（决定了什么词有效）

官方的标注流程是：用 VLM（推荐 Gemma 4 / Qwen 3.5 27B / Qwen 3.5 35B-A3B）把训练图重新写成 caption，规范原文要求：

- `Describe the composition, key subjects, actions, setting, colors, lighting, and artistic style in detail.`
- `Include only information visible in the image.`

也就是说，模型见惯的 caption 是「**构图 → 主体 → 动作 → 场景 → 颜色 → 光线 → 画风**」这个顺序、且**只描述可见内容**的散文。由这个事实推出两条硬性写法：

1. 顺序照抄上面那个顺序写，最贴训练分布（见 §2）。
2. 不可见的信息（相机型号、渲染引擎、软件名、作者名）不在 caption 分布里，单独写基本没有效果；要写它们对应的**可见结果**（见 `diagnostics/sources.md`）。

## 2. 语序契约

文本编码器是 Qwen3.5-9B，**从左到右读**。前面写下的词给整段定调，后面才补的词很难覆盖前面。

### 2.1 推荐顺序

```text
光线与色温 → 媒介与镜头 → 主体（年龄/骨相/发色/表情/服饰） → 动作与接触关系 → 场景与背景 → 材质与收尾
```

**最常见的错误是把光源写在句尾。**「白衬衫」先写完，末尾才补「只有顶上一根绿灯管」——模型会把绿灯管画出来，衬衫依旧是暖白平光。把绿灯与暗室写在句首，后面的衬衫和皮肤才会被染上色。

### 2.2 多主体排序

- 第一个描述的主体给整图定调（人种、年龄、画风、主色温），**把主要角色放第一段**。
- 第二段起，句首直接写反向特征切断继承：`In sharp contrast, the girl on the right wears NO glasses, has spotless skin with zero freckles...`
- 更细的多人分区写法见各风格文件。

### 2.3 段落与分隔

- 默认用自然语言分段（真实换行），每段一个话题：光线、主体、场景、文字。
- `<|xxx|>...<|/xxx|>` 这类闭合标签**不在官方文档里**，属社区写法。它可能借 Qwen 聊天模板的 `|<|` 定界符习惯起作用，但官方未确认。要用就先自己 A/B 一次，有效再用；不要当成默认。
- 不要用 `[Image Composition]`、`### 人物` 这类 Markdown 标题当分隔，模型对它们的反应远不如一句自然的方位句。

## 3. 长度

| 档 | 词量 | 适用 |
| :--- | :--- | :--- |
| 短 | 20~50 词 | 单一物体、极简需求、用户明确说要简单 |
| 中 | 60~140 词 | 单人像、单场景插画的默认档 |
| 长 | 150~300 词 | 多人、复杂空间、图内大量文字、Layout 前身 |

规则：

- **不要为了长度加词。**官方 enhancer 原文：`Avoid redundant quality tags, unrequested style changes, arbitrary word budgets`。用户说「极简」，就写极简。
- 上限约 4K tokens，正常使用碰不到的。
- 短提示词要把 CFG 调高一点（官方：`常规长 Prompt 用 3.0 即可; 短 Prompt 建议适当调高`）。

## 4. 语言

- 官方推荐英文（训练量最多），中文也支持。
- 默认：**英文正文**；英文提示词在解剖、光线、材质上的词汇粒度明显更细。
- 例外用中文：① 用户明确要中文；② 画面里要渲染大段中文，让「要显示的文字」和描述语同语言省事；③ 中文特有的东西（书法、印章、中式器物命名）直接用中文更准。
- 混排可以，但一条提示词里别又在同一件事上中英各写一遍——重复不加强，只占 token。

## 5. 可抄骨架

```text
[光照与色温句]. [媒介与镜头句].
[主体：年龄 + 骨相 + 发色与发质 + 表情 + 服饰 + 配饰].
[动作：静态结果，写「已经处于什么状态」而不是「正在做某个动作」].
[场景：位置 + 材质 + 背景层次].
[收尾：皮肤/材质/颗粒等质感句].
```

「静态结果」这条在多主体与衣物互动时尤其重要：写 `shirt already pushed up, hem already lifted` 而不是 `pulling up her shirt`——后者要占两只手，模型很容易多长一只手。

## 6. 反模式

| 别写 | 为什么 | 改成 |
| :--- | :--- | :--- |
| `masterpiece, best quality, 8k, ultra detailed, trending on artstation` | 空转，不在 caption 分布里 | 写具体的质感与笔触 |
| 相机/引擎/软件型号 | 不可见信息 | 写对应的可见结果 |
| `very beautiful, nice lighting` | 无信息量 | `single warm beam from the back-left, deep shadow on the front` |
| `[填入角色名]` 之类占位符 | 交付物不完整 | 要么写具体内容，要么删掉这一项 |
| 把 JSON、bbox、坐标写进 caption | 工具说明不是画面内容 | 放到提示词外面 |
| 同一特征用中英各写一遍 | 浪费 token | 只留一种语言 |

## 7. 从用户的模糊需求到成稿（示例）

用户说：「来个在便利店门口的女生，夜雨。」

```text
Cool blue-white fluorescent light spilling from a convenience store window onto wet asphalt, 85mm lens at eye level, shallow depth of field with bokeh from the store sign.
A slender 20-year-old East Asian woman in a soaked oversized grey hoodie and black shorts stands under the awning just outside the glass door, wet strands of black hair stuck to her cheek, hugging a paper bag to her chest, looking off to her left with an exhausted half-smile.
Behind her the glass door reflects rows of shelves and a faint green price tag; a wet plastic bag drifts in a puddle in the near foreground.
Rain droplets caught in the harsh fluorescent light, realistic wet skin highlights, natural fabric folds, muted teal-and-amber night palette.
```

第一句先把蓝白光与湿沥青写死；第二句才是主体；第三句补足空间关系；末句收质感。
