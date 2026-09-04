# Data

This directory is reserved for the datasets used throughout the NPFL Data Analytics project.

## Expected contents

The `data/` directory would ordinarily contain the source and prepared datasets used for the analysis, including data relating to:

- NPFL matches and match results
- Team performance and statistics
- Player performance and statistics
- Seasons and league structure
- Stadiums and match venues
- Nigerian states and population
- Other supporting datasets used during the analysis and modelling process

The data was subsequently cleaned, transformed and structured for use across the project's **SQL warehouse, Python analysis and Power BI reporting layers**.

## Why the data is not included

The underlying datasets were obtained through a **paid FootyStats subscription**. Because the downloaded data is subject to FootyStats' terms of use and redistribution restrictions, the original or FootyStats-derived datasets are **not publicly redistributed in this repository**.

This also applies to cleaned and transformed versions that substantially reproduce the original dataset.

As a result, this directory has intentionally been left empty.

## Reproducibility

Although the source data is not included, the repository contains the project's analytical work and methodology, including:

- SQL database and warehouse scripts
- Data transformation logic
- Python analysis and notebooks
- Power BI report development
- DAX calculations
- Analytical findings and recommendations

Hopefully this allows the technical approach and analytical process to be reviewed without publicly redistributing the licensed source data.

> **Note:** The absence of the datasets from this repository does not indicate that the data was unavailable during development. The analysis was performed using legitimately obtained licensed data.
