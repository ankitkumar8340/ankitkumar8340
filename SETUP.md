# Setup Guide — Ankit Kumar's GitHub Profile README

This makes your GitHub profile page (the one that shows at
`github.com/ankitkumar8340`) look like a dashboard, using a special
repo GitHub recognizes automatically.

## 1. Create the special profile repository

1. On GitHub, create a **new repository** named **exactly** your username:
   `ankitkumar8340` (must match your GitHub username, case-sensitive).
2. Make it **Public**.
3. Check "Add a README file" or just push these files into it — GitHub
   auto-detects a repo with your username as the profile repo and shows
   its README on your profile page.

## 2. Add these files

Copy this whole folder's contents into that repo:

```
ankitkumar8340/
├── README.md
├── assets/
│   └── banner.svg
└── .github/
    └── workflows/
        └── snake.yml
```

Push it:
```bash
git init
git add .
git commit -m "Add profile dashboard README"
git branch -M main
git remote add origin https://github.com/ankitkumar8340/ankitkumar8340.git
git push -u origin main
```

## 3. Enable the Contribution Snake workflow

The snake animation (the one that "eats" your commit squares) is generated
by a GitHub Action, not a static file — it needs to run once to create the
image.

1. In your repo, go to the **Actions** tab.
2. If prompted, click **"I understand my workflows, enable them"**.
3. Find **"Generate Snake Animation"** in the left sidebar → click
   **"Run workflow"** → **Run workflow** (green button). This does the
   first manual run; after that it also runs automatically every day and
   on every push to `main`.
4. Wait ~30–60 seconds for it to finish (check the green checkmark).
5. It will create/update an **`output`** branch automatically with the
   generated SVG/GIF files — the README already points at that branch,
   so once this runs once, the snake section will render.

> If the snake doesn't appear right away, hard-refresh your profile page
> (Ctrl+Shift+R) — GitHub caches profile READMEs for a few minutes.

## 4. Everything else is automatic — no extra setup needed

These all pull live data just from your usernames already in the README,
so nothing else to configure:
- GitHub stats, streak, top languages → `github-readme-stats`
- Contribution graph → `github-readme-activity-graph`
- LeetCode stats + heatmap → `leetcard.jacoblin.cool`
- GitHub Trophies → `github-profile-trophy`
- Random dev quote → refreshes each time the README is viewed
- Profile view counter → `komarev.com` badge, increments automatically

## 5. Customizing later

- **Colors**: most badge URLs in `README.md` take `&bg_color=`, `&title_color=`,
  `&text_color=`, `&theme=` query params — swap hex codes to restyle.
- **Banner**: `assets/banner.svg` is plain SVG/SMIL — open it in any text
  editor (or Illustrator/Figma) to tweak text, colors, or the gradient
  animation speed.
- **Featured projects**: the pin cards reference repo names directly in
  the URL (`&repo=SplashBook` etc.) — swap in any repo name you own; the
  card auto-fills stars/forks/description from GitHub.
- **Add WakaTime "This week I spent" panel** (optional, needs a free
  WakaTime account + IDE plugin tracking your coding time):
  1. Sign up at wakatime.com, install their VS Code extension.
  2. Add a secret `WAKATIME_API_KEY` in repo Settings → Secrets → Actions.
  3. Add the `athul/waka-readme` action to `.github/workflows/` — ask me
     and I'll wire this in for you.

## Troubleshooting

| Symptom | Fix |
|---|---|
| README not showing on profile | Repo name must exactly match your username, and be Public |
| Snake section blank | Run the workflow manually once (Step 3); check Actions tab for errors |
| Stats cards show "Error" | github-readme-stats free instance sometimes rate-limits — wait a few minutes, or self-host it (ask me) |
| Banner not rendering | Make sure `assets/banner.svg` was pushed and the path in README.md matches |
