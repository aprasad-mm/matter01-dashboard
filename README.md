# matter01 Dashboard

Live initiative dashboard for matter01 — Factory Launch, hosted on GitHub Pages and auto-refreshed daily from Linear.

---

## One-time setup (5 minutes)

### 1. Create a GitHub repo

1. Go to [github.com/new](https://github.com/new)
2. Name it `matter01-dashboard` (or anything you like)
3. Set it to **Private** (recommended) or Public
4. Click **Create repository**

### 2. Upload these files

Drag and drop all files from this folder into the repo on GitHub.com (or use `git push`). The structure should look like:

```
matter01-dashboard/
├── index.html
├── build_v2.py
├── README.md
└── .github/
    └── workflows/
        └── refresh.yml
```

> **Note:** If you don't see `.github/` folder on your computer, it may be hidden. Make sure to upload it — it contains the automation workflow.

### 3. Add your Linear API key as a GitHub Secret

1. Go to your repo → **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Name: `LINEAR_API_KEY`
4. Value: your Linear API key (starts with `lin_api_...`)
5. Click **Add secret**

The key is encrypted and never appears in logs or the HTML file.

### 4. Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Under **Source**, select **Deploy from a branch**
3. Branch: `main` / Folder: `/ (root)`
4. Click **Save**

GitHub will give you a URL like: `https://yourusername.github.io/matter01-dashboard/`

Share that link with your team. ✓

### 5. Trigger the first refresh

1. Go to your repo → **Actions** tab
2. Click **Refresh Dashboard** in the left sidebar
3. Click **Run workflow** → **Run workflow**

This fetches live data from Linear and updates `index.html`. After ~30 seconds, your dashboard will show today's data.

---

## How it works

| What | How |
|------|-----|
| **Daily refresh** | GitHub Actions runs at 9 AM PT, calls Linear API, regenerates `index.html`, commits it back |
| **API key security** | Key is stored as a GitHub Secret — never in the HTML, never in git history |
| **Hosting** | GitHub Pages serves the static `index.html` |
| **Shareable URL** | `https://yourusername.github.io/matter01-dashboard/` |

---

## Manual refresh

To refresh the data immediately:
1. Repo → **Actions** → **Refresh Dashboard** → **Run workflow**

Or push any change to `main` — the workflow also runs on every push.

---

## Updating milestone data

The Linear API returns milestone completion (0% or 100%) but not partial progress. Detailed progress percentages live in the `PROJECTS` snapshot inside `build_v2.py`. To update them:

1. Edit `build_v2.py` — find the `SNAPSHOT` list and update the `"progress"` values in each project's `"milestones"` array
2. Commit and push → GitHub Actions regenerates the dashboard automatically
