# pypistats CLI

A terminal tool for checking Python package download stats and health scores from [pypistats.com](https://pypistats.com).

## Installation

```bash
pip install pypistats-cli
```

Requires Python 3.9+.

## Setup

An API key is required. Free tier keys work.

1. Sign up at [pypistats.com](https://pypistats.com)
2. Go to your Dashboard and generate an API key
3. Export it in your shell:

```bash
export PYPISTATS_API_KEY=pyps_your_key_here
```

Add that line to your `~/.bashrc`, `~/.zshrc`, or equivalent to make it permanent.

## Usage

### `pypistats check <package>`

Show download stats, health score, and version breakdown for a package.

```bash
pypistats check requests
pypistats check fastapi --days 7
pypistats check django --days 90
```

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| `--days N` | `30` | Number of days of download history to analyze |

**Output includes:**

- Download sparkline and total for the period
- Trend — week-over-week growth or decline
- Health score (0–100) with color-coded bar
- License and author
- Top versions by download share
- AI summary (Pro/Enterprise accounts)

**Example output:**

```
╭─────────────────── requests v2.32.3 ───────────────────╮
│                                                         │
│  Downloads (30d):  ▃▄▅▄▅▆▅▆▇█  847.2M                 │
│  Trend:            +8.3% ↑                              │
│  Health:           ██████████ 94/100                    │
│  License:          Apache 2.0                           │
│  Author:           Kenneth Reitz                        │
│                                                         │
│  Top Versions                                           │
│  2.32.3      ████████████████     78.4%                 │
│  2.31.0      ████                 19.2%                 │
│  2.28.2      █                     2.4%                 │
│                                                         │
╰─────────────────────────────────────────────────────────╯
```

### `pypistats --version`

Print the installed version.

```bash
pypistats --version
```

### `pypistats --help`

```bash
pypistats --help
pypistats check --help
```

## Health score

Scores are calculated from:

- Download trend (growing vs declining)
- Release cadence (how frequently the package is updated)
- GitHub activity (issues, commits, stars)
- Security advisories from [deps.dev](https://deps.dev)

| Score | Risk |
|-------|------|
| 70–100 | LOW — healthy package |
| 40–69 | MEDIUM — worth reviewing |
| 0–39 | HIGH — consider alternatives |

## Environment variables

| Variable | Description |
|----------|-------------|
| `PYPISTATS_API_KEY` | **Required.** Your API key from the Dashboard |
| `PYPISTATS_BASE_URL` | Override the API base URL (default: `https://pypistats.com`) |

## Links

- [PyPI](https://pypi.org/project/pypistats-cli/)
- [pypistats.com](https://pypistats.com)
- [Issues](https://github.com/diverdale/pypistats/issues)

---

*[← Back to Getting Started](getting-started.md)*
