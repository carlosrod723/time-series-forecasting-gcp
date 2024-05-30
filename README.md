## Time Series Forecasting of Daily Weather Conditions Using Google Cloud Platform and Vertex AI

### I- Business Objective

The objective of this project is to develop a time series forecasting model that can accurately predict daily weather conditions (e.g., temperature, precipitation) based on historical data. Accurate weather forecasting is a cornerstone of numerous industries, impacting decision-making processes throughout the global economy. For example, Transportation and logistics industries rely on accurate predictions to plan routes, avoid disruptions, and ensure the safety of both cargo and passengers. By developing a robust time series forecasting model for daily weather conditions, this project aims to provide a valuable tool that can be applied across these diverse sectors.

### II- Methods:

**Google Cloud Platform (GCP)**- I will utilize GCP as the cloud computing infrastructure due to its scalability, managed services, and seamless integration with various data processing and machine learning tools.

**BigQuery**- I will leverage BigQuery for storing, managing, and preprocessing weather data. BigQuery's powerful SQL-like query language and ability to handle large datasets make it ideal for data wrangling tasks.

**Vertex AI**- This platform will be used for deploying the machine learning model. Vertex AI offers a user-friendly interface and simplifies the entire machine learning workflow.

**GHCN-Daily Dataset**- The Global Historical Climatology Network Daily (GHCN-Daily) dataset from BigQuery's public data is the primary source of the weather data. This dataset contains daily summaries of weather observations from thousands of stations worldwide. For the data, I've selected the following tables:

1. ghcnd_2022- This table is useful to get a full year of recent historical data for training the model.

2. ghcnd_2023- This table provides more decent data, which can be used for both training and evaluating model performance on unseen data.

3. ghcnd_stations- This table contains metadata about the weather stations, including their location (latitude and longitude). This will be used to filter the analysis to specific regions or to join with other datasets if needed.

The main focus in these datasets will be TMAX (maximum temperature), TMIN (minimum temperature) and PRCP (precipitation). These three elements are considered fundamental for understanding and predicting weather patterns and influence our daily experiences. TMAX, TMIN, and PRCP are among the most commonly measured and widely available weather variables, which ensures sufficient data for analysis and modeling, and reduces the likelihood of encountering missing or unreliable values.

It's important to note that the GHCN-Daily dataset stores temperature values in tenths of degrees Celsius. So for example, a value of -319.0 actually represents -31.9 degrees Celsius.

### III- Model Selection- Feedforward Neural Network

A simple Feedforward Neural Network (FNN) is the chosen machine learning model, which are relatively lightweight and easy to train. They can provide valuable insights and predictions for daily weather patterns. Feedforward Neural Networks (FNNs) are an excellent choice for the time series forecasting project due to their ability to efficiently model complex relationships between input features and predicted weather variables. Their layered structure enables them to learn hierarchical representations of the data, capturing underlying patterns that drive weather dynamics. By adjusting the weights and biases of the connections between neurons, FNNs can adapt to the specific characteristics of the dataset, making them a flexible and powerful tool for predicting daily weather conditions. While they may not explicitly model temporal dependencies, FNNs can still be highly effective for forecasting tasks when combined with appropriate feature engineering and preprocessing techniques that incorporate temporal information.

### IV- Preparing Data for Analysis

To prepare the weather data for analysis, a comprehensive cleaning and preprocessing pipeline was implemented in BigQuery.  First, weather observations from 2022 and 2023 were consolidated and joined with station metadata, ensuring a complete dataset for model training and evaluation.

Missing values, a common challenge in real-world data, were addressed through imputation. This strategy involves replacing missing data points with estimated values based on existing patterns in the data, preserving the overall integrity of the dataset and preventing potential biases that could arise from simply discarding incomplete records. 

Outliers, data points that significantly deviate from the norm, were identified using a threshold of three standard deviations from the mean. However, the initial identification revealed a substantial number of outliers, suggesting that a more flexible approach was warranted. To strike a balance between outlier removal and data retention, a refined table was created where values exceeding five standard deviations were capped. This strategy mitigates the influence of extreme outliers while retaining valuable information contained within the dataset.

Finally, temperature values, originally recorded in tenths of a degree Celsius, were transformed to the standard degree Celsius unit. This standardization ensures consistency and simplifies subsequent analysis and interpretation of the data.

For a detailed walkthrough of the data cleaning and preprocessing steps, including the BigQuery code used, please refer to the 'bigquery_analysis.md' file.

### V- Exploratory Data Analysis Visualizations

Leveraging the capabilities of Looker Studio, BigQuery charts, and Python Notebooks, a comprehensive exploratory data analysis (EDA) was conducted on the weather data stored in BigQuery. The resulting visualizations unveiled key insights into temperature and precipitation patterns.

Both daily and monthly average maximum and minimum temperatures exhibited clear seasonal trends, highlighting the cyclical nature of temperature variations. Daily total precipitation showcased a more episodic pattern, with frequent peaks indicating days of substantial rainfall interspersed with periods of lower precipitation. The correlation matrix revealed a negligible relationship between precipitation and temperature extremes, suggesting independent influences on weather conditions. Distribution plots illustrated the relative stability in temperature data compared to the variability in precipitation, characterized by a skewed distribution with a long tail.

These findings underscore the importance of incorporating seasonal variables and understanding the distinct behavior of temperature and precipitation when developing predictive models. 

For a deeper dive into the code, visualizations, and detailed analysis of each chart, please refer to the 'EDA_visualizations.md' file.

### VI- 


