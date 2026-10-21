# silver-moss-image-prompt-skill

[English](README.md) · **简体中文**

写给 [MOSS-Image](https://github.com/OpenMOSS/MOSS-Image) 的提示词 skill。把一个想法、一段参考描述或一堆 Danbooru tag，写成一段模型真想画的 caption，外加一条负面提示词和一组采样参数。

三条风格通道——**写实**、**二次元**、**混合**（跨次元合成、三渲二、媒介叠合、同图双画风）——之下是一层风格无关的技法词典：镜头、构图、美学。

## 它不是什么

- 不是 OpenMOSS 官方项目，只是按官方规范写出来的工作方法（出处见 [NOTICE.md](NOTICE.md)）
- 不是模板库，没有一键套用的固定句式大全
- 不生成图片，纯 Markdown，无脚本、无依赖

## 为什么拆成多个文件

一份 900 行的单文件 skill，每次加载有七成内容与当前任务无关，改一条规则要在几千字里翻。这里每一层只放一类知识：

| 层 | 目录 | 放什么 | 加载时机 |
| :--- | :--- | :--- | :--- |
| 路由 | `SKILL.md` | 判据表、五步流程、自检、红线 | 每次 |
| 契约 | `references/core/` | caption 写法、采样、负面词、图内文字、Layout | 首次 + 按需 |
| 风格 | `references/styles/` | 写实 / 二次元 / 混合，只写该通道独有的决定 | 一次只读一个 |
| 技法 | `references/craft/` | 镜头、构图、美学——与画风无关 | 按条目查 |
| 诊断 | `references/diagnostics/` | 症状排查、出处与证据等级 | 出错或要溯源时 |

单次任务通常只加载 `SKILL.md` + 1 个 core + 1 个 style（+ 1 个 craft），约 250~400 行，占全仓 2043 行的一小部分，且全部命中当前任务。

## 安装

放进 Agent Skills 目录，目录名需与 frontmatter 里的 `name` 一致：

```text
<skills-dir>/silver-moss-image-prompt-skill/SKILL.md
```

支持 [Agent Skills 规范](https://agentskills.io/specification) 的客户端可直接使用。也可以把 `SKILL.md` 粘进系统提示词末尾，其余文件当参考手册查。

## 目录

```text
SKILL.md                            路由、流程、自检（117 行）
references/
├── core/
│   ├── caption.md                  散文交付物：语序、长度、语言、反模式
│   ├── params.md                   采样参数、两档预设、分辨率速查
│   ├── negative.md                 负面词分层
│   ├── text-in-image.md            字号估算、竖排陷阱、文字反噬主体
│   └── layout.md                   Layout JSON（实验性，默认不用）
├── styles/
│   ├── photo.md                    写实：开场模组、暗部控制、骨相、剧照感
│   ├── anime.md                    二次元：画种、版式容器、完成度、LoRA
│   └── hybrid.md                   混合：跨次元、三渲二、媒介叠合、双画风
├── craft/
│   ├── camera.md                   焦距、景别、机位、景深、画幅
│   ├── composition.md              版式、三层空间、留白、群像、事故预防
│   └── aesthetics.md               光位、色彩、技法、流派、材质、情绪
└── diagnostics/
    ├── troubleshooting.md          症状 → 原因 → 改法
    └── sources.md                  出处、证据等级、明确不采用的社区说法
examples/
├── photo.md                        写实两例
└── anime.md                        二次元两例
```

## 三个设计决定

**规则与参数档绑定。** 官方用户指南里唯一一句机制性断言是：关闭 SLG 会让画面更真实，但可能造成细节崩坏。本 skill 由此划两档——**Q**（开 SLG、50 步、≥1M 像素，交付用）与 **R**（关 SLG、低步数、0.6M 像素，快出图）。规则后标 `[Q]` / `[R]`，因为防崩词在 Q 档会过冲，在 R 档不写就崩。多数提示词教程把技巧堆成不分前提的清单，这是它们最大的可移植性缺陷。

**只写可见信息。** 官方标注规范要求描述构图、主体、动作、场景、颜色、光线与画风，且只描述图上可见内容。所以相机型号、渲染引擎、软件名、画师 ID 单写基本无效——要写它们造成的可见结果。这条贯穿全部文件。

**证据分级，不许含糊。** 每条规则标【官方】【推断】【社区】【实测】【未验证】。当前状态是：绝大多数为官方与推断，**实测一栏为空**。这不是写作缺口，而是现状；`sources.md` 专门列出了本 skill **明确不采用**的社区流传说法。

## 已知边界

- **Layout 默认降级。** 官方标为实验性，坐标要手工换算、跨分辨率易漂移，`core/layout.md` 只作备用路径。
- **没有联网引用。** 技法层来自摄影与插画的通行知识。凡「在本模型上更有效」这类断言都标了【需核】，没有一条有对照实验支撑。
- **只写了三条通道。** 多分镜漫画、海报排版、游戏 HUD 尚未成篇；core 与 craft 的条目大多可以复用，但各自缺专项规则。

## 待做

- [ ] 补【实测】：每条【需核】至少做一次同 seed A/B（模板见 `sources.md`）
- [ ] 多分镜漫画通道（待 Layout 稳定性改善）
- [ ] 海报与图文版面通道
- [ ] 游戏实机截图 / HUD 通道
- [ ] ComfyUI 与 Python API 字段对照（官方 API 是 `uncond_skip_layers`，各界面命名不一）

## 致谢

- [OpenMOSS/MOSS-Image](https://github.com/OpenMOSS/MOSS-Image)：模型、用户指南、标注规范与 Layout schema（Apache-2.0），署名见 [NOTICE.md](NOTICE.md)
- 技法层的中英对照，以及「术语必须降维成可见事实」这一原则，整理自摄影、电影摄影与插画教学的通行内容

## 许可证

[Apache License 2.0](LICENSE)。选它有两个理由：与上游 MOSS-Image 同协议；文中包含大量可被复制进工具链的英文提示词片段，Apache-2.0 对此没有歧义。

允许商用、修改与再分发；分发时需保留版权声明、`LICENSE` 与 [NOTICE.md](NOTICE.md) 中的署名，修改过的文件需标明改动。不提供担保，但包含明示的专利授权。
