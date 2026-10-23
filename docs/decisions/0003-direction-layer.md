# 0003 视觉导演层独立成层

- 日期：2026-10-23
- 状态：已采纳

## 背景

创意层解决了「画什么、为什么特别」，但没有回答「怎么让观众第一眼看到它」。现有 `craft/` 是查表用的技法词典：想写引导线就查引导线，缺的是拿到概念后先决定「选哪几项」的动作。外部评审建议新增一整层美术指导，并给出九份参考文件的目录。

## 选项

| 方案 | 说明 | 结论 |
| :--- | :--- | :--- |
| A. 按建议建 `art_direction/` 九份文件 | 含 composition、camera、lighting、color、material 等 | 否决：与 `craft/` 三份文件重叠 85%–95%，会出现两套漂移的摄影词典，并与「表格只增不删」冲突 |
| B. 建两份薄文件，技巧全部指向 `craft/` | `brief.md` 只写决策流程，`poster.md` 补真正的空白 | **采纳** |
| C. 只把六问塞进 `creative/concept.md` | — | 否决：创意文件会变成两种职责，且海报版式无处落脚 |

## 决定

1. 新增 `references/direction/brief.md`：导演简报六问、决策上限 2–5 项（按强度 2 / 3–4 / 4–5）、删减规则、约束五级优先级、六类任务档案、术语到句子的转译表、自检六条。
2. 新增 `references/direction/poster.md`：信息层级、标题安全区、阅读路径、图文关系、边距与比例适配、文字风险。字号与坐标仍归 `core/text-in-image.md` 与 `core/layout.md`。
3. 约束优先级（用户要求 > 既有画面 > 任务功能 > 创意钩子 > 美术优化）写入 `brief.md` §4，`concept.md` §3 改为引用，不再重复表述。
4. 原「奇观五问」并入通用六问，`concept.md` §8.3 只保留奇观档的追加四条，避免两份问卷。
5. 不引入第二套强度命名，沿用 克制 / 强化 / 奇观。
6. 语序冲突显式记录：通用经验「先写主体」与本仓库「光源句最前」不一致，保留后者，并在 `brief.md` §6 说明如何兼容。

## 影响

- 影响文件：`SKILL.md`（路由、流程、自检 12–13）、新增 `references/direction/brief.md`、新增 `references/direction/poster.md`、`references/creative/concept.md`、`references/diagnostics/sources.md`（一次只改 1–2 个变量）、两份 README、`CHANGELOG.md`
- 不改动 `craft/` 任何表格。
- 待验证：决策上限与优先级排序均为经验判断，未做对照；验证时基线取「只有概念层」的提示词。
