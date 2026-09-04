# SQL Data Warehouse

This directory contains the SQL Server data warehouse developed for the NPFL Data Analytics project.

The SQL layer was used to structure, clean and prepare the football data for downstream analysis in Python and Power BI.

## Warehouse architecture

The warehouse follows a dimensional structure using separate staging, dimension and fact schemas:

    Source CSV Data
          ↓
       Staging
          ↓
      Dimensions
          ↓
        Facts
          ↓
    Python / Power BI

The warehouse was designed to separate descriptive entities from measurable football performance data and provide a structured analytical foundation for the project.

## Schemas

Three schemas were created:

- `stg` — staging and temporary data preparation
- `dim` — dimension tables containing descriptive attributes
- `fact` — fact tables containing football performance metrics

The schema structure provides a clear separation between source preparation, descriptive entities and analytical measures.

## Dimension tables

The warehouse contains six primary dimension tables.

### `dim.dim_states`

Contains Nigerian state-level geographic and demographic information.

Key attributes include:

- State key
- State name
- State code
- Geopolitical zone
- Zone code
- State capital
- Population
- Population rank

This dimension supports the geographic and population analysis performed in Python and Power BI.

### `dim.dim_seasons`

Contains NPFL season-level information.

Key attributes include:

- Season key
- Season
- Status
- Number of clubs
- Total matches
- Start date
- End date
- Abridged-season indicator
- Season order

The season dimension provides the basis for season-aware analysis across the six-season study period.

### `dim.dim_players`

Contains player-level descriptive information.

Key attributes include:

- Player key
- Full name
- Age
- Birthday
- Position
- Nationality

Player performance measures are stored separately in the player fact table.

### `dim.dim_dates`

Contains calendar attributes used for time-based analysis.

Key attributes include:

- Date key
- Full date
- Day number
- Day name
- Week number
- Month number
- Month name
- Quarter number
- Year number
- Weekend indicator

The date dimension provides a dedicated time structure for analytical reporting.

### `dim.dim_stadiums`

Contains stadium and venue information.

Key attributes include:

- Stadium key
- Stadium name
- Capacity
- State
- State key

A staging table was used when loading stadium data because some capacity values required conversion before being inserted into the final dimension.

### `dim.dim_teams`

Contains NPFL club information.

Key attributes include:

- Team key
- Team name
- State
- State key

Teams are linked to Nigerian states through the state key, allowing club performance to be analysed geographically.

## Fact tables

The warehouse contains three major fact tables.

### `fact.fact_matches`

Contains match-level NPFL data.

The table includes:

- Match key
- Date
- Season
- Stadium
- Home team
- Away team
- Game week
- Pre-match PPG
- Home and away PPG
- Match goals
- Half-time goals
- Expected goals
- Match outcome-related metrics
- Betting odds
- BTTS-related odds

Foreign-key relationships connect match records to:

- `dim.dim_dates`
- `dim.dim_seasons`
- `dim.dim_stadiums`
- `dim.dim_teams`

A staging table was used during the load process to allow fields such as game week to be safely converted before insertion into the final fact table.

## `fact.fact_player_stats`

Contains player performance by team and season.

Key measures include:

- Minutes played
- Appearances
- Goals
- Assists
- Clean sheets
- Goals conceded
- Yellow cards
- Red cards
- Shots faced
- xG
- xA
- Non-penalty xG

The table uses a composite player-team-season key to represent a player's statistical record within a particular team and season.

A staging table was used during ingestion to allow source values to be converted into appropriate SQL data types.

`TRY_CAST()` was used for fields where the source data could contain non-numeric values.

Duplicate player-team-season records were handled using `SELECT DISTINCT` during the final insertion.

## `fact.fact_team_stats`

Contains team-level performance statistics by season.

This is the largest analytical fact table in the warehouse and contains metrics covering:

- Matches played
- Wins, draws and losses
- Points per game
- League position
- Performance rank
- Goals scored
- Goals conceded
- Goal difference
- Home performance
- Away performance
- Clean sheets
- BTTS
- Failed to score
- First team to score
- Shots
- Shots on target
- Possession
- Fouls
- Cards
- Corners
- First-half performance
- Second-half performance
- Goal timing
- Expected goals
- Win percentages
- Clean-sheet percentages
- Half-time performance
- Second-half performance
- Other team-level performance indicators

The table contains both overall and home/away versions of many measures, allowing detailed team-performance analysis without repeatedly reconstructing these statistics from match-level records.

## Data preparation and cleaning

The SQL warehouse includes several data-preparation techniques.

### Staging tables

Temporary staging tables were used when source data required transformation before loading into the final warehouse tables.

For example, stadium capacity was initially loaded as text because the source contained non-numeric values.

The staging data was then converted before insertion into the final dimension.

### Data type conversion

`TRY_CAST()` was used to safely convert source fields into appropriate SQL data types.

Examples include:

- Game week → integer
- Stadium capacity → integer
- Player shots → integer
- Player xG → decimal
- Player xA → decimal
- Player non-penalty xG → decimal

This prevents problematic source values from causing the entire load process to fail.

### Duplicate handling

Player statistics were loaded using `SELECT DISTINCT` to prevent duplicate player-team-season records from being inserted into the final fact table.

### Referential integrity

Foreign-key constraints were created to maintain relationships between fact and dimension tables.

Examples include:

    fact_matches → dim_dates
    fact_matches → dim_seasons
    fact_matches → dim_stadiums
    fact_matches → dim_teams

    fact_player_stats → dim_players
    fact_player_stats → dim_seasons
    fact_player_stats → dim_teams

    fact_team_stats → dim_teams
    fact_team_stats → dim_seasons

This provides a controlled relational structure for downstream analysis.

## Analytical data model

The warehouse supports a dimensional/star-schema style analytical model.

At a high level:

    dim_states
         ↑
    dim_teams
         ↑
    fact_team_stats
         ↑
    dim_seasons

And:

    dim_players ───────┐
                       ↓
              fact_player_stats
                       ↑
                  dim_teams
                       ↑
                  dim_seasons

Match analysis follows:

    dim_dates ─────────┐
    dim_seasons ───────┤
    dim_stadiums ──────┤
    dim_teams ─────────┤
                       ↓
                 fact_matches

This structure allows the same descriptive dimensions to be reused across different analytical areas.

## SQL techniques demonstrated

The SQL work demonstrates practical data-engineering and analytical SQL skills, including:

- Schema creation
- Table creation
- Primary keys
- Foreign keys
- Temporary staging tables
- `BULK INSERT`
- Data type conversion
- `TRY_CAST()`
- `SELECT DISTINCT`
- Constraint creation
- Relational data modelling
- Data validation
- Record-count reconciliation
- Separation of staging, dimension and fact layers

## Data validation

A final verification query was included to compare record counts across the warehouse tables.

This provides a simple validation step to confirm that the expected tables were populated after the loading process.

The validation covers:

- Teams
- Stadiums
- Seasons
- Dates
- Players
- States
- Matches
- Player statistics
- Team statistics

## Relationship to Python and Power BI

The SQL warehouse represents the structured data layer of the project.

The overall analytical workflow was:

    Licensed FootyStats Data
             ↓
       Data Preparation
             ↓
       SQL Data Warehouse
             ↓
        Python Analysis
             ↓
     Statistical / ML Analysis
             ↓
        Power BI / DAX
             ↓
       Analytical Report
             ↓
     Key Findings & Recommendations

SQL therefore provided the relational foundation on which the Python analysis and Power BI reporting were built.

## Data availability

The underlying football datasets used in the warehouse were obtained through a paid FootyStats subscription.

The original datasets and database records are therefore not redistributed through this repository.

The public SQL code is intended to demonstrate:

- Warehouse design
- Data modelling
- Transformation logic
- Data-loading techniques
- Data-quality handling
- Referential integrity
- Analytical data preparation

Source-data paths should be replaced with local placeholders when using the scripts outside the original development environment.

## Security and reproducibility

The repository intentionally does not include:

- SQL database backups
- `.bak` files
- Full database dumps
- Source CSV files
- Cleaned copies that substantially reproduce the licensed source data

## Role within the project

The SQL warehouse forms the central structured-data layer of the NPFL Data Analytics project.

It demonstrates the transition from raw football datasets into a relational analytical warehouse that can support repeatable analysis across:

- Seasons
- Teams
- Players
- Matches
- Stadiums
- Nigerian states
- Geopolitical zones
- Population
- Football performance

The resulting warehouse provides the foundation for the project's Python statistical analysis and Power BI reporting.
