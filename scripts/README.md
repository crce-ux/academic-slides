# scripts/

**这里是运行版。正本在 [`research-workflow`](https://github.com/crce-ux/research-workflow) 的 `scripts/`**——开发与测试都在那边。

改脚本请改总仓，再同步过来；**不要只改这里**。

> ⚠️ **PPT 工具链这十个互为本地依赖**（互相 `sys.path.insert` + import），
> 要**整个目录一起用**，单独拷一个出去会 import 失败。

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
| **`ppt-master`** | 🔴 **不在本仓**——`ppt_build.py` 的合并层依赖它。先跑 `bash scripts/setup.sh` 拉到 `vendor/` |
| 浏览器 / headless chrome | `render_*` 系列要用 |

## 先跑 setup

```bash
bash scripts/setup.sh      # 拉 ppt-master 到 vendor/（不进 git）+ 装 pip 依赖
```

`ppt-master` 是 [Hugo He](https://github.com/hugohe3/ppt-master) 的第三方 **MIT** 项目，731 MB。
本仓库**不分发它**——只放一个脚本，用的时候自己拉。

`ppt_build.py` 会自动在 `vendor/` 下找到合并层；也可以用环境变量 `PPT_MASTER=<...>/svg_to_pptx.py` 指到别处。
