# skyejen / generalist-tech

Generalist tech portfolio: full-stack side projects, tools, and experiments that don't sit neatly in one discipline, most of them built while pairing with AI. Part of [skyejen.github.io](https://skyejen.github.io) and live at **https://skyejen.github.io/**.

## Local development

This site shares a design system with my other repos via the `sj-theme` git submodule.

```bash
git clone https://github.com/skyejen/generalist-tech.git
cd generalist-tech
git submodule update --init            # pull in sj-theme
pip install "mkdocs-material>=9.7,<10" "pymdown-extensions>=10,<11"
mkdocs serve                           # http://127.0.0.1:8004
```

## Structure

- `docs/portfolio/` — full-stack builds and write-ups
- `docs/sj-theme/` — shared theme (git submodule)
- `overrides/` — theme customisations

Deploys automatically to GitHub Pages on push to `main` (see `.github/workflows/deploy.yml`).
