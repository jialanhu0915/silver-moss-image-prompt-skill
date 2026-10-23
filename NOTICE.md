# NOTICE

本仓库的文档由本项目作者撰写。其中的**事实性规范条目**引自 OpenMOSS 的 MOSS-Image 仓库，遵循 Apache License 2.0：

- 上游项目：<https://github.com/OpenMOSS/MOSS-Image>
- 版权：Copyright OpenMOSS Team
- 许可证：Apache License 2.0（本仓库 `LICENSE` 为同一份文本）

被引用的上游材料（均为事实与规范，不是文案转述）：

| 内容 | 上游文件 |
| :--- | :--- |
| 推理参数、Prompt 规范、负面 tag、tag 排序、文字换行规则 | `USERGUIDE.md` / `USERGUIDE_ZH.md` §Inference Parameters、§Prompt Guidelines |
| Layout JSON schema、`abs_centralized` / `yxyx` 定义与坐标换算规则 | `USERGUIDE.md` / `USERGUIDE_ZH.md` §Layout Prompts |
| 训练 caption 规范（`Include only information visible in the image` 等） | `USERGUIDE.md` / `USERGUIDE_ZH.md` §Image Annotation |
| 模型架构、Base 与 SFT 差异、Python API 参数名 | `README.md` / `README_ZH.md` |
| Layout 可选字段（`palette`、`tags`）、像素草稿到中心坐标的编译规则 | `skills/moss-image-prompt-enhancer/`（`SKILL.md`、`references/layout.md`、`scripts/compile_prompt.py`） |

**本项目不是 OpenMOSS 官方项目，未获其背书或审阅。** 上游若更新参数或 schema，以官方文档为准。

## 免责与使用者责任

使用者责任、禁止用途与责任限制见 [DISCLAIMER.md](DISCLAIMER.md)（[English](DISCLAIMER_EN.md)）。

## 上游脚本与原创内容

本项目未基于任何第三方提示词 skill 改写，也未复制上游 prompt-enhancer 的提示词文案。上游 `compile_prompt.py` 原样随附于 `scripts/vendor/openmoss/compile_prompt.py`，来源、固定 commit 与更新方式见 [`scripts/UPSTREAM.md`](scripts/UPSTREAM.md)；该脚本遵循 Apache License 2.0，本仓库 `LICENSE` 与固定版本上游许可证文本一致。分区结构、证据分级体系、档位（Q/R）划分、`craft/` 技法层均为本项目原创设计。
