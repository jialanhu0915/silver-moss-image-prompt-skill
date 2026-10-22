# silver-moss-image-prompt-skill

[English](README.md) · **简体中文**

写给 [MOSS-Image](https://github.com/OpenMOSS/MOSS-Image) 的提示词 skill。把一个想法、一段参考描述或一堆 Danbooru tag，写成一段模型真想画的 caption，外加一条负面提示词和一组采样参数。

三条风格通道——**写实**、**二次元**、**混合**（跨次元合成、三渲二、媒介叠合、同图双画风）——之下是一层风格无关的技法词典：镜头、构图、美学。

## 它不是什么

- 不是 OpenMOSS 官方项目，只是按官方规范写出来的工作方法（出处见 [NOTICE.md](NOTICE.md)）
- 不是模板库，没有一键套用的固定句式大全
- 不生成图片，纯 Markdown，无脚本、无依赖

## 内容怎么组织

skill 在任务命中时才被加载，所以结构直接决定模型实际读到什么。这里每一层只放一类知识：

| 层 | 目录 | 放什么 | 加载时机 |
| :--- | :--- | :--- | :--- |
| 路由 | `SKILL.md` | 判据表、五步流程、自检、红线 | 每次 |
| 契约 | `references/core/` | caption 写法、采样、负面词、图内文字、Layout | 首次 + 按需 |
| 风格 | `references/styles/` | 写实 / 二次元 / 混合，只写该通道独有的决定 | 一次只读一个 |
| 技法 | `references/craft/` | 镜头、构图、美学——与画风无关 | 按条目查 |
| 诊断 | `references/diagnostics/` | 症状排查、出处与证据等级 | 出错或要溯源时 |

一次任务通常读 `SKILL.md` + 一个契约文件 + 一个风格文件，只有需要某种具体技法时才去翻对应的 craft 文件。

维护规则：所有对照表只增不删。可以新增词条、修正词条，但不删除、不合并；压缩只针对表格之外的文字。

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
├── anime.md                        二次元两例
└── layout.md                       实验性 JSON Layout：草稿与编译结果
docs/decisions/                     决策记录（ADR）及索引
```

## 三个设计决定

**规则与参数档绑定。** 官方用户指南指出：关闭 SLG 会让画面更真实，但可能造成细节崩坏。本 skill 由此划两档——**Q**（开 SLG、50 步、≥1M 像素，交付用）与 **R**（关 SLG、低步数、0.6M 像素，快出图）。依赖档位的规则标 `[Q]` / `[R]`（未标的两档都成立），因为防崩词在 Q 档会过冲，在 R 档不写就崩。

**只写可见信息。** 官方标注规范要求描述构图、主体、动作、场景、颜色、光线与画风，且只描述图上可见内容。所以相机型号、渲染引擎、软件名、画师 ID 单写基本无效——要写它们造成的可见结果。这条贯穿全部文件。

**证据分级，写在前面。** 证据分【官方】【推断】【社区】【实测】【未验证】五级（见 `sources.md`）。已标注的条目以官方与推断为主；未标注的断言是作者未经验证的工作经验；凡是需要对照实验才能下结论的，一律标为未验证，而不是当作事实陈述。`sources.md` 还列出了本 skill **明确不采用**的社区流传说法。

## 已知边界

- **Layout 实验性且默认关闭。** 上游提供编译脚本；本 skill 增加了一个示例：其坐标转换在调整副标题框之前通过过编译器验证；调整后的框目前仅手算、尚未重跑编译器；MOSS-Image 实际出图未测试。见 `core/layout.md` 与 `examples/layout.md`。
- **规则尚未做受控测试。** 技法层来自摄影与插画的通行知识；「在本模型上更有效」这类断言均标为未验证。
- **只写了三条通道。** 多分镜漫画、海报排版、游戏 HUD 尚未成篇；core 与 craft 的条目大多可以复用，但各自缺专项规则。

## 待做

- [ ] 为每条未验证条目补同 seed 的 A/B 对照（模板见 `sources.md`）
- [ ] 多分镜漫画通道（待 Layout 稳定性改善）
- [ ] 海报与图文版面通道
- [ ] 游戏实机截图 / HUD 通道
- [ ] ComfyUI 与 Python API 字段对照（官方 API 是 `uncond_skip_layers`，各界面命名不一）

## 致谢

- [OpenMOSS/MOSS-Image](https://github.com/OpenMOSS/MOSS-Image)：模型、用户指南、标注规范与 Layout schema（Apache-2.0），署名见 [NOTICE.md](NOTICE.md)
- 技法层的中英对照，以及「术语必须降维成可见事实」这一原则，整理自摄影、电影摄影与插画教学的通行内容

变更记录见 [CHANGELOG.md](CHANGELOG.md)。

## 法律声明

本项目不构成法律意见，按现状提供。生成内容及其使用的全部法律风险由使用者自行承担；本项目不强制内容过滤（私人部署自行决定）。涉及未成年人或幼态外观的性内容是绝对红线。使用前请阅读 [DISCLAIMER.md](DISCLAIMER.md)（[English](DISCLAIMER_EN.md)）。

## 许可证

[Apache License 2.0](LICENSE)，与上游 MOSS-Image 同协议。允许商用、修改与再分发；分发时需保留版权声明、`LICENSE` 与 [NOTICE.md](NOTICE.md) 中的署名，修改过的文件需标明改动。不提供担保，但包含明示的专利授权。
