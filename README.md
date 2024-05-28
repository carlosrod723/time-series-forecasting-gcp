## Time Series Forecasting of Daily Weather Conditions Using Google Cloud Platform and Vertex AI

### I- Business Objective

The objective of this project is to develop a time series forecasting model that can accurately predict daily weather conditions (e.g., temperature, precipitation) based on historical data. The ability to forecast weather patterns has numerous applications, such as optimizing energy consumption, planning agricultural activities, and preparing for extreme weather events.

### II- Methods:

**Google Cloud Platform (GCP)**- I will utilize GCP as the cloud computing infrastructure due to its scalability, managed services, and seamless integration with various data processing and machine learning tools.

**BigQuery**- I will leverage BigQuery for storing, managing, and preprocessing weather data. BigQuery's powerful SQL-like query language and ability to handle large datasets make it ideal for data wrangling tasks.

**Vertex AI**- This platform will be used for developing, training, and deploying the machine learning model. Vertex AI offers a user-friendly interface and simplifies the entire machine learning workflow.

**GHCN-Daily Dataset**- The Global Historical Climatology Network Daily (GHCN-Daily) dataset from BigQuery's public data project is the primary source of the weather data. This dataset contains daily summaries of weather observations from thousands of stations worldwide. For the data, I've selected the following tables:

1. ghcnd_2022- This table is useful to get a full year of recent historical data for training the model.

2. ghcnd_2023- This table provides more decent data, which can be used for both training and evaluating model performance on unseen data.

3. ghcnd_stations- This table contains metadata about the weather stations, including their location (latitude and longitude). This will be used to filter the analysis to specific regions or to join with other datasets if needed.

**Feedforward Neural Network (FNN)**- A simple FNN is the initial machine learning model. FNNs are relatively lightweight and easy to train. They can provide valuable insights and predictions for daily weather patterns.

### III- Model Justification

Feedforward Neural Networks (FNNs) are an excellent choice for the time series forecasting project due to their ability to efficiently model complex relationships between input features and predicted weather variables. Their layered structure enables them to learn hierarchical representations of the data, capturing underlying patterns that drive weather dynamics. By adjusting the weights and biases of the connections between neurons, FNNs can adapt to the specific characteristics of the dataset, making them a flexible and powerful tool for predicting daily weather conditions. While they may not explicitly model temporal dependencies, FNNs can still be highly effective for forecasting tasks when combined with appropriate feature engineering and preprocessing techniques that incorporate temporal information.
