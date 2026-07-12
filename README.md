# NBA Players Data 2022-2023

A short Jupyter notebook that scrapes, cleans, and structures per-game NBA
player statistics for the 2022-23 season, producing a tidy CSV ready for
downstream analysis.

## Data

The notebook pulls the "Per Game" stats table directly from
[Basketball-Reference's 2022-23 NBA season page](https://www.basketball-reference.com/leagues/NBA_2023_per_game.html)
using `requests` and `BeautifulSoup`, then saves the result as
`nba_2022_2023.csv`. This is the same per-game data distributed on Kaggle as
[NBA Players Data 2022-2023](https://www.kaggle.com/datasets/bryanchungweather/nba-players-data-2022-2023).

Each row is one player-team stint for the season (Player, Pos, Age, Tm, and
24 counting/percentage columns such as G, MP, FG%, TRB, AST, STL, BLK, TOV,
and PTS).

## Method / What was done

1. Scrape the per-game stats table from Basketball-Reference and load it into
   a pandas DataFrame with the 29 expected columns.
2. Write the raw scraped table to `nba_2022_2023.csv`.
3. Handle players who were traded mid-season: Basketball-Reference lists a
   row per team plus a combined "TOT" (total) row for any player who
   changed teams. The notebook identifies these duplicate player names and
   keeps only the "TOT" row for each, so every player appears once with
   season-long totals.
4. Convert the counting and percentage columns from strings to numeric
   types so the data is ready for statistical analysis.

## Key findings

- The scrape returned 679 player-team rows across 29 columns for the 2022-23
  season.
- 140 of those rows were per-team duplicates from mid-season trades; after
  keeping only the combined "TOT" row for traded players, the cleaned
  dataset contains 539 unique players.

## Repository structure

- `NBA_Players_Data_2022_2023.ipynb`: the notebook that scrapes
  Basketball-Reference, exports the raw CSV, and de-duplicates traded
  players.
- `nba_2022_2023.csv`: the raw scraped output (679 rows, one per player-team
  stint) written by the notebook.
- `LICENSE`: MIT license.
- `.gitignore`: standard Python/Jupyter ignores.

## How to run

Written for Python 3.11 (library versions are historical, from 2023, rather
than pinned). Main libraries used:

- `requests`
- `beautifulsoup4`
- `pandas`

Install them, then open `NBA_Players_Data_2022_2023.ipynb` in Jupyter and run
all cells in order. The notebook makes a live HTTP request to
Basketball-Reference, so it requires an internet connection; the exact
per-game numbers returned may drift slightly if the source page is updated
after a season's stats are finalized.

## License

Released under the MIT License. See `LICENSE` for details.
