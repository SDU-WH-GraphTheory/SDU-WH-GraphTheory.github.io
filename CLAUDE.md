# CLAUDE.md

## 项目概览

山东大学威海图染色课题组网站。Hugo 静态站点，使用 Hugo Blox (Wowchemy) 主题，部署在 GitHub Pages。

- **URL**: https://sdu-wh-graphtheory.github.io/
- **仓库**: https://github.com/SDU-WH-GraphTheory/SDU-WH-GraphTheory.github.io
- **部署**: push 到 `main` 分支 → GitHub Actions 自动部署，2-3 分钟后生效
- **技术栈**: Hugo + Hugo Blox (blox-bootstrap/v5) + KaTeX 数学渲染

## Git 工作流（多人协作必读）

```
git pull origin main          # 开始前先拉最新
git checkout -b your-branch   # 在自己的分支干活
# ... 做修改 ...
git add <具体文件>             # 不要用 git add -A，避免误加敏感文件
git commit -m "描述改动"
git push -u origin your-branch
# 然后去 GitHub 创建 PR 合并到 main
```

- 不要在 main 分支直接 commit。永远在自己的分支工作，通过 PR 合并
- 提交前先 `git pull origin main` 避免冲突
- 二进制文件（图片）每次新增不超过 5MB 为宜

## 内容类型与对应目录

| 网站位置 | 目录 | 说明 |
|----------|------|------|
| 首页 | `content/_index.md` | Landing page |
| 近闻 | `content/post/` | 新闻/博文 |
| 成员 | `content/people/index.md` + `content/authors/<姓名>/_index.md` | 团队介绍 |
| 大事记 | `content/event/` | 讨论班活动记录 |
| 文章 | `content/publication/` | 论文列表 |
| 联系方式 | `content/contact/index.md` | |

所有内容用 Markdown 编写，支持 LaTeX（`\(...\)` 行内 / `\[...\]` 行间）。

## 大事记（event）格式规范

**文件夹命名**：`YYYY-MM-DD-session-XX-slug/`

**Frontmatter 模板**（必须使用 `math: true`）：
```yaml
---
title: "讨论班主题"
event: "图论与组合数学讨论班"
event_url: ""
location: 北衡楼 1216
address:
  city: 威海
  region: 山东
  country: 中国
summary: 简短摘要
abstract: 详细摘要
date: 'YYYY-MM-DDTHH:MM:00+08:00'
date_end: 'YYYY-MM-DDTHH:MM:00+08:00'
all_day: false
publishDate: 'YYYY-MM-DDTHH:MM:00+08:00'
authors: [主讲人]
featured: false
image:
  caption: '第X次讨论班海报'
  focal_point: Right
  filename: poster.png
math: true
---
```

**正文结构**：基本信息列表 → 内容概要段落 → 海报图片嵌入

## 海报图片处理

- **格式**：必须用 **WebP**（比 PNG 小 85%），不要用 PNG
- **存储位置**：
  - `static/uploads/posters/xxx.webp` — 正文 Markdown 嵌入用
  - `content/event/<event-folder>/poster.webp` — 封面图（frontmatter `image.filename: poster.webp`）
- **PDF → WebP 转换**：
  ```bash
  # 从 PDF 转 WebP（1200px 宽，quality 85）
  python3 -c "
  from PIL import Image
  from pdf2image import convert_from_path
  img = convert_from_path('input.pdf', dpi=150, first_page=1)[0]
  w, h = img.size
  img = img.resize((1200, int(h*1200/w)), Image.LANCZOS)
  img.save('output.webp', 'WEBP', quality=85)
  "
  ```
- **单张控制在 200KB 以内**，否则拖慢 push 和部署

## 论文（publication）格式

```yaml
---
title: "论文标题"
authors: [admin, 合作者]
date: "2018-01-01T00:00:00Z"
publication_types: ["article-journal"]
publication: "*期刊名*, 卷, 页码"
---
```

## 博文（post）格式

```yaml
---
title: 文章标题
date: YYYY-MM-DD
authors: [作者]
summary: 摘要
---
正文，支持 Markdown + LaTeX...
```

## 网站配置

所有配置在 `config/_default/` 下：
- `hugo.yaml` — Hugo 主配置 + cascade
- `params.yaml` — 外观、功能开关（math、搜索等）
- `menus.yaml` — 导航菜单
- `module.yaml` — Hugo 模块依赖
- `languages.yaml` — 语言设置

KaTeX 数学渲染已全局启用（`params.yaml` 中 `features.math.enable: true` + `hugo.yaml` 中 cascade 设置 `math: true`）。

## 注意事项

- 不要提交 `.DS_Store`、`.claude/` 等本地文件（已在 `.gitignore` 中）
- 不要用 `git add -A` 或 `git add .`
- LaTeX 公式用 `\(...\)` 而不是 `$...$`
- 海报图片必须用 WebP 格式，不超过 200KB
- 修改 `config/` 下的配置后要确认不会影响其他人
- 任何不确定的事，先问再改
