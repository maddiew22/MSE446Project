# Stock Anomaly Detection Pipeline

This project analyzes historical stock data to detect anomalous behavior in individual stocks relative to market benchmarks. The pipeline combines statistical methods, time-series techniques, and supervised and unsupervised machine learning techniques.

We want to explore how supervised and unsupervised models perform for the same task. In doing so, we hope to gain insights into how model development for the same problem varies between supervised and unsupervised approaches.

## Folder Structure
```
project-root/
│
├── data/                  # Raw and processed datasets
│   └── all stock data     # Multiple CSV files containing stock and S&P 500 hisotrical prices
│
├── notebook.ipynb         # Main machine learning file
├── requirements.txt       # Python dependencies
├── README.md              # Project documentation
└── EDA.ipynb              # Exploratory data analysis
└── .gitignore             

```

## Dependencies 
Main dependencies include
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn

## How to Run the Code
Clone Repository

```git clone https://github.com/maddiew22/MSE446Project.git```

Install required dependencies from requirements.txt

```pip install -r requirements.txt```

Once done, iterate through the jupyter notebook section by section to make sure that each step of data works. The main loop takes ~ 20 minutes to run.

## Machine Learning Process

### 1. Load Stock Dataset
- Load historical stock price data (Open, High, Low, Close, Volume) for one or more equities. (We chose 'AABA_2006-01-01_to_2018-01-01.csv')
- Load market index data for comparison (We're using S&P 500).

### 2. Clean and Preprocess Data
- Handle missing or irregular data.
- Ensure continuous trading days.
- Convert date columns to proper datetime objects.
- Remove all data before 2010.

### 3. Feature Engineering
- Compute log returns and rolling volatility measures.
- Calculate range-based volatility.
- Compute z-scores of volume and other relevant metrics.
- Merge market index data to derive excess returns.
- Compare log returns of the stock and the index fund, then label data as outlier if it 3 sd away from the mean (Only done for Random Forest approach)
- Scale all values using Robust Scalar

### 4. Isolation Forest and Random Forest Anomaly Detection
- Train an unsupervised Isolation Forest model on unlabeled data.
- Train a Random Forest Model on the labeled data created from Feature Engineering Step
- Identify points that are statistically isolated from the majority of observations.

### 5. Hyper Parameter Tuning
- Use sklearn’s TimeSeries Split (time series K fold CV) to find best Hyper Parameter combinations and F1 scores to evaulate its effectiveness
- The score separation (decision function spread) is used to compare the isolation forest model, where a larger spread between top/bottom percentiles of anomaly scores indicates clearer separation between normal points and anomalies.

### 6. Calculate Train and Test Scores
Once the Isolation and Random Forest models are calculated, we show the train and test scores for each

<img width="814" height="281" alt="Screenshot 2026-03-26 at 11 30 56 AM" src="https://github.com/user-attachments/assets/73e8bfbf-fc27-4d31-a854-eccc17b7a9a4" />

### 6. Results/Visualization
- Plot time-series of stock prices and volatility.
- Highlight detected anomalies on charts.
- Compare stock behavior to index benchmarks to illustrate deviations.

### Isolation Forest Results
<img width="595" height="430" alt="Screenshot 2026-03-26 at 11 23 09 AM" src="https://github.com/user-attachments/assets/7477f85c-f983-459d-ac6a-27ca42b90994" />

### Random Forest Results
<img width="503" height="441" alt="Screenshot 2026-03-26 at 11 24 02 AM" src="https://github.com/user-attachments/assets/b3f419bf-394d-461c-89fc-88c9ac5b679a" />

