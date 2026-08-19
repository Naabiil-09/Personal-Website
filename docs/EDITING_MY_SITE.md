# Editing Mostafa Zaman's Academic Website

This guide covers the routine workflow for updating, previewing, and publishing the site. You do not need to edit layouts, theme gems, or generated `_site` files.

## 1. The normal GitHub Desktop workflow

1. Open **GitHub Desktop**.
2. Confirm the current repository is **Naabiil-09/Personal-Website** and the branch is **main**.
3. Select **Fetch origin** before starting. If GitHub has newer changes, select **Pull origin**.
4. Edit the relevant file in VS Code or another text editor.
5. Return to GitHub Desktop and review every changed file.
6. Write a short commit summary, for example `Add new publication` or `Update biography`.
7. Select **Commit to main**, then **Push origin**.
8. Open the repository on GitHub and check the **Actions** tab.

Changes become public only after they are committed and pushed.

## 2. What to edit

| Goal | File or folder |
| --- | --- |
| Change homepage biography | `_pages/about.md` |
| Change research narrative | `_pages/research.md` |
| Change teaching narrative | `_pages/teaching.md` |
| Add or update a CV item | `_data/cv.yml` |
| Add a publication | `_bibliography/papers.bib` |
| Add a project | `_projects/` |
| Add a short announcement | `_news/` |
| Change email/profile links | `_data/socials.yml` |
| Change name, description, or site URL | `_config.yml` |
| Replace homepage photograph | `assets/img/mostafa-zaman.jpg` |
| Replace the downloadable CV | `assets/pdf/Academic_Mostafa_Zaman_CV.pdf` |

Avoid editing `_site/`; it is generated and overwritten.

## 3. Markdown basics

Most pages use Markdown:

```markdown
## Section title

This is a paragraph with **bold text** and a [link](https://example.com/).

- First item
- Second item
```

Keep the YAML block between the first two `---` markers at the top of a page. That block controls the title, navigation, description, and layout.

## 4. Add a publication

Add a BibTeX record to `_bibliography/papers.bib`:

```bibtex
@article{zaman2026example,
  title       = {Paper Title},
  author      = {Zaman, Mostafa and Collaborator, Name},
  journal     = {Journal Name},
  year        = {2026},
  doi         = {10.xxxx/example},
  html        = {https://doi.org/10.xxxx/example},
  bibtex_show = {true},
  selected    = {true}
}
```

Use a unique citation key such as `zaman2026example`. Set `selected = {true}` only when the paper should also appear on the homepage.

## 5. Add a project

Copy one of the files in `_projects/`, rename it with lowercase words and hyphens, and update its front matter:

```yaml
---
layout: page
title: Project name
description: One-sentence card description.
img: assets/img/project-image.png
importance: 4
category: research
---
```

Write the longer project description below the closing `---`. Lower `importance` numbers appear first.

## 6. Update the CV

The CV has two parts:

- `_data/cv.yml` controls the readable CV page on the website.
- `assets/pdf/Academic_Mostafa_Zaman_CV.pdf` is your original downloadable PDF.

To replace the PDF, copy the new CV into `assets/pdf/` using the exact filename `Academic_Mostafa_Zaman_CV.pdf`. GitHub Desktop will detect the replacement; commit and push it normally.

Edit `_data/cv.yml`. RenderCV is strict about indentation:

- Use spaces, not tabs.
- Keep indentation consistent.
- Put each list item after `-`.
- Keep one entry type per section. For example, all education items use `institution`, `area`, and `degree`.

When this file is pushed, `.github/workflows/render-cv.yml` validates the website CV data and also generates a formatted backup PDF. The website's download button continues to use your original PDF in `assets/pdf/`.

If RenderCV reports validation errors, expand the failed **RenderCV** step in GitHub Actions. The table shows the field location and rejected value. Fix that field in `_data/cv.yml`, commit, and push again.

## 7. Replace the photograph

Use a landscape or portrait JPG with reasonable dimensions, ideally under 2 MB. Either:

- Replace `assets/img/mostafa-zaman.jpg` with a new file using the same name; or
- Add a differently named file and change `profile.image` in `_pages/about.md`.

The current photograph is the official VCU Outstanding Graduate Research Award image and can be replaced later with a formal headshot.

## 8. Preview locally

### Docker Desktop method

From a terminal opened in the repository:

```bash
docker compose up
```

Open <http://localhost:8080/Personal-Website/>. When finished:

```bash
docker compose down
```

### Ruby/Jekyll method

If Ruby and Bundler are installed:

```bash
bundle install
bundle exec jekyll serve
```

Open <http://localhost:4000/Personal-Website/>. Stop the server with `Ctrl+C`.

## 9. GitHub Pages settings

The repository is named `Personal-Website`, so `_config.yml` uses:

```yaml
url: https://naabiil-09.github.io
baseurl: /Personal-Website
```

On GitHub, open **Settings → Pages**. Under **Build and deployment**, select **Deploy from a branch**, choose the `gh-pages` branch and `/(root)` folder, then save. The `Deploy site` workflow rebuilds that branch after every content update.

If you rename the repository to `Naabiil-09.github.io`, change `baseurl` to an empty value and the public URL becomes `https://naabiil-09.github.io/`.

## 10. Before pushing

Run the lightweight checks when possible:

```bash
npm ci
npm run lint:prettier
npm run lint:style-contract
bundle exec jekyll build
```

After pushing, check both workflows:

- **Deploy** — builds and publishes the website.
- **Render a CV** — validates the CV and updates its PDF.

One can succeed even if the other fails, so open the specific failed workflow for its logs.
