---
name: silver-moss-image-prompt-skill
description: >-
  Write and debug MOSS-Image prompts with deliberate visual direction. Turn an
  idea, a reference description or a Danbooru tag dump into a caption-style
  positive/negative prompt plus sampling settings, covering three style channels —
  photoreal, anime and hybrid (2D-in-3D,
  toon-shaded 3D, mixed media, split-style) — with in-image text rendering,
  word-order rules, layered negatives and symptom-driven debugging.
  适用于 MOSS-Image 提示词编写与排错、写实/二次元/混合三条风格通道、图内文字渲染、负面词分层；简略需求默认做视觉润色，而非逐字翻译。
  Use when the user mentions MOSS-Image / MOSS 出图 / moss-image, or wants image
  prompts written, rewritten or fixed for it.
license: Apache-2.0
version: 0.3.0
---

# MOSS-Image 提示词

Qwen3.5-9B 编码器 → 42 层单流 DiT → FLUX.2 VAE。吃长而具体的散文，不是 tag 堆；条件上限约 4K tokens。

先弄清用户想要什么样的图片，再决定润色幅度：描述详细走忠实模式，保真细化；想法粗略走增强或自由模式，先定概念再写提示词（`references/creative/concept.md`）。只在关键意图不明时追问，不重复询问用户已经说清的内容。细则见 `references/core/caption.md` §4.1。

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
| 仅给主题、开放式创作、要概念图 / 海报 / 记忆点 | `creative/concept.md` |
| 概念已定，要定构图 / 镜头 / 空间 / 光色 | `direction/brief.md` |
| 海报、封面、带标题的图文版式 | `direction/poster.md` |
| 已指定完整画面、「别改我的构图」、商品图 / 技术示意 / 复现参考 | 跳过创意层与导演层，直接编译 caption |
| 镜头、焦距、景别、机位 | `craft/camera.md` |
| 版式、空间层次、留白、群像 | `craft/composition.md` |
| 光位、色彩、画种流派、材质 | `craft/aesthetics.md` |
| 图内文字 | `core/text-in-image.md` |
| 参数不确定 | `core/params.md` |
| 视觉润色、语序、长度、语言、tag 串 | `core/caption.md` |
| 出图有毛病 | `diagnostics/troubleshooting.md` |
| 规则出处 | `diagnostics/sources.md` |
| 完整范例 | `examples/photo.md`、`examples/anime.md`、`examples/creative.md` |
| 用户明确要求 Layout / 精确控位 | `core/layout.md`、`examples/layout.md`（实验性） |

`core/caption.md` 与 `core/negative.md` 是全局契约，首次使用时过一遍。

## 流程

1. **定通道**：写实 / 二次元 / 混合。混合先答三问——谁是主体、靠什么融合、边界在哪（`styles/hybrid.md`）。
2. **确认意图与抽需求**：先判断用户是否已说清想要什么图。主体、数量、关系、媒介、风格、必须出现的文字和排除项一项不丢；若缺失的信息会彻底改变画面，先问一个聚焦问题，不发问卷。
3. **定概念与强度（仅开放式需求）**：按 `creative/concept.md` §2 判模式（忠实 / 增强 / 自由）、§2.1 定强度（克制 / 强化 / 奇观），固化不可动的项，再用 §6 的机制改写定出主焦点与视觉钩子；淘汰判据见 §7，执行预算与奇观追加要求见 §8。用户已给完整画面时跳过，只做保真细化。
4. **定导演决策（2–5 项）**：读 `direction/brief.md`，按约束优先级挑出服务主焦点的少数决策（镜头 → 空间 → 光色）；海报、封面加读 `direction/poster.md`。具体写法查 `craft/`，只写可见结果，不写术语名。
5. **编译成可见描述**：光线与色温在前，主体居中段，服饰动作在后；多主体先主后次，次角色句首写反向特征。机制名、模式名、强度名、决策名都不进 caption。
6. **配参数与负面**：按 `core/params.md` 选档，按 `core/negative.md` 分层拼词。
7. **自检**（§自检），不过就改。

## 参数档

| 档 | 用途 | 分辨率 | Steps | CFG | SLG |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q**（默认） | 有文字、精细几何、交付图 | 1M~2M | 50 | 3.0 | 开，`uncond_skip_layers=[22]` |
| **R** | 快速试构图、要真实感 | 0.6M | 16~30 | 3.0 | 关 |

Shift 5.0、Euler 通用。**规则与档绑定**：标 `[R]` 的条目只在关 SLG 的低步数下需要，跑 Q 档不用堆。速查表见 `core/params.md`。

## 模板

```text
【正面提示词】
[光线与色温句], [媒介、镜头与构图钩子]. [主体：年龄骨相 + 发型发质 + 表情 + 服饰]. [动作与接触关系]. [场景与背景]. [材质与收尾].
【负面提示词】
worst quality, bad anatomy, watermark, jpeg artifact, [L1], [L2 风格封杀], [L3 场景追加]
【采样参数】
1024×1536 / Steps 50 / CFG 3.0 / Shift 5.0 / Euler / SLG uncond_skip_layers=[22] / Seed 随机
```

`nsfw` 不是过滤器，加不加看需求，真正的审核在部署层（`negative.md` §1、`DISCLAIMER.md`）。有图内文字时去掉 `watermark` 和 `text`（`negative.md` §2 L0）。二次元可参考 `anime.md` §5 的分段骨架（默认自然分段，闭合标签需自测）；有文字按 `text-in-image.md` 加引号串。

## 自检

1. 主体数量、关系、媒介、排除项有无丢失。
2. 光线与色温是否在主体名词之前。
3. 图内文字是否逐字保留、带引号、换行用 `\n`。
4. 图内文字会不会带偏人物年龄体型；若会，正文与负面是否同步。
5. 负面的风格封杀组是否与所选通道一致（写实不带 `photorealistic`，二次元不带 `anime`）。
6. 所用规则是否属于当前参数档。
7. 有无 `masterpiece, 8k, ultra detailed` 这类空转词，或把相机型号、渲染引擎当画面效果写。
8. 混合画面是否只写一套光，并写明谁接受谁的光、边界在哪。
9. 有图内文字时，负面里是否已去掉 `watermark`、`text`。
10. 润色幅度是否符合用户描述的详略？粗略需求有无补足画面方向；细致需求有无保住其独特选择，而非套入另一套风格？
11. 开放式需求是否只有一个主焦点？不可能元素是否已落地（参照物、光向、投影），或平面类是否说得清「版面发生了什么」？
12. 导演决策是否 ≤5 项，且每项都服务同一个焦点？有没有互相打架的组合（对称 + 荷兰角、柔光 + 硬阴影）？
13. 海报 / 封面是否留了低细节的标题安全区与一条阅读路径？必须准确的文案是否注明后期排版或 Layout？

这两档是本 skill 的预设组合，官方只给单项推荐值。

## Layout

官方标为 Experimental。本仓库附带上游编译器的原样副本 `scripts/vendor/openmoss/compile_prompt.py` 和一个 JSON 示例；**尚未验证 MOSS-Image 实际出图质量**。**默认只交付 caption。**用户明确要求 Layout，或文字 / 元素必须精确落位时，读 `core/layout.md`；示例见 `examples/layout.md`。

## 红线

1. 不编造用户没给的事实（人名、品牌、事件、规格），画面内必须出现的文字除外。
2. 不把不可见信息当画面效果写（型号、引擎、软件名），改写成可见结果。
3. 不把工具说明写进 caption（`bbox`、`JSON`、坐标、模板说明）。
4. 不为涉及未成年人或幼态外观的性内容提供写法，无论角色真实、虚构或二次元、无论设定年龄。
5. 不协助以真实人物肖像生成性内容、诽谤或欺诈内容。

使用者自行承担生成与使用的全部法律风险，见 `DISCLAIMER.md`。
