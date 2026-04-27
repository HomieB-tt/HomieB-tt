# HomieB-tt GitHub Profile Setup Guide

This folder contains a ready-to-use GitHub profile README setup for:
- username: `HomieB-tt`
- name: `Jeremiah Carlton`
- visual style: hacker / futuristic / cyberpunk
- colors: teal, sky blue, violet, pink accents on black

## What This Bundle Contains

- `README.md` — your profile README
- `assets/profile-hero.svg` — custom futuristic cyberpunk banner
- `assets/profile-footer.svg` — matching cyberpunk footer banner
- `.github/workflows/snake.yml` — GitHub Action that generates the animated contribution snake

## Step 1: Create the special GitHub profile repository

GitHub profile READMEs only work when the repository name matches your username exactly.

Create this repository on GitHub:
- repo name: `HomieB-tt`
- visibility: public

The full repo should be:
- `https://github.com/HomieB-tt/HomieB-tt`

## Step 2: Copy these files into that repo

Expected structure:

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

## Step 3: Push the repo

Example commands:

```bash
git init
git branch -M main
git add .
git commit -m "feat: add animated GitHub profile README"
git remote add origin git@github.com:HomieB-tt/HomieB-tt.git
git push -u origin main
```

If you use HTTPS instead of SSH:

```bash
git remote add origin https://github.com/HomieB-tt/HomieB-tt.git
```

## Step 4: Enable the snake animation

After pushing:
- open the repo on GitHub
- go to the `Actions` tab
- allow workflows if GitHub asks
- run the `Generate Snake` workflow manually once

That workflow will:
- generate the contribution snake SVG files
- push them to an `output` branch
- make the image URL in your README work

## Step 5: Featured projects

I preselected these based on your public repositories and tech spread:
- `HostelHop` — Flutter / Dart
- `Chatter` — Swift
- `Whust` — Rust
- `BlueChat` — Flutter / Dart

Why these four:
- they reflect your mobile focus
- they show language range
- they look coherent together on a profile page

To change a featured project, edit the `repo=` value in a project card URL.

Example:

```md
https://github-readme-stats.vercel.app/api/pin/?username=HomieB-tt&repo=HostelHop
```

Swap `HostelHop` with any other repo name, like:
- `drop-nwsc-app`
- `LandSecureProject`
- `alffy-site`

## Step 6: Skills section guidance

Right now your skills section emphasizes what is already visible from your repos and what you told me directly.

Primary:
- Flutter
- Dart
- Swift
- iOS
- Android

Secondary:
- Python
- Rust
- Ruby

Foundational identity:
- Networking
- Cybersecurity

That is a strong profile because it tells a clear story:
- mobile-first engineer
- systems-aware
- cross-language learner
- hacker/futuristic aesthetic

Good additions later if true:
- Firebase
- Django
- REST APIs
- UI/UX
- Git
- Linux
- Reverse engineering
- App security

## Step 7: Contact and social badges

The README now includes a `CONTACT UPLINKS` section.

Right now:
- GitHub is live
- LinkedIn is a placeholder
- X is a placeholder
- email is a placeholder
- portfolio is a placeholder

Replace these URLs and badge labels in `README.md`:

### LinkedIn
Replace:
```text
https://www.linkedin.com/in/ADD-YOUR-LINKEDIN
```
with your real LinkedIn profile URL.

### X / Twitter
Replace:
```text
https://x.com/ADD-YOUR-HANDLE
```
with your real handle URL.

### Email
Replace:
```text
mailto:your-email@example.com
```
with your real email address.

### Portfolio
Replace:
```text
https://your-portfolio.example.com
```
with your real site URL.

If you do not want one of them, simply remove that badge line.

## Suggested professional title

Best default title for you right now:

`Mobile Engineer | Flutter • iOS • Android`

Alternatives:
- `Flutter & Mobile Engineer`
- `Mobile App Developer | Flutter • Swift`
- `Mobile Engineer with Networking & Cybersecurity Roots`

## Important GitHub README limitation

Your profile README does not run JavaScript directly.

The “animation” comes from:
- generated SVGs
- external dynamic stat cards
- the snake workflow
- image-based typing animations

So this setup is the GitHub-safe way to get that futuristic animated look.

## If something does not render

Check these first:
- the repo name is exactly `HomieB-tt`
- the repo is public
- Actions are enabled
- the `Generate Snake` workflow has run successfully
- the `output` branch exists

## Nice optional next upgrades

If you want, the next version can include:
- a custom dark SVG footer
- real social/contact links after you send them
- a pinned `currently building` section
- a project matrix grouped by language
- a cleaner minimalist variant for a future mood swing
