# Football results, Elo and event data

I put this together because I love football data and wanted one place where match results, club Elo ratings and detailed match events all join up. I'm sharing it so anyone can use it: for analysis, research, teaching, side projects, or just digging around. It's free to use under the licences below. All I ask is that you credit the sources the way their licences say.

## What's in it

- **Match results:** 1,066,044 matches from 271 competitions (leagues, domestic cups, national-team tournaments and continental club competitions). They run from 1888 to 2026 and also include scheduled fixtures up to June 2027. Each match has its teams, kickoff, status, score and how it was decided (regulation, extra time or penalties).
- **Teams and people:** 10,809 teams (clubs and national teams) and 6,784 players and managers, with their names.
- **Elo ratings:** 270,476 BeyondELO club ratings (rating dates from 1994 to 2026), plus home and away Elo for 73,262 matches between 2011 and 2027.
- **football-data.co.uk results:** 283,240 results. They cover the main European leagues from 1993/94 to 2025/26, plus Argentina, Austria, Brazil, China, Denmark, Finland, Ireland, Japan, Mexico, Norway, Poland, Romania, Russia, Sweden, Switzerland and the USA.
- **OpenPlay match events:** 41.6 million on-ball events with pitch coordinates. They cover 25,531 fixtures: the top five European leagues, the Champions League, the Europa League and the UEFA Super Cup from 2014/15 to 2025/26, plus World Cups, Euros, Copa América, AFCON, the Club World Cup, the Nations League and the Bundesliga relegation play-offs. There are also 631,556 shots, 733,824 player-match stat lines, line-ups and formations, cards, and 7.9 million event qualifiers for the international tournaments.
- **Outcome labels:** 582,851 finished matches with ready-made labels (1X2, both teams score, total goals, over 1.5/2.5/3.5, clean sheets).
- **Images:** 606 badges and player, manager and stadium photos from Wikimedia Commons, each with its own licence and credit line.

## Where the files are

The big tables are gzipped CSV files attached to the release:
**https://github.com/PrinceGOdsplan/football-results-elo-events/releases/tag/archive-pg-1**

The images and documentation live in this git repository.

| Release file | What it holds | Rows | Dates | Coverage |
|---|---|---:|---|---|
| `canonical__match.csv.gz` | One row per match | 1,066,044 | 08/09/1888 to 06/06/2027 | 271 competitions |
| `canonical__match_outcome.csv.gz` | How each match was decided, and the winner | 1,038,721 | matches above | |
| `canonical__score_observation.csv.gz` | Scores as reported by each source | 1,907,840 | matches above | |
| `canonical__canonical_result.csv.gz` | The accepted score for each match | 1,034,692 | matches above | |
| `canonical__match_source.csv.gz`, `canonical__score_observation_match.csv.gz` | Link tables | 1,331,065 / 1,047,224 | | |
| `canonical__competition*.csv.gz`, `canonical__season_mapping.csv.gz` | Competitions, editions and id mappings | 271 / 3,085 / 805 / 86 | | |
| `canonical__party*.csv.gz` | Teams and team names | 10,809 each | | 10,214 clubs, 595 national teams |
| `canonical__person*.csv.gz` | Players and managers, and their names | 6,784 each | | |
| `beyondelo_rating.csv.gz` | BeyondELO club Elo per match side | 270,476 | ratings 07/05/1994 to 06/11/2026 | 122 competitions |
| `elo_prematch.csv.gz` | Home and away Elo per match | 73,262 | 06/11/2011 to 06/06/2027 | 116 competitions |
| `training_labels.csv.gz` | Outcome labels from the 90-minute score | 582,851 | | finished matches |
| `fdcouk_results.csv.gz` | football-data.co.uk results | 283,240 | 23/07/1993 to 04/11/2026 | 38 leagues |
| `openplay__openplay_event_events_<comp>_<season>.csv.gz` (125 files) | Match events | 41,594,510 | 2014/15 to 2026 | see above |
| `openplay__openplay_event_qualifier_events_<comp>_<season>.csv.gz` (22 files) | Event qualifiers | 7,893,166 | 2015 to 2026 | AFCON, Copa América, Euros, Nations League A/B, World Cup |
| `openplay__openplay_shot.csv.gz` | Shots | 631,556 | | |
| `openplay__openplay_player_stat.csv.gz` | Player match stats | 733,824 | | |
| `openplay__openplay_formation.csv.gz` | Formations and line-ups | 245,468 | | |
| `openplay__openplay_card.csv.gz` | Cards | 115,499 | | |
| `openplay__openplay_fixture.csv.gz` | OpenPlay fixtures linked to matches | 25,531 | | |
| `openplay__*` (other) | Links and load counts | small | | |
| `metadata__*.csv.gz` | Seasons, the five sources behind the match tables, and the rules for picking a result | small | seasons 1993/94 to 2026/27 | |
| `SHA256SUMS` | SHA-256 checksum of every file | | | |

Every column of every file is listed in **[DATA_DICTIONARY.md](DATA_DICTIONARY.md)**, along with how the ids join and the share of empty values in each column.

## Things to know before you use it

- **Missing means null.** An empty field is a value I don't have. It never means zero. Please don't fill it with 0.
- Scores are the 90-minute (regulation) score unless the `component` column says otherwise (`after_extra_time_cumulative` or `penalties`).
- Matches with status `scheduled` haven't been played yet, so they have no score.
- Very old matches often only have a date (`kickoff_precision = date`), not a kickoff time.
- Some BeyondELO and OpenPlay rows couldn't be linked to a match with confidence. Those are marked (`mapping_class`, `openplay_unconfirmed_*`), so you can include or exclude them as you like.
- Times with a `+01` offset are local time in UTC+1. Fields ending in `_utc` or `Z` are UTC.

## Download and check

With the [GitHub CLI](https://cli.github.com/):

```bash
mkdir football-data && cd football-data
gh release download archive-pg-1 -R PrinceGOdsplan/football-results-elo-events
```

Or download single files from the release page in your browser.

To check everything you downloaded against the published checksums:

```bash
sha256sum -c SHA256SUMS --ignore-missing
```

## Load it

**DuckDB** (no setup, reads the gzip directly):

```sql
SELECT m.kickoff_on, h.name AS home, a.name AS away, s.home_goals, s.away_goals
FROM read_csv_auto('canonical__match.csv.gz') m
JOIN read_csv_auto('canonical__canonical_result.csv.gz') r ON r.match_id = m.match_id AND r.component = 'regulation'
JOIN read_csv_auto('canonical__score_observation.csv.gz') s ON s.score_observation_id = r.score_observation_id
JOIN read_csv_auto('canonical__party_name.csv.gz') h ON h.party_id = m.home_party_id
JOIN read_csv_auto('canonical__party_name.csv.gz') a ON a.party_id = m.away_party_id
LIMIT 10;
```

**pandas:**

```python
import pandas as pd
matches = pd.read_csv("canonical__match.csv.gz")
```

**PostgreSQL:** create a table with the columns from the header (see DATA_DICTIONARY.md), then:

```bash
gunzip -c canonical__match.csv.gz | psql -d football -c "\copy match FROM STDIN WITH (FORMAT csv, HEADER true)"
```

Empty fields load as NULL with `FORMAT csv`, which is what you want.

## Sources and credit

This dataset builds on other people's generous work. If you use it, please credit them as well as me:

- **BeyondELO** club Elo ratings, https://beyondelo.com. Licence: CC BY 4.0. Credit: "beyondELO (https://beyondelo.com)".
- **OpenPlay** event data, data-v0.1.0. Licence: CC BY 4.0. Credit: "openplay (Noah Bair)".
- **football-data.co.uk** results, https://www.football-data.co.uk/. Please credit football-data.co.uk.
- **schochastics/football-data** match results, https://github.com/schochastics/football-data. Licence: Open Data Commons Attribution License (ODC-By 1.0). Credit: "schochastics/football-data".
- **eatpizzanot/soccer-dataset** fixtures and results, https://huggingface.co/datasets/eatpizzanot/soccer-dataset. Licence: CC BY 4.0. Credit: "eatpizzanot". Its upstream source is API-Football (https://www.api-football.com), which eatpizzanot asks users to credit as well.
- **Wikimedia Commons** images. Each image keeps its own licence (CC BY, CC BY-SA, CC0 or public domain). The author, licence and source link for every file are in [`images/ATTRIBUTION.csv`](images/ATTRIBUTION.csv). If you reuse an image, use its credit line, and keep CC BY-SA images under CC BY-SA.

More detail is in [SOURCES.md](SOURCES.md). Club and competition names and badges belong to their owners, and no trademark rights are given.

## Licence

My own work here (the compiled and linked match tables, the outcome labels, the id maps and the documentation) is released under **Creative Commons Attribution 4.0 International (CC BY 4.0)**. See [LICENSE](LICENSE). You can share and adapt it for any purpose, including commercial use, as long as you give credit.

Third-party material keeps its own licence, listed above.

## How to cite

> PrinceGOdsplan (2026). *Football results, Elo and event data* (release archive-pg-1, 19/11/2026). https://github.com/PrinceGOdsplan/football-results-elo-events. CC BY 4.0. Includes data from beyondELO (CC BY 4.0), openplay (Noah Bair, CC BY 4.0), eatpizzanot (CC BY 4.0), schochastics/football-data (ODC-By 1.0) and football-data.co.uk.

```bibtex
@misc{princegodsplan2026football,
  author = {PrinceGOdsplan},
  title  = {Football results, Elo and event data},
  year   = {2026},
  note   = {Release archive-pg-1. CC BY 4.0. Includes beyondELO, openplay and eatpizzanot (CC BY 4.0), schochastics/football-data (ODC-By 1.0) and football-data.co.uk data},
  url    = {https://github.com/PrinceGOdsplan/football-results-elo-events}
}
```

Found a mistake or have a question? Open an issue. I'd love to hear what you build with it.
