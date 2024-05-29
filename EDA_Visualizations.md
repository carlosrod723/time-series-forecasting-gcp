## Exploratory Data Analysis Visualizations

In this part, I will utilize Looker Studio to create visualizations from the weather data stored in BigQuery. Looker Studio provides a powerful interface for transforming raw data into insightful charts and graphs, making it easier to identify trends and patterns. 

#### 1. Average Max Temperature (Tmax) by Date

**Query:**

![Avg Max Query](BigQuery-images/Avg-Max-Query.png)

![Avg Max Chart](BigQuery-images/Avg-Max-Temp.png)

This cyclical trend highlights the predictable nature of temperature variations, which are crucial for developing accurate weather forecasting models. The data shows a clear increase in temperatures starting from late winter, reaching a peak in mid-summer, followed by a gradual decline as winter approaches again.

#### 2. Daily Average Minimum Temperature (TMIN)

**Query:**

![Avg Min Temp](BigQuery-images/Avg-Min-Query.png)

![Avg Min Chart](BigQuery-images/Avg-Min-Chart.png)

The chart of the Daily Average Minimum Temperature (TMIN) exhibits clear seasonal trends similar to those observed in the maximum temperature chart. Minimum temperatures rise gradually from late winter to peak during the summer months and then decline as winter approaches. These cyclical patterns highlight the predictability of seasonal temperature changes, which is essential for developing robust weather forecasting models. The consistent troughs and peaks underscore the importance of incorporating seasonal variables in predictive analytics to improve the accuracy of forecasts.

#### 3. Daily Total Precipitation (PRCP) by Date

**Query:**

![Daily Total PRCP](BigQuery-images/Total-PRCP-Query.png)

![Daily Total PRCP](BigQuery-images/Total-PRCP-Chart.png)

The data shows fluctuations with frequent peaks, indicating days of significant rainfall interspersed with periods of lower precipitation. This pattern underscores the episodic nature of precipitation, which is essential for understanding and predicting weather conditions.

#### 4. Monthly Average Maximum Temperature (TMAX)

**Query:**

![Monthly Avg](BigQuery-images/TMAX-Month-Query.png)

![Month Chart](BigQuery-images/TMAX-Month-Chart.png)

Temperatures steadily rise from January, peaking during the summer months of July and August, and then gradually decrease towards October. This pattern aligns with typical seasonal variations, where the summer months exhibit the highest temperatures and the winter months the lowest. The data highlights the expected temperature fluctuations over the course of the year, providing valuable insights for forecasting and planning purposes.

#### 5. Monthly Average Minimum Temperature (TMIN)

**Query:**

![Monthly Min](BigQuery-images/Month-TMIN-Query.png)

![Month Min Chart](BigQuery-images/Month-TMIN-Chart.png)
