 Correlation Between News and Stock Movement**

### **Project Title: Stock Sentiment Analysis Dashboard**

---

## **Overview**

This task involves analyzing the relationship between news sentiment and stock price movements. By aligning news data with stock price data and performing sentiment analysis, we aim to calculate correlations between news sentiment and daily stock returns.

---

## **Folder Structure**

The recommended folder structure for Task 3 is:

```
├── .vscode/
│   └── settings.json              # VSCode settings
├── .github/
│   └── workflows/
│       └── unittests.yml          # CI/CD workflow for GitHub Actions
├── .gitignore                     # Ignore unnecessary files for Git
├── requirements.txt               # Project dependencies
├── README.md                      # Documentation for Task 3
├── data/
│   ├── stock_data.csv             # Stock price dataset
│   └── news_data.csv              # News headlines dataset
├── src/
│   ├── __init__.py                # Initialization for source code
│   └── sentiment_correlation.py   # Script for sentiment analysis and correlation
├── notebooks/
│   └── task3_correlation.ipynb    # Jupyter notebook for analysis
├── tests/
│   ├── __init__.py                # Initialization for tests
└── scripts/
    └── run_task3_analysis.py      # Script to run Task 3 analysis
```

---

## **Steps to Complete the Task**

### **1. Merging Task 2 Branch**

1. **Merge `task-2` into `main` via Pull Request (PR)**:
   - Create a PR in GitHub to merge `task-2` into `main`.
   - Ensure the PR has a detailed description.
   - After review, merge the PR.

2. **Create a New Branch for Task 3**:
   ```bash
   git checkout -b task-3
   ```

---

### **2. Setting Up the Environment**

1. **Activate Virtual Environment**:
   ```bash
   source venv/bin/activate
   ```

2. **Install Dependencies**:

   Add the following libraries to `requirements.txt`:

   ```text
   pandas
   numpy
   matplotlib
   nltk
   textblob
   scipy
   ```

   **Install the dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Download NLTK Data**:
   ```python
   import nltk
   nltk.download('punkt')
   nltk.download('vader_lexicon')
   ```

---

### **3. Loading and Preparing Data**

#### **Stock Data (`stock_data.csv`)**

Ensure your stock data has the following columns:

- **Date**
- **Close**

#### **News Data (`news_data.csv`)**

Ensure your news data has the following columns:

- **Date**
- **Headline**

### **Sample Code for Data Loading**

```python
import pandas as pd

# Load stock data
stock_df = pd.read_csv('data/stock_data.csv', parse_dates=['Date'])
stock_df.set_index('Date', inplace=True)

# Load news data
news_df = pd.read_csv('data/news_data.csv', parse_dates=['Date'])
news_df.set_index('Date', inplace=True)

print(stock_df.head())
print(news_df.head())
```

---

### **4. Normalizing Dates**

Align the dates in the news dataset with the trading days in the stock dataset.

### **Sample Code for Date Alignment**

```python
# Ensure news dates align with stock trading days
news_df = news_df[news_df.index.isin(stock_df.index)]
```

---

### **5. Sentiment Analysis**

Use **TextBlob** or **NLTK's Vader** to perform sentiment analysis on news headlines.

### **Sample Code for Sentiment Analysis**

```python
from nltk.sentiment import SentimentIntensityAnalyzer

# Initialize Sentiment Analyzer
sia = SentimentIntensityAnalyzer()

# Function to compute sentiment score
def get_sentiment_score(headline):
    sentiment = sia.polarity_scores(headline)
    return sentiment['compound']

# Apply sentiment analysis to news headlines
news_df['Sentiment'] = news_df['Headline'].apply(get_sentiment_score)

print(news_df.head())
```

---

### **6. Calculating Daily Stock Returns**

Compute daily percentage changes in the closing prices to represent stock movements.

### **Sample Code for Daily Returns**

```python
# Calculate daily returns
stock_df['Daily_Return'] = stock_df['Close'].pct_change()

print(stock_df.head())
```

---

### **7. Aggregating Daily Sentiments**

Compute the average sentiment score for each day if there are multiple news articles on the same day.

### **Sample Code for Aggregating Sentiments**

```python
# Group by date and calculate average sentiment score
daily_sentiment = news_df.groupby('Date')['Sentiment'].mean()

print(daily_sentiment.head())
```

---

### **8. Correlation Analysis**

Calculate the **Pearson correlation coefficient** between daily sentiment scores and stock returns.

### **Sample Code for Correlation**

```python
from scipy.stats import pearsonr

# Align data
combined_df = pd.concat([stock_df['Daily_Return'], daily_sentiment], axis=1).dropna()

# Calculate Pearson correlation
correlation, p_value = pearsonr(combined_df['Daily_Return'], combined_df['Sentiment'])

print(f"Pearson Correlation: {correlation:.2f}")
print(f"P-Value: {p_value:.4f}")
```

---

### **9. Visualizing the Correlation**

### **Sample Code for Visualization**

```python
import matplotlib.pyplot as plt

plt.scatter(combined_df['Sentiment'], combined_df['Daily_Return'], alpha=0.7)
plt.title('Correlation between News Sentiment and Stock Returns')
plt.xlabel('Average Daily Sentiment Score')
plt.ylabel('Daily Stock Return')
plt.grid(True)
plt.show()
```

---

## **Key Performance Indicators (KPIs)**

1. **Proactivity to Self-Learn**:
   - Share references or resources used for learning sentiment analysis and correlation techniques.

2. **Sentiment Analysis**:
   - Ensure sentiment scores accurately reflect the tone of the news headlines.

3. **Correlation Strength**:
   - Evaluate the strength and significance of the correlation coefficient.

---

## **How to Run the Project**

1. **Activate Virtual Environment**:
   ```bash
   source venv/bin/activate
   ```

2. **Run Analysis Script**:
   ```bash
   python scripts/run_task3_analysis.py
   ```

3. **Open the Jupyter Notebook**:
   ```bash
   jupyter notebook notebooks/task3_correlation.ipynb
   ```

---

## **Commit History Guidelines**

- **Commit Example 1**:
  ```bash
  git commit -m "Performed sentiment analysis on news headlines"
  ```

- **Commit Example 2**:
  ```bash
  git commit -m "Calculated daily stock returns and aligned datasets"
  ```

- **Commit Example 3**:
  ```bash
  git commit -m "Performed correlation analysis between sentiment scores and stock returns"
  ```
