---
name: news-post
description: 将会议记录/转写内容整理为"近闻"文章，本地预览后推送到 GitHub Pages。用户提供讨论内容后，自动生成符合项目格式的新闻纪要并发布。
---

# 近闻文章发布流程

## 前置条件

确保本地是最新代码：

```bash
cd <项目目录>
git pull origin main
```

如果还没有克隆项目，先克隆：

```bash
git clone https://github.com/SDU-WH-GraphTheory/SDU-WH-GraphTheory.github.io.git
```

## 执行步骤

### 1. 收集信息

向用户确认以下内容（用户已提供的无需再问）：
- **讨论时间**：日期和具体时间
- **参与人**：所有参与讨论的人员姓名
- **讨论内容**：会议转写文本、笔记或要点
- **是否需要修改**：是否有特定的表述要求

### 2. 写文章

按照以下规范创建文章文件：

- **文件路径**：`content/post/YYYY-MM-DD-slug/index.md`
- **目录命名**：`日期-简短英文关键词`（如 `2026-05-16-total-coloring-ai`）
- **Frontmatter 格式**：
  ```yaml
  ---
  title: <中文标题>
  date: YYYY-MM-DD
  authors: [作者1, 作者2, 作者3]
  summary: <一句话摘要，显示在列表页>
  ---
  ```

**正文要求**：
- 开头写一段概述（时间、人物、讨论主题）
- 用 `<!--more-->` 分隔摘要和正文
- 正文以二级标题 `##` 分节，按主题组织
- 保留学术讨论的专业性，去掉口语化表述
- 去掉落款处的 `@某人` 标记，改为自然表述
- 数学公式用 `\(...\)` 和 `\[...\]` 包裹
- 参考现有文章 `content/post/2026-04-08-conditional-probability-martingale/index.md` 的风格

**内容调整原则**：
- 标题精简概括，突出核心决策或结论
- 合并过于零碎的小点，归类到合适的二级标题下
- "待办事项"部分改为"后续计划"自然段落
- 技术名词保持原文（如 LP、Total Coloring、DeepSeek、Claude Code 等）

### 3. 本地预览

```bash
hugo server -D --bind=127.0.0.1 -p 1313
```

用浏览器打开 `http://localhost:1313/post/` 让用户查看效果。

### 4. 确认后推送

用户确认内容无误后，执行：

```bash
git add content/post/YYYY-MM-DD-slug/index.md
git commit -m "Add <文章标题>"
git push origin main
```

**注意**：
- 推送前确认 `.git` 目录存在且 remote 正确指向 `https://github.com/SDU-WH-GraphTheory/SDU-WH-GraphTheory.github.io.git`
- 如果本地没有 git 配置，设置 `git config user.name` 和 `git config user.email`
- 分支名为 `main`，不是 `master`

### 5. 完成后提醒

推送后告知用户：GitHub Actions 会自动构建部署，等待 1-2 分钟后可在 `https://sdu-wh-graphtheory.github.io/post/` 查看上线效果。
