---
layout: post
title: 如何在 Eternity-Sky 博客中贡献文章
date: 2024-11-15 20:44 +0800
last_modified_at: 2024-11-15 20:44:00 +0800
tags: [contribution, guide, pull request]
toc: true
---

# 如何在 Eternity-Sky 博客中贡献文章

欢迎来到 Eternity-Sky 博客！如果你有精彩的文章想要分享，欢迎通过拉取请求（Pull Request）提交到我们的 [GitHub 仓库](https://github.com/Eternity-Sky/Eternity-Sky.github.io.git)。以下是详细的步骤和格式要求。

## 提交步骤

1. **Fork 仓库**：
   - 首先，点击仓库页面右上角的 "Fork" 按钮，将仓库复制到你的 GitHub 账户中。

2. **克隆仓库**：
   - 在你的本地机器上克隆你 Fork 的仓库。
   ```bash
   git clone https://github.com/your-username/Eternity-Sky.github.io.git
   ```

3. **创建新分支**：
   - 为你的文章创建一个新的分支。
   ```bash
   git checkout -b add-your-article
   ```

4. **添加文章**：
   - 在 `_posts` 文件夹中创建一个新的 Markdown 文件，命名格式为 `YYYY-MM-DD-title.md`。
   - 参考以下格式撰写文章： 


5. **提交更改**：
   - 提交你的更改并推送到 GitHub。
   ```bash
   git add _posts/YYYY-MM-DD-title.md
   git commit -m "Add new article: 你的文章标题"
   git push origin add-your-article
   ```

6. **创建拉取请求**：
   - 在 GitHub 上，访问你 Fork 的仓库，点击 "Compare & pull request" 按钮。
   - 填写拉取请求的标题和描述，然后提交。

## 格式要求

- **文件命名**：`YYYY-MM-DD-title.md`
- **Front Matter**：包括 `layout`、`title`、`date`、`last_modified_at`、`tags`、`toc`、`author`
- **内容结构**：使用 Markdown 语法，确保内容清晰易读

## 创作者标识

请在文章中标明你的名字或昵称，以便我们在发布时给予你应有的荣誉。

## 结语

感谢你对我们博客的贡献！期待看到你的精彩文章。如果有任何问题或建议，欢迎在评论区留言或通过邮件联系我们。
