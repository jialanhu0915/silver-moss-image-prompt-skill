# 图内文字渲染

## 1. 基本写法（官方）

- 要渲染的字符串用**引号**包起来，跟描述语混在同一段散文里。
- 换行直接写 `\n` 或真实换行，模型照着断行，不写就由模型自己排；中英文都能渲染，中文直接给中文正文，不要用英文描述「一段中文标题」。

```text
A wide view of a refrigerator beside a kitchen counter with a fruit bowl. A small sticky note on the refrigerator door is handwritten in Chinese:
"记得买牛奶和鸡蛋！\n牛奶两盒，鸡蛋一打。\n顺便带一袋面包。"
```

## 2. 字号能不能放下（没有脚本时怎么估）

```text
字高(px) ≈ 区域高度 ÷ 行数
每行字数 ≈ 区域宽度 ÷ 字高
能放下的总字数 ≈ 每行字数 × 行数
```

| 字高 | 结果 |
| :--- | :--- |
| ≥ 40px | 汉字稳定清晰 |
| 24~40px | 多数能读，偶尔错笔画 |
| < 24px | 必糊，别写 |

放不下时的处理顺序：**① 提高分辨率 → ② 扩大区域 → ③ 精简文案**。**不许删掉用户要的字，也不许把字压扁**——压扁的字形会变成粘连的墨块。

反例：40 个汉字塞进 200×100 的区域 → 字高 25px、每行 8 字 → 五行，实际上必崩。要么区域加到 400×250，要么把文案砍到 12 字。

## 3. 竖排中文的坑

竖排（`vertical Chinese text`）按日式/中式网格逐格排字，两个高频故障：

- **半角阿拉伯数字**会被挤进一个汉字格，几位数叠成一坨。→ 竖排框里的金额、年龄、数量改写成汉字数字：`720日元` → `七百二十日元`，`28岁` → `二十八岁`。横排印刷体（包装盒、屏幕、招牌）保留阿拉伯数字。
- **姓名中间的半角空格**会被画成一个圆圈 `O`。→ 连写：`一色凛`，不要 `一色 凛`。竖排 / 横排都要在 caption 里写清。

```text
Clean vertical Chinese text reading "七百二十日元" inside the frame.
Clean horizontal Chinese text reading "¥720" printed on the price tag.
```

## 4. 文字会反过来污染画面

| 图内文字 | 副作用 | 对策 |
| :--- | :--- | :--- |
| `LOLITA`、`148cm`、`12岁` | 人物被画成幼童 | 改印 `15岁` 之类；正文写清体型；负面加 `child, toddler, loli, babyface` |
| `AGE : 19`、`BUST 92` | 人物被画胖、画成熟 | 正文写 `very slender, flat stomach, visible collarbone, small A-cup`；负面加 `fat, chubby, curvy, large breasts` |
| `cosplay`、`コスプレ` | 假发感、塑料服装 | 删掉这个词，改写成「天生就长这样」 |

## 5. 提高正确率的四个手段

1. **降字数**：单块文字越短越准，长文案拆成多个文字块。
2. **加分辨率与 SLG**：整页小字必须 ≥1.5M + Steps 50 + `uncond_skip_layers=[22]`。
3. **给字体感而不是字体名**：`bold condensed sans-serif with tight letter spacing`（粗压缩黑体、字距紧）比 `思源黑体 Bold` 有用，品牌字体名基本无效。
4. **给版面关系**：`centered at the top`、`left-aligned on two lines`、`small caption in the lower-right corner`；只说「有标题」模型会把字随手丢。

## 6. 与 Layout 的关系

精确落位（海报、封面、表格）本该走 Layout 的 `label: "text"` + `text` + bbox，当前版本不稳定，默认走 caption：用**方位词 + 版面关系**近似控制，如 `a large title across the top third`、`a narrow vertical banner along the right edge`。真要像素级落位时读 `core/layout.md`，并接受可能要重试几次。
