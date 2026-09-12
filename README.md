# SiNZeRo.github.io

Markdown-first GitHub Pages site.

## Add an article

Copy `_drafts/article-template.md` to the appropriate topic directory, rename it, edit front matter, and commit.

Example:

```text
ai-slops/
  harness/
    codex/
      my-note.md
```

Use `article_parent` to make the article appear in that section's list. Use `permalink` for a clean URL.

## Taxonomy

Sections are ordinary `index.md` files with `layout: section` and a `parent` URL. This supports deeper nesting without changing the layouts.

## Legacy

- `archive/legacy-2026-09-12` is a full snapshot of the previous site.
- `/legacy/` keeps the previous homepage available on the live site.
- Existing `/blog/...` pages and old assets remain in place.
