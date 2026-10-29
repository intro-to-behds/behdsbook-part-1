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
- `index.qmd`: corrected the preface sentence listing the book websites (now "The websites for the two parts of the book"), which point to the intro-to-behds adaptation, and moved the links to Irizarry's original version into explicit footnotes with unique labels.
- Enabled a PDF download button in the book navbar (`book: downloads: [pdf]`).
- `productivity/ai-assisted-coding.qmd`: revised the draft chapter — full language pass, corrected the ChatGPT release date (late 2022) and tempered the claims about LLM capability to match `intro.qmd`, replaced the `rnorm` silent-error example with `behdslabs::app_task_completion` (percentage-vs-proportion bug), added the `@fig-ai-three-steps` ggplot2 figure and the "dark side" illustration, resolved all `<...>` author notes, and added inline citations (LLM definition, code-trained-on-web, vibe coding, multiverse analysis) plus a further-reading link to the ONDA Lab guide.
- `productivity/ai-assisted-coding.qmd`: added bad-vs-good example prompts for drafting code (with a callout warning against over-relying on AI drafting early in one's learning) and for verifying/checking code, plus a new "Disclaimers on the use of AI" section citing APA Style, COPE, and ICMJE guidance on disclosing AI use.
- Began migrating the book off the `dslabs` package name to `behdslabs` (its own fork, not on CRAN), chapter by chapter. `R/getting-started.qmd`: install instructions now use `remotes::install_github("intro-to-behds/behdslabs")` instead of `install.packages("dslabs")`, and `library(dslabs)` → `library(behdslabs)`. `dataviz/intro-dataviz.qmd`: `library(dslabs)` → `library(behdslabs)`, fixing a leftover reference left over from the dataset swap below. Remaining chapters are migrated incrementally in later sessions; both package names stay installed side by side in the meantime so nothing breaks.
- `dataviz/distributions.qmd` and `dataviz/dataviz-principles.qmd`: the distribution case study now uses the `ux_scores` dataset (`behdslabs` ≥ 0.12.0), UX questionnaire scores of desktop and mobile users, instead of `reaction_times`, whose values are now a realistic, right-skewed simulation. `wrangling/string-processing.qmd` names `ux_scores` among the datasets extracted from raw data. `R/tidyverse.qmd`, `R/data-table.qmd` and `dataviz/ggplot2.qmd` keep `reaction_times`, which they use only to show code mechanics.

### Added
- `basic-stats/`: new part "Basic Statistics" (refresher, read-only), added as the last part of the book so that no existing chapter is renumbered. Part intro `basic-stats/intro-basic-stats.qmd`, pointing to free books (Navarro, Poldrack, Lakens). Original material, drafts written with Claude on 2026-10-29, not yet reviewed (each chapter carries a Draft callout).
- `basic-stats/central-tendency-dispersion.qmd`: new chapter "Central Tendency and Dispersion" (mean, median, mode; range, variance, SD, IQR, MAD; standard units; SD vs SE), on `reaction_times` and `ux_scores`.
- `basic-stats/correlation.qmd`: new chapter "Correlation" (Pearson as the average product of z-scores, misleading cases, Spearman, `cor.test()`, correlation as an effect size), on `app_engagement_experiment`.
- `basic-stats/anova.qmd`: new chapter "Comparing More Than Two Groups: ANOVA" (draft, 2026-10-29): one-way and two-way between-subjects and one-way repeated-measures ANOVA with `afex::aov_ez()`, post-hoc tests with `pairwise.t.test()`, hidden multiplicity in multiway ANOVA (Cramer et al., 2016), planned contrasts, Kruskal–Wallis. Adds `afex` (and its dependencies) to `renv.lock`.
- `basic-stats/multiple-comparisons.qmd`: new short chapter "Multiple Comparisons" (draft, 2026-10-29): the problem by simulation, FWER vs FDR, Bonferroni, Holm, Benjamini–Hochberg, Benjamini–Yekutieli with pros and cons, planned contrasts, open sources.
- `basic-stats/chi-square.qmd`: new chapter "Two Categorical Variables: the Chi-square Test" (draft, 2026-10-29): contingency tables, expected counts, `chisq.test()`, two-by-two tables (`tech_grant_funding_gender_gap`), assumptions, Fisher's exact test, Cramér's V, goodness of fit.
- `basic-stats/comparing-two-groups.qmd`: chapter "Comparing Two Groups: the t-test and the Wilcoxon Test", moved from Part 2 (`inference/comparing-two-groups.qmd`, draft of 2026-10-14) so that Part 2 keeps Irizarry's structure. Cross-references to Part 2 became links to its published pages; a further-reading section was added.
- `productivity/ai-assisted-coding.qmd`: new chapter "AI and responsible coding" (by Giorgio Arcara), added as the last chapter of the Productivity part.

### Replaced
- `dataviz/intro-dataviz.qmd`: all four motivating examples replaced with `behdslabs` (fork of `dslabs`) datasets — `murders` → `app_data_breaches` (opening table + scatterplot), `us_contagious_diseases` (measles/vaccines) → `fitness_app_downloads_by_state` (Guided Meditation app downloads, "vaccine introduced" reframed as "free OS feature bundled"), `nyc_regents_scores` → `cognitive_battery_scores` (histogram), `gapminder` → `global_tech_adoption` (animated/faceted scatter, world health/economics reframed as global tech adoption).
