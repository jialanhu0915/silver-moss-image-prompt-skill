# silver-moss-image-prompt-skill

写给 [MOSS-Image](https://github.com/OpenMOSS/MOSS-Image) 的提示词 skill。把一个想法、一段参考描述或一堆 Danbooru tag，写成一段模型真想画的 caption，外加一条负面提示词和一组采样参数。

覆盖两条风格通道：**三次元写实**与**二次元插画**，外加一层风格无关的技法词典（镜头 / 构图 / 美学）。

## 它不是什么

- 不是 OpenMOSS 官方项目，只是按官方规范写的工作方法（见 `NOTICE.md`）
- 不是「提示词模板库」，没有一键套用的固定句式大全
- 不帮你出图，也不依赖任何脚本或第三方依赖——纯 Markdown

## 为什么这样分文件

一份 900 行的单文件 skill，每次加载有七成内容与当前任务无关，而且改一条规则要在几千字里找半天。这里按「一层只放一类知识」切开：

| 层 | 目录 | 放什么 | 加载时机 |
| :--- | :--- | :--- | :--- |
| 路由与流程 | `SKILL.md` | 判据表、五步流程、自检、红线 | 每次 |
| 契约层 | `references/core/` | caption 写法、参数、负面词、图内文字、Layout | 首次 + 按需 |
| 风格层 | `references/styles/` | 写实 / 二次元，只写该风格的独有决定 | 一次只读一个 |
| 技法层 | `references/craft/` | 镜头、构图、美学词汇——风格无关 | 需要时按条查 |
| 诊断层 | `references/diagnostics/` | 症状排查、出处与证据等级 | 出错或要溯源时 |

单次任务通常只加载 `SKILL.md` + 1 个 core + 1 个 style（+ 1 个 craft），约 400~500 行，且全部命中当前任务。

## 安装

放进 Agent Skills 目录，目录名需与 `SKILL.md` 里的 `name` 一致：

```text
<skills-dir>/silver-moss-image-prompt-skill/SKILL.md
```

支持 [Agent Skills 规范](https://agentskills.io/specification) 的客户端可直接使用；也可以把 `SKILL.md` 粘进系统提示词末尾，其余文件当参考手册查。

## 目录

```text
SKILL.md                            路由 + 流程 + 自检（约 180 行）
references/
├── core/
│   ├── caption.md                  散文交付物：语序、长度、语言、反模式
│   ├── params.md                   采样参数、两档配置、分辨率速查表
│   ├── negative.md                 负面词分层拼法
│   ├── text-in-image.md            图内文字：字号估算、竖排、污染画面
│   └── layout.md                   Layout JSON（实验性，默认不用）
├── styles/
│   ├── photo.md                    写实通道：开场模组、暗部、骨相、剧照感
│   └── anime.md                    二次元通道：画种、版式、完成度、LoRA
├── craft/
│   ├── camera.md                   焦距、景别、机位、景深、缺陷、画幅
│   ├── composition.md              版式、三层空间、留白、群像、事故预防
│   └── aesthetics.md               光位、色彩、技法、流派、材质、情绪
└── diagnostics/
    ├── troubleshooting.md          症状 → 原因 → 改法
    └── sources.md                  出处、证据等级、不采用的社区说法
examples/
├── photo.md                        写实两例（完整提示词 + 参数 + 自检记录）
└── anime.md                        二次元两例
```

## 三个设计决定

**1. 规则与参数档绑定。** 官方唯一一句机制断言是「关闭 SLG 更真实，但可能造成细节崩坏」。本 skill 由此划两档：**Q**（开 SLG + 50 步 + ≥1M，交付用）与 **R**（关 SLG + 低步数 + 0.6M，快出图）。规则后标 `[Q]` / `[R]`，因为防崩词在 Q 档会过冲，在 R 档不写就崩。多数提示词教程把技巧堆成不分前提的清单，这是它们最大的可移植性缺陷。

**2. 只写可见信息。** 官方标注规范要求 caption 只描述图上可见内容，维度是构图 / 主体 / 动作 / 场景 / 颜色 / 光线 / 画风。所以相机型号、渲染引擎、软件名、画师 ID 单写基本无效——要写它们造成的可见结果。这条贯穿全部文件。

**3. 证据分级，不许含糊。** 每条规则标【官方】/【推断】/【社区】/【实测】/【未验证】。当前状态是：绝大多数为【官方】与【推断】，【实测】几乎为空。这不是缺陷，是诚实的现状——`sources.md` 里列了哪些社区说法本 skill **明确不采用**。

## 已知边界

- **Layout 降级处理**：官方标为实验性，当前版本坐标要手工换算、跨分辨率易错位，`core/layout.md` 只作备用路径。
- **没有联网引用**：`craft/` 三份文档的技法条目来自摄影与绘画的通行知识，凡是涉及「在本模型上更有效」的断言都标了【需核】，没有一条有对照实验支撑。
- **只覆盖两条通道**：多分镜漫画、海报排版、游戏 HUD、跨次元混合暂未收录，`craft/` 与 `core/` 里的条目大多可以复用，但缺各自的专项规则。

## 待做

- [ ] 补【实测】：每条【需核】至少做一次同 seed A/B（记录模板在 `sources.md`）
- [ ] 多分镜漫画通道（依赖 Layout 稳定性改善）
- [ ] 海报与图文版面通道
- [ ] 游戏实机截图 / HUD 通道
- [ ] ComfyUI 与 Python API 的字段对照（官方 API 是 `uncond_skip_layers`，各界面命名不一）

## 致谢

- [OpenMOSS/MOSS-Image](https://github.com/OpenMOSS/MOSS-Image)：模型、用户指南、标注规范与 Layout schema（Apache-2.0）
- 技法层的中英对照与「术语必须转成可见事实」这一原则，整理自摄影、电影摄影与插画教学的通行内容

## 许可证

[Apache License 2.0](LICENSE)，与上游一致。若你想改用 CC-BY-4.0 等文档类许可证，替换 `LICENSE` 并改本节即可；`NOTICE.md` 里对上游的署名请保留。
