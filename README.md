# Stock Anomaly Detection Pipeline

This project analyzes historical stock data to detect anomalous behavior in individual stocks relative to market benchmarks. The pipeline combines statistical methods, machine learning, and time-series techniques.

## Steps

### 1. Load Stock Dataset
- Load historical stock price data (Open, High, Low, Close, Volume) for one or more equities.
- Load market index data for comparison.

### 2. Clean and Preprocess Data
- Handle missing or irregular data.
- Ensure continuous trading days.
- Convert date columns to proper datetime objects.
- Standardize column names and formats.

### 3. Feature Engineering
- Compute log returns and rolling volatility measures.
- Calculate range-based volatility.
- Compute z-scores of volume and other relevant metrics.
- Merge market index data to derive excess returns.
- Compare log returns of the stock and the index fund, then label data as outlier if it 3 sd away from the mean

### 4. Robust Statistical Baseline Detector
- Compute the mean and standard deviation of excess returns.
- Flag observations that deviate significantly from the statistical baseline.

### 5. Isolation Forest Anomaly Detection
- Train an unsupervised Isolation Forest model on features like returns and volatility.
- Identify points that are statistically isolated from the majority of observations.

### 6. Change-Point Detection on Volatility
- Detect sudden structural changes in volatility over time.
- Helps identify periods of market regime shifts or unusual stock behavior.

### 7. Thresholding + Anomaly Labeling
- Compute z-scores for excess returns.
- Apply thresholds to classify individual observations as outliers (0 = normal, 1 = anomalous).

### 8. Evaluation / Sanity Checks
- Verify that outliers align with known market events or extreme stock movements.
- Perform cross-validation or manual inspection to ensure model reliability.

### 9. Visualization
- Plot time-series of stock prices and volatility.
- Highlight detected anomalies on charts.
- Compare stock behavior to index benchmarks to illustrate deviations.
