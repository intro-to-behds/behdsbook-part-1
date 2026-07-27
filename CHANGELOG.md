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
- Began migrating the book off the `dslabs` package name to `behdslabs` (its own fork, not on CRAN), chapter by chapter. `R/getting-started.qmd`: install instructions now use `remotes::install_github("intro-to-behds/behdslabs")` instead of `install.packages("dslabs")`, and `library(dslabs)` → `library(behdslabs)`. Remaining chapters are migrated incrementally in later sessions; both package names stay installed side by side in the meantime so nothing breaks.

### Added
- (new chapters land here as they're written)

### Replaced
- `dataviz/intro-dataviz.qmd`: all four motivating examples replaced with `behdslabs` (fork of `dslabs`) datasets — `murders` → `app_data_breaches` (opening table + scatterplot), `us_contagious_diseases` (measles/vaccines) → `fitness_app_downloads_by_state` (Guided Meditation app downloads, "vaccine introduced" reframed as "free OS feature bundled"), `nyc_regents_scores` → `cognitive_battery_scores` (histogram), `gapminder` → `global_tech_adoption` (animated/faceted scatter, world health/economics reframed as global tech adoption).
