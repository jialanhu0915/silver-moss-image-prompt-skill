# 出处与证据等级

本 skill 的证据分五级（下表）；带出处或等级标记的条目按其标记使用，**没有标注来源的断言，一律视为作者未验证的个人偏好。**已标注的条目以【官方】与【推断】为主；【实测】自 2026-10 起有同 seed A/B 记录，见 §五，但只有单 seed、单一权重，属方向性证据。

| 标记 | 含义 | 你需要做什么 |
| :--- | :--- | :--- |
| 【官方】 | 可在 MOSS-Image 官方仓库原文中找到 | 直接用 |
| 【推断】 | 由官方事实 + 通用知识推出的机制解释 | 可以用，但它不是实验结论 |
| 【社区】 | 来自公开 skill、论坛、他人经验 | 先自己 A/B 一次再用 |
| 【实测】 | 作者在指定参数下验证过 | 注意参数档，不要外推 |
| 【未验证】 | 流传很广但没有任何公开对照实验 | 不要当成规则 |

## 一、官方出处清单

全部来自 `OpenMOSS/MOSS-Image`（Apache-2.0）：

| 内容 | 出处 |
| :--- | :--- |
| 分辨率 1M/1.5M/2M、可外推 0.25M~4M、边长必须是 16 的正整数倍 | `USERGUIDE_ZH.md` §推理参数配置 |
| Steps ≥ 50 最佳 | 同上 |
| CFG 默认 3.0（区间 3.0–6.0）；长 prompt 用 3.0，短 prompt 适当调高 | 同上 |
| Shift 5.0；Sampler 默认 Euler（Flow-matching） | 同上 / `README_ZH.md` §采集参数 |
| SLG 两种：标准（scale 3, 0.01–1.0）与二次采样（`uncond skip`，skip layer 22，22/24/26 均可） | 同上 |
| `关闭 SLG 会使输出的图像非常真实, 但是可能会造成细节的崩坏` | 同上 |
| Python API 参数名 `height/width/num_inference_steps/guidance_scale/uncond_skip_layers`；负面提示词默认为空 | `README_ZH.md` §Python |
| 语言：默认推荐英文，中文等多语言亦支持 | `USERGUIDE_ZH.md` §Prompt 规范 |
| 推荐负面 tag：`nsfw, worst quality, bad anatomy, watermark, jpeg artifact` | 同上 |
| Tag 顺序：`Quality -> Score -> Meta -> Year -> Character -> Series -> Artist -> General`（示例含 `@foo bar`） | 同上 |
| 文字排版：模型会自动换行但未必符合预期，需要精确控制时写 `\n` 或真实换行 | 同上 |
| Layout JSON 标为实验性；`bbox_coord_space: "abs_centralized"`（中心原点）、`bbox_format: "yxyx"`、字段 `summary.caption/meta/canvas` 与 `items[].label/caption/text/bbox`；`label` 三值 `object/character/text`；`canvas` 三值 `single/multi_panel/collage`；左上原点坐标分别减 `W/2`、`H/2` 转换 | `USERGUIDE_ZH.md` §Layout Prompt、`README_ZH.md` §Layout 布局生成 |
| Layout 可选字段 `summary.palette`、`items[].tags`、`items[].palette`（字符串数组）；像素草稿（`abs` + `xyxy`）经脚本编译为 `abs_centralized` + `yxyx`，左上取 floor、右下取 ceil，越界直接报错 | `skills/moss-image-prompt-enhancer/`（`SKILL.md`、`references/layout.md`、`scripts/compile_prompt.py`），非 `USERGUIDE` |
| 采用绝对像素坐标的理由：`更适合不同分辨率和长宽比下的布局控制` | 同上 |
| 自然语言与结构化输入可混用 | 同上 |
| 训练 caption 规范：`Describe the composition, key subjects, actions, setting, colors, lighting, and artistic style in detail.` / `Include only information visible in the image.` / 逐字保留可见文字、不做翻译改写 / Watermark 用 0–1000 归一化坐标 | `USERGUIDE_ZH.md` §图片标注 §Caption Prompt |
| 官方推荐的 caption 模型：Gemma 4、Qwen 3.5 27B、Qwen 3.5 35B-A3B；建议开 thinking | `USERGUIDE_ZH.md` §Caption Model |
| 训 LoRA 时保持 Text Encoder 冻结 | `USERGUIDE_ZH.md` §LoRA |
| 核心特点：布局控制、文字渲染、4K tokens 长提示词、动漫与照片级写实、5B 主干 | `README_ZH.md` §动态 |
| Base 与 SFT 对比：SFT 的文字分组更清晰、排版更有条理 | `README_ZH.md` §Base 与 SFT 对比 |
| 架构：5B 单流 DiT（42 层）、Qwen3.5-9B 文本编码器、FLUX.2 VAE | `README_ZH.md`（HTML 注释与正文） |

## 二、推断链（机制解释，非实验结论）

### 推断 1：语序敏感 → `caption.md` §1、各风格文件的「开头词组」

**事实**：文本编码器是 Qwen3.5-9B，一个解码器式因果语言模型。**推断**：条件文本按从左到右编码，前置 token 给后续 token 提供上下文，因此**写在前面的词给整图定调，末尾补的词很难覆盖前面**。官方没有讨论语序，也没有语序的对照实验——这条属于工程共识，方向上可信，强度未知。

### 推断 2：写「器材名」不如写「可见结果」 → `photo.md` §2、`anime.md` §7

**事实**：训练 caption 规范要求 `Include only information visible in the image`，且列出的维度是 composition/subjects/actions/setting/colors/lighting/artistic style。**推断**：相机型号、胶片型号、渲染引擎名、画师 ID 属于不可见信息，不会出现在生成的 caption 里；模型没有学过「型号 → 质感」的映射，所以型号名只有和它造成的可见结果写在同一句里才安全。**边界**：官方 tag 串排序里确实有 Artist 位，说明**标签形式的**画师信息在训练数据中存在——「画师名完全无效」不成立，准确说法是「散文形式里很弱」。社区流传的「80% 训练 caption 由 VLM 重新生成」这个比例，官方文档只写了会重写并给了 prompt、没有给比例，**不要引用这个数字**，除非你能在技术报告里找到页码。

### 推断 3：档 R 需要人工补偿 → `params.md` §2、`photo.md` §9、`anime.md` §9

**官方原话**：关闭 SLG 更真实，但可能造成细节崩坏。**推断**：档 R（关 SLG + 低步数 + 低像素）用真实感换来了细节风险，因此需要显式的防崩词与固化描述来补偿；档 Q（开 SLG + 50 步）已经有收敛机制，继续堆防崩词会过冲、边缘发硬。这是本 skill 用来组织规则的结构性假设：把「一堆技巧」按档取用。

### 推断 4：长负面池的边际收益未知 → `negative.md` §3

**事实**：官方只给 5 个推荐 tag，且没有关于负面词长度的实验；社区池长到几百词，但没有任何公开消融。**立场**：本 skill 限制在 40~80 词，理由是「超出部分没有证据支持，且 CFG 3.0 下额外词权重很低」。如果有人做出 A/B，欢迎改这一条。

### 推断 5：`craft/` 三份文件的定位

**事实**：官方标注规范把 `colors`、`lighting`、`artistic style` 列为必描述维度。**推断**：落在这三个维度里的词（光位、色相、笔触、材质）有稳定像素对应；不落在其中的词（作者名、平台名、渲染器名）没有。**边界**：`craft/camera.md`、`craft/composition.md`、`craft/aesthetics.md` 里的技法条目来自摄影与绘画的通行知识，**不是**本模型上的实验结论。凡涉「在本模型上更有效」处已标【需核】，引用时请保留该标注。

## 三、明确不采用的社区说法

| 说法 | 状态 | 本 skill 的处理 |
| :--- | :--- | :--- |
| `<\|概念\|>...<\|/概念\|>` 闭合标签能把信噪比提升十几倍 | 【未验证】官方文档无此语法，也未给出任何分隔格式实验 | 标为实验性，默认用自然分段；要用先自测（`caption.md` §1） |
| `SLG=""` 是「写实/二次元」的画风开关 | 【推断】官方只说关闭更真实、可能崩细节 | 改述为：关 SLG 提升真实感，画风由提示词本体决定 |
| 指定「负向分支跳过第 22 层」对应某种画风 | 【未验证】官方只说 22/24/26 都能改善质量 | 不赋予层号画风含义 |
| `single_layers` / `double_layers` 是通用参数名 | 【未验证】这是某个 ComfyUI 节点的字段命名 | 统一用官方 Python API 的 `uncond_skip_layers`，并提示用户以自己界面的字段为准 |
| 具体相机型号、渲染引擎名能切画风 | 【未验证】与推断 2 冲突 | 一律改成可见结果描述 |
| 单写某个画师名或 `XXX style` 能还原笔触 | 【推断】散文 caption 里不可见 | 走 LoRA |

## 四、如何自己补一条【实测】

```text
日期 / 模型版本(Base 或 SFT) / 参数档(Q 或 R)
固定项：尺寸、Steps、CFG、Shift、SLG、Seed
变量：只改一处，写清改前改后完整句子
结果：3~5 张同 seed 出图的差异描述，最好附图
判定：有效 / 无效 / 只在某条件下有效
```

判定标准（自用即可，不必追求论文级）：**有效** = 换回原句后差异消失，且换第二次仍然复现；**方向性有效** = 差异存在但幅度小，只在特定题材出现；**无效** = A/B 看不出可辨认差异。

验证创意层或导演层时，另守两条：

1. **一次只改 1–2 个变量**（先只换概念，再只加镜头，再只加光色），否则无法归因。
2. **基线 = 只有概念层的提示词**；对照组才加导演决策。关闭 prompt upsampler，或两组都开，不要一边开一边关。

补完把结论写进对应文件，并在这里加一行记录。

## 五、已实测记录

共同条件：MOSS-Image 权重为社区微调版（型号不公开）、本机 ComfyUI、1360×752（16:9 / 1MP）、Steps 25、CFG 3.0、Euler + simple、SLG 关闭、每组同 seed，只有正面 caption 与 upsampler 开关变动。**全部为单 seed，认定为方向性证据，不可外推为统计结论。**

| # | 结论 | 变量 | 判定 | 图 |
| :--- | :--- | :--- | :--- | :--- |
| T1 | caption 独有的光色与材质信息（绿檐灯、湿路面绿反射、冷暖分区、蒸汽受光）在关闭 upsampler 后稳定落到画面；开启时基线被改写器补成合格画面，两组差距明显压缩 | seed 738835547678523；upsampler 开/关 × 基线/skill | 方向性有效 | `imgs/a_*_off.png`、`imgs/a_*_up.png` |
| T2 | 尺度参照（人/桌/窗/月）、窗棂切割与冷暖分区，即使在 upsampler 开启下也没被抹平；基线把「图书馆」漂成「哥特庄园」，且无任何尺度参照 | seed 197301879477886；upsampler 开 | 方向性有效 | `imgs/b_*_up.png` |
| T3 | 「落进褐色阴影」写成绝对句会把主体一起埋掉（报纸不可读、人脸沉暗）；补上「窗光为主光 + 前景栏杆占下六分之一 + 报纸亮到能读出行边」后，盖碗、可读报纸、红尾灯、栏杆条四项同时落地 | seed 551418087126216；upsampler 关 | 有效（修正前后非同参数对照，只确认修正版成立） | `imgs/c_*_off.png` |

**附带观察（未做对照，标【未验证】）**：改写器对信息量少的基线增益更大，因此任何「开着 upsampler 比较两版提示词」的测试都会低估写法差异；要判断写法本身，必须关掉它。完整 caption 与参数见 `examples/ab-test.md`。
