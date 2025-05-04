
# 📊 Basic Finance Data Analysis with Python

This is a beginner-friendly project for analyzing financial stock data using Python.  
We focus on three major tickers: **AAPL (Apple)**, **MSFT (Microsoft)**, and **META (Meta Platforms)**.

The project includes all fundamental steps in a data analysis workflow: importing data, cleaning, exploring, and visualizing key insights.

---

## 📦 Technologies Used

- Python 3.x
- [yfinance](https://pypi.org/project/yfinance/)
- pandas
- numpy
- matplotlib
- seaborn

---

## 🚀 Project Steps

### ✅ Step 1: Import Libraries & Get Data

Use the `yfinance` library to download historical stock data.

```python
import yfinance as yf
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

tickers = ['AAPL', 'MSFT', 'META']
dfs = []

for ticker in tickers:
    df = yf.download(ticker, start='2015-01-01', rounding=True)
    df['Ticker'] = ticker
    df.reset_index(inplace=True)
    dfs.append(df)
```

---

### ✅ Step 2: Concatenate Data

Combine all individual ticker data into one DataFrame.

```python
df_all = pd.concat(dfs, ignore_index=True)
```

---

### ✅ Step 3: Access & Explore Data

- `.info()` – Understand the structure of the data
- `.describe()` – View summary statistics
- `.head()` – Preview the first few rows

---

### ✅ Step 4: Clean Data

- Remove duplicate entries
- Handle missing values
- Add useful columns for time-based analysis

```python
df_all.drop_duplicates(inplace=True)
df_all.dropna(inplace=True)

df_all['Year'] = df_all['Date'].dt.year
df_all['Month'] = df_all['Date'].dt.month
df_all['Quarter'] = df_all['Date'].dt.quarter
df_all['DayOfWeek'] = df_all['Date'].dt.day_name()
```

---

### ✅ Step 5: Visualize Data

Create various charts to extract insights from the data:

- **📅 Average high price by day of the week**
- **📈 Quarterly volume trends**
- **📊 Yearly average closing prices by ticker**
- **📉 Open vs Close trends**

Example: Plot average high prices by day of the week across all tickers.

```python
avg_high = df_all.groupby(['Ticker', 'DayOfWeek'])['High'].mean().reset_index()
sns.barplot(data=avg_high, x='DayOfWeek', y='High', hue='Ticker')
plt.title('Average High Price by Day of Week')
plt.xticks(rotation=15)
plt.tight_layout()
plt.show()
```

---

## 📌 Goals

- Practice real-world financial data analysis
- Understand time-series and categorical breakdowns
- Build clean, informative visualizations
- Enhance Python and data analysis skills

---

## 📁 Folder Structure (Optional)

```
project/
│
├── data/               # Optional: saved CSVs or raw data
├── visuals/            # Plots and charts
├── scripts/            # Jupyter Notebooks or .py files
├── README.md
```

---

## 🗒️ To-Do Ideas (Optional Extensions)

- Add rolling average calculations
- Compare performance between tickers
- Build interactive dashboards using Plotly or Streamlit

---

## 📬 Contact

Feel free to open an issue or submit a pull request if you'd like to contribute or report an improvement.

---
