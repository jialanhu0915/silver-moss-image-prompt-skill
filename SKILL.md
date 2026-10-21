---
name: silver-moss-image-prompt-skill
description: >-
  Write and debug MOSS-Image prompts. Turn an idea, a reference description or a
  Danbooru tag dump into a caption-style positive/negative prompt plus sampling
  settings, covering three style channels — photoreal, anime and hybrid (2D-in-3D,
  toon-shaded 3D, mixed media, split-style) — with in-image text rendering,
  word-order rules, layered negatives and symptom-driven debugging.
  适用于 MOSS-Image 提示词编写与排错、写实/二次元/混合三条风格通道、图内文字渲染、负面词分层。
  Use when the user mentions MOSS-Image / MOSS 出图 / moss-image, or wants image
  prompts written, rewritten or fixed for it.
license: Apache-2.0
version: 0.1.0
---

# MOSS-Image 提示词

MOSS-Image 是 OpenMOSS 的文生图模型：Qwen3.5-9B 作文本编码器 → 42 层单流 DiT → FLUX.2 VAE。它不是 SDXL 那类「短 tag + 权重语法」的模型，提示词越长越具体越吃得住，条件上限约 4K tokens。本 skill 只做一件事：**把需求写成一段模型真想画的英文散文（或中文散文），再配一条负面提示词和一组采样参数。**

## 1. 交付物

默认产出三块，缺一不可：

```text
【正面提示词】
<一段或多段连贯散文，不是 tag 堆>

【负面提示词】
<分层词表，见 references/core/negative.md>

【采样参数】
分辨率 W×H / Steps / CFG / Shift / Sampler / SLG / Seed
```

交付时不要夹带与提示词无关的说明，也不要在正面提示词里留下 `[填入XX]` 占位符。

## 2. 先读哪个文件

**不要一次读完全部文件。**按下面判据只读 2~3 个。

| 用户要的画面 | 必读 | 按需追加 |
| :--- | :--- | :--- |
| 真人、摄影、电影剧照、写实商品/场景 | `references/styles/photo.md` | `core/text-in-image.md`（有字） |
| 二次元插画、动漫截图、Galgame、番剧、海报插画 | `references/styles/anime.md` | `core/text-in-image.md`（有字） |
| 2D 角色放进真实场景、3D 结构 + 2D 描边、照片上手绘拼贴、同图两种画风 | `references/styles/hybrid.md` | 对应通道的 core 文件 |
| 需要指定镜头、焦距、景别、机位 | `references/craft/camera.md` | 对应 style 文件 |
| 需要指定版式、空间层次、留白、群体排布 | `references/craft/composition.md` | 对应 style 文件 |
| 需要指定光位、色彩关系、画种流派、材质 | `references/craft/aesthetics.md` | 对应 style 文件 |
| 画面里有任何要渲染的文字 | `core/text-in-image.md` | 对应 style 文件 |
| 不确定参数怎么填 | `core/params.md` | — |
| 写散文时不确定语序/长度/语言 | `core/caption.md` | — |
| 出图有明确毛病（多头、字糊、脸发白、Q 版化…） | `diagnostics/troubleshooting.md` | 对应 style 文件 |
| 想知道某条规则凭什么这么说 | `diagnostics/sources.md` | — |
| 想看完整范例（需求 → 提示词 → 参数 → 自检） | `examples/photo.md` 或 `examples/anime.md` | — |

`core/caption.md` 与 `core/negative.md` 是全局契约，**第一次给某个用户写提示词时扫一遍**，之后可跳过。

`references/craft/` 三个文件是**风格无关的技法词典**：镜头、构图、美学词汇。它们不规定画风，只提供「想表达某个视觉效果时该写什么英文短语」。任何通道都可以只挑其中需要的条目，不必整篇读完。

## 3. 固定流程

1. **判断通道**：写实（photo）、二次元（anime）、混合（hybrid）。混合不是各写一半，先定哪一层是主体、靠什么融合（光影 / 描边 / 调色 / 介质 / 分屏线）、边界在哪，见 `styles/hybrid.md` 的三问。
2. **清需求**：抽出用户给的主体、数量、关系、媒介、风格、排除项、必须出现的文字。这些一项都不能丢。
3. **补可见细节**：主体外观与动作 → 场景 → 光线与色温 → 镜头/景别 → 材质与氛围。只写眼睛能看见的东西。
4. **定语序**：光线与色温在前，主体在中，服饰动作细节在后；多主体按「主角色先写、次角色句首写反向特征」排列。详见 `core/caption.md`。
5. **配参数与负面词**：按 `core/params.md` 选档，按 `core/negative.md` 分层拼负面词。
6. **自检**（见 §6），不过就回去改，不要交半成品。

## 4. 默认参数

| 档位 | 用途 | 分辨率 | Steps | CFG | SLG |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q（质量档，默认）** | 有文字、有精细几何、要交付的图 | 1M~2M（如 1024×1536、1456×1456） | 50 | 3.0 | 开，`uncond_skip_layers=[22]` |
| **R（写实快档）** | 快速试构图、追求真实感 | 0.6M（如 720×832、768×784） | 16~30 | 3.0 | 关 |

Shift 5.0、Sampler Euler 两档通用。**档位决定规则有效性**：`photo.md` / `anime.md` 里标 `[R]` 的条目只在关 SLG 的低步数下必要，跑档 Q 时不用堆。完整表格与比例速查见 `core/params.md`。

这两档是本 skill 的预设组合，不是官方推荐值：官方只给单项推荐（1M/1.5M/2M、Steps ≥50、CFG 3.0、Shift 5.0、Euler、SLG skip layer 22）与「关 SLG 更真实但可能崩细节」这一句。

## 5. 输出模板

写实（档 Q）：

```text
【正面提示词】
[光线与色温句], [媒介与镜头句]. [主体：年龄骨相 + 发型发质 + 表情 + 服饰]. [动作与接触关系]. [场景与背景]. [材质与收尾质感句].

【负面提示词】
nsfw, worst quality, bad anatomy, watermark, jpeg artifact, [L1 通用], [L2 风格封杀], [L3 场景追加]

【采样参数】
1024×1536 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

二次元走 `anime.md` 的四段式骨架；有图内文字时按 `text-in-image.md` 加引号串。

## 6. 交付前自检

1. 用户给的主体数量、关系、媒介、排除项，有没有一项被悄悄改掉？
2. 光线与色温词是否出现在主体名词**之前**？
3. 要渲染的文字是否逐字保留、被引号包住、需要换行的地方写了 `\n`？
4. 图内文字会不会反过来污染人物年龄与体型（如 `148cm`、`AGE: 19`）？若是，正文体型词与负面词是否同步补齐？
5. 负面词里的风格封杀组，与正面提示词选的通道是否**一致**（写实不能带 `photorealistic`，二次元不能带 `anime`）？
6. 参数档与规则档是否匹配（用了 `[R]` 档的补偿词却在跑档 Q）？
7. 有没有出现 `masterpiece, best quality, 8k, ultra detailed` 这类空转质量词？
8. 有没有把相机型号、渲染引擎名当成画面效果来写？（单写无效，见 `photo.md` / `anime.md`）
9. 混合画面是否只写了一套光，并写清了「谁接受谁的光」与「边界在哪」？（见 `styles/hybrid.md` §7）

## 7. Layout 现状

MOSS-Image 的 JSON Layout 在官方文档里标为 **Experimental**：坐标需手工换算中心原点，跨分辨率容易漂移，多个框也会互相挤占。**v1 默认只交付 caption 提示词。**

只有一种情况值得试 Layout：文字必须精确落在某个位置（海报、封面、图内表格）。此时读 `core/layout.md`，按里面的手算表格换算，并在交付时把宽高写在提示词外面。

## 8. 三条红线

1. **不编造用户没给的事实**：具体人名、品牌、事件细节、规格参数，除了画面里必须出现的文字，一律不加。
2. **不写看不见的东西当画面效果**：相机型号、胶片型号、渲染引擎、软件名单独写基本无效；要写它们对应的可见结果（颗粒、暗角、硬投影、扫描线）。机制见 `diagnostics/sources.md`。
3. **不把工具说明写进画面描述**：`bbox`、`JSON`、`坐标`、`按模板填写` 这些词不该出现在 caption 里。
