# Technical Details

This file explains, in plain terms, how this repository is put together and how it turns into the published book. It's meant as an onboarding note for anyone (including future-you) who needs to understand the moving parts without re-deriving them from scratch.

## 1. What kind of project this is

This is a [Quarto](https://quarto.org/) **book project**. Quarto takes a collection of `.qmd` files (plain text + R code chunks, like R Markdown) and renders them into a full book — an HTML website and a PDF — following the recipe in `_quarto.yml`.

It is a behavioural-science adaptation of Rafael Irizarry's *Introduction to Data Science: Data Wrangling and Visualization with R*. See `CLAUDE.md` for the adaptation rule and `CHANGELOG.md` for the running list of what was changed from the original.

## 2. How the content is organised

Each **top-level folder is a "part" of the book** (a group of chapters), matching the `book: chapters:` list in `_quarto.yml`:

| Folder | Part |
|---|---|
| `R/` | Getting started with R |
| `dataviz/` | Data visualization |
| `wrangling/` | Data wrangling |
| `productivity/` | Productivity tools |

Inside each folder:
- One **unnumbered intro file**, e.g. `productivity/intro-productivity.qmd` — a short motivating paragraph for the part, no sections.
- One **numbered chapter file per topic**, e.g. `dataviz/distributions.qmd` — these become the actual chapters, in the order listed under `chapters:` in `_quarto.yml`.

`index.qmd` (the preface) and `intro.qmd` sit at the repo root, outside any part, since they open the book before Part 1 begins.

Adding a new chapter means: create the folder/files following that pattern, register them in `_quarto.yml`, and log the addition in `CHANGELOG.md` — this is spelled out in `CLAUDE.md`.

## 3. How a `.qmd` file becomes a page in the book

Each chapter file mixes narrative text with R code chunks (tables, plots, computed numbers referenced inline). When Quarto renders a chapter it actually **runs that R code**, which means:
- it needs a working R environment (see `renv.lock` / `renv/` — the project's pinned package versions),
- it can be slow (some chapters download data or fit models), and
- if any external resource the code depends on changes or disappears, the rendered numbers could change or the render could break — even though nothing in the `.qmd` file itself changed.

## 4. The output: `docs/`

`_quarto.yml` sets `output-dir: docs`. Rendering the whole book writes the finished HTML site into `docs/`. This repository **publishes straight from that folder** — there's no separate CI build step — so `docs/` is committed to git, and GitHub Pages simply serves whatever is currently sitting there.

**Practical implication:** if you edit a chapter and don't re-render + commit `docs/`, the published site goes out of sync with the source. `docs/` needs to travel together with the content change that produced it.

## 5. The cache: `_freeze/` — and why it's committed

`_quarto.yml` also sets:
```yaml
execute:
  cache: true
  freeze: auto
```

`freeze: auto` tells Quarto: *before re-running a chapter's R code, check whether a cached result already matches this exact source file; if so, reuse it instead of executing the code again.* Those cached results (computed values, tables, and rendered figures) live in `_freeze/<chapter>/`.

This repo has deliberately committed `_freeze/` since early on (see `git log -- _freeze`), for two reasons:

1. **Reproducibility.** Several chapters download external data or scrape the web (e.g. `wrangling/text-analysis.qmd`, `wrangling/web-scraping.qmd`). If a data source changes or goes offline later, a fresh render from scratch could silently produce different numbers, or fail outright. A committed freeze cache means the book you get is the one that was actually verified, regardless of what happens to those external sources afterwards.
2. **Speed and consistency for anyone else rendering the book.** Without a shared cache, a full render re-executes *every* chapter's R code every time. With it, only chapters whose `.qmd` actually changed get re-executed — and everyone (you, a collaborator, a future you on a different machine) gets identical output rather than whatever a fresh run happens to produce.

**Practical implication, same as for `docs/`:** when a chapter's content changes, re-render it and commit the updated `_freeze/` entry alongside the source change — otherwise the cache is just stale (harmless, Quarto will simply recompute it locally) but nobody else benefits from it being shared.

The trade-off is repo size — `_freeze/` and `docs/` add up over time (currently ~18MB and ~52MB respectively) because they include every rendered plot image. That's considered an acceptable cost here in exchange for reproducibility and a zero-step publishing flow.

## 6. What's deliberately *not* committed

A few things are excluded from git on purpose (see `.gitignore`):
- Standard local/editor cruft (`.Rproj.user`, `.Rhistory`, `.DS_Store`, `.quarto/`, etc.).
- `*_files/` directories and `*_cache` — intermediate knitr working directories, distinct from the curated `_freeze/` cache described above.
- `*.tex` / `*.pdf` — generated LaTeX/PDF build byproducts, **except** the hand-written source partials `preamble.tex`, `before-body.tex`, and `cover-page.tex`'s successor, which are real source files Quarto's PDF template needs (they're explicitly un-ignored). The rendered book PDF `docs/Introduction-to-Behavioural-Data-Science.pdf` is also un-ignored, because the site's "Download PDF" link points to it and GitHub Pages can only serve what is committed.
- `wrangling/*.jsonl` — see next section.

## 7. Do the `wrangling/*.jsonl` files need to be stored anywhere else?

**Short answer: not required, but worth a backup if you want extra safety.**

What they are: `wrangling/finance.jsonl`, `medicine.jsonl`, `open_qa.jsonl`, and `wiki_csai.jsonl` are local copies of the [HC3 dataset](https://huggingface.co/datasets/Hello-SimpleAI/HC3) (human vs. AI-generated answers), used by `wrangling/text-analysis.qmd`. That chapter downloads them itself:

```r
if (!file.exists(file)) download.file(paste0(base_url, file), file, quiet = TRUE)
```

So on any machine, rendering that chapter once will re-download them automatically — that's why they're gitignored rather than committed: they're a regenerable cache, not authored content, and bundling a third-party dataset (with its own, different license) inside this CC BY-NC-SA repo isn't appropriate.

Because of that self-healing download step, you generally don't need to keep a separate copy anywhere. Two situations where you might still want one:
- **If Hugging Face ever removes or changes that dataset**, the download guard would fail or silently fetch different data next time someone renders from scratch. A backup protects against that.
- **If you want to render offline** without depending on Hugging Face being reachable.

If you do want a safety copy, keep it *outside* this git repo — for example:
- alongside the course's other external datasets on **OSF** (the project already uses OSF for domain-specific data per `CLAUDE.md`), or
- a plain local/cloud backup folder (e.g. your Drive/OneDrive), since these are just working copies, not something that needs version history.

Either way, they shouldn't go back into this git repo — the `_freeze/`/`docs/` reasoning above doesn't apply to them, since it's third-party raw data rather than something this repo's own build process produces from its own code.
