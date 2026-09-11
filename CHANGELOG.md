# Changelog

All notable changes from the upstream Irizarry *Introduction to Data Science*
(`rafalab/dsbook-part-1`) are documented here, as required by the
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0) license
under which this adaptation is distributed.

## [Unreleased] — Behavioural Data Science adaptation

### Changed
- Retitled to "Introduction to Behavioural Data Science".
- Split `index.qmd` preface/acknowledgments into separate, clearly labeled sections for the adaptation vs. the original Irizarry edition.
- Updated self-referential GitHub/site links (navbar, footnotes, git tutorial example) from the upstream `rafalab/dsbook-part-1` repo to this fork, `intro-to-behds/behdsbook-part-1`.
- Enabled a PDF download button in the book navbar (`book: downloads: [pdf]`).
- `productivity/ai-assisted-coding.qmd`: revised the draft chapter — full language pass, corrected the ChatGPT release date (late 2022) and tempered the claims about LLM capability to match `intro.qmd`, replaced the `rnorm` silent-error example with `behdslabs::app_task_completion` (percentage-vs-proportion bug), added the `@fig-ai-three-steps` ggplot2 figure and the "dark side" illustration, resolved all `<...>` author notes, and added inline citations (LLM definition, code-trained-on-web, vibe coding, multiverse analysis) plus a further-reading link to the ONDA Lab guide.
- `productivity/ai-assisted-coding.qmd`: added bad-vs-good example prompts for drafting code (with a callout warning against over-relying on AI drafting early in one's learning) and for verifying/checking code, plus a new "Disclaimers on the use of AI" section citing APA Style, COPE, and ICMJE guidance on disclosing AI use.
- Began migrating the book off the `dslabs` package name to `behdslabs` (its own fork, not on CRAN), chapter by chapter. `R/getting-started.qmd`: install instructions now use `remotes::install_github("intro-to-behds/behdslabs")` instead of `install.packages("dslabs")`, and `library(dslabs)` → `library(behdslabs)`. `dataviz/intro-dataviz.qmd`: `library(dslabs)` → `library(behdslabs)`, fixing a leftover reference left over from the dataset swap below. Remaining chapters are migrated incrementally in later sessions; both package names stay installed side by side in the meantime so nothing breaks.

### Added
- `productivity/ai-assisted-coding.qmd`: new chapter "AI and responsible coding" (by Giorgio Arcara), added as the last chapter of the Productivity part.

### Replaced
- `dataviz/intro-dataviz.qmd`: all four motivating examples replaced with `behdslabs` (fork of `dslabs`) datasets — `murders` → `app_data_breaches` (opening table + scatterplot), `us_contagious_diseases` (measles/vaccines) → `fitness_app_downloads_by_state` (Guided Meditation app downloads, "vaccine introduced" reframed as "free OS feature bundled"), `nyc_regents_scores` → `cognitive_battery_scores` (histogram), `gapminder` → `global_tech_adoption` (animated/faceted scatter, world health/economics reframed as global tech adoption).
