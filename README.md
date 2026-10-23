# Chloe’s Tech Notes

基于 [Chirpy Starter](https://github.com/cotes2020/chirpy-starter) 的综合技术博客。

站点地址（部署成功后）：https://chloe-zh97.github.io

## 写文章

1. 在 `_drafts/algorithm-first-post.md` 写第一篇算法文章；草稿默认不会发布。
2. 完成后移到 `_posts/YYYY-MM-DD-your-slug.md`，添加实际发布日期 `date`，包含正确时区偏移。
3. 提交到 `main`，GitHub Actions 自动构建、检查内部链接并部署。

也可以复制 `templates/post.md` 到 `_posts/` 开始新文章。文件名建议使用英文 slug。

## 分类约定

`categories` 是层级，最多建议两层；`tags` 是可跨方向复用的知识点。

| 方向 | categories 示例 | tags 示例 |
| --- | --- | --- |
| 算法 | `[Algorithm, Binary Search]` | `[binary-search, invariants]` |
| Agent | `[Agent, Tool Use]` | `[llm, tool-calling]` |
| 分布式系统 | `[Distributed Systems, Consensus]` | `[raft, consistency]` |

分类与标签页由已发布文章自动生成，无需提前创建空分类。首页按时间展示全部文章。

## 本地预览

需要 Ruby 3.4 和 Bundler：

```sh
bundle install
bundle exec jekyll serve
# 包含草稿
bundle exec jekyll serve --drafts
# 生产构建与内部链接检查
bash tools/test.sh
```

打开 http://127.0.0.1:4000 。生产部署不包含草稿。

## GitHub Pages

仓库必须命名为 `chloe-zh97.github.io`。在 Settings → Pages → Build and deployment → Source 选择 **GitHub Actions**。
部署配置位于 `.github/workflows/pages-deploy.yml`。首次启用 Pages 后可从 Actions 手动运行 Build and Deploy。

`_config.yml` 已配置站点 URL、中文界面、作者和时区。`_tabs/about.md` 是关于页；`_data/contact.yml` 配置 GitHub 与 RSS。

代码高亮、目录、搜索、归档、亮暗主题由 Chirpy 提供。公式使用 `math: true`，流程图使用 `mermaid: true`。
图片可放在 `assets/img/posts/<slug>/`，正文用 `![说明](/assets/img/posts/<slug>/image.png)` 引用。

主题升级通过 Gemfile 的版本范围管理；升级后应检查构建与页面。

## License

保留上游 MIT 许可证，见 LICENSE。
