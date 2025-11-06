# Generative-AI-for-Demand-Forecasting-in-the-Door-Industry
Designed a forecasting pipeline that helps optimize inventory planning in the door industry. 

Partnered with Trimlite LLC to build a Machine Learning driven forecasting pipeline designed to reduce inventory losses caused by manual forecasting.

Using their historical weekly sales and inventory (structured and unstructured) data, I engineered temporal features (lags, rolling averages, week/month flags) to give models meaningful inputs.

I benchmarked three open-source approaches, balancing interpretability, speed and complexity:
1. SARIMA: the statistical baseline. With just a few parameters, it was able to model some seasonality and autocorrelation on a 100+ point series and was easy to explain to stakeholders.
2. Prophet: Meta's changepoint model. It fit quickly and handled occasional missing weeks, but its piecewise-linear trend segments smoothed out the consistent seasonal swings, so it never fully captured the true amplitude of our weekly and monthly patterns.
3. LSTM: a sequence model for non-linear spikes. After grid-searching layer depth, dropout and learning rate, it still struggled and led to overfitting.

I ran grid searches for SARIMA (p, d, q) and LSTM hyperparameters, then backtested all models using MAE , MSE and several other metrics. 
Outputs were then fed to a dashboard where users could toggle models, adjust parameters, filter by SKU group and download forecasts making our insights clear, actionable and easy to share across teams.

SARIMA emerged as the most robust on our sparse time series. But the real win was also understanding which approaches didn’t fit our constraints.

Interesting cues: Trimlite’s SKU nomenclature often embeds performance specs
For example, any door ending with “20m” or “60m”, “90m” is generally a 20(or 60 or 90)-minute fire-rated door-meaning it’s certified to withstand fire exposure for at least 20 minutes without allowing flames through. That single code tells you material, core construction and safety rating all at once!
