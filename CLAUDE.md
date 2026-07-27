# CLAUDE.md

## What this repo is

Quarto book source for **Part 1** of the *Behavioural Data Science* course (PS0000002, UniPD, AY 2026/2027) — a behavioural-science adaptation of Rafael Irizarry's *Introduction to Data Science: Data Wrangling and Visualization with R*. Fork of https://github.com/giorgioarcara/dsbook-part-1, published at https://github.com/intro-to-behds/behdsbook-part-1.

Course planning (week-by-week structure, assessment, Moodle organisation) lives in the separate course hub: `/Users/giorgioarcara/Documents/Teaching/2026 - Behavioural Data Science/CLAUDE.md` and `BDS_course_structure.md`.

## Adaptation rule

Irizarry's original datasets (US murders, baseball, elections) must be replaced with behavioural equivalents — reaction times, accuracy scores, survey data, experiment logs. Use the sibling `behdslabs` package (fork of `dslabs`) for datasets where domain is secondary, or OSF / Open Psychometrics for domain-specific data.

## Structure

Chapters are top-level folders (`dataviz/`, `productivity/`, etc.), each containing `.qmd` files. Rendered via Quarto (`_quarto.yml`) to `docs/`.

## Adding a new chapter

1. Create a new top-level folder (mirrors `productivity/`, `dataviz/`, etc.) containing:
   - An unnumbered part-intro file, e.g. `<folder>/intro-<folder>.qmd` — one motivating paragraph, no `##` sections (pattern: `productivity/intro-productivity.qmd`).
   - One or more numbered chapter files using `# Title {#sec-<slug>}` headers (pattern: `dataviz/distributions.qmd`).
2. Register it in `_quarto.yml` under `book: chapters:` as a new `- part: <folder>/intro-<folder>.qmd` block with nested `chapters:`, positioned where it fits the course's topic sequence.
3. Log the addition under `### Added` in `CHANGELOG.md`.

## Attribution & licensing

This is a CC BY-NC-SA 4.0 adaptation of Rafael A. Irizarry's *Introduction to Data Science* — see the attribution notice in `index.qmd` and `CHANGELOG.md` for the full record of changes from upstream.
