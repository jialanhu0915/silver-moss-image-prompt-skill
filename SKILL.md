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

Qwen3.5-9B 编码器 → 42 层单流 DiT → FLUX.2 VAE。吃长而具体的散文，不是 tag 堆；条件上限约 4K tokens。

## 交付物

```text
【正面提示词】<连贯散文，不留占位符>
【负面提示词】<分层词表>
【采样参数】W×H / Steps / CFG / Shift / Sampler / SLG / Seed
```

不加与提示词无关的说明。

## 路由

按需求读 2~3 个文件，不要通读。

| 需求 | 读 |
| :--- | :--- |
| 真人、摄影、电影剧照、写实商品 | `styles/photo.md` |
| 二次元插画、动漫截图、Galgame、番剧 | `styles/anime.md` |
| 2D 角色进实景、3D+2D 描边、照片上手绘、同图双画风 | `styles/hybrid.md` |
| 镜头、焦距、景别、机位 | `craft/camera.md` |
| 版式、空间层次、留白、群像 | `craft/composition.md` |
| 光位、色彩、画种流派、材质 | `craft/aesthetics.md` |
| 图内文字 | `core/text-in-image.md` |
| 参数不确定 | `core/params.md` |
| 语序、长度、语言、tag 串 | `core/caption.md` |
| 出图有毛病 | `diagnostics/troubleshooting.md` |
| 规则出处 | `diagnostics/sources.md` |
| 完整范例 | `examples/photo.md`、`examples/anime.md` |

`core/caption.md` 与 `core/negative.md` 是全局契约，首次使用时过一遍。

## 流程

1. **定通道**：写实 / 二次元 / 混合。混合先答三问——谁是主体、靠什么融合、边界在哪（`styles/hybrid.md`）。
2. **抽需求**：主体、数量、关系、媒介、风格、排除项、必须出现的文字，一项不丢。
3. **补可见细节**：外观动作 → 场景 → 光线色温 → 镜头景别 → 材质氛围。只写看得见的。
4. **定语序**：光线与色温在前，主体居中段，服饰动作在后；多主体先主后次，次角色句首写反向特征。
5. **配参数与负面**：按 `core/params.md` 选档，按 `core/negative.md` 分层拼词。
6. **自检**（§自检），不过就改。

## 参数档

| 档 | 用途 | 分辨率 | Steps | CFG | SLG |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q**（默认） | 有文字、精细几何、交付图 | 1M~2M | 50 | 3.0 | 开，`uncond_skip_layers=[22]` |
| **R** | 快速试构图、要真实感 | 0.6M | 16~30 | 3.0 | 关 |

Shift 5.0、Euler 通用。**规则与档绑定**：标 `[R]` 的条目只在关 SLG 的低步数下需要，跑 Q 档不用堆。速查表见 `core/params.md`。

## 模板

```text
【正面提示词】
[光线与色温句], [媒介与镜头句]. [主体：年龄骨相 + 发型发质 + 表情 + 服饰]. [动作与接触关系]. [场景与背景]. [材质与收尾].
【负面提示词】
nsfw, worst quality, bad anatomy, watermark, jpeg artifact, [L1], [L2 风格封杀], [L3 场景追加]
【采样参数】
1024×1536 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

二次元走 `anime.md` 四段式骨架；有文字按 `text-in-image.md` 加引号串。

## 自检

1. 主体数量、关系、媒介、排除项有无丢失。
2. 光线与色温是否在主体名词之前。
3. 图内文字是否逐字保留、带引号、换行用 `\n`。
4. 图内文字会不会带偏人物年龄体型；若会，正文与负面是否同步。
5. 负面的风格封杀组是否与所选通道一致（写实不带 `photorealistic`，二次元不带 `anime`）。
6. 所用规则是否属于当前参数档。
7. 有无 `masterpiece, 8k, ultra detailed` 这类空转词，或把相机型号、渲染引擎当画面效果写。
9. 混合画面是否只写一套光，并写明谁接受谁的光、边界在哪。

这两档是本 skill 的预设组合，官方只给单项推荐值。

## Layout

官方标为 Experimental：坐标要手算中心原点，跨分辨率易漂移，多框互相挤占。**默认只交付 caption。**只有文字必须精确落位（海报、封面、表格）才用，见 `core/layout.md`。

## 红线

1. 不编造用户没给的事实（人名、品牌、事件、规格），画面内必须出现的文字除外。
2. 不把不可见信息当画面效果写（型号、引擎、软件名），改写成可见结果。
3. 不把工具说明写进 caption（`bbox`、`JSON`、坐标、模板说明）。
