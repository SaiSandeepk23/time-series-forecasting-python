# time-series-forecasting-wiki

This repository contains a series of analysis, transforms and forecasting models frequently used when dealing with time series. The aim of this repository is to showcase how to model time series from scratch. For this, we are using a real use case dataset (Beijing air pollution dataset: https://archive.ics.uci.edu/ml/datasets/Beijing+PM2.5+Data) to avoid perfect use cases far from reality that are often present in these types of tutorials. If you want to rerun the notebooks, make sure you install all necessary dependencies (see docs/setup.md).

<img src="results/beijing.jpg">

You can find a more detailed table of contents in the main notebook: time-series-forecasting-tutorial.ipynb

# Dataset

The dataset used is the Beijing air quality public dataset. This dataset contains pollution data from 2014 to 2019 sampled every 10 minutes along with extra weather features such as pressure, temperature, etc. We decided to resample the dataset with daily frequency for both easier data handling and proximity to a real use case scenario (predicting pollution 1 day ahead is more realistic than 10 minutes ahead). In this case, the series is already stationary with some small seasonalities which change every year.

In order to obtain an exact copy of the dataset used in this tutorial, please run the script under datasets/download_datasets.py which will automatically download the dataset and preprocess it for you.

# Analysis and transforms

* Time series decomposition
  * Level
  * Trend
  * Seasonality 
  * Noise
  
* Stationarity
  * AC and PAC plots
  * Rolling mean and std
  * Dickey-Fuller test
  
* Making our time series stationary
  * Difference transform
  * Log scale
  * Smoothing
  * Moving average

# Models tested

* Autoregression (AR)
* Moving Average (MA)
* Autoregressive Moving Average (ARMA)
* Autoregressive integrated moving average (ARIMA)
* Seasonal autoregressive integrated moving average (SARIMA)
* Bayesian regression
* Lasso
* SVM
* RandomForest
* Nearest neighbors
* XGBoost
* LightGBM
* Prophet
* Long short-term memory with TensorFlow (LSTM)
* DeepAR

# Forecasting results

We will divide our results based on whether the extra feature columns (such as temperature or pressure) were used by the model, as this represents a significant step in metrics and represents two different scenarios.

## Evaluation Metrics
* Mean Absolute Error (MAE) 
* Mean Absolute Percentage Error (MAPE)
* Root Mean Squared Error (RMSE)
* Coefficient of determination (R2)

<table class="table table-bordered table-hover table-condensed">
<thead><tr><th title="Field #1">Model</th>
<th title="Field #2">mae</th>
<th title="Field #3">rmse</th>
<th title="Field #4">mape</th>
<th title="Field #5">r2</th>
</tr></thead>
<tbody><tr>
<td>EnsembleXG+TF</td>
<td align="right">27.64</td>
<td align="right">40.23</td>
<td align="right">0.42</td>
<td align="right">0.76</td>
</tr>
<tr>
<td>EnsembleLIGHT+TF</td>
<td align="right">27.34</td>
<td align="right">39.27</td>
<td align="right">0.42</td>
<td align="right">0.77</td>
</tr>
<tr>
<td>EnsembleXG+LIGHT+TF</td>
<td align="right">27.63</td>
<td align="right">39.69</td>
<td align="right">0.44</td>
<td align="right">0.76</td>
</tr>
<tr>
<td>EnsembleXG+LIGHT</td>
<td align="right">29.95</td>
<td align="right">42.7</td>
<td align="right">0.52</td>
<td align="right">0.73</td>
</tr>
<tr>
<td>Randomforest tunned</td>
<td align="right">40.79</td>
<td align="right">53.2</td>
<td align="right">0.9</td>
<td align="right">0.57</td>
</tr>
<tr>
<td>SVM RBF GRID SEARCH</td>
<td align="right">38.57</td>
<td align="right">50.34</td>
<td align="right">0.78</td>
<td align="right">0.62</td>
</tr>
<tr>
<td>DeepAR</td>
<td align="right">71.37</td>
<td align="right">103.97</td>
<td align="right">0.96</td>
<td align="right">-0.63</td>
</tr>
<tr>
<td>Tensorflow simple LSTM</td>
<td align="right">30.13</td>
<td align="right">43.08</td>
<td align="right">0.42</td>
<td align="right">0.72</td>
</tr>
<tr>
<td>Prophet multivariate</td>
<td align="right">38.25</td>
<td align="right">50.45</td>
<td align="right">0.74</td>
<td align="right">0.62</td>
</tr>
<tr>
<td>Kneighbors</td>
<td align="right">57.05</td>
<td align="right">80.39</td>
<td align="right">1.08</td>
<td align="right">0.03</td>
</tr>
<tr>
<td>SVM RBF</td>
<td align="right">40.81</td>
<td align="right">56.03</td>
<td align="right">0.79</td>
<td align="right">0.53</td>
</tr>
<tr>
<td>Lightgbm</td>
<td align="right">30.21</td>
<td align="right">42.76</td>
<td align="right">0.52</td>
<td align="right">0.72</td>
</tr>
<tr>
<td>XGBoost</td>
<td align="right">32.13</td>
<td align="right">45.59</td>
<td align="right">0.56</td>
<td align="right">0.69</td>
</tr>
<tr>
<td>Randomforest</td>
<td align="right">45.84</td>
<td align="right">59.45</td>
<td align="right">1.03</td>
<td align="right">0.47</td>
</tr>
<tr>
<td>Lasso</td>
<td align="right">39.24</td>
<td align="right">54.58</td>
<td align="right">0.71</td>
<td align="right">0.55</td>
</tr>
<tr>
<td>BayesianRidge</td>
<td align="right">39.24</td>
<td align="right">54.63</td>
<td align="right">0.71</td>
<td align="right">0.55</td>
</tr>
<tr>
<td>Prophet univariate</td>
<td align="right">61.33</td>
<td align="right">83.64</td>
<td align="right">1.26</td>
<td align="right">-0.05</td>
</tr>
<tr>
<td>AutoSARIMAX (1, 0, 1),(0, 0, 0, 6)</td>
<td align="right">51.29</td>
<td align="right">71.49</td>
<td align="right">0.91</td>
<td align="right">0.23</td>
</tr>
<tr>
<td>SARIMAX</td>
<td align="right">51.25</td>
<td align="right">71.33</td>
<td align="right">0.91</td>
<td align="right">0.23</td>
</tr>
<tr>
<td>AutoARIMA (0, 0, 3)</td>
<td align="right">47.01</td>
<td align="right">64.71</td>
<td align="right">1.0</td>
<td align="right">0.37</td>
</tr>
<tr>
<td>ARIMA</td>
<td align="right">48.25</td>
<td align="right">66.39</td>
<td align="right">1.06</td>
<td align="right">0.34</td>
</tr>
<tr>
<td>ARMA</td>
<td align="right">47.1</td>
<td align="right">64.86</td>
<td align="right">1.01</td>
<td align="right">0.37</td>
</tr>
<tr>
<td>MA</td>
<td align="right">49.04</td>
<td align="right">66.2</td>
<td align="right">1.05</td>
<td align="right">0.34</td>
</tr>
<tr>
<td>AR</td>
<td align="right">47.24</td>
<td align="right">65.32</td>
<td align="right">1.02</td>
<td align="right">0.36</td>
</tr>
<tr>
<td>HWES</td>
<td align="right">52.96</td>
<td align="right">74.67</td>
<td align="right">1.11</td>
<td align="right">0.16</td>
</tr>
<tr>
<td>SES</td>
<td align="right">52.96</td>
<td align="right">74.67</td>
<td align="right">1.11</td>
<td align="right">0.16</td>
</tr>
<tr>
<td>Yesterdays value</td>
<td align="right">52.67</td>
<td align="right">74.52</td>
<td align="right">1.04</td>
<td align="right">0.16</td>
</tr>
<tr>
<td>Naive mean</td>
<td align="right">59.38</td>
<td align="right">81.44</td>
<td align="right">1.32</td>
<td align="right">-0.0</td>
</tr>
</tbody></table>

# Additional resources and literature

## Models not tested but gaining popularity 
There are several models not yet included in these tutorials as they originate from academic research and implementations are being finalized, but they are worth noting:

* Neural basis expansion analysis for interpretable time series forecasting (N-BEATS)
* ESRRN (M4 Forecasting Competition)

## References

- Adhikari, R., & Agrawal, R. K. (2013). An introductory study on time series modeling and forecasting.
- Introduction to Time Series Forecasting With Python (Machine Learning Mastery).
- Deep Learning for Time Series Forecasting (Machine Learning Mastery).
- The Complete Guide to Time Series Analysis and Forecasting (Towards Data Science).
- How to Decompose Time Series Data into Trend and Seasonality (Machine Learning Mastery).

# Contributing
Want to see another model tested? Do you have anything to add or fix? I am actively maintaining this project and would be happy to discuss improvements. Please feel free to open an issue or submit a pull request.

# Maintainer
**Sai Sandeep Kethiboina**
AI and Machine Learning Engineer

AI/ML Engineer and Data Scientist with over 5 years of experience designing, developing, and deploying scalable Artificial Intelligence, Machine Learning, and Deep Learning solutions. Specialized in building data-driven products and predictive systems using Python, TensorFlow, PyTorch, and Scikit-learn.

* GitHub: https://github.com/saisandeepkethiboina
* LinkedIn: https://www.linkedin.com/in/saisandeepkethiboina/