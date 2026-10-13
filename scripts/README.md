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

## 交付前体检

| 脚本 | 干什么 |
|---|---|
| `check_assets.py` | 资产检查 |

## 依赖

| 项 | 说明 |
|---|---|
| `openpyxl` / `Pillow` / `lxml` | 部分脚本需要 |
| **`ppt-master`** | 🔴 **不在本仓**——`ppt_build.py` 的合并层依赖它；缺了渲染那一步会断 |
| 浏览器 / headless chrome | `render_*` 系列要用 |

**`ppt_build.py` 不是自包含的。** 用之前先确认 `ppt-master` 在环境里。
