# Mostafa Zaman — Academic Website

This repository contains the source for Mostafa Zaman's academic website, built with the [al-folio](https://github.com/alshedivat/al-folio) Jekyll starter and published with GitHub Pages.

Site URL after deployment: <https://naabiil-09.github.io/Personal-Website/>

## Edit the site

The most frequently edited files are:

- `_pages/about.md` — homepage biography and research summary
- `_pages/research.md` — research program and future directions
- `_pages/teaching.md` — teaching philosophy and experience
- `_data/cv.yml` — website CV and automatically generated PDF
- `_bibliography/papers.bib` — publications
- `_projects/` — project cards and detailed project pages
- `_news/` — homepage announcements
- `_data/socials.yml` — email and academic-profile links
- `_config.yml` — name, description, site URL, and global behavior

See [docs/EDITING_MY_SITE.md](docs/EDITING_MY_SITE.md) for step-by-step GitHub Desktop, preview, publishing, and troubleshooting instructions.

## Quick publishing workflow

1. Edit and save files in this repository.
2. Open GitHub Desktop and review the **Changes** tab.
3. Enter a clear summary such as `Update research page`.
4. Select **Commit to main**.
5. Select **Push origin**.
6. On GitHub, open **Actions** and wait for the deployment workflow to finish.

The RenderCV workflow updates the downloadable CV PDF after `_data/cv.yml` changes. The website deployment and CV generation are separate GitHub Actions.

## Local preview

With Docker Desktop running:

```bash
docker compose up
```

Then open <http://localhost:8080/Personal-Website/>. Stop the preview with:

```bash
docker compose down
```

The upstream al-folio documentation remains available in [`docs/`](docs/README.md).
