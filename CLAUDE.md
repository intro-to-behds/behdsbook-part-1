# CLAUDE.md

## What this repo is

Quarto book source for **Part 1** of the *Behavioural Data Science* course (PS0000002, UniPD, AY 2026/2027) — a behavioural-science adaptation of Rafael Irizarry's *Introduction to Data Science: Data Wrangling and Visualization with R*. Fork of https://github.com/giorgioarcara/dsbook-part-1, published at https://github.com/intro-to-behds/behdsbook-part-1.

Course planning (week-by-week structure, assessment, Moodle organisation) lives in the separate course hub: `/Users/giorgioarcara/Documents/Teaching/2026 - Behavioural Data Science/CLAUDE.md` and `BDS_course_structure.md`.

## Adaptation rule

Irizarry's original datasets (US murders, baseball, elections) must be replaced with behavioural equivalents — reaction times, accuracy scores, survey data, experiment logs. Use the sibling `behdslabs` package (fork of `dslabs`) for datasets where domain is secondary, or OSF / Open Psychometrics for domain-specific data.

## Structure

Chapters are top-level folders (`dataviz/`, `productivity/`, etc.), each containing `.qmd` files. Rendered via Quarto (`_quarto.yml`) to `docs/`.

Rendering notes: render with `LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8` set (Quarto can hang silently without a locale). The knitr cache (`cache: true`) is keyed on the installed `behdslabs` version and data hash by a hook in `.Rprofile`, so updating the package re-executes cached chunks on the next render. `freeze: auto` is separate: a full project render does not re-execute chapters whose source is unchanged, so after a `behdslabs` data change render the affected chapters one by one (`quarto render <file>.qmd` always executes) or delete their `_freeze/` folders. GitHub Pages serves `docs/` (branch `main`, path `/docs`); a root-level `site_libs/` is not used and is ignored.

## Adding a new chapter

1. Create a new top-level folder (mirrors `productivity/`, `dataviz/`, etc.) containing:
   - An unnumbered part-intro file, e.g. `<folder>/intro-<folder>.qmd` — one motivating paragraph, no `##` sections (pattern: `productivity/intro-productivity.qmd`).
   - One or more numbered chapter files using `# Title {#sec-<slug>}` headers (pattern: `dataviz/distributions.qmd`).
2. Register it in `_quarto.yml` under `book: chapters:` as a new `- part: <folder>/intro-<folder>.qmd` block with nested `chapters:`, positioned where it fits the course's topic sequence.
3. Put the attribution line for a new chapter directly under each title (see *Chapter attribution line* below).
4. Log the addition under `### Added` in `CHANGELOG.md`.

## Attribution & licensing

This is a CC BY-NC-SA 4.0 adaptation of Rafael A. Irizarry's *Introduction to Data Science* — see the attribution notice in `index.qmd` and `CHANGELOG.md` for the full record of changes from upstream.

### Chapter attribution line

Every page in the sidebar except `index.qmd` and `work-in-progress.qmd` starts with a short italic line, directly under its `# Title {...}` line and before any setup chunk or Draft callout. It says who wrote the original and, in a few words, what changed in this edition. It is the only place that says who wrote a chapter: don't add `_by ..._` lines or "this chapter is original material" callouts. Never mention AI assistance here (or anywhere in a chapter's visible text): AI use is declared once for the whole book, in the *Disclaimers* of `index.qmd`.

**Default every time a chapter is drafted, reflavoured, gains or loses a section, or a hidden chapter is restored to `_quarto.yml`:** write or update its line in the same commit, following the rule below, and put every detail it leaves out in the chapter's `CHANGELOG.md` entry in that same commit.

The line says explicitly, without details, only:
1. whether the content is Irizarry's original;
2. whether the change is only in the datasets (or examples): "the datasets are replaced with behavioural ones", or "the examples …" for chapters with no dataset;
3. which sections are new, as a short list of their titles;
4. generically, whether passages are rephrased, shortened or removed ("some passages are rephrased or shortened").

No dataset or package names, no old → new mappings, no per-section list of edits, no exercise numbers: all of that goes to `CHANGELOG.md`. A one-off note that explains something the reader will see is fine (e.g. "the screenshots still come from the original edition").

Use one of these three forms (`URL` is the same page in Irizarry's book, `https://rafalab.dfci.harvard.edu/dsbook-part-{1,2}/<path>.html`; `CHANGELOG-URL` is `https://github.com/intro-to-behds/<repo>/blob/main/CHANGELOG.md`):

- Unchanged Irizarry chapter: `_Original chapter by Rafael A. Irizarry, from [*Introduction to Data Science*](URL). Unchanged in this edition, except for links and package names._`
- Adapted Irizarry chapter: `_Original chapter by Rafael A. Irizarry, from [*Introduction to Data Science*](URL). Adapted by Giorgio Arcara: <only the parts that apply, in this order: the datasets are replaced with behavioural ones; new sections *A* and *B*; some passages are rephrased or shortened>; the text is otherwise Irizarry's. Details in the [CHANGELOG](CHANGELOG-URL)._`
  Example: `… Adapted by Giorgio Arcara: the datasets are replaced with behavioural ones; new sections *A binary predictor: dummy variables* and *Adjusting for a confounder*; the text is otherwise Irizarry's. Details in the [CHANGELOG](…)._`
- New chapter: `_Written for this book by <authors>. This chapter is not in Irizarry's *Introduction to Data Science*._` (authors: `Giorgio Arcara`, `Cristiano Costa, with Giorgio Arcara`, …; for a part-intro page, write "This part").
