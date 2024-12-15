 Quantitative Analysis using PyNance and TA-Lib**

### **Project Title: Stock Price Analysis Dashboard**

---

## **Overview**

This task involves using **PyNance** and **TA-Lib** to perform quantitative analysis on stock price data. The focus is on loading and preparing financial data, calculating technical indicators, and visualizing the results for better insights into market trends.

---

## **Folder Structure**

The recommended folder structure for Task 2 is:

```
├── .vscode/
│   └── settings.json              # VSCode settings
├── .github/
│   └── workflows/
│       └── unittests.yml          # CI/CD workflow for GitHub Actions
├── .gitignore                     # Ignore unnecessary files for Git
├── requirements.txt               # Project dependencies
├── README.md                      # Documentation for Task 2
├── data/
│   └── stock_data.csv             # Stock price dataset
├── src/
│   ├── __init__.py                # Initialization for source code
│   └── analysis.py                # Script for quantitative analysis
├── notebooks/
│   ├── __init__.py                # Initialization for notebooks
│   └── task2_analysis.ipynb       # Jupyter notebook for visual analysis
├── tests/
│   ├── __init__.py                # Initialization for tests
└── scripts/
    ├── __init__.py                # Initialization for scripts
    └── run_analysis.py            # Script to run analysis and visualization
```

---

## **Steps to Complete the Task**

### **1. Merging Task 1 Branch**

1. **Merge `task-1` into `main` via Pull Request (PR)**:
   - Create a PR in GitHub to merge `task-1` into `main`.
   - Ensure the PR has a detailed description.
   - After review, merge the PR.

2. **Create a New Branch for Task 2**:
   ```bash
   git checkout -b task-2
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
   matplotlib
   numpy
   pynance
   TA-Lib
   ```
   
   **Install the dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

   **Note**: TA-Lib may require installation of system dependencies:
   - **Linux**:
     ```bash
     sudo apt-get install libta-lib-dev
     ```
   - **macOS**:
     ```bash
     brew install ta-lib
     ```

---

### **3. Loading and Preparing Data**

Ensure your stock data is in a CSV format with the following columns:

- **Date**
- **Open**
- **High**
- **Low**
- **Close**
- **Volume**

### **Sample Code for Data Loading**

```python
import pandas as pd

# Load stock data
df = pd.read_csv('data/stock_data.csv', parse_dates=['Date'])
df.set_index('Date', inplace=True)

print(df.head())
```

---

### **4. Calculating Technical Indicators with TA-Lib**

Use TA-Lib to calculate common indicators like **Moving Averages (SMA)**, **RSI**, and **MACD**.

### **Sample Code for Indicators**

```python
import talib

# Simple Moving Average (SMA)
df['SMA_20'] = talib.SMA(df['Close'], timeperiod=20)

# Relative Strength Index (RSI)
df['RSI'] = talib.RSI(df['Close'], timeperiod=14)

# Moving Average Convergence Divergence (MACD)
df['MACD'], df['MACD_signal'], df['MACD_hist'] = talib.MACD(df['Close'])
```

---

### **5. Financial Metrics with PyNance**

Use PyNance to compute additional financial metrics.

### **Sample Code for Financial Metrics**

```python
import pynance as pn

# Fetch stock data for a ticker (e.g., AAPL)
data = pn.data.get("AAPL", start="2022-01-01", end="2023-01-01")
print(data.head())
```

---

### **6. Visualizing Data**

Create visualizations to analyze the data and understand the impact of the indicators.

### **Sample Code for Visualization**

```python
import matplotlib.pyplot as plt

# Plot Close Price and SMA
plt.figure(figsize=(12, 6))
plt.plot(df.index, df['Close'], label='Close Price', alpha=0.7)
plt.plot(df.index, df['SMA_20'], label='20-Day SMA', alpha=0.9)
plt.title('Stock Close Price and 20-Day SMA')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.grid(True)
plt.show()

# Plot RSI
plt.figure(figsize=(12, 4))
plt.plot(df.index, df['RSI'], label='RSI', color='purple')
plt.axhline(70, linestyle='--', color='red', label='Overbought')
plt.axhline(30, linestyle='--', color='green', label='Oversold')
plt.title('Relative Strength Index (RSI)')
plt.xlabel('Date')
plt.ylabel('RSI')
plt.legend()
plt.grid(True)
plt.show()
```

---

## **Key Performance Indicators (KPIs)**

1. **Proactivity to Self-Learn**:
   - Share references or resources used for learning TA-Lib and PyNance.

2. **Accuracy of Indicators**:
   - Ensure calculated indicators match expected values.

3. **Completeness of Data Analysis**:
   - Perform a comprehensive analysis including multiple indicators and visualizations.

---

## **How to Run the Project**

1. **Activate Virtual Environment**:
   ```bash
   source venv/bin/activate
   ```

2. **Run Analysis Script**:
   ```bash
   python scripts/run_analysis.py
   ```

3. **Open the Jupyter Notebook**:
   ```bash
   jupyter notebook notebooks/task2_analysis.ipynb
   ```

---

## **Commit History Guidelines**

- **Commit Example 1**:
  ```bash
  git commit -m "Loaded stock data and calculated SMA, RSI, and MACD indicators"
  ```

- **Commit Example 2**:
  ```bash
  git commit -m "Added visualizations for stock price and technical indicators"
  ```

- **Commit Example 3**:
  ```bash
  git commit -m "Integrated PyNance for financial metrics"
  ```

