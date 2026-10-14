# academic-slides

[![Skill self-check](https://github.com/crce-ux/academic-slides/actions/workflows/structure.yml/badge.svg)](https://github.com/crce-ux/academic-slides/actions/workflows/structure.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**学术汇报 PPT 的制作全链路——从内容稿到能上台的成品。**

---

## 覆盖哪些环节

```
①  待核清零          内部工作标记扫成 0 —— 它们不得走到台上
②  理解确认（G3）     闭卷过四关 —— 「写完了」≠「懂了」
③  制作稿七项         把内容稿变成制作稿
④  分镜与 SVG 骨架     ppt_init → make_svg_skeletons
⑤  渲染出片           ppt_build（一条命令）｜ ppt_check 源体检
⑥  成品体检           render_and_qa_pptx —— 像素级
⑦  讲稿与备注         讲稿规格六样 ｜ make_notes 生成 PPT 备注
⑧  上台前            念一遍找磕巴 ｜ 可压缩页与不可压页
```

**② 是门禁**：过不了就不该进 ③。**① 是铁律**：任何一步发现新的待核，退回 ①。

两头是最容易塌的——**上游**：内容稿带着「待核」便签就被拖进幻灯片，作者其实没真懂；
**下游**：PPT 做完了，讲的人没内化，一被问就露馅。本 skill 把两头接上，中间那段自己带工具链。

---

## 三个核心

### 1. 待核清零

把 `待核 / ⏳ / 疑为 / 核不到 / 待补 / TODO` 扫成 **0**。

每一项只有两条路：**核到写实数**，或**删掉**。

> 🔴 **不允许「保留但标注待核」。**
> 这些是给自己的便签——跟着稿子走到台上，就是你当着所有人承认「这里我没查」。
> 而且念到它时的**停顿**比内容本身更显眼。

### 2. 理解确认四测试（G3 门禁）

| # | 测试 |
|---|---|
| 1 | **术语表**——全片术语，能一句不加术语的话解释 + 属性明确 |
| 2 | **数字表**——每个数字的口径 / 基准 / 量级感 |
| 3 | **追问清单**——8–12 个最可能被问的，**合上讲稿**答 |
| 4 | **逐页一句话**——翻开每页，合上讲稿说「这页在说什么」 |

**加上最快的一条**：

> 🔎 **磕巴判据**——把讲稿念一遍，**凡是念得磕巴的地方，就是没内化的地方**。
> 不需要任何表格，念一遍就知道。

### 3. 制作稿七项

`PPT 标题 / 版式建议 / 页面文字 / 表格数据 / 图注 / 讲稿备注 / 口径提醒`

> ⚠️ **「口径提醒」最容易漏、也最救命**——它记的是「这个数字不要念错成另一个」这类临场提醒。

---

## 还包含

- **讲稿规格**——240 字/分钟、每页 200–500 字、**六样必带**（用时表 / 本页纪律 /
  落点清单 / 主动交代清单 / 可压缩页含**不可压页** / 页码对应）
- **版面算术预测**——画之前先算，特别是配图可读性判据 `图内字号 × 显示宽 ÷ 图宽 < 9px`
- **文献原图**——图注三样（出处 / 说什么 / 口径）；**贴图必须与文字换，不是加**
- **去味分力度**——表格数据不动、讲稿备注重改

---

## 工具链

```bash
bash scripts/setup.sh                  # 一次性：拉 ppt-master 到 vendor/（不进 git）
python scripts/ppt_init.py             # 起项目骨架
python scripts/ppt_check.py            # 源体检（ERROR=0 才导出）
python scripts/ppt_build.py            # 讲稿 → 分镜 → 渲染 → 导出，一条命令出片
python scripts/render_and_qa_pptx.py   # 成品像素体检
python scripts/check_talk.py 制作稿.md  # 全链路机检（待核/字数/加粗/时长/七项/六样）
```

**两道体检不能省**：源过不代表成品过。

> ⚠️ `ppt_build.py` 的合并层是第三方的 **`ppt-master`**（Hugo He，MIT），
> 不在本仓——`setup.sh` 会拉到 `vendor/`。**没有它就不能出片。**

---

## 自检

```bash
python scripts/selfcheck.py --strict
```

结构 + 语法 + 依赖，一条命令。

---

## 与相邻工具的关系

| 谁 | 管什么 |
|---|---|
| `ppt-master` / `nature-paper2ppt` | **幻灯片本身**——版式、视觉、合并 |
| **本 skill** | **整条链**——上游内容把关 + 出片工具链 + 下游讲者准备 |

`ppt_build.py` 的合并层调用 `ppt-master`；其余环节自足。

---

## 结构

```
SKILL.md                                全链路八步 + 规格 + Anti-Patterns
references/comprehension-gate.md        四测试逐项做法 + 磕巴判据 + 未解决项处理
references/script-spec.md               规格、版面算术、文献原图、去味分力度、九条红线
scripts/                                工具链 10 个 + 机检 3 个 + 自检 1 个
```

---

## 来源

整理自作者 2026-09 的汇报 PPT 产出流程手册，
含其组会汇报的实际复盘（100+ 处词汇调整、14 处文献论据错误、39 处表述精确性问题）。

原为「讲者侧」单一定位（`talk-readiness`），**2026-10-14 扩为制作全链路**（`academic-slides`）。

---

## 许可

MIT
