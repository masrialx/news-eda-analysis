 Git and GitHub**

### **Project Title: News Data Analysis Pipeline**

---

## **Overview**

This task focuses on setting up a Python environment, managing version control with Git and GitHub, and configuring CI/CD workflows. Additionally, it includes performing **Exploratory Data Analysis (EDA)** on a news dataset, covering descriptive statistics, sentiment analysis, topic modeling, time series analysis, and publisher analysis.

---

## **Folder Structure**

The suggested folder structure for this task is:

```
├── .vscode/
│   └── settings.json            # VSCode settings
├── .github/
│   └── workflows/
│       └── unittests.yml        # GitHub Actions workflow for CI/CD
├── .gitignore                   # Ignore unnecessary files for Git
├── requirements.txt             # Project dependencies
├── README.md                    # Documentation for Task 1
├── src/
│   ├── __init__.py              # Initialization for the source code
├── notebooks/
│   ├── __init__.py              # Initialization for notebooks
│   └── README.md                # Notebook documentation
├── tests/
│   ├── __init__.py              # Initialization for tests
└── scripts/
    ├── __init__.py              # Initialization for scripts
    └── README.md                # Script documentation
```

---

## **Steps to Complete the Task**

### **1. Setting Up Python Environment**

1. **Create a Virtual Environment**:
   ```bash
   python -m venv venv
   ```
2. **Activate the Virtual Environment**:
   - **On Windows**:
     ```bash
     .\venv\Scripts\activate
     ```
   - **On macOS/Linux**:
     ```bash
     source venv/bin/activate
     ```

3. **Install Dependencies**:
   Create a `requirements.txt` file and add necessary libraries:
   ```text
   pandas
   numpy
   matplotlib
   seaborn
   nltk
   textblob
   ```
   Install dependencies using:
   ```bash
   pip install -r requirements.txt
   ```

---

### **2. Git Version Control**

1. **Initialize Git Repository**:
   ```bash
   git init
   ```

2. **Create a New Branch for Task 1**:
   ```bash
   git checkout -b task-1
   ```

3. **Commit Changes Frequently**:
   ```bash
   git add .
   git commit -m "Initial setup for Task 1: Project structure and dependencies"
   ```

4. **Push to GitHub**:
   ```bash
   git remote add origin <your-repository-url>
   git push -u origin task-1
   ```

---

### **3. CI/CD Configuration**

Add a GitHub Actions workflow in `.github/workflows/unittests.yml`:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - task-1

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run tests
        run: pytest
```

---

## **4. Exploratory Data Analysis (EDA)**

### **Descriptive Statistics**

1. **Headline Length Statistics**:
   - Calculate basic statistics (mean, median, min, max) for headline lengths.

2. **Articles per Publisher**:
   - Count the number of articles per publisher to identify active sources.

3. **Publication Trends**:
   - Analyze publication dates to detect trends during specific events or days.

### **Sample Code for Descriptive Statistics**

```python
import pandas as pd

# Load the dataset
df = pd.read_csv('news_data.csv')

# Headline length statistics
df['headline_length'] = df['headline'].apply(len)
print(df['headline_length'].describe())

# Articles per publisher
print(df['publisher'].value_counts())
```

---

### **Text Analysis (Sentiment Analysis & Topic Modeling)**

1. **Sentiment Analysis**:
   - Use `TextBlob` to classify headlines as positive, negative, or neutral.

2. **Keyword/Topic Extraction**:
   - Identify common keywords or significant topics using NLP techniques.

### **Sample Code for Sentiment Analysis**

```python
from textblob import TextBlob

# Function for sentiment analysis
def get_sentiment(text):
    return TextBlob(text).sentiment.polarity

df['sentiment'] = df['headline'].apply(get_sentiment)
print(df[['headline', 'sentiment']])
```

---

### **Time Series Analysis**

1. **Publication Frequency**:
   - Analyze the frequency of news publications over time to detect spikes related to events.

### **Sample Code for Time Series Analysis**

```python
df['date'] = pd.to_datetime(df['date'])
df.set_index('date', inplace=True)

# Plot publication frequency
df.resample('D').size().plot(title='Publication Frequency')
```

---

### **Publisher Analysis**

1. **Identify Top Publishers**:
   - Determine which publishers contribute the most articles.

2. **Domain Analysis** (if emails are used as publishers):
   - Extract unique domains from email addresses to identify frequent contributors.

### **Sample Code for Publisher Analysis**

```python
# Top publishers
print(df['publisher'].value_counts().head(10))
```

---

## **Key Performance Indicators (KPIs)**

- **Development Environment Setup**: Successfully set up the Python environment and dependencies.
- **Git Workflow**: Frequent and descriptive commits.
- **CI/CD Pipeline**: Configured automated testing using GitHub Actions.
- **EDA Analysis**: Completed descriptive statistics, sentiment analysis, time series, and publisher analysis.

---

## **How to Run the Project**

1. **Activate Virtual Environment**:
   ```bash
   source venv/bin/activate
   ```

2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Run EDA Script**:
   ```bash
   python scripts/eda_analysis.py
   ```

---

## **Commit History Guidelines**

- **Commit Example 1**:
  ```bash
  git commit -m "Added initial folder structure and requirements.txt"
  ```

- **Commit Example 2**:
  ```bash
  git commit -m "Performed headline length analysis and publisher counts"
  ```

- **Commit Example 3**:
  ```bash
  git commit -m "Added sentiment analysis for news headlines"
  ```

