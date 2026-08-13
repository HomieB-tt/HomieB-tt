# HomieB-tt GitHub Profile Setup Guide

This folder contains a ready-to-use GitHub profile README setup for:
- username: `HomieB-tt`
- name: `Jeremiah Carlton`
- visual style: hacker / futuristic / cyberpunk
- colors: teal, cyan, violet, pink accents on dark slate `#02040A`
- portfolio site: `https://homieb-tt.github.io/homieb-tt-portfolio/`

## What This Bundle Contains

- `README.md` — your profile README
- `assets/profile-hero.svg` — custom futuristic cyberpunk hero banner
- `assets/profile-footer.svg` — matching cyberpunk footer banner
- `.github/workflows/snake.yml` — GitHub Action that generates the animated contribution snake

## Step 1: Verify Repo Name

GitHub profile READMEs only render on your GitHub landing page when the repository name matches your username exactly:
- repo name: `HomieB-tt`
- visibility: public
- full URL: `https://github.com/HomieB-tt/HomieB-tt`

## Step 2: Directory Structure

```text
HomieB-tt/
├── README.md
├── SETUP.md
├── assets/
│   ├── profile-hero.svg
│   └── profile-footer.svg
└── .github/
    └── workflows/
        └── snake.yml
```

## Step 3: Git Commit & Push

To commit and push these updates to GitHub:

```bash
cd /home/buddy/Projects/HomieB-tt
git add .
git commit -m "style: overhaul cyberpunk profile README & hero assets"
git push origin main
```

## Step 4: Enable the Contribution Snake Animation

After pushing:
1. Open `https://github.com/HomieB-tt/HomieB-tt` on GitHub.
2. Go to the **Actions** tab.
3. Select the **Generate Snake** workflow.
4. Click **Run workflow** manually once.

This workflow will:
- Generate `github-contribution-grid-snake-dark.svg`
- Push it to the `output` branch automatically
- Activate the snake animation render in your profile README

## Step 5: Live Uplinks & Social Links

Configured live links:
- **Portfolio**: `https://homieb-tt.github.io/homieb-tt-portfolio/`
- **LinkedIn**: `https://www.linkedin.com/in/jeremiah-carlton-21b4962a7/`
- **X (Twitter)**: `https://x.com/Jerry_Lander17`
- **Email**: `montanajeremy160@outlook.com`
- **GitHub**: `https://github.com/HomieB-tt`

## Step 6: Featured Projects

Pinned repositories featured in the README:
- `hostelhop_mobile` — Flutter & Supabase mobile app
- `Chatter` — Swift mobile app
- `Whust` — Rust project
- `hostelhop_admin` — React + TypeScript & Vite admin dashboard

To swap a featured repo, update the `repo=` parameter in the project card URL inside `README.md`.
