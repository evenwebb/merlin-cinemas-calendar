> **Superseded** — This project has been replaced by **[merlin-cinemas](https://github.com/evenwebb/merlin-cinemas)**. Kept for reference only.

<div align="center">

# 🎟️ Merlin Cinemas Calendar Scraper

Scrapes upcoming film releases from Merlin Cinemas across Cornwall locations and publishes per-cinema iCalendar feeds plus a GitHub Pages index for easy subscription.

**Links:** [Repository](https://github.com/steven/merlin-cinemas-calendar)

</div>

---

## 📚 Table of Contents

- [⚡ Quick Start](#-quick-start)
- [✨ Features](#-features)
- [📦 Installation](#-installation)
- [🚀 Usage](#-usage)
- [⚙️ Configuration](#️-configuration)
- [🤖 GitHub Actions Automation](#-github-actions-automation)
- [🌐 GitHub Pages Setup](#-github-pages-setup)
- [🧩 Dependencies](#-dependencies)
- [🛠️ Troubleshooting](#️-troubleshooting)
- [⚠️ Known Limitations](#️-known-limitations)
- [📄 License](#-license)

---

## ⚡ Quick Start

```bash
git clone https://github.com/evenwebb/wtw-cinemas-calendar.git
cd wtw-cinemas-calendar
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 cinema_scraper.py
```

✅ Generated output:

- `docs/merlin-<cinema>.ics` (one per enabled cinema)
- `docs/index.html`
- cache/history files (`.film_cache.json`, `.tmdb_cache.json`, `.release_history.json`)

---

## ✨ Features

| Feature | Description |
|---|---|
| `🎭 Multi-Cinema Support` | Scrapes any enabled Merlin Cornwall cinema (Bodmin, Helston, Falmouth, Redruth, St Ives, Penzance, The Ritz). |
| `📝 Rich Event Details` | Adds runtime, synopsis, cast, and booking URLs where available. |
| `💾 Smart Caching` | Uses local film/TMDb caches to reduce unnecessary repeat scraping and API usage. |
| `🔔 Configurable Notifications` | Optional calendar reminders (day-before, same-day, weekly, or custom time). |
| `📅 Per-Cinema iCal Feeds` | Generates separate `.ics` files for each cinema with stable deduplicated events. |
| `🧰 Robust Parsing` | Handles Merlin page structures and multiple date formats with retry/backoff requests. |
| `🌐 GitHub Pages Output` | Builds `docs/index.html` with subscribe links and publishes via Pages. |
| `🤖 Automated Workflow` | Daily GitHub Actions run with retries, conditional commits, and optional failure issue creation. |

---

## 📦 Installation

```bash
git clone https://github.com/evenwebb/wtw-cinemas-calendar.git
cd wtw-cinemas-calendar
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

---

## 🚀 Usage

```bash
python3 cinema_scraper.py
```

The script fetches releases for enabled cinemas and updates `docs/` output for local use or GitHub Pages.

---

## ⚙️ Configuration

Primary settings are in `cinema_scraper.py`.

| Option | Default | Description |
|---|---|---|
| `CINEMAS` | all 4 enabled | Cinema locations to scrape (enable/disable individually). |
| `NOTIFICATION_TIME` | `09:00` | Default reminder time for notifications. |
| `NOTIFICATIONS` | disabled | Optional VALARM rules in calendar events. |
| `CACHE_FILE` | `.film_cache.json` | Film details cache file. |
| `CACHE_EXPIRY_DAYS` | `7` | Film cache retention in days. |
| `TMDB_CACHE_FILE` | `.tmdb_cache.json` | TMDb enrichment cache file. |
| `TMDB_CACHE_DAYS` | `30` | TMDb cache retention in days. |
| `CALENDAR_TIMEZONE` (env) | `Europe/London` | Timezone for generated calendar events. |
| `TMDB_API_KEY` (env/secret) | unset | Enables TMDb enrichment when set. |

---

## 🤖 GitHub Actions Automation

This repo includes `.github/workflows/scrape_cinema.yml`:

- `⏰` Runs daily at `09:00 UTC`
- `🖱️` Supports manual runs (`workflow_dispatch`)
- `🔁` Retries scraper runs before failing (`SCRAPER_RUN_ATTEMPTS`, default `2`)
- `📝` Commits only changed output/cache/history files
- `🚨` Optionally opens or updates a GitHub issue on failure (`CREATE_FAILURE_ISSUE=true`)

Recommended repository secrets:

- `TMDB_API_KEY` (optional)
- `SCRAPER_RUN_ATTEMPTS` (integer)
- `CREATE_FAILURE_ISSUE` (`true`/`false`)

---

## 🌐 GitHub Pages Setup

1. Open **Settings -> Pages** in GitHub.
2. Choose **Deploy from a branch**.
3. Select branch `main` and folder `/docs`.
4. Save.

Published index page:

- [https://evenwebb.github.io/wtw-cinemas-calendar/](https://evenwebb.github.io/wtw-cinemas-calendar/)

---

## 🧩 Dependencies

| Package | Purpose |
|---|---|
| `requests` | HTTP requests for listings/details/TMDb |
| `beautifulsoup4` | HTML parsing for listing and detail extraction |

---

## 🛠️ Troubleshooting

- `🧱` If no films appear, verify Merlin page structure hasn’t changed.
- `🔑` If TMDb metadata is missing, check `TMDB_API_KEY` and quota status.
- `📜` Review `cinema_log.txt` for parsing/runtime errors.
- `🔁` Increase `SCRAPER_RUN_ATTEMPTS` if failures are intermittent.

---

## ⚠️ Known Limitations

- `🌐` Scraping depends on current Merlin site markup and wording.
- `🎯` TMDb matching is best-effort and may occasionally choose imperfect results.

---

## 📄 License

This project is provided as-is for personal use. Please respect the source website terms of service.
