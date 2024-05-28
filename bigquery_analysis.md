## BigQuery Analysis

This document details the exploration, preprocessing, and analysis of the GHCN-Daily weather data within BigQuery. The goal is to understand the data, identify relevant variables, and prepare it for feature engineering and model training.

### I- Initial Queries

#### 1. Retreiving Data from a Single Station

To understand the structure and content of the GHCN-Daily dataset, I start with some simple queries to retrieve data for a specific station. This will give me a feel for the available variables and their values.

**Query**



The results showcase various weather elements like wind direction (WDF5), average wind speed (AWND), snowfall (SNOW), and snow depth (SNWD) measured at different dates in 2023. Notably, some elements like snowfall and snow depth have zero values, suggesting no snowfall occurred on those specific dates. The query also includes mflag, qflag, and sflag columns, likely indicating measurement, quality, and source flags respectively, but these columns contain null values in the returned rows

#### 2. Filter for Specific Weather Elements

**Query**

