# O*NET Data - Oct 2026 Human Edge Studio

O\*NET collects data on descriptions of what each US occupation involves: tasks, skills, abilities, knowledge, tools and education. The raw data contains 46 different files, which spans both data and data dictionaries. Source: the **O\*NET 31.0 database** (August 2026), from the O*NET Resource Center. The data is one snapshot, with no data for years.

## Files

| File | One row per | Contents |
|---|---|---|
| `onet_occupations.csv` | Occupation | 1,016 codes: `ONET_TITLE`, description, `SOC_2018`, Job Zone, `IS_BASE_CODE` |
| `onet_skills.csv` | Occupation | Importance (`IMP_`) and level (`LVL_`) for skills (Essential + Transferable) |
| `onet_descriptors.csv` | Occupation x element | Abilities (52), Knowledge (33), Work Activities (41), stacked |
| `onet_tasks.csv` | Occupation x task | 18,838 task statements, Core or Supplemental |
| `onet_software_skills.csv` | Occupation x software example | Software and tools in 134 categories |
| `onet_education.csv` | Occupation x scale x category | Share of workers by education level |

## Keys

| Join to | Key | Notes |
|---|---|---|
| Lightcast (all tables) | `ONET` | 8-digit O\*NET-SOC code, e.g. `15-1252.00`. Please note that O\*NET has no year, so values will repeat for each Lightcast `YEAR`. |
| OEWS | `SOC_2018` | First 7 characters of `ONET`. Please note that 76 SOC codes have more than one O\*NET code, so OEWS rows repeat after a join, e.g. Registered Nurses (SOC 29-1141) has five O*NET codes (29-1141.00 to 29-1141.04)  |
| AEI tasks | `TASK_ID` | 1,687 of 1,689 AEI task ids match. |
| AEI work activities | `ELEMENT_ID` (domain Work Activities) | 35 of 41 appear in AEI. |

## Notes and limitations

- **Coverage vs Lightcast:** all 972 classified Lightcast codes are here. 44 O\*NET codes have no Lightcast rows (mostly small occupations).
- **Not every occupation has every table:** skills 910, descriptors 911, tasks and software 923, education 901 occupations. Job Zone is blank for 93 occupations, expect blanks after a join.
- **Importance (1 to 5) and level (0 to 7) are different scales.**
- **Suppressed and "not relevant" ratings are kept as flags.** Filter on them deliberately. In `onet_skills.csv` suppressed values are blank.
- **Education has two scales** (`RL`, `RQ`). Check O\*NET documentation before combining them.
- **Software is a list of examples.** It has no key to Lightcast `SKILL_ID`; matching will mean matching on names.
- **Base codes (`.00`) and variants (e.g. `.01`):**