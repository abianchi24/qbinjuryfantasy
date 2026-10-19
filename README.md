# How a Starting QB Injury Affects RB, WR, and TE Fantasy Scoring

When an NFL team loses its starting quarterback, how much do its running backs,
wide receivers, and tight ends lose in fantasy points, and why?

## Data
NFL data from 2016–2025 regular seasons via [nflverse](https://nflverse.nflverse.com/)
(`nflreadr`): weekly player stats, injury reports, depth charts, schedules, and snap counts.

## Method
- **QB1** is the depth chart starter in weeks when no starting-caliber QB is injured,
  carried across injury weeks.
- **Treatment:** QB1 is listed Out/Doubtful or on injured reserve, and a different QB starts.
- **Sample:** RB/WR/TE with at least 50% offensive snap share in games with QB1
  (21,052 player-games).
- **Model:** fixed-effects regression of PPR points on the QB-out indicator, with
  player-season fixed effects, opponent defensive strength, and home/away, using
  standard errors clustered by team-season (`fixest`).
- Fantasy points were broken into scoring components to see where the losses come from.

## Findings

<img width="1340" height="372" alt="qb_findings_table" src="https://github.com/user-attachments/assets/ebca0386-eba6-46cf-9ee0-480a88ef6672" />

| Position | Effect (PPR pts/game) | Main driver |
|---|---|---|
| RB | −1.84*** | Fewer targets and rushing TDs; carries and yards per carry unchanged |
| WR | −0.54 (p ≈ 0.08) | Same targets, about 0.36 fewer yards per target |
| TE | −0.62 (p ≈ 0.09) | Mostly fewer receiving TDs |

Starting RBs lose the most, and the RB–WR gap is statistically significant (p < 0.05).

## Repository contents
- `R/qb_injury_model.R`: full pipeline, from data download through models and CSV export
- `output/`: exported model results
- `powerbi/`: Power BI report and table screenshot

## Reproduce
Install `nflreadr`, `dplyr`, `tidyr`, `fixest`, and `readr`, then run
`R/qb_injury_model.R` from the project folder.
