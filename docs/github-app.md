# GitHub App

The PyPI Stats GitHub App automatically scans dependency files on every pull request and posts a health check comment and check run.

## Installation (one-time)

**Requirements:** Pro or Enterprise subscription, owner or admin access to the GitHub account or org.

1. Go to your **pypistats.com Dashboard**.
2. Find the **GitHub App** panel.
3. Click **Install GitHub App**.
4. On GitHub's installation page, choose **All repositories** or select specific repos.
5. Authorize and complete the installation.
6. Return to the Dashboard — the panel will show the connected account.

## Configuration

Three settings are available in the GitHub App panel on your Dashboard.

### Block merges on high-risk dependencies

**Default: off**

- **Off** — the check run always passes. Comments are posted but PRs are never blocked. Use this to start informational-only.
- **On** — if any dependency has a health score below 40 or an active security advisory, the check run posts a `failure` conclusion. If your branch protection rules require this check, the PR cannot be merged until the issue is resolved.

> Recommendation: start with this **off** to build familiarity. Enable it once your team has resolved existing HIGH-risk dependencies.

### Only comment when issues are found

**Default: off**

- **Off** — the bot comments on every PR that touches a dependency file, even if everything is healthy.
- **On** — the bot stays silent on healthy PRs. A comment only appears when at least one WARNING or CRITICAL finding is present.

> Recommendation: turn this **on** to reduce noise in active repos.

### Ignore list

A comma-separated list of packages to exclude from health checks. Useful for internal packages, packages you've accepted the risk on, or transitive deps you can't control.

Example: `ruamel.yaml, boto3, internal-utils`

Click **Save** after editing. The button turns green to confirm.

## How it works

The scan fires when a PR is **opened**, **synchronized** (new commits pushed), or **reopened**, and the PR diff includes any of:

- `requirements.txt` / `requirements-dev.txt`
- `requirements/base.txt` / `requirements/prod.txt`
- `setup.py`
- `pyproject.toml`

If none of these files changed, the bot takes no action.

## Understanding the PR comment

```
📦 PyPI Stats — Dependency Health Check

2 high-risk dependencies found — ✅ 14 healthy · ⚠️ 1 warning · 🚨 2 critical
```

The comment includes:

**Packages needing attention** — MEDIUM and HIGH risk packages, sorted with HIGH first:

| Package | Health Score | Risk | Advisories |
|---------|-------------|------|------------|
| `paramiko` | 41/100 | 🚨 HIGH | ⚠️ 9 |
| `requests` | 55/100 | ⚠️ MEDIUM | — |

Package names link to their pypistats.com page. Healthy packages and ignored packages are shown collapsed.

## Understanding the check run

| Scenario | Check result |
|----------|-------------|
| Block merges **off** | Always `success` |
| Block merges **on**, no HIGH risk | `success` |
| Block merges **on**, MEDIUM risk only | `neutral` (informational) |
| Block merges **on**, HIGH risk present | `failure` (blocks merge if required) |

## Responding to findings

**HIGH risk (🚨)** — health score below 40 or active security advisory:

1. **Upgrade** — `pip install package --upgrade` and check if the advisory is resolved
2. **Replace** — find an alternative with a higher health score
3. **Pin and accept** — add to the ignore list in Dashboard settings and document why
4. **Override** — if you need to merge anyway, temporarily disable block merges, merge, then re-enable

**MEDIUM risk (⚠️)** — health score 40–69, no advisories. Not a blocker. Worth reviewing the package page to understand the score; usually safe to merge.

**Unknown packages** — not yet in the database. The bot automatically requests them for processing. They should appear with scores within a few hours. Push a new commit to the PR to trigger a re-scan.

## Re-triggering a scan

Push any commit to the branch. The bot updates the existing comment in place and refreshes the check run.

---

*[← Stack Analyzer](stack-analyzer.md) · [Back to Getting Started](getting-started.md)*
