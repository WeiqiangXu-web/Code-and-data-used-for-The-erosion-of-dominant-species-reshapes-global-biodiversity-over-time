# BioTIME 2.0 Abundance-Weighted Population Trends

reproducable code for of 'Disproportionate declines of formerly abundant species underlie insect loss' Reproducible code for of 'The erosion of dominant species reshapes global biodiversity over time'. This repository contains the scripts used to process data, fit models, and create visualizations for examining how population trends vary across different abundance classes in marine, terrestrial, and freshwater ecosystems.

**files and their functions:**

Data Processing and Preparation

-   `'01_Preprocess and rarefy data.R': Handles the BioTIME 2.0 database, filters data, creates spatial grids, performs resampling, and calculates diversity indices. Generates basic datasets for further analysis.`
-   `'FUNCTION calculate metrics.R': Contains functions for calculating various biodiversity metrics, including diversity indices, evenness, and abundance distributions. Used to add zero counts for species not observed in some years but present in others. This script was developed by van Klink et al. 2024 https://doi.org/10.1038/s41586-023-06861-4`

Modeling

-   `'02_Population models.R': Analyzes population trends using INLA hierarchical Bayesian models. Focuses on examining dynamics across different abundance classes. Models require ~200GB RAM and may take several hours to complete per model.`

-   `'02.1_Extract effects.R': Extracts and processes posterior distributions from INLA models. Performs two main tasks: 1) extracting fixed and random effects for taxonomic analysis, and 2) calculating abundance-weighted population trends. Requires substantial memory (50-200GB).`

-   `'03_Abundance models.R': Analyzes community-level abundance trends across different realms (Marine, Terrestrial, Freshwater). Uses INLA for hierarchical Bayesian modeling with multiple random effects levels. Requires ~100GB RAM.`

Analysis and Attribution

-   `'04_Attribution analysis.R': Performs attribution analysis to link biodiversity trends with environmental drivers. Extracts and processes temperature data (HadISST for marine, CRU TS for terrestrial) and human footprint data, then analyzes relationships across realms and abundance classes.`

Sensitivity Analysis

-   `'06_Sensitivity analysis.R': Performs five sensitivity analyses: 1) Community metrics, 2) Time series length sensitivity, 3) Zero abundance sensitivity, 4) SAD binning sensitivity, and 5) Regression-to-mean sensitivity. Results validate the robustness of the main findings.`

Visualization

-   `'05_plot_main_figure.R': Generates all figures for the main text and supplementary materials. Visualizes results from population and community trend analyses, including abundance trends, taxonomic patterns, and attribution analyses.`

**Data**

This repository does not include the BioTIME 2.0 database directly. The database can be accessed through the **Dornelas *et al*. 2025** (<https://doi.org/10.1111/geb.70003>). The intermediate datasets generated during analysis are:

-   **01_bt_Intcount_species_grid.Rdata**: Filtered BioTIME 2.0 data containing integer counts at species resolution with spatial grid information.
-   **01_diversity_data.Rdata**: Contains various diversity metrics (richness, Shannon, Simpson, Hill numbers) calculated for each assemblage and year.
-   **01_meta_info.Rdata**: Contains metadata information for each assemblage, including geographic coordinates, taxonomic information, and study identifiers.
-   **02_Population_data.Rdata**: Main population dataset containing abundance values classified into abundance classes based on first-year relative abundance. Used for population trend modeling.
-   **02.1_abundance_weighted.Rdata**: Contains abundance-weighted trend estimates that account for species abundance distributions in the calculation of community-level trends.
-   **02.1_posterior_effects.Rdata**: Contains posterior distributions of fixed and random effects from population models, including realm and taxonomic effects.
-   **03_Abundance_data.Rdata**: Community-level abundance data used for modeling total abundance trends across realms.
-   **03_Abundance_posterior.Rdata**: Contains posterior distributions for abundance trends at community level by realm and taxonomic group.
-   **04_Abundance_trends.Rdata**: Contains abundance trends linked with environmental covariates (temperature change and human impact).
-   **04_site_level_SADinterval_abundance_trends.Rdata**: Contains site-level abundance trends broken down by abundance class with environmental covariates for attribution analysis.
-   **06_community_posterior.Rdata**: Posterior distributions for various community metrics (richness, evenness, Hill diversity) used in sensitivity analysis.
-   **06_posterior_effects_nonZero.Rdata**: Posterior distributions when species with first-year abundance of zero are removed from analysis.
-   **06_RtM_Sensitivity.Rdata**: Results from regression-to-mean sensitivity analysis comparing different censoring approaches (0, 1, or 3 years).
-   **06_Sensitivity_5yr_posterior.Rdata**: Results from time series length sensitivity analysis using only the first 5 years of data.
-   **06_Sensitivity_quantile_posterior.Rdata**: Results from SAD binning sensitivity analysis using quartile-based abundance bins instead of fixed percentage intervals.

External Data Sources

The analysis also relies on the following external datasets (not included):

-   BioTIME 2.0 database (available at <https://doi.org/10.1111/geb.70003>)

-   HadISST sea surface temperature data (available at <http://www.metoffice.gov.uk/hadobs/hadisst>)

-   CRU TS land surface temperature data (available at <https://crudata.uea.ac.uk/cru/data/hrg/>)

-   Human footprint index raster data (available at <https://doi.org/10.1002/pan3.10071>)

**Computational Requirements**

These analyses are computationally intensive:

-   INLA models require 100-200GB RAM

-   Each model may take several hours to complete

-   Full analysis pipeline may take several days on a high-performance computing system

**Dependencies**

The code relies on the following R packages:

-   `INLA` (for hierarchical Bayesian modeling)

-   `dplyr, tidyverse, data.table` (for data manipulation)

-   `ggplot2, cowplot, ggridges` (for visualization)

-   `ncdf4, raster` (for climate and spatial data)

-   `vegan` (for biodiversity metrics)

-   `BioTIMEr` (for handling BioTIME database)

**Model Workflow**

1.  Process and filter BioTIME data

2.  Calculate abundance classes based on first-year relative abundance

3.  Fit hierarchical models for each abundance class

4.  Extract posterior distributions and calculate abundance-weighted trends

5.  Link trends with environmental drivers

6.  Perform sensitivity analyses

7.  Create visualizations
