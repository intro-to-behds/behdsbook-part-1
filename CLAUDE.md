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

Every page in the sidebar except `index.qmd` and `work-in-progress.qmd` starts with a two-sentence italic line, directly under its `# Title {...}` line and before any setup chunk or Draft callout. The first sentence says who wrote the original, the second what changed in this edition. It is the only place that says who wrote a chapter: don't add `_by ..._` lines or "this chapter is original material" callouts. The details go in `CHANGELOG.md`. Use one of these three forms (`URL` is the same page in Irizarry's book, `https://rafalab.dfci.harvard.edu/dsbook-part-{1,2}/<path>.html`):

- Unchanged Irizarry chapter: `_Original chapter by Rafael A. Irizarry, from [*Introduction to Data Science*](URL). Unchanged in this edition, except for links and package names._`
- Adapted Irizarry chapter: `_Original chapter by Rafael A. Irizarry, from [*Introduction to Data Science*](URL). Adapted by Giorgio Arcara: <what changed: old → new datasets, added sections by name>; the text is otherwise Irizarry's, with small edits to fit the new examples._`
- New chapter: `_Written for this book by <author>. This chapter is not in Irizarry's *Introduction to Data Science*._` (author: `Giorgio Arcara`, `Cristiano Costa, with Giorgio Arcara`, or `Giorgio Arcara, with an AI assistant (Claude)` for chapters drafted with Claude; for a part-intro page, write "This part").

Keep the line up to date: when a chapter is reflavoured, gains or loses a section, or a hidden chapter is restored to `_quarto.yml`, update or add its line in the same commit.
