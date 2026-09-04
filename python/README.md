# Python Analysis

This directory contains the Python-based analytical work completed as part of the NPFL Data Analytics project.

Python was used primarily for data exploration, preparation, statistical analysis, feature engineering, player and team performance analysis, and predictive modelling before the results were incorporated into the Power BI reporting layer.

## Analytical workflow

The Python analysis followed an end-to-end analytical workflow:

1. Data loading and inspection
2. Data quality assessment
3. Cleaning and preparation
4. Feature engineering
5. Team performance aggregation
6. Player performance analysis
7. Home and away performance analysis
8. Geographic and population analysis
9. League competitiveness analysis
10. Statistical testing
11. Player and team efficiency analysis
12. Predictive modelling
13. Model evaluation and interpretation
14. Preparation of analytical outputs for Power BI

## Team performance analysis

Team-level analysis examined performance across the six-season period using metrics including:

- Matches played
- Wins
- Draws
- Losses
- Goals scored
- Goals conceded
- Goal difference
- Points
- Points per game (PPG)
- Home PPG
- Away PPG
- League position

League points were derived using the standard scoring system:

    Points = (Wins × 3) + Draws

Team performance was then aggregated across seasons to identify sustained high-performing clubs and changes in performance over time.

## Home advantage analysis

Home and away performance was analysed separately to measure the strength of home advantage within the NPFL.

The analysis compared:

- Home PPG
- Away PPG
- Home and away wins
- Home and away goals
- Home advantage PPG
- Home-to-away PPG ratio

This was used to evaluate how strongly match outcomes were associated with playing at home.

## Geographic and population analysis

Club performance was examined alongside geographic and demographic information, including:

- Nigerian state
- Geopolitical zone
- Population
- Population rank
- Club performance
- Average PPG
- Total points

Statistical tests were then used to determine whether population size was associated with club performance.

Pearson correlation was used to examine population against average PPG, while Spearman correlation was used to examine population against total points.

The analysis found no statistically significant relationship between population size and club performance within the project sample.

## League competitiveness analysis

League competitiveness was evaluated across all six seasons using both total points and PPG.

The analysis calculated:

- Maximum PPG
- Minimum PPG
- PPG gap
- PPG standard deviation
- PPG coefficient of variation
- Total-points gap
- Total-points standard deviation
- Total-points coefficient of variation

The results were compared across seasons to determine whether competitive balance was changing over time.

The 2022/23 season was treated as an important analytical exception because it was an abridged season.

## Club performance trends

Club performance was tracked across seasons using PPG and league position.

The analysis was used to identify:

- Consistently strong clubs
- Improving clubs
- Declining clubs
- Start-to-end performance changes
- Clubs with repeated Top-5 finishes

This provided the basis for the sustained club-success analysis presented in Power BI.

## Player performance analysis

Player-level analysis focused on attacking contribution and scoring efficiency.

Metrics included:

- Goals
- Appearances
- Minutes played
- Goals per 90
- Position
- Goal contribution by position
- Expected goals (xG) and related metrics where available

Goals per 90 was calculated as:

    Goals per 90 = (Goals × 90) / Minutes played

A minimum playing-time threshold was applied to the scoring-efficiency analysis to reduce the distortion caused by players with very limited appearances.

## xG efficiency

Team scoring output was compared with modelled expected goals to identify differences between actual goals and expected goals.

An actual-goals-to-xG ratio was used as an efficiency indicator.

This metric was treated cautiously because the underlying xG model requires appropriate calibration and validation before the ratio can be interpreted as a definitive measure of finishing ability.

## First-half and second-half analysis

Match performance was also examined across different stages of the match.

First-half and second-half performance metrics were compared to identify teams that:

- Improved after half-time
- Declined after half-time
- Maintained relatively stable performance

This provided an additional view of team performance beyond final match results.

## Predictive modelling

A Random Forest classification model was developed to investigate the relationship between team and match-performance features and match outcomes.

Features included measures such as:

- PPG differential
- Win percentage
- Goals scored per match
- Goals conceded per match
- Clean-sheet percentage
- Shots on target
- Possession
- xG for
- xG against

Feature importance was examined to identify which variables contributed most strongly to the model's predictions.

The model achieved approximately 64.9% overall accuracy.

However, model evaluation identified substantial class imbalance. The model strongly favoured home-win predictions while performing poorly in identifying draws and away wins.

Consequently, the accuracy figure was not treated as evidence of balanced predictive performance.

## Data quality considerations

The analysis also involved identifying and accounting for limitations within the source data, including:

- Duplicate player records
- Missing stadium information
- Incomplete advanced player statistics
- Inconsistent league-position values
- Geographic mapping limitations
- Different numbers of matches across seasons
- The abridged 2022/23 season
- Limitations in the underlying xG data

Where appropriate, calculations were reconstructed from more reliable underlying fields rather than relying blindly on pre-existing derived columns.

## Relationship to the Power BI report

Python represents the main analytical and statistical layer of the project.

The outputs from the Python analysis were subsequently incorporated into the Power BI reporting layer for visual exploration and communication.

The overall project workflow can therefore be represented as:

    Licensed FootyStats Data
            ↓
      Data Preparation
            ↓
      SQL Data Warehouse
            ↓
       Python Analysis
            ↓
    Statistical & ML Analysis
            ↓
        Power BI / DAX
            ↓
      Analytical Report
            ↓
      Key Findings & Recommendations

## Data availability

The original datasets used for the analysis were obtained through a paid FootyStats subscription and are not included in this repository due to data redistribution restrictions.

The public Python notebooks therefore focus on demonstrating the analytical methodology and code rather than redistributing the underlying licensed datasets.

Where necessary, dataset paths or loading sections may reference files that are intentionally excluded from the public repository.

## Tools and libraries

The Python analysis primarily used the Python data-analysis ecosystem, including tools for:

- Data manipulation and preparation
- Statistical analysis
- Data visualisation
- Machine learning
- Model evaluation

The notebooks document the specific analytical workflow used to produce the project's findings.
