# Chloe’s Tech Notes

A technical blog built with [Chirpy Starter](https://github.com/cotes2020/chirpy-starter), Jekyll, and GitHub Pages.

**Website:** https://chloe-zh97.github.io

## Write a Post

1. Start your first algorithm article in `_drafts/algorithm-first-post.md`. Drafts are not included in the published website.
2. When ready, move it to `_posts/YYYY-MM-DD-your-slug.md` and add the actual publication `date` with the correct timezone offset.
3. Commit to `main`. GitHub Actions builds the site, checks internal links, and deploys it automatically.

For other articles, copy `templates/post.md` into `_posts/`. Use an English filename slug and update the example date before publishing.

## Categories and Tags

Categories form a hierarchy; one or two levels are usually enough. Tags describe specific concepts and can be shared across categories.

| Topic | Example categories | Example tags |
| --- | --- | --- |
| Algorithms | `[Algorithm, Binary Search]` | `[binary-search, invariants]` |
| Agents | `[Agent, Tool Use]` | `[llm, tool-calling]` |
| Distributed systems | `[Distributed Systems, Consensus]` | `[raft, consistency]` |

Category and tag pages are generated from published posts. There is no need to create empty categories in advance. The home page lists all published posts chronologically.

## Local Preview

Use Ruby 3.4 and Bundler:

```sh
bundle install
bundle exec jekyll serve
# Include drafts in the local preview
bundle exec jekyll serve --drafts
# Build for production and check internal links
bash tools/test.sh
```

Open http://127.0.0.1:4000 . Production deployments do not include drafts.

## GitHub Pages

This repository is named `chloe-zh97.github.io`. In **Settings → Pages → Build and deployment → Source**, select **GitHub Actions**.

The deployment workflow is `.github/workflows/pages-deploy.yml`. You can also run **Build and Deploy** manually from the Actions tab.

## Site Configuration

- `_config.yml`: site URL, English interface, author, description, and timezone.
- `_tabs/about.md`: About page.
- `_data/contact.yml`: GitHub and RSS links.
- `_drafts/`: work in progress, excluded from the live website.
- `_posts/`: published articles with dated filenames.
- `templates/`: reusable writing templates, excluded from the website.

Chirpy provides syntax highlighting, a table of contents, search, archives, and light/dark modes. Set `math: true` for equations or `mermaid: true` for diagrams in a post's front matter.

Store post images in `assets/img/posts/<slug>/` and reference them with `![Description](/assets/img/posts/<slug>/image.png)`.

Theme updates are managed through the version range in `Gemfile`. Check the build and rendered pages after an upgrade.

## License

The upstream MIT license is preserved in `LICENSE`.
