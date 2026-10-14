# scripts/

**本目录是运行版。正本在 [`research-workflow`](https://github.com/crce-ux/research-workflow) 的 `scripts/`**——开发与测试都在 `research-workflow`。

改脚本请改总仓，再同步过来；**不要只改本目录**。

> ⚠️ **PPT 工具链的十个脚本互为本地依赖**（互相 `sys.path.insert` + import），
> 要**整个目录一起用**，单独拷一个出去会 import 失败。

## 讲者侧机检

| 脚本 | 查什么 |
|---|---|
| `check_talk.py` | 待核清零 / 洗白词 / 每页 200–500 字 / 加粗 ≤3 / 总字数↔时长 / 制作稿七项 / 讲稿六样 |
| `slide_fit.py` | **画之前的版面算术**：容量、带高之和 vs 区域高、**配图可读性**（图内字号 × 显示宽 ÷ 图宽 < 9px） |

页的认法按真实产物：制作稿 `## S1 · 标题`、讲稿 `# 01_封面`（`--page-re` 可覆盖）。
**它不查判断类**——四测试判据、磕巴判据、去味力度仍归人。

## 出片

| 脚本 | 干什么 |
|---|---|
| `ppt_init.py` | 起一个 PPT 项目骨架 |
| `ppt_build.py` | 讲稿 → 分镜 → 渲染 → 导出，一条命令出片 |
| `ppt_check.py` | 版面体检（溢出 / 越界 / 字号） |
| `make_svg_skeletons.py` | 生成整页 SVG 骨架 |
| `make_notes.py` | 生成讲稿备注 |
| `render_svg.py` | SVG 渲染 |
| `render_templates.py` | 模板渲染（可拼联系表） |
| `render_and_qa_pptx.py` | 渲染 PPTX 并质检 |
| `ppt_kit.py` | 构件库（被上面几个 import） |
| `ppt_style.py` | 视觉规范（同上） |

## 依赖

| 项 | 说明 |
|---|---|
| `openpyxl` / `Pillow` / `lxml` | 部分脚本需要 |
| `check_skill_structure.py` | 结构校验（官方 Agent Skills 规范）：name / description / 正文长度 / 深链 / **声明落地** |
| `selfcheck.py` | **一条命令自检**：结构 + 语法 + 依赖。见下 |
| **`ppt-master`** | 🔴 **不在本仓**——`ppt_build.py` 的合并层依赖它。先跑 `bash scripts/setup.sh` 拉到 `vendor/` |
| 浏览器 / headless chrome | `render_*` 系列要用 |

## 先跑 setup

```bash
bash scripts/setup.sh      # 拉 ppt-master 到 vendor/（不进 git）+ 装 pip 依赖
```

`ppt-master` 是 [Hugo He](https://github.com/hugohe3/ppt-master) 的第三方 **MIT** 项目，731 MB。
本仓库**不分发它**——只放一个脚本，用的时候自己拉。

`ppt_build.py` 会自动在 `vendor/` 下找到合并层；也可以用环境变量 `PPT_MASTER=<...>/svg_to_pptx.py` 指到别处。

## 自检

```bash
python scripts/selfcheck.py            # 结构 + 语法 + 依赖
python scripts/selfcheck.py --strict   # 结构警告也算失败（CI 用这个）
```

查三样：**结构**（官方规范）· **语法**（逐个编译 `scripts/*.py`）· **依赖**（哪些脚本要装第三方库，只报不判）。
下载本 skill 后想确认「东西是齐的、没坏的」，跑 `selfcheck.py` 就够。
