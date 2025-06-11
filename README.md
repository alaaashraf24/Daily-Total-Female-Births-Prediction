# Daily Total Female Births Prediction

This notebook explores time series analysis and forecasting techniques to predict the daily total female births based on a provided dataset. Various models, including ARIMA family models, Support Vector Regression (SVR), and Long Short-Term Memory (LSTM) networks, are applied and evaluated.

## Table of Contents

- [Dataset](#dataset)
- [Data Exploration and Preprocessing](#data-exploration-and-preprocessing)
- [Time Series Analysis](#time-series-analysis)
  - [Stationarity Check (ADF Test)](#stationarity-check-adf-test)
  - [Autocorrelation and Partial Autocorrelation (ACF and PACF)](#autocorrelation-and-partial-autocorrelation-acf-and-pacf)
  - [Time Series Decomposition](#time-series-decomposition)
  - [Differencing](#differencing)
- [Modeling](#modeling)
  - [ARIMA Family Models (AR, MA, ARMA, ARIMA, SARIMA)](#arima-family-models-ar-ma-arma-arima-sarima)
  - [Support Vector Regressor (SVR)](#support-vector-regressor-svr)
  - [Long Short-Term Memory (LSTM)](#long-short-term-memory-lstm)
- [Evaluation](#evaluation)
- [Conclusion](#conclusion)

## Dataset

The notebook uses the "DailyTotalFemaleBirths.csv" dataset, which contains the number of female births per day in California in 1959.

## Data Exploration and Preprocessing

- The dataset is loaded and inspected.
- The 'Date' column is converted to datetime objects and set as the index.
- Missing values are checked (none are present).
- Descriptive statistics are displayed.

## Time Series Analysis

Initial analysis of the time series is performed to understand its characteristics.

### Stationarity Check (ADF Test)

The Augmented Dickey-Fuller (ADF) test is used to check if the time series is stationary. The p-value from the test indicates whether the series is likely stationary or non-stationary.

### Autocorrelation and Partial Autocorrelation (ACF and PACF)

ACF and PACF plots are generated to identify potential dependencies in the time series at different lags, which helps in determining the parameters for ARIMA models.

### Time Series Decomposition

The series is decomposed into its trend, seasonal, and residual components to visualize underlying patterns.

### Differencing

The first difference of the time series is computed and plotted. Differencing is a common technique to make a non-stationary time series stationary.

## Modeling

Different time series forecasting models are applied and evaluated. The data is split into 80% for training and 20% for testing.

### ARIMA Family Models (AR, MA, ARMA, ARIMA, SARIMA)

- **AR (Autoregressive) Model:** An AR(1) model is fitted.
- **MA (Moving Average) Model:** An MA(1) model is fitted.
- **ARMA (Autoregressive Moving Average) Model:** An ARMA(1,1) model is fitted.
- **ARIMA (Autoregressive Integrated Moving Average) Model:** An ARIMA(1,1,1) model is fitted.
- **SARIMA (Seasonal Autoregressive Integrated Moving Average) Model:** A SARIMA(1,1,1)(1,1,0,7) model is fitted, considering a weekly seasonality.

Each model's summary is printed, and forecasts on the test set are generated and plotted against the actual values. Evaluation metrics (MSE, MAE, AIC, BIC) are calculated for each model.

The models are compared based on their performance metrics (lower is better for MSE, MAE, AIC, and BIC). AIC and BIC balance model fit and complexity. The notebook provides a conclusion on which ARIMA family model appears to be the best based on these metrics.

### Support Vector Regressor (SVR)

- Lagged features are created from the time series data to use as input for the SVR model.
- The data is scaled using `StandardScaler`.
- An SVR model with a linear kernel is trained.
- Predictions are made for one-step ahead and a rolling three-step ahead forecast.
- MSE and MAE are calculated for both prediction horizons.
- Actual vs. Predicted plots are shown for both 1-step and 3-step forecasts.

### Long Short-Term Memory (LSTM)

- The data is split and scaled using `MinMaxScaler`.
- `TimeseriesGenerator` is used to prepare the data in the required format for the LSTM model, using a sequence length of 12.
- A sequential LSTM model with multiple layers is defined and compiled with 'adam' optimizer and 'mse' loss.
- The model is trained on the generated sequences.
- One-step ahead predictions are made on the test data.
- The predictions are inverse scaled to the original scale.
- MSE and MAE are calculated for the LSTM predictions.
- A plot of actual vs. predicted values from the LSTM model is displayed.

## Evaluation

The notebook evaluates the performance of each applied model using standard regression metrics:

- **Mean Squared Error (MSE):** Measures the average of the squared errors between actual and predicted values.
- **Mean Absolute Error (MAE):** Measures the average of the absolute differences between actual and predicted values.
- **Akaike Information Criterion (AIC):** A measure used for model selection, balancing goodness of fit with the complexity of the model. Lower AIC is preferred.
- **Bayesian Information Criterion (BIC):** Another measure for model selection, similar to AIC but with a stronger penalty for the number of parameters. Lower BIC is preferred.

The performance of the ARIMA family models is explicitly compared using these metrics, and the best model among them is identified based on AIC, BIC, MSE, and MAE. SVR and LSTM models are evaluated separately based on their respective predictions and metrics.

## Conclusion

The notebook demonstrates a comprehensive approach to time series forecasting on the Daily Female Births dataset, applying and evaluating different statistical and machine learning models. The results from each model's evaluation metrics provide insights into their suitability for this particular time series prediction task.
