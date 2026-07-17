# SexualMinorities_Psychedelic_MentalHealth_NSDUH_Code

Analysis code for a study testing whether **sexual identity moderates the associations between lifetime MDMA/ecstasy and psilocybin use and mental-health outcomes** in U.S. adults, using pooled **National Survey on Drug Use and Health (NSDUH) 2015–2019** data.

> ****
> Survey-weighted R analysis testing sexual-identity moderation of lifetime psychedelic (MDMA/ecstasy, psilocybin) associations with psychological distress, suicidality, and major depressive episodes in NSDUH 2015–2019.

---

## Overview

Population-based work has linked lifetime classic-psychedelic use to lower odds of psychological distress, suicidality, and major depressive episodes, but these associations may not extend uniformly across marginalized identities. This project asks whether **sexual identity (heterosexual, gay/lesbian, bisexual)** moderates those associations across six mental-health outcomes, using design-based survey methods.

The analysis is **exploratory and largely null**; results are intended to be interpreted as hypothesis-generating. See the accompanying manuscript for full framing and interpretation.

## Repository contents

| File | Description |
|------|-------------|
| `SexualMinorities_Psychedelic_MentalHealth_NSDUH.Rmd` | The full analysis notebook: data import, cleaning/recoding, survey design, models, and publication tables. |
| `README.md` | This file. |

> The R Markdown notebook is the single source of the analysis; running it end-to-end reproduces all reported tables.

## Data availability

Data are **not** included in this repository. The analysis uses the **NSDUH public-use files (2015–2019)**, which are freely available from the Substance Abuse and Mental Health Data Archive (SAMHSA):

- https://www.datafiles.samhsa.gov/

Download each annual public-use file, save them as `NSDUH2015Data.RDS` … `NSDUH2019Data.RDS`, and place them in the working directory before running the notebook.

## Requirements

- **R** (version recorded by `sessionInfo()` in the final chunk)
- R packages: `survey`, `dplyr`, `tidyr`/`labelled`, `tableone`, `knitr`, `plyr` (installed automatically via `pacman::p_load()` at the top of the notebook)

## How to run

1. Download the five NSDUH public-use files and save them as `NSDUH2015Data.RDS` … `NSDUH2019Data.RDS` in the working directory.
2. Open the `.Rmd` in RStudio and **Knit** (or run chunks sequentially).
3. The notebook reproduces Table 1, the interaction screen (Table 2), the stratified subgroup models (Table 3), and the full-sample supplementary table.

No random-number generation is used, so results are **deterministic**.

## Analysis summary

- **Design:** Survey-weighted multivariable logistic regression via `survey::svyglm(family = quasibinomial())`, with `id = ~verep`, `strata = ~vestr`, `nest = TRUE`. The single-year analysis weight is rescaled for five-year pooling (`ANALWT_C / 5`) per SAMHSA guidance.
- **Outcomes (6):** past-month psychological distress (K6 ≥ 13), past-year suicidal ideation, past-year suicidal planning, and past-year, lifetime, and severe past-year major depressive episode.
- **Exposures:** lifetime MDMA/ecstasy use; lifetime psilocybin use.
- **Two-step approach:** (1) a full-sample interaction screen (sexual identity × substance) for each substance–outcome combination; (2) stratified subgroup models reported only for combinations reaching significance in Step 1.
- **Inference:** odds ratios, 95% CIs, and p-values are all computed on the same residual design degrees of freedom (helper functions `or_table()` / `or_confint()`), with a `check_consistency()` routine confirming CI–p agreement. Benjamini–Hochberg false-discovery-rate q-values are reported across the interaction screen.

## Associated manuscript

[Add full citation / DOI / preprint link once available.]

## How to cite

If you use this code, please cite the associated manuscript (above) and/or this repository:

> Seale MA. *SexualMinorities_Psychedelic_MentalHealth_NSDUH_Code.* GitHub repository. [URL] [year].

## License

[Add a license — e.g., MIT for the code. NSDUH data are governed by SAMHSA's terms of use and are not redistributed here.]

## Author

Maya A. Seale (she/her) — [affiliation / contact]
