# 负面提示词

## 1. 官方基线

官方测试给出的有效负面 tag：

```text
nsfw, worst quality, bad anatomy, watermark, jpeg artifact
```

注意两点官方事实：

- Python API 的负面提示词**默认为空**，负面词得自己填。
- 训练数据不做质量过滤（官方标注规范要求「记录水印而不是过滤掉」），所以**想要什么得在正面写出来**，负面词只能压制方向，不能替代正面描述。

## 2. 分层拼法

拼装顺序：`L0 → L1 → L2 → L3`，从官方基线往外扩。**不要把所有层都塞满**，按场景取用。

### L0 官方基线（默认必带）

```text
nsfw, worst quality, bad anatomy, watermark, jpeg artifact
```

画面要出现文字时，把 `watermark`、`text` 这类词处理干净——它们会把正常文字一起压掉。改用 `watermark, signature, ui artifacts` 这类更精确的词。

### L1 通用解剖与画质

```text
blurry, out of focus, lowres, jpeg artifacts, bad anatomy, bad hands, extra limbs, extra arms, extra legs, extra hands, extra fingers, fused fingers, missing fingers, deformed hands, fused bodies, malformed limbs, distorted face, asymmetrical eyes, cross-eyed, worst quality, low quality
```

多人场景追加：

```text
twins, identical faces, same hair color, cloned faces, duplicated heads
```

### L2 风格封杀（两套互斥，**不能混用**）

写实通道（`styles/photo.md`）：

```text
anime, 2d, illustration, cel shading, painting, 3d render, cgi, doll, plastic skin, airbrushed skin, smooth waxy skin, cosplay, wig, synthetic hair, digital art
```

二次元通道（`styles/anime.md`）：

```text
photorealistic, real human, photograph, live action, camera flash, film grain, microscopic pores, 3d render, cgi, plastic skin, sketch, rough sketch, uncolored patches, thick black outlines, vector art, oversaturated neon colors
```

**这张表最容易出事**：把写实那套负面词粘进二次元提示词，画面会被硬推向照片；反之亦然。

### L3 场景追加

| 场景 | 追加 |
| :--- | :--- |
| 遮眼 / 闭眼 / 熟睡 | `visible eyes, open eyes, pupils, looking at viewer, eye contact` |
| 悬空腿 / 高脚凳 | `feet on floor, standing, touching the ground` |
| 脚部特写 | `missing toes, fused toes, extra toes` |
| 图内印字可能导致幼化 | `child, toddler, loli, babyface` |
| 图内印字可能导致发胖 | `fat, chubby, plump, thick thighs, wide hips` |
| 黑白 / 单色画面 | `color, colorful, red, blue, saturated` |
| 去掉多余人头（分镜 inset） | `multiple heads, extra head` |

## 3. 纪律

1. **同一系列图，负面提示词一字不改。** 固定 Seed 做系列时，哪怕加一个 `orange skin` 都会让全图偏移。单张图的特殊要求在**正面**解决。
2. **长度别贪。** 官方只给 5 个词，社区池动辄几百词，但**没有任何公开的消融实验**证明长负面池更好。本 skill 的做法是：L0 必带，L1 少量，L2 一套，L3 按需，总长度控制在 40~80 词。想加长，先自己做一次 A/B。
3. **负面词不是越狠越好。** `ugly, worst quality, bad` 这类堆叠会同时压低细节能量，档 Q 下尤其明显（有 SLG 收敛边缘时更容易把画面压平）。
4. **负面词无法修正结构性错误。** 多一只手、气泡指错人、人物跨出格子，删词没用，要改正面的分块/坐标/描述。

## 4. 交付格式

```text
nsfw, worst quality, bad anatomy, watermark, jpeg artifact, blurry, out of focus, lowres, bad hands, extra fingers, fused fingers, deformed hands, distorted face, anime, 2d, illustration, cel shading, 3d render, cgi, doll, plastic skin, cosplay, wig
```

一行写完，逗号分隔，不要换行分块——负面提示词不是结构化输入，换行只会增加噪声。
