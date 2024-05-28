## BigQuery Analysis

This document details the exploration, preprocessing, and analysis of the GHCN-Daily weather data within BigQuery. The goal is to understand the data, identify relevant variables, and prepare it for feature engineering and model training.

#### 1. Create tables for 2022, 2023 & Stations Data

a) 2022 Table

**Query:**

![2022 Table](BigQuery-images/Table-1.png)

b) 2023 Table

**Query:**

![2023 Table](BigQuery-images/Table-2.png)

c) Stations

**Query:**

![Station](BigQuery-images/Station.png)

d) Combine data from 2022 and 2023

**Query:**

![Combine Data 2022-2023](BigQuery-images/Combined-Data.png)

e) Join with Stations

**Query:**

![Join with Station](BigQuery-images/Join-with-Station.png)

#### 2. Data Preprocessing & Cleaning

a) Identify Missing Values

**Query:**

![Missing Values](BigQuery-images/Missing-Values.png)

a.1) New Table with Imputed Values

**Query:**

![Imputed Table](BigQuery-images/Imputed-Data.png)

a.2) Verify New Table

**Query:**

![Verification](BigQuery-images/Verification.png)
