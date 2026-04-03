# Getting Started with PyPI Stats

[pypistats.com](https://pypistats.com) provides Python package download analytics and dependency health monitoring.

## What it does

- **Package analytics** — download trends, version breakdowns, country/system stats for any PyPI package
- **Stack Analyzer** — deep health analysis of your full dependency tree
- **GitHub App** — automatic dependency health checks on every PR
- **Alerts** — spike/drop/new-version notifications for packages you follow

## The recommended workflow

```
New project → Analyze stack → Install GitHub App → Open PRs (auto-scanned) → Monitor ongoing
```

## Docs

| Guide | Description |
|-------|-------------|
| [Stack Analyzer](stack-analyzer.md) | Analyze your dependency tree before and after changes |
| [GitHub App](github-app.md) | Automatic health checks on every pull request |

## Quick Reference

| Action | Where |
|--------|-------|
| Analyze a stack | pypistats.com → Stacks → New Stack |
| Install GitHub App | Dashboard → GitHub App panel → Install |
| Configure block/comment settings | Dashboard → GitHub App panel |
| Add packages to ignore list | Dashboard → GitHub App panel → Ignore list |
| View PR health check | GitHub → PR → Checks tab or PR comment |
| Check stack alerts | Stacks → select stack → Alerts tab |
| Enable weekly digest | Dashboard → Stack Digest toggle |
| Look up a package | pypistats.com/packages/[name] |

## Supported dependency file formats

| File | Notes |
|------|-------|
| `requirements.txt` | Strips version specifiers and extras |
| `requirements-dev.txt` | Same as requirements.txt |
| `requirements/base.txt` | Same as requirements.txt |
| `requirements/prod.txt` | Same as requirements.txt |
| `setup.py` | Extracts `install_requires` |
| `pyproject.toml` | PEP 621 `[project] dependencies` and Poetry `[tool.poetry.dependencies]` |

`-r other_file.txt` includes and `# comments` are ignored. Version specifiers are stripped — only the package name is used.

---

*[pypistats.com](https://pypistats.com) · [Report an issue](../../issues/new)*
