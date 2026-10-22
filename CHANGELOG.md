# 版本记录

## 未发布

**法律与内容策略**
- 新增 `DISCLAIMER.md` / `DISCLAIMER_EN.md`：使用者责任、禁止用途、无担保、责任限制、赔偿、与 Apache-2.0 的关系
- 默认负面基线去掉强制的 `nsfw`（过滤由部署者决定）；SKILL.md 红线加入：不提供涉及未成年人或幼态外观的性内容的写法、不协助以真实人物生成性/诽谤/欺诈内容
- 不限制人物年龄；`text-in-image.md` 去掉「改印 15 岁」与罩杯描写的对策，儿童题材（如亲子照）无需处理

**修正**
- `watermark` 与有图内文字的矛盾：有文字时负面去掉 `watermark` 与 `text`（`negative.md`、`troubleshooting.md`、SKILL.md 自检第 9 条、`examples/anime.md`）
- 二次元分段骨架默认改为自然分段，`<|xxx|>` 闭合标签降为可选的社区写法，与 `sources.md` 一致
- 更正「每条规则都标了 [Q]/[R] 与证据等级」的不实表述（`params.md`、两份 README、`sources.md`）；统一 `[Q,R]` 写法与【社区】括号
- `negative.md` L1 去掉与 L0 重复的 `worst quality`、`jpeg artifacts`、`bad anatomy`
- 更正 v0.2.0 记录：「表格零损失」仅指 craft 三文件；`troubleshooting.md` 由表改列表，34 条症状合并为 30 条 bullet，标题保留全部症状，无内容丢失


## v0.2.0 — 2026-10-21

全仓按「只留能用的话」重写，结构与文件职责不变。

**结构**
- 新增 `references/styles/hybrid.md`：跨次元合成、三渲二、媒介叠合、同图双画风
- 新增 `core/caption.md` §6 tag 串：官方 tag 顺序、清洗步骤、禁止权重语法
- `SKILL.md` 路由表扩到 12 条，流程与自检同步三通道判定

**压缩**
- 2043 → 1776 行（−13%）：删机制解释、重复提醒、元叙述与自我评价
- 表格零损失：camera 108、composition 62、aesthetics 131 条词条压缩前后逐条一致
- 新增维护规则：对照表只增不删

**修正**
- 删去 Layout 一节无依据的「实测」断言，改为官方 Experimental 事实
- 明确 Q/R 两档是本 skill 的预设组合，非官方推荐值
- 修 `caption.md` 重编号导致的 §引用失效，以及两处措辞错误
- README 删去对其他实现的比较与评断，改为双语（`README.md` / `README_ZH.md`）

## v0.1.0 — 2026-10-21

首次发布。写实 / 二次元两条通道、五个 core 文件、三份技法词典、症状排查与出处清单，附四例完整走查。
