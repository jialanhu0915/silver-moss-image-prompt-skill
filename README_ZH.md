# silver-moss-image-prompt-skill

[English](README.md) · **简体中文**

写给 [MOSS-Image](https://github.com/OpenMOSS/MOSS-Image) 的提示词 skill。把一个想法、一段参考描述或一堆 Danbooru tag，按需求详略润色成 caption：细致描述以保真细化为主，粗略想法则补足画面方向；再配上负面提示词和采样参数。

三条风格通道——**写实**、**二次元**、**混合**（跨次元合成、三渲二、媒介叠合、同图双画风）——之下是一层风格无关的技法词典：镜头、构图、美学。

## 它不是什么

- 不是 OpenMOSS 官方项目，只是按官方规范写出来的工作方法（出处见 [NOTICE.md](NOTICE.md)）
- 不是模板库，没有一键套用的固定句式大全
- 不生成图片。可选的 Layout 编译脚本只校验并转换 JSON 草稿；使用 Python 标准库，不额外安装依赖

## 内容怎么组织

skill 在任务命中时才被加载，所以结构直接决定模型实际读到什么。这里每一层只放一类知识：

| 层 | 目录 | 放什么 | 加载时机 |
| :--- | :--- | :--- | :--- |
| 路由 | `SKILL.md` | 判据表、流程、自检、红线 | 每次 |
| 契约 | `references/core/` | caption 写法、采样、负面词、图内文字、Layout | 首次 + 按需 |
| 创意 | `references/creative/` | 模式判定、创意机制、淘汰判据、执行预算 | 开放式需求 |
| 导演 | `references/direction/` | 导演简报、2–5 项上限、约束优先级、任务档案、海报版式 | 概念定下后 |
| 风格 | `references/styles/` | 写实 / 二次元 / 混合，只写该通道独有的决定 | 一次只读一个 |
| 技法 | `references/craft/` | 镜头、构图、美学——与画风无关 | 按条目查 |
| 诊断 | `references/diagnostics/` | 症状排查、出处与证据等级 | 出错或要溯源时 |

一次任务通常读 `SKILL.md` + 一个契约文件 + 一个风格文件，只有需要某种具体技法时才去翻对应的 craft 文件；开放式需求会先读创意层。

维护规则：所有对照表只增不删。可以新增词条、修正词条，但不删除、不合并；压缩只针对表格之外的文字。

## 同 seed 对照看到了什么

三对同 seed，1360×752，Steps 25，CFG 3.0，Euler + simple，SLG 关闭；只改 caption，另在 A 组加了改写器开关。**单 seed、单一社区权重，只能算方向性证据，不是统计结论。**完整 caption、负面与保留意见见 [`examples/ab-test.md`](examples/ab-test.md)。

**写实：光在主体前。** 关掉改写器，skill 写法把绿檐灯、湿路面上的绿反射、蓝黑街道与暖色货架同时推进了画面；基线是一张平光暖调、没有雨的图。

| 基线 | skill 写法 |
| :---: | :---: |
| ![基线](imgs/a_base_off.png) | ![skill](imgs/a_skill_off.png) |

**创意层 + 导演层。** 基线把图书馆漂成哥特庄园：月亮居中、无人、无尺度；skill 写法保住了窗棂切月、冷月光、一盏琥珀台灯与右侧成排的绿罩灯。

| 基线 | skill 写法 |
| :---: | :---: |
| ![基线](imgs/b_base_up.png) | ![skill](imgs/b_skill_up.png) |

**导演层，两项决策。** 上一版用绝对句（「落进褐色阴影」「前景虚焦栏杆」）把主体埋掉了；补上可读下限、前景占比与主光后，报纸、盖碗、红尾灯、栏杆条同时入画。

| 基线 | skill 写法 |
| :---: | :---: |
| ![基线](imgs/c_base_off.png) | ![skill](imgs/c_skill_off.png) |

这三对说明：写得具体、有顺序的 caption 会被执行。它们**不**说明画面变好看了——基线图本身站得住，skill 版是「更明确」而不是「更讨喜」。

## 安装

放进 Agent Skills 目录，目录名需与 frontmatter 里的 `name` 一致：

```text
<skills-dir>/silver-moss-image-prompt-skill/SKILL.md
```

支持 [Agent Skills 规范](https://agentskills.io/specification) 的客户端可直接使用。也可以把 `SKILL.md` 粘进系统提示词末尾，其余文件当参考手册查。

## 目录

```text
SKILL.md                            路由、流程、自检
DISCLAIMER.md / DISCLAIMER_EN.md    法律声明与使用者责任
references/
├── core/
│   ├── caption.md                  散文交付物：语序、tag 串、长度、语言
│   ├── params.md                   采样参数、两档预设、分辨率速查
│   ├── negative.md                 负面词分层
│   ├── text-in-image.md            字号估算、竖排陷阱、文字反噬主体
│   └── layout.md                   Layout JSON（实验性，默认不用）
├── creative/
│   └── concept.md                  先定概念：模式、强度、创意机制、执行预算
├── direction/
│   ├── brief.md                    导演简报：六问、2–5 项上限、任务档案
│   └── poster.md                   海报层级、标题安全区、阅读路径、图文关系
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
scripts/
├── UPSTREAM.md                       上游脚本来源与更新流程
└── vendor/openmoss/compile_prompt.py 可选 Layout 草稿编译器
examples/
├── photo.md                        写实两例
├── anime.md                        二次元两例
├── creative.md                     创意四例，含海报改前 / 改后
├── ab-test.md                      同 seed 对照：caption、参数、观察记录
└── layout.md                       实验性 JSON Layout：草稿与编译结果
docs/decisions/                     决策记录（ADR）及索引
imgs/                               README 引用的同 seed 对照图
```

## 三个设计决定

**规则与参数档绑定。** 官方用户指南指出：关闭 SLG 会让画面更真实，但可能造成细节崩坏。本 skill 由此划两档——**Q**（开 SLG、50 步、≥1M 像素，交付用）与 **R**（关 SLG、低步数、0.6M 像素，快出图）。依赖档位的规则标 `[Q]` / `[R]`（未标的两档都成立），因为防崩词在 Q 档会过冲，在 R 档不写就崩。

**只写可见信息。** 官方标注规范要求描述构图、主体、动作、场景、颜色、光线与画风，且只描述图上可见内容。所以相机型号、渲染引擎、软件名、画师 ID 单写基本无效——要写它们造成的可见结果。这条贯穿全部文件。

**证据分级，写在前面。** 证据分【官方】【推断】【社区】【实测】【未验证】五级（见 `sources.md`）。已标注的条目以官方与推断为主；未标注的断言是作者未经验证的工作经验；凡是需要对照实验才能下结论的，一律标为未验证，而不是当作事实陈述。`sources.md` 还列出了本 skill **明确不采用**的社区流传说法。

## 已知边界

- **Layout 实验性且默认关闭。** 随附编译器可校验草稿字段并转换坐标，不校验语义位置是否吻合或实际出图质量。示例已通过编译；MOSS-Image 实际出图未测试。见 `core/layout.md` 与 `examples/layout.md`。
- **规则只做了部分验证。** 目前有一轮同 seed 对照（`examples/ab-test.md`、`sources.md` §五），单 seed、单一社区权重；技法层其余条目仍来自摄影与插画的通行知识，「在本模型上更有效」这类断言维持未验证标记。
- **创意层是品味，不是测量。** 模式、机制清单与淘汰判据是作者判断，均标未验证；它们说明「怎么想一张图」，不说明模型会画出什么。`examples/creative.md` 四例都没有确认出图。
- **导演层借用的是影视与设计通行经验。** 构图、镜头、光色建议不针对本模型实测；「2–5 项」上限是防提示词臃肿的护栏，不是验证过的阈值。
- **只写了三条通道。** 多分镜漫画、游戏 HUD 尚未成篇；海报已有 `direction/poster.md` 的层级、标题安全区、阅读路径与图文关系，但复杂信息图、多栏宣传物、精确文字落位仍缺专项流程与实测；core 与 craft 的条目大多可以复用，但各自缺专项规则。

## 待做

- [ ] 为每条未验证条目补同 seed 的 A/B 对照（模板见 `sources.md`；首轮见 [`examples/ab-test.md`](examples/ab-test.md)）
- [ ] 四场景创意 A/B（关 upsampler）：图书馆（强化）、宇宙海报（奇观）、城堡石桥（忠实）、茶海报（平面）；每组 2–3 seed，盲评第一眼冲击力、概念独特性、构图清晰度、需求符合度
- [x] 导演层 A/B：同一概念，基线 vs 只加 1–2 项决策——已完成一对（单 seed），见 `examples/ab-test.md` §C
- [ ] 把同 seed 对照补到 2–3 个 seed，并在预定 Q 下重做一轮，再考虑把结果写成通用结论
- [ ] 多分镜漫画通道（待 Layout 稳定性改善）
- [ ] 扩展海报专项：复杂信息图、多栏宣传物、精确文字落位（基础版式见 `direction/poster.md`）
- [ ] 游戏实机截图 / HUD 通道
- [ ] ComfyUI 与 Python API 字段对照（官方 API 是 `uncond_skip_layers`，各界面命名不一）

## 致谢

- [OpenMOSS/MOSS-Image](https://github.com/OpenMOSS/MOSS-Image)：模型、用户指南、标注规范、Layout schema 与随附的 Layout 编译器（Apache-2.0）；署名见 [NOTICE.md](NOTICE.md) 和 [`scripts/UPSTREAM.md`](scripts/UPSTREAM.md)
- 技法层的中英对照，以及「术语必须降维成可见事实」这一原则，整理自摄影、电影摄影与插画教学的通行内容

变更记录见 [CHANGELOG.md](CHANGELOG.md)。

## 法律声明

本项目不构成法律意见，按现状提供。生成内容及其使用的全部法律风险由使用者自行承担；本项目不强制内容过滤（私人部署自行决定）。涉及未成年人或幼态外观的性内容是绝对红线。使用前请阅读 [DISCLAIMER.md](DISCLAIMER.md)（[English](DISCLAIMER_EN.md)）。

## 许可证

[Apache License 2.0](LICENSE)，与上游 MOSS-Image 同协议。允许商用、修改与再分发；分发时需保留版权声明、`LICENSE` 与 [NOTICE.md](NOTICE.md) 中的署名，修改过的文件需标明改动。不提供担保，但包含明示的专利授权。
