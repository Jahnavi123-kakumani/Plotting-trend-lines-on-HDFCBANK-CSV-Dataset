## Plotting-trend-lines-on-HDFCBANK-CSV-Dataset

## Overview
This repository contains the **HDFCBANK dataset**, which includes historical data for HDFC Bank's stock performance. The purpose of this project is to analyze the data and plot trend lines to understand key trends and patterns.

---

## Dataset
The dataset contains the following key columns:
- **Date**: The date of the record.
- **Open**: Opening stock price.
- **Close**: Closing stock price.
- **High**: Highest stock price for the day.
- **Low**: Lowest stock price for the day.
- **Volume**: Number of shares traded.

---

## Requirements
To work with this dataset and plot trend lines, install the following dependencies:

```bash
pip install pandas matplotlib numpy
```

---

## Plotting Trend Lines

### 1. Load the Dataset
Ensure that the dataset (e.g., `HDFCBANK.csv`) is in the root directory. Load it using Pandas:

```python
import pandas as pd

# Load the dataset
df = pd.read_csv('HDFCBANK.csv')

# Convert 'Date' column to datetime
df['Date'] = pd.to_datetime(df['Date'])

# Sort by date
df = df.sort_values(by='Date')
```

---

### 2. Plot the Trend Lines
We will use `matplotlib` to plot the trend lines for the **Close** price:

```python
import matplotlib.pyplot as plt
import numpy as np

# Extract data
dates = df['Date']
close_prices = df['Close']

# Convert dates to numerical format for trend line
dates_numeric = (dates - dates.min()).dt.days

# Fit a linear trend line
coefficients = np.polyfit(dates_numeric, close_prices, 1)
trend_line = np.polyval(coefficients, dates_numeric)

# Plot the data
plt.figure(figsize=(12, 6))
plt.plot(dates, close_prices, label='Close Prices', color='blue')
plt.plot(dates, trend_line, label='Trend Line', color='red', linestyle='--')

# Add labels and legend
plt.title('HDFC Bank Stock Prices with Trend Line')
plt.xlabel('Date')
plt.ylabel('Close Price')
plt.legend()
plt.grid()
plt.show()
```

---

### 3. Save the Plot
You can save the plot to a file using:

```python
plt.savefig('hdfcbank_trend_line.png')
```

---

## Output
The output graph will show:
1. The actual **Close Price** over time.
2. A **trend line** indicating the overall price trend.

---

## Contributing
Feel free to contribute by:
- Adding more trend analysis methods (e.g., polynomial regression).
- Visualizing other columns like **Volume** or **High/Low** prices.

---

## License
This project is licensed under the MIT License.
