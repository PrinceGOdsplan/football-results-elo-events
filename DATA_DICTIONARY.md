# Data dictionary

Every file is a gzipped, comma-separated CSV with a header row and UTF-8 text. An empty field means the value is missing (null). It never means zero.

Ids that end in `_id` join across files: `match_id` and `canonical_match_id` point to `canonical__match.match_id`; `party_id`, `home_party_id`, `away_party_id` and `winner_party_id` point to `canonical__party.party_id`; `person_id` points to `canonical__person.person_id`; `score_observation_id` points to `canonical__score_observation`. Ids starting with `provider_` are the original source ids. `decision_id` and `source_record_id` are internal reference numbers kept so rows stay traceable; there is no table for them in this release.

The "% empty" figure is the share of rows where that column is null in this release.

## Ratings and labels

### `beyondelo_rating.csv.gz`

Club Elo ratings from BeyondELO, one row per club per match side, linked to a match_id where a match was found.

Rows: 270,476

| Column | % empty |
|---|---|
| `source_kind` | 0.0 |
| `mapping_class` | 0.0 |
| `provider_match_id` | 54.2 |
| `canonical_match_id` | 7.5 |
| `side` | 0.0 |
| `elo` | 0.0 |
| `rating_date` | 0.0 |
| `kickoff_on` | 0.0 |
| `competition` | 0.0 |
| `season` | 0.0 |
| `club_name` | 54.2 |
| `usable_prematch` | 0.0 |
| `source_file` | 0.0 |

### `elo_prematch.csv.gz`

Home and away club Elo for each match, taken from the BeyondELO ratings.

Rows: 73,262

| Column | % empty |
|---|---|
| `canonical_match_id` | 0.0 |
| `kickoff_on` | 0.0 |
| `competition` | 0.0 |
| `season` | 0.0 |
| `home_elo` | 0.0 |
| `away_elo` | 0.0 |
| `home_source` | 0.0 |
| `away_source` | 0.0 |
| `home_rating_date` | 0.0 |
| `away_rating_date` | 0.0 |
| `home_missing` | 0.0 |
| `away_missing` | 0.0 |
| `both_clubs` | 0.0 |

### `training_labels.csv.gz`

Outcome labels for each finished match, worked out from the 90-minute score.

Rows: 582,851

| Column | % empty |
|---|---|
| `match_id` | 0.0 |
| `regulation_home_goals` | 0.0 |
| `regulation_away_goals` | 0.0 |
| `result_1x2` | 0.0 |
| `btts` | 0.0 |
| `total_goals` | 0.0 |
| `over_1_5` | 0.0 |
| `over_2_5` | 0.0 |
| `over_3_5` | 0.0 |
| `away_clean_sheet` | 0.0 |
| `home_clean_sheet` | 0.0 |
| `score_component` | 0.0 |
| `score_observation_id` | 0.0 |

## football-data.co.uk results

### `fdcouk_results.csv.gz`

Match results from football-data.co.uk (date, teams, full-time goals). `provider_match_id` is the source file and row number.

Rows: 283,240

| Column | % empty |
|---|---|
| `match_id` | 0.0 |
| `provider` | 0.0 |
| `provider_match_id` | 0.0 |
| `competition_season_id` | 0.0 |
| `match_date` | 0.4 |
| `kickoff` | 57.9 |
| `date_reliability` | 0.0 |
| `status` | 0.0 |
| `home_team_id` | 0.8 |
| `away_team_id` | 0.8 |
| `home_goals` | 0.4 |
| `away_goals` | 0.4 |
| `source_file` | 0.0 |
| `row_sha256` | 0.0 |
| `source_record_id` | 94.8 |
| `canonical_match_id` | 94.8 |

### `fdcouk_providers.csv`

The football-data.co.uk source row and its attribution.

Rows: 1

| Column | % empty |
|---|---|
| `provider_id` | 0.0 |
| `name` | 0.0 |
| `attribution` | 0.0 |
| `url` | 0.0 |

## Matches, teams and people

### `canonical__canonical_result.csv.gz`

Which score observation is the accepted result for each match and score component.

Rows: 1,034,692

| Column | % empty |
|---|---|
| `canonical_result_id` | 0.0 |
| `match_id` | 0.0 |
| `component` | 0.0 |
| `score_observation_id` | 0.0 |
| `precedence_policy_id` | 0.0 |
| `decision_id` | 0.0 |
| `recorded_at` | 0.0 |

### `canonical__competition.csv.gz`

Competitions (league, domestic cup, national tournament, continental club).

Rows: 271

| Column | % empty |
|---|---|
| `competition_id` | 0.0 |
| `name` | 0.0 |
| `competition_kind` | 0.0 |
| `gender` | 0.0 |
| `team_kind` | 0.0 |
| `association_id` | 100.0 |
| `level` | 100.0 |

### `canonical__competition_edition.csv.gz`

A competition in a given season.

Rows: 3,085

| Column | % empty |
|---|---|
| `edition_id` | 0.0 |
| `competition_id` | 0.0 |
| `season_id` | 0.0 |

### `canonical__competition_mapping.csv.gz`

Source competition and season ids mapped to these competitions and seasons.

Rows: 805

| Column | % empty |
|---|---|
| `competition_mapping_id` | 0.0 |
| `provider_competition_id` | 0.0 |
| `competition_id` | 0.0 |
| `scope` | 0.0 |
| `provider_season_id` | 32.5 |
| `season_id` | 32.5 |
| `valid_from` | 32.5 |
| `valid_to` | 32.5 |
| `decision_id` | 0.0 |

### `canonical__match.csv.gz`

One row per match: competition edition, kickoff, home and away team, status.

Rows: 1,066,044

| Column | % empty |
|---|---|
| `match_id` | 0.0 |
| `edition_id` | 42.2 |
| `provider_competition_id` | 0.0 |
| `kickoff_at` | 48.9 |
| `kickoff_on` | 0.0 |
| `kickoff_precision` | 0.0 |
| `home_party_id` | 0.0 |
| `away_party_id` | 0.0 |
| `neutral` | 0.0 |
| `venue_association_id` | 100.0 |
| `status` | 0.0 |
| `decision_id` | 0.0 |

### `canonical__match_outcome.csv.gz`

How each match was decided (regulation, extra time, shootout) and the winner.

Rows: 1,038,721

| Column | % empty |
|---|---|
| `match_id` | 0.0 |
| `decided_by` | 0.0 |
| `extra_time_played` | 0.0 |
| `shootout_played` | 0.0 |
| `regulation_known` | 0.0 |
| `after_extra_time_known` | 0.0 |
| `shootout_score_known` | 0.0 |
| `after_extra_time_observation_id` | 99.8 |
| `shootout_observation_id` | 100.0 |
| `uncertain_final_line_observation_id` | 99.7 |
| `winner_party_id` | 25.7 |
| `classification_basis` | 0.0 |
| `classification_reason` | 0.0 |
| `decision_id` | 0.0 |
| `recorded_at` | 0.0 |

### `canonical__match_source.csv.gz`

Links from each match to the source records it was built from, with match confidence.

Rows: 1,331,065

| Column | % empty |
|---|---|
| `match_id` | 0.0 |
| `source_record_id` | 0.0 |
| `confidence` | 0.0 |
| `method` | 0.0 |
| `decision_id` | 0.0 |

### `canonical__party.csv.gz`

Teams (clubs and national teams).

Rows: 10,809

| Column | % empty |
|---|---|
| `party_id` | 0.0 |
| `party_kind` | 0.0 |
| `parent_party_id` | 100.0 |
| `founded_on` | 100.0 |
| `dissolved_on` | 100.0 |
| `successor_party_id` | 100.0 |

### `canonical__party_name.csv.gz`

Team names, with a folded (lower-case, accent-free) version for matching.

Rows: 10,809

| Column | % empty |
|---|---|
| `party_name_id` | 0.0 |
| `party_id` | 0.0 |
| `name` | 0.0 |
| `name_fold` | 0.0 |
| `name_kind` | 0.0 |
| `valid_from` | 100.0 |
| `valid_to` | 100.0 |
| `decision_id` | 0.7 |

### `canonical__person.csv.gz`

People (players and managers) who appear in the OpenPlay or eatpizzanot data.

Rows: 6,784

| Column | % empty |
|---|---|
| `person_id` | 0.0 |
| `decision_id` | 0.0 |

### `canonical__person_name.csv.gz`

Names for each person.

Rows: 6,784

| Column | % empty |
|---|---|
| `person_name_id` | 0.0 |
| `person_id` | 0.0 |
| `name` | 0.0 |
| `name_kind` | 0.0 |
| `decision_id` | 0.0 |

### `canonical__score_observation.csv.gz`

Every score reported by a source (home_goals, away_goals) for a given component.

Rows: 1,907,840

| Column | % empty |
|---|---|
| `score_observation_id` | 0.0 |
| `source_record_id` | 0.0 |
| `component` | 0.0 |
| `home_goals` | 0.0 |
| `away_goals` | 0.0 |
| `decision_id` | 100.0 |

### `canonical__score_observation_match.csv.gz`

Links score observations to matches.

Rows: 1,047,224

| Column | % empty |
|---|---|
| `score_observation_id` | 0.0 |
| `component` | 0.0 |
| `match_id` | 0.0 |

### `canonical__season_mapping.csv.gz`

Source season ids mapped to seasons.

Rows: 86

| Column | % empty |
|---|---|
| `provider_season_id` | 0.0 |
| `season_id` | 0.0 |
| `decision_id` | 0.0 |

## Reference tables

### `metadata__association.csv.gz`

Football associations (empty in this release).

Rows: 0

| Column | % empty |
|---|---|
| `association_id` | 0.0 |
| `name` | 0.0 |
| `fifa_code` | 0.0 |
| `valid_from` | 0.0 |
| `valid_to` | 0.0 |

### `metadata__party_association.csv.gz`

Team to association links (empty in this release).

Rows: 0

| Column | % empty |
|---|---|
| `party_association_id` | 0.0 |
| `party_id` | 0.0 |
| `association_id` | 0.0 |
| `relationship` | 0.0 |
| `valid_from` | 0.0 |
| `valid_to` | 0.0 |
| `decision_id` | 0.0 |
| `source_record_id` | 0.0 |

### `metadata__precedence_policy.csv.gz`

Name of the rule set used to pick one result when sources disagree.

Rows: 1

| Column | % empty |
|---|---|
| `precedence_policy_id` | 0.0 |
| `name` | 0.0 |
| `created_at` | 0.0 |

### `metadata__precedence_rank.csv.gz`

Source ranking inside that rule set (1 = preferred).

Rows: 3

| Column | % empty |
|---|---|
| `precedence_policy_id` | 0.0 |
| `provider_id` | 0.0 |
| `rank` | 0.0 |

### `metadata__research_policy.csv.gz`

Rule flags for how inferred or uncertain results are treated.

Rows: 1

| Column | % empty |
|---|---|
| `policy_id` | 0.0 |
| `name` | 0.0 |
| `allow_inferred_ordinary` | 0.0 |
| `allow_inferred_uncertain` | 0.0 |
| `allow_unknown` | 0.0 |

### `metadata__season.csv.gz`

Seasons with start and end dates (1993/1994 to 2026/2027).

Rows: 34

| Column | % empty |
|---|---|
| `season_id` | 0.0 |
| `label` | 0.0 |
| `starts_on` | 0.0 |
| `ends_on` | 0.0 |

### `metadata__source.csv.gz`

The sources behind the match tables, with licence, attribution and link. `provider_id` here is the id used in `metadata__precedence_rank`.

Rows: 5

| Column | % empty |
|---|---|
| `provider_id` | 0.0 |
| `name` | 0.0 |
| `licence` | 0.0 |
| `attribution` | 0.0 |
| `url` | 20.0 |

## OpenPlay

### `openplay__openplay_card.csv.gz`

Yellow and red cards from OpenPlay events.

Rows: 115,499

| Column | % empty |
|---|---|
| `provider_match_id` | 0.0 |
| `provider_event_id` | 0.0 |
| `provider_team_id` | 0.0 |
| `provider_player_id` | 2.0 |
| `card` | 0.0 |
| `minute` | 0.0 |
| `second` | 0.0 |
| `period` | 0.0 |
| `canonical_match_id` | 5.6 |

### `openplay__openplay_event_load.csv.gz`

Row counts per loaded OpenPlay event file.

Rows: 125

| Column | % empty |
|---|---|
| `source_file` | 0.0 |
| `rows_read` | 0.0 |
| `rows_inserted` | 0.0 |
| `status` | 0.0 |
| `finished_at` | 0.0 |

### `openplay__openplay_event_source.csv.gz`

Event counts per OpenPlay match file.

Rows: 25,100

| Column | % empty |
|---|---|
| `provider_match_id` | 0.0 |
| `canonical_match_id` | 0.0 |
| `source_file` | 0.0 |
| `event_count` | 0.0 |
| `dataset_version` | 0.0 |
| `licence` | 0.0 |
| `attribution` | 0.0 |

### `openplay__openplay_fixture.csv.gz`

OpenPlay fixtures with their linked match_id and team ids.

Rows: 25,531

| Column | % empty |
|---|---|
| `provider_match_id` | 0.0 |
| `canonical_match_id` | 0.0 |
| `has_events` | 0.0 |
| `event_availability` | 0.0 |
| `provider_home_team_id` | 1.7 |
| `provider_away_team_id` | 1.7 |
| `canonical_home_party_id` | 0.0 |
| `canonical_away_party_id` | 0.0 |
| `provider_competition` | 0.0 |
| `provider_season` | 0.0 |
| `canonical_competition` | 0.5 |
| `canonical_season` | 0.5 |
| `dataset_version` | 0.0 |
| `licence` | 0.0 |
| `attribution` | 0.0 |
| `matching_evidence` | 0.0 |

### `openplay__openplay_formation.csv.gz`

Formations, line-ups, captains and substitutions per team per period.

Rows: 245,468

| Column | % empty |
|---|---|
| `provider_match_id` | 0.0 |
| `provider_team_id` | 0.0 |
| `side` | 0.0 |
| `formation` | 0.0 |
| `formation_id` | 0.0 |
| `period` | 0.0 |
| `start_minute` | 0.0 |
| `end_minute` | 0.0 |
| `captain_player_id` | 0.0 |
| `sub_on_player_id` | 44.8 |
| `sub_off_player_id` | 44.8 |
| `player_ids` | 0.0 |
| `formation_slots` | 0.0 |
| `canonical_match_id` | 5.5 |

### `openplay__openplay_player_stat.csv.gz`

Per-player match stats: minutes, goals, assists, shots, key passes.

Rows: 733,824

| Column | % empty |
|---|---|
| `provider_match_id` | 0.0 |
| `provider_player_id` | 0.0 |
| `provider_team_id` | 0.0 |
| `canonical_match_id` | 0.0 |
| `started` | 0.0 |
| `starter_source` | 0.0 |
| `position` | 0.0 |
| `minutes` | 0.0 |
| `goals` | 0.0 |
| `assists` | 0.0 |
| `shots` | 0.0 |
| `shots_on_target` | 0.0 |
| `key_passes` | 0.0 |
| `subbed_on` | 0.0 |
| `subbed_off` | 0.0 |
| `source_file` | 0.0 |
| `dataset_version` | 0.0 |
| `licence` | 0.0 |

### `openplay__openplay_qualifier_load.csv.gz`

Row counts per loaded OpenPlay qualifier file.

Rows: 125

| Column | % empty |
|---|---|
| `source_file` | 0.0 |
| `event_rows` | 0.0 |
| `q_columns` | 0.0 |
| `expected_rows` | 0.0 |
| `copied_rows` | 0.0 |
| `rows_inserted` | 0.0 |
| `zero_numeric_dropped` | 0.0 |
| `status` | 0.0 |
| `seconds` | 0.0 |
| `finished_at` | 0.0 |

### `openplay__openplay_shot.csv.gz`

Every shot with pitch location, goal-mouth location, body part and result.

Rows: 631,556

| Column | % empty |
|---|---|
| `provider_match_id` | 0.0 |
| `event_id` | 0.0 |
| `event_id_sub` | 0.0 |
| `canonical_match_id` | 0.0 |
| `provider_team_id` | 0.0 |
| `provider_player_id` | 0.0 |
| `period` | 0.0 |
| `minute` | 0.0 |
| `second` | 0.0 |
| `x` | 0.0 |
| `y` | 0.0 |
| `goal_mouth_y` | 11.5 |
| `goal_mouth_z` | 11.5 |
| `body_part` | 0.0 |
| `play_pattern` | 0.0 |
| `shot_zone` | 0.0 |
| `shot_target` | 10.9 |
| `result` | 0.0 |
| `is_goal` | 0.0 |
| `is_own_goal` | 0.0 |
| `is_shootout` | 0.0 |
| `source_file` | 0.0 |
| `dataset_version` | 0.0 |
| `licence` | 0.0 |

### `openplay__openplay_team_link.csv.gz`

OpenPlay team ids linked to team (party) ids.

Rows: 344

| Column | % empty |
|---|---|
| `provider_team_id` | 0.0 |
| `canonical_party_id` | 0.0 |
| `party_conflict` | 0.0 |
| `team_name` | 0.0 |
| `dataset_version` | 0.0 |

### `openplay__openplay_unconfirmed_link.csv.gz`

OpenPlay matches linked by a looser rule, with the evidence.

Rows: 131

| Column | % empty |
|---|---|
| `provider_match_id` | 0.0 |
| `home_party_id` | 0.0 |
| `away_party_id` | 0.0 |
| `canonical_match_id` | 0.0 |
| `link_outcome` | 0.0 |
| `method` | 0.0 |
| `home_name` | 0.0 |
| `away_name` | 0.0 |
| `match_date` | 0.0 |
| `home_goals` | 0.0 |
| `away_goals` | 0.0 |
| `resolved_at` | 0.0 |

### `openplay__openplay_unconfirmed_match.csv.gz`

OpenPlay matches that could not be linked to a match_id.

Rows: 1,316

| Column | % empty |
|---|---|
| `provider_match_id` | 0.0 |
| `competition` | 0.0 |
| `season` | 0.0 |
| `match_date` | 0.0 |
| `home_team` | 0.0 |
| `away_team` | 0.0 |
| `home_goals_90` | 0.0 |
| `away_goals_90` | 0.0 |
| `status_code` | 0.0 |
| `n_events` | 0.0 |
| `source_file` | 0.0 |

### `openplay__openplay_event_events_<competition>_<season>.csv.gz` (125 files)

Every OpenPlay match event (passes, shots, tackles, and so on) with pitch coordinates, one file per competition and season.

Rows across all files: 41,594,510

| Column | % empty |
|---|---|
| `source_file` | 0.0 |
| `provider_match_id` | 0.0 |
| `event_id` | 0.0 |
| `event_id_sub` | 0.0 |
| `event_type` | 0.0 |
| `period` | 0.0 |
| `minute` | 0.0 |
| `second` | 0.2 |
| `expanded_minute` | 0.0 |
| `provider_team_id` | 0.0 |
| `provider_player_id` | 1.0 |
| `outcome` | 0.0 |
| `x` | 0.0 |
| `y` | 0.0 |
| `end_x` | 34.5 |
| `end_y` | 34.5 |
| `is_shot` | 0.0 |
| `is_goal` | 0.0 |
| `body_part` | 95.2 |
| `play_pattern` | 98.2 |
| `related_event_id` | 97.8 |
| `related_player_id` | 97.8 |
| `team_event_id` | 0.1 |

### `openplay__openplay_event_qualifier_events_<competition>_<season>.csv.gz` (22 files)

Event qualifiers (extra attributes such as pass length or body part) as name and value pairs, one file per competition and season.

Rows across all files: 7,893,166

| Column | % empty |
|---|---|
| `source_file` | 0.0 |
| `provider_match_id` | 0.0 |
| `event_id` | 0.0 |
| `event_id_sub` | 0.0 |
| `event_type` | 0.0 |
| `qualifier_name` | 0.0 |
| `qualifier_value` | 0.0 |

## Files in the git repository

| Path | Contents |
|---|---|
| `images/wikimedia/` | Badges, player, manager and stadium images from Wikimedia Commons, in two sizes (`-sm`, `-md`) as WebP. |
| `images/ATTRIBUTION.csv` | One row per image: kind, id, name, licence, author, credit line, Commons source URL and file name. |
| `canonical/id_map.json` | Team id remaps and synthetic ids used when joining sources. |
