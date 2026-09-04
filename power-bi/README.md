# Power BI Report

This directory contains the exported Power BI report produced as part of the NPFL Data Analytics project.

## Report

The Power BI report presents the results of the six-season NPFL analysis through a series of analytical report pages covering:

- NPFL league overview
- Club performance and home advantage
- Geography, population and club success
- League competitiveness and club trends
- Player performance and goal contribution
- Stadium and match environment

The report was designed to move beyond descriptive reporting by combining performance metrics, statistical analysis and comparative visualisation to answer specific analytical questions about the league.

## Technical implementation

The Power BI report demonstrates the use of:

- Relational data modelling
- Fact and dimension tables
- DAX measures and calculated columns
- Season-aware calculations
- Ranking and performance calculations
- Filter context and context-aware measures
- Conditional formatting
- Matrix and heatmap analysis
- Scatter plots for relationship analysis
- Time-series comparisons
- Multi-page analytical report design
- Data validation and quality handling
- Analytical storytelling

Examples of calculated metrics developed for the report include:

- League points
- League position
- Top-5 finishes
- Goals per 90
- Home PPG
- Away PPG
- Home advantage
- Match count
- Competitiveness measures

## Report distribution

The original `.pbix` file is not included in this repository because it contains embedded data obtained from a paid FootyStats subscription.

The PDF export is provided instead as a static representation of the completed Power BI report. This allows the analytical output and report design to be reviewed without publicly distributing the underlying licensed dataset.

## Data source

The analysis was performed using licensed football data obtained through FootyStats.

The underlying source and transformed datasets are intentionally not redistributed in this repository. See the `data/` directory for further information.

## Relationship to the rest of the project

The Power BI report represents the visualisation and reporting layer of the project:

    Licensed football data
            ↓
       SQL Warehouse
            ↓
      Python Analysis
            ↓
        DAX / Power BI
            ↓
      Analytical Report
            ↓
       Key Insights

The accompanying analytical findings and recommendations are available in the `key-insights/` directory.
