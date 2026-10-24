# OEWS Employment and Wage Data - Oct 2026 Human Edge Studio

OEWS has data on employment and wages by occupation for the United States and its states. To narrow the scope, we focus on the **United States** and **Massachusetts**. Source: BLS Occupational Employment and Wage Statistics (OEWS), **May 2025 release**, SOC 2018. The data is one snapshot from May 2025.

## Files

| File | One row per | Contents |
|---|---|---|
| `oews_by_area.csv` | Area x occupation | Employment, annual and hourly wages, reliability (RSE) and status flags. 830 US rows, 737 MA rows. `AREA` is `US` or `MA`. |

## Keys

| Join to | Key | Notes |
|---|---|---|
| Lightcast, O*NET | `SOC_2018` = first 7 characters of `ONET` | - |
| AEI | `ONET` |- |
| Area | `AREA` (`US`, `MA`) | Lightcast uses `US_` and `MA_` column prefixes. |

## Notes and limitations

- **Employment repeats after a join.** Several O*NET codes share one SOC code. Summing employment after the join overcounts (about 26% for the US).
- **Not every occupation matches.** Of 867 O*NET SOC codes, 818 match exactly, 15 map to a combined OEWS row, and 34 have no match.
- **Detailed occupations only.** Totals and group rows are left out. Group by `SOC_2` for higher levels.
- **Blanks have reasons.** `EMPLOYMENT_STATUS` and `WAGE_STATUS` say why. 61 MA occupations have no employment figure.
- **`LOCATION_QUOTIENT` and `JOBS_PER_1000` are Massachusetts only.**
- **Annual-only and hourly-only wages** are flagged (`ANNUAL_ONLY`, `HOURLY_ONLY`)
- OEWS counts jobs, not people, and excludes the self-employed. Wages exclude benefits.