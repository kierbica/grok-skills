---
name: lw-ai-tell-audit
description: The pre-delivery AI-tell audit for lyrics (歌词 AI 味诊断). Run this on every draft before it ships. The eight enumerable symptoms that make AI-written lyrics recognisable in one listen, which are machine-countable and which need a person, the diagnostic path from symptom to owning skill, why a draft that passes every check can still be lifeless, and the remediation list. Use when a lyric draft is about to be delivered, when a draft reads fine but feels generic, when deciding whether to accept a version, or when a lyric passed LYR-LINT but still sounds machine-written. AI 味、歌词诊断、验收、太泛、像 AI 写的、交稿前检查。
---

# 歌词 AI 味诊断（AI-Tell Audit）

**每一稿交出去之前都要过这个 skill。这是本库的终检。**

> **核心命题**：AI 写的词不是"用词不好"，是**「没有人做过选择」**。
> 它写出来的四段词语法正确、押韵工整、意象丰富，
> **而这四段可以属于任何一首歌。**

## 按任务读哪几节

| 任务 | 读 |
|---|---|
| 刚写完，要验收 | §2 八条 → §3 |
| "读着没问题但就是泛" | ★ §2（**逐条查，不要凭感觉**） |
| 全过了还是像 AI | ★ §4 |
| 查出问题要改 | §5 |

## 边界

| 不归这里 | 归哪 |
|---|---|
| 规格写完时的检查 | **LYR-LINT 十条**（`lw-workflow` §5.2） |
| 具体怎么改 | 各 L1/L2 skill（§5 给路由） |
| 倒字的判定 | `lw-tone-check` |
| 生成出来的**音频**像不像 AI | **库一** `mc-ai-tell-audit` |

> ★ **与 LYR-LINT 的分工**：
> **lint 问"规格填完没有"，本 skill 问"这词像不像人写的"。**
> **两者都过才算完。** 十条全过的词照样可能满是 AI 味。

---

## 1. 开工前

| 必填 | 问法 |
|---|---|
| **① 这一稿的版本与来源** | AI 直写？skill 引导？手写？**做 AB 时这一栏是全部** |
| **② 语言** | 中文要额外查倒字/辙口 |
| **③ 有没有旋律** | 没有的话第 5 条查不了 |

---

## 2. ★ 八条枚举

**逐条打勾。不要凭整体印象。**

| # | AI 味症状 | 对抗的 LYR-SPEC 字段 | 可自动 | 归谁管 |
|---|---|---|---|---|
| **1** | **名词全是抽象的** | `imagery.concrete_nouns` 必填、`forbidden` 黑名单 | ✅ 词性与词表统计 | `lw-imagery` |
| **2** | **结构对称到死** | `asymmetry` 三项必填 | ✅ 每段字数方差 | `lw-structure` |
| **3** | **什么都解决了，没有悬着的** | `narrative.withholding` 必填 | ⚠ 半自动 | `lw-narrative` |
| **4** | **没有视角和时间** | `narrative.pov` ＋ `tense_anchor` | ⚠ 人称代词检测可辅助 | `lw-narrative` |
| **5** | **倒字不管** | `prosody` ＋ 倒字检测器 | ✅ **完全可算** | `lw-tone-check` |
| **6** | **辙口只挑最顺的** | `rhyme.che` ＋ 辙口分布统计 | ✅ | `lw-mandarin` |
| **7** | **押韵永远选第一个想到的字** | `rhyme.surprise_notes` | ✅ 韵脚词频 | `lw-rhyme` |
| **8** | **副歌各遍全同，且末遍既没改一字也没加尾**（全同本身在语料里占 27%，不是病） | `asymmetry.chorus_variation` | ✅ 文本 diff | `lw-structure` §6.0 |

★ **八条里六条可算**（第 3、4 半自动）。
**这个比例比库一（十四条里九条）更硬，因为文本不需要检测。**

> ★ **这张表一张三用**：本 skill 的骨架、LYR-LINT 十条的来源、AB 实验评判表的骨架。
> **改一处要同步三处。**

### 2.1 ★ 三条最致命的

**不是因为最难查，而是因为它们读起来都不"错"：**

| # | 为什么致命 |
|---|---|
| **1（名词全抽象）** | ★ **最直接的 AI 指纹**。"时光"、"远方"、"梦"、"自由"——每个都对，合起来是空的 |
| **2（对称到死）** | 四段每段四句、每句七字、句句押韵。**技术上完美，听感上是表格** |
| **3（什么都解决了）** | AI 会把情绪走完整：难过→释怀→祝福。**真人写词经常停在难受里** |

### 2.2 四个立刻能数的粗筛

```bash
# 抽象词命中数 / 具体名词数
# 每段字数方差
# 副歌各遍的文本 diff（★ 只看末遍有没有改动；前两遍相同不算问题）
# 韵脚字的词频排名
```

这四项**人工数**——每项一分钟以内，不需要脚本。

---

## 3. 两个数，不许合并

| | 问什么 | 怎么得 |
|---|---|---|
| **LYR-LINT 通过数** | 规格填完了多少 | 十条 |
| **AI 味旗标数** | 词有多少条机器指纹 | 本 skill 八条 |

```
lint 全过 + 旗标少  → 好，交
lint 全过 + 旗标多  → 规格对但词空，改
lint 没过            → 先补规格
```

**永远不要把两个数加在一起当"总分"。**

---

## 4. 全过了还是像 AI

八条全勾了还是空，通常是因为：

- 意象成套了，但**没有一件事发生**
- 视角有了，但**说话的人没有态度**
- 结构不对称了，但**每一段都在说同一件事**

这时回到 `lw-song-intent` 的五个问题，尤其是「只说一件事」和「锚定物件」。

---

## 5. 改法路由

| 症状 | 去哪个 skill |
|---|---|
| 抽象名词多 | `lw-imagery` |
| 结构太对称 | `lw-structure` |
| 什么都解决了 | `lw-narrative` |
| 没有视角/时间 | `lw-narrative` |
| 倒字 | `lw-tone-check` |
| 辙口太顺 | `lw-mandarin` |
| 韵脚太熟 | `lw-rhyme` |
| 副歌全同 | `lw-structure` |

---

## 6. 验收标准

- 八条逐条勾过
- LYR-LINT 十条也过
- 读起来有「有人在这里做过选择」的感觉
