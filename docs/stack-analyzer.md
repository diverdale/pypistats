# Stack Analyzer

The Stack Analyzer runs a deep health analysis of your full Python dependency tree — both direct and transitive dependencies.

## When to use it

- Before your first commit on a new project
- When adding a significant new dependency
- When reviewing an inherited codebase
- Periodically to catch packages that have gone stale

## Running an analysis

**Requirements:** Pro or Enterprise subscription.

1. Go to **pypistats.com** and sign in.
2. Navigate to **Stacks** in the sidebar.
3. Click **New Stack**.
4. Give your stack a name (e.g. `my-api-service`).
5. Provide your dependency file:
   - **Upload** — drag and drop `requirements.txt`, `pyproject.toml`, etc.
   - **GitHub URL** — paste any GitHub blob URL (e.g. `https://github.com/you/repo/blob/main/requirements.txt`); it is automatically converted to a raw URL.
6. Click **Analyze Stack**.

Resolution runs in the background. A progress bar tracks resolved packages. Typical stacks (20–50 packages) resolve in under a minute.

## Understanding the results

### Packages tab

Every direct and transitive dependency with:

| Column | Description |
|--------|-------------|
| Health score | 0–100 composite score: download trends, release cadence, GitHub activity, open issues |
| Risk level | LOW / MEDIUM / HIGH |
| Advisory count | Known security advisories from deps.dev |
| Trend | Week-over-week download change |

Sort by risk level to triage. Any package marked HIGH needs a decision: find an alternative, pin a safe version, or add it to the ignore list.

### Graph tab

Visual dependency graph of the full tree. Useful for tracing which direct dependency is pulling in a high-risk transitive package.

### AI Report tab

AI-generated narrative summarizing stack health, flagging concerns, and suggesting alternatives. Regeneratable once per 24 hours.

### Alerts tab

Checks for:

- **STALE** — package has not had a release in a long time
- **VERSION DRIFT** — your pinned version is significantly behind the latest release

Click **Check for Alerts** to run a fresh check.

## What to do with findings

| Finding | Action |
|---------|--------|
| HIGH risk, has advisories | Replace or upgrade to a patched version |
| HIGH risk, low health score | Evaluate alternatives; if unavoidable, add to ignore list |
| MEDIUM risk | Note it; pin a specific version and monitor |
| STALE | Check if abandoned; consider a maintained fork |
| VERSION DRIFT | Update pinned version; run tests |

## Ongoing monitoring

### Stack Digest email

Enable **Stack Digest** in your Dashboard to receive a weekly email summary of alerts across all stacks. Sent every Monday at 9:00 AM UTC.

### Package alerts

For individual packages, set up alerts on your Dashboard:

- **Download spike** — unusual volume increase (can indicate supply chain attacks or viral adoption)
- **Download drop** — significant decrease (can indicate a project losing adoption)
- **New version** — notify when a new release is published

---

*[← Back to Getting Started](getting-started.md) · [GitHub App →](github-app.md)*
