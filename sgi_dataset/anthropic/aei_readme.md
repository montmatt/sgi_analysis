# Anthropic Economic Index (AEI) Data - Oct 2026 Human Edge Studio

Anthropic collects data on Claude usage internationally to share in their Anthropic Economic Index. You'll see that the raw data spans different countries. The data shows where Claude conversations land in the occupational map, narrowed to the **United States** and **Massachusetts**. Source: Anthropic Economic Index, **June 2026 release ("Cadences", 26 June 2026)**, Claude.ai usage (chat and Cowork). Covers **April and May 2026**.

## Files

| File | One row per | Contents |
|---|---|---|
| `aei_by_occupation.csv` | Area x month x occupation | `AEI_PCT`: percent of an area's conversations mapped to the occupation |
| `aei_other_metrics_long.csv` | Area x month x node x metric | Everything else: usage by task, work activity, request topic and SOC major group, plus overall behavior metrics |

`AREA` is `US` or `MA`. `DATE_START` is `2026-04-01` or `2026-05-01`.

## Keys

| Join to | Key | Notes |
|---|---|---|
| Lightcast, O*NET | `ONET` | 632 codes; 629 are in Lightcast. |
| OEWS | `SOC_2018` (first 7 characters of `ONET`) | - |
| O*NET tasks | `NODE_EXTERNAL_ID` = `TASK_ID` | `CATEGORY_NAME = onet`, level 0 |
| O*NET work activities | `NODE_EXTERNAL_ID` = `ELEMENT_ID` | `CATEGORY_NAME = onet`, level 3 |

## Metrics

| Level | US | Massachusetts |
|---|---|---|
| Occupation (`aei_by_occupation.csv`) | usage share only | usage share only |
| Tasks, request topics | usage share only | usage share only |
| SOC major group, work activity, request cluster | usage share + 51 behavior metrics | usage share only |
| Whole sample (`overall`) | 52 behavior metrics | 52 behavior metrics |

Autonomy, collaboration style, and similar metrics are not reported per occupation. For Massachusetts, they are reported only for the whole sample.

## Notes and limitations

- **`AEI_PCT` is a usage share, not a share of workers, users or time.** Read Anthropic documentation and research for more information.
- **Missing is not zero.** AEI withholds small cells. 632 of 1,016 O*NET codes have US data, and 265 have Massachusetts data.
- **Massachusetts is a small sample.**
- **Two usage indexes use different bases.** `usage_per_capita_index` for the US may look relative to the world and for MA relative to the US. Conduct more research before jumping into usage.
- **Claude.ai only.** Not the API or other AI tools.
- **Timing differs.** AEI is April and May 2026, Lightcast is 2023 to September 2026, OEWS is May 2025.
- **Automation and augmentation are labels given to conversations**, showing how people worked with Claude (e.g. handing off a task vs. working back and forth). This doesn't necessarily show what is happening to jobs. Describe results as “where Claude is being used”.