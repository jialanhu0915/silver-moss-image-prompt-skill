# 负面提示词

## 1. 官方基线

官方测试给出的有效负面 tag（原文，供参考；本 skill 的默认基线见 §2 L0）：

```text
nsfw, worst quality, bad anatomy, watermark, jpeg artifact
```

**`nsfw` 的位置**：本 skill 的默认基线不带它（决定见 `docs/decisions/0001`）。两点要分清：
1. 负面词只是把采样推离某个方向，**不是内容过滤器**——既不保证拦住，也替代不了部署层的审核与年龄核验。
2. 不带它，等于模型对该方向没有额外压制，输出会更放。公开服务、多人共用、可能触达未成年人的场景，把 `nsfw` 加回 L0，**并且**在部署层做真正的审核。

责任划分见 `DISCLAIMER.md`。

- Python API 的负面提示词**默认为空**，负面词得自己填。
- 训练数据不做质量过滤，**想要什么得在正面写出来**；负面词只能压制方向，不能替代正面描述。

## 2. 分层拼法

拼装顺序 `L0 → L1 → L2 → L3`，从官方基线往外扩，**不要把所有层都塞满**，按场景取用。

### L0 基线（默认必带）

`worst quality, bad anatomy, watermark, jpeg artifact`，默认不带 `nsfw`，需要更保守的输出时前面加上（见 §1）。

画面要出现文字时，**去掉 `watermark` 和 `text`**，只留 `worst quality, bad anatomy, jpeg artifact`，必要时加 `signature`。这两个词会把正常文字一起压掉（【推断】，官方未单独测过，出现“字整体消失”时先查这里）。

### L1 通用解剖与画质

```text
blurry, out of focus, lowres, bad hands, extra limbs, extra arms, extra legs, extra hands, extra fingers, fused fingers, missing fingers, deformed hands, fused bodies, malformed limbs, distorted face, asymmetrical eyes, cross-eyed, low quality
```

多人场景追加 `twins, identical faces, same hair color, cloned faces, duplicated heads`。

### L2 风格封杀（两套互斥，**不能混用**）

写实通道（`styles/photo.md`）：`anime, 2d, illustration, cel shading, painting, 3d render, cgi, doll, plastic skin, airbrushed skin, smooth waxy skin, cosplay, wig, synthetic hair, digital art`

二次元通道（`styles/anime.md`）：`photorealistic, real human, photograph, live action, camera flash, film grain, microscopic pores, 3d render, cgi, plastic skin, sketch, rough sketch, uncolored patches, thick black outlines, vector art, oversaturated neon colors`

把写实那套粘进二次元提示词，画面会被硬推向照片；反之亦然。

### 混合通道（`styles/hybrid.md`）

写实组里的 `anime, 2d, illustration` 会杀掉你要的 2D 角色，二次元组里的 `photorealistic, photograph` 会杀掉你要的实景。混合画面**不能把两套 L2 都打开**，只封杀你不想要的第三态：`white outline, sticker edge, cut-out edge, pasted-on look, style bleeding, gradient between styles, blended styles, plastic skin, toy figure`

三渲二额外封 `photorealistic skin, subsurface scattering, glossy plastic`；同图双画风额外封 `half-colored, smeared transition`。

### L3 场景追加

| 场景 | 追加 |
| :--- | :--- |
| 遮眼 / 闭眼 / 熟睡 | `visible eyes, open eyes, pupils, looking at viewer, eye contact` |
| 悬空腿 / 高脚凳 | `feet on floor, standing, touching the ground` |
| 脚部特写 | `missing toes, fused toes, extra toes` |
| 图内印字可能导致幼化（本意不是幼年角色时） | `child, toddler, loli, babyface` |
| 图内印字可能导致发胖 | `fat, chubby, plump, thick thighs, wide hips` |
| 黑白 / 单色画面 | `color, colorful, red, blue, saturated` |
| 去掉多余人头（分镜 inset） | `multiple heads, extra head` |

## 3. 纪律

1. **同一系列图，负面提示词一字不改**（哪怕加一个 `orange skin` 都会让全图偏移）；单张图的特殊要求在**正面**解决。
2. **长度别贪**：官方只给 5 个词，社区池动辄几百词；本 skill 的做法是 L0 必带、L1 少量、L2 一套、L3 按需，总长度控制在 40~80 词。没有公开的消融实验证明长负面池更好，想加长先自己做一次 A/B。
3. **负面词不是越狠越好**：`ugly, worst quality, bad` 这类堆叠会同时压低细节能量，档 Q 下尤其明显。
4. **负面词无法修正结构性错误**：多一只手、气泡指错人、人物跨出格子，删词没用，要改正面的分块/坐标/描述。

## 4. 交付格式

```text
worst quality, bad anatomy, watermark, jpeg artifact, blurry, out of focus, lowres, bad hands, extra fingers, fused fingers, deformed hands, distorted face, anime, 2d, illustration, cel shading, 3d render, cgi, doll, plastic skin, cosplay, wig
```

一行写完，逗号分隔，不要换行分块。
