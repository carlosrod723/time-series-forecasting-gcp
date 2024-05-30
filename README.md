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

### V- Exploratory Data Analysis: Visualizations

Leveraging the capabilities of Looker Studio, BigQuery charts, and Python Notebooks, a comprehensive exploratory data analysis (EDA) was conducted on the weather data stored in BigQuery. The resulting visualizations unveiled key insights into temperature and precipitation patterns.

Both daily and monthly average maximum and minimum temperatures exhibited clear seasonal trends, highlighting the cyclical nature of temperature variations. Daily total precipitation showcased a more episodic pattern, with frequent peaks indicating days of substantial rainfall interspersed with periods of lower precipitation. The correlation matrix revealed a negligible relationship between precipitation and temperature extremes, suggesting independent influences on weather conditions. Distribution plots illustrated the relative stability in temperature data compared to the variability in precipitation, characterized by a skewed distribution with a long tail.

These findings underscore the importance of incorporating seasonal variables and understanding the distinct behavior of temperature and precipitation when developing predictive models. 

For a deeper dive into the code, visualizations, and detailed analysis of each chart, please refer to the 'EDA_visualizations.md' file.

### VI- Feature Engineering

Feature engineering, a critical step in enhancing machine learning models, involves transforming raw data into more informative features that better capture underlying patterns.  This process aims to improve the model's ability to learn and make predictions. In the context of the weather forecasting project, feature engineering was employed to extract relevant information from the datetime data and create features that capture temporal dependencies in the data.

First, the 'date' column was converted to a datetime format to enable easy extraction of year, month, day, and day of the week. These features provide valuable information about seasonal and weekly patterns in weather conditions.

Next, rolling mean features were calculated for tmax (maximum temperature), tmin (minimum temperature), and prcp (precipitation) using 7-day and 30-day windows. These features capture short-term and medium-term trends in the data, smoothing out daily fluctuations and highlighting broader patterns.

Lag features were also created by shifting the values of tmax, tmin, and prcp by 1 and 7 days. These features allow the model to consider past weather conditions when making predictions, incorporating the temporal dependencies inherent in weather data.

Finally, any missing values introduced by the rolling and lag features were filled using a combination of forward-fill and backward-fill methods. This ensures that the dataset is complete and ready for model training.

By enriching the dataset with these engineered features, I have provided the feedforward neural network with a more comprehensive view of the weather data, enabling it to learn and generalize better, ultimately leading to more accurate predictions.

For the Python code implementation of feature engineering and subsequent model development, please refer to the 'weather_model(3).ipynb' file.

### VII- Building the FeedForward Neural Network Model

Having engineered informative features, the next step involved building the model. To align with my goal of simplicity due to limited computational resources, a feedforward neural network was chosen as the modeling approach.

The relevant features for prediction, namely tmin (minimum temperature) and prcp (precipitation), were designated as input variables (X), while tmax (maximum temperature) was identified as the target variable (y). The dataset was then split into training and testing sets, with 80% of the data allocated for training and the remaining 20% reserved for evaluating the model's performance on unseen data.

The neural network architecture comprises an input layer with 32 neurons (Dense 32), followed by two hidden layers with 16 neurons each (Dense 16), and finally, an output layer with a single neuron (Dense 1) representing the predicted maximum temperature. The rectified linear unit (ReLU) activation function, known for its computational efficiency and ability to mitigate the vanishing gradient problem, was employed in the hidden layers. ReLU's non-linearity allows the model to capture complex relationships within the data.

The Adam optimizer, an adaptive learning rate optimization algorithm, was selected to update the model's weights during training. Adam dynamically adjusts the learning rate for each parameter, leading to faster convergence and potentially better performance. The mean squared error (MSE) loss function was chosen to measure the discrepancy between predicted and actual maximum temperatures. MSE penalizes larger errors more heavily, encouraging the model to prioritize accuracy.

The mean absolute error (MAE) metric was included to provide an interpretable measure of the average magnitude of prediction errors. MAE calculates the average absolute difference between predicted and actual values, offering a straightforward assessment of model performance.

For a detailed implementation of the model building process and the code, please refer to the 'weather_model(3).ipynb' notebook file.

### VIII- Training the FFN Model

To train the feedforward neural network, I employed the model.fit function, specifying key parameters to guide the learning process. The epochs parameter was set to 10, indicating that the model would iterate over the entire training dataset 10 times (opting for simplicity). While a higher number of epochs could potentially lead to better performance, it also increases the risk of overfitting, where the model becomes too specialized to the training data and performs poorly on unseen data. Ten epochs were chosen as a reasonable starting point, balancing the need for learning with the risk of overfitting.

The validation_split parameter was set to 0.2, meaning that 20% of the training data was reserved for validation during each epoch. This validation set serves as a proxy for unseen data, allowing us to monitor the model's performance and generalization ability during training.  The 0.2 split provides a sufficient amount of data for validation while leaving enough data for training the model effectively.

The verbose parameter was set to 1, which controls the level of information displayed during training. A value of 1 indicates that progress bars will be shown for each epoch, providing real-time feedback on the training process. While verbose settings don't directly impact the model's performance, they are helpful for monitoring and debugging during development.

For a detailed implementation of the model training process and the code, please refer to the 'weather_model(3).ipynb' notebook file.

### IX- Model Evaluation (Mean Absolute Error)

Following the training phase, the model's performance was evaluated using the model.evaluate function, which calculates the loss (mean squared error in this case) and mean absolute error (MAE) on the held-out test set. However, in this case, the focus is on the mae value, which is a more interpretable metric for regression problems.  The verbose=0 setting suppresses the output of detailed evaluation results during this process.

The Mean Absolute Error (MAE) is a widely used metric that measures the average magnitude of the errors in a set of predictions, without considering their direction. It calculates the absolute difference between the predicted and actual values and then takes the mean of those differences. A lower MAE value indicates better performance, as it means the predictions are closer to the actual values on average.

The mean absolute error (MAE) of 1.7628 provides valuable insight into the model's predictive accuracy. It signifies that, on average, the model's predictions for maximum temperature (TMAX) deviate from the actual values by approximately 1.76 degrees Celsius. In the context of weather forecasting, an MAE of 1.76 can be considered reasonable, as weather patterns can be inherently complex and subject to various external influences.

The feedforward neural network, despite its simplicity and limited computational resources, demonstrated a satisfactory ability to predict maximum temperatures based on minimum temperature and precipitation data. This suggests that the chosen architecture, activation functions, optimizer, and loss function were appropriate for capturing the underlying relationships in the data.

For further analysis, code and a more in-depth examination of the model's performance, please refer to the 'weather_model(3).ipynb' notebook file.

### X. 
