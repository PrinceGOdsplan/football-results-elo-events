# Sources and attribution

## BeyondELO

- Files: `beyondelo_rating.csv.gz`, and the ratings inside `elo_prematch.csv.gz`
- Source: BeyondELO public API and season files, https://beyondelo.com
- Licence: CC BY 4.0
- Credit: beyondELO (https://beyondelo.com)

## OpenPlay

- Files: `openplay__*.csv.gz`
- Source: OpenPlay data-v0.1.0
- Licence: CC BY 4.0
- Credit: openplay (Noah Bair)
- The `licence` and `attribution` columns in the OpenPlay files repeat this on every row.

## football-data.co.uk

- Files: `fdcouk_results.csv.gz`, `fdcouk_providers.csv`, and results inside the `canonical__*` tables
- Source: https://www.football-data.co.uk/ (field notes: https://www.football-data.co.uk/notes.txt)
- Credit: football-data.co.uk

## Other result sources

### schochastics/football-data

- Files: results inside the `canonical__*` tables
- Source: https://github.com/schochastics/football-data
- Licence: Open Data Commons Attribution License (ODC-By 1.0)
- Credit: schochastics/football-data

### eatpizzanot/soccer-dataset

- Files: results, teams and people inside the `canonical__*` tables
- Source: https://huggingface.co/datasets/eatpizzanot/soccer-dataset
- Licence: CC BY 4.0
- Credit: eatpizzanot

The `canonical__*` match tables combine football-data.co.uk, schochastics/football-data, eatpizzanot, OpenPlay and BeyondELO. All five are listed in `metadata__source.csv.gz`, and the order used when result sources disagree is in `metadata__precedence_rank.csv.gz`.

## Wikimedia Commons images

- Files: `images/wikimedia/`
- Source: Wikimedia Commons
- Licence: per file, recorded in `images/ATTRIBUTION.csv` (CC BY 2.0 to 4.0, CC BY-SA 2.0 to 4.0, CC0, public domain)
- Credit: use the `credit` column for each image, and keep CC BY-SA images under the same licence

## My own work

- Files: the `canonical__*` compilation and links, `training_labels.csv.gz`, `elo_prematch.csv.gz` (the match linking), `metadata__*`, `canonical/id_map.json`, and all documentation
- Licence: CC BY 4.0 (see LICENSE)
- Credit: PrinceGOdsplan, https://github.com/PrinceGOdsplan/football-results-elo-events
