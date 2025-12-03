# Panda Time Series

## **Explanation of Each Function**

1. **`pd.to_datetime()`**:
   - Converts a column or Series to `datetime` format.
   - Example: Convert the `Date` column in the DataFrame to a `datetime` object for time series operations.
1. **`df.resample()`**:
   - Aggregates time series data into specified intervals (e.g., daily, weekly).
   - Example: Resample the data into 2-day intervals and sum the `Value` column within each interval.
1. **`df.shift()`**:
   - Shifts the data in a column forward or backward by a specified number of periods.
   - Example: Shift the `Value` column forward by one period, and backward by one period.

```python
# Panda Time Series

import pandas as pd
import numpy as np

# Create sample time series data
data = {
    'Date': ['2024-01-01', '2024-01-02', '2024-01-03', '2024-01-04', '2024-01-05'],
    'Value': [100, 200, 300, 400, 500]
}

# Create a DataFrame
df = pd.DataFrame(data)
print("Original DataFrame:")
print(df)
print("\n")

# ------------------------------
# 1. pd.to_datetime(): Convert 'Date' column to datetime object
# ------------------------------
df['Date'] = pd.to_datetime(df['Date'])
print("DataFrame with 'Date' column as datetime object:")
print(df)
print("\n")

# Set the 'Date' column as the index for time series operations
df.set_index('Date', inplace=True)

# ------------------------------
# 2. df.resample(): Aggregate time series data
# ------------------------------
# Resample the data to 2-day intervals, summing the 'Value' column
resampled_df = df.resample('2D').sum()
print("Resampled DataFrame (2-day intervals, summed values):")
print(resampled_df)
print("\n")

# ------------------------------
# 3. df.shift(): Shift data by a specified number of periods
# ------------------------------
# Shift the 'Value' column forward by one period
df['Shifted Value'] = df['Value'].shift(1)
print("DataFrame with 'Value' column shifted forward by one period:")
print(df)
print("\n")

# Shift the 'Value' column backward by one period
df['Backward Shifted Value'] = df['Value'].shift(-1)
print("DataFrame with 'Value' column shifted backward by one period:")
print(df)
print("\n")


'''
OUTPUT
Original DataFrame:
         Date  Value
0  2024-01-01    100
1  2024-01-02    200
2  2024-01-03    300
3  2024-01-04    400
4  2024-01-05    500


DataFrame with 'Date' column as datetime object:
        Date  Value
0 2024-01-01    100
1 2024-01-02    200
2 2024-01-03    300
3 2024-01-04    400
4 2024-01-05    500


Resampled DataFrame (2-day intervals, summed values):
            Value
Date
2024-01-01    300
2024-01-03    700
2024-01-05    500


DataFrame with 'Value' column shifted forward by one period:
            Value  Shifted Value
Date
2024-01-01    100            NaN
2024-01-02    200          100.0
2024-01-03    300          200.0
2024-01-04    400          300.0
2024-01-05    500          400.0


DataFrame with 'Value' column shifted backward by one period:        
            Value  Shifted Value  Backward Shifted Value
Date
2024-01-01    100            NaN                   200.0
2024-01-02    200          100.0                   300.0
2024-01-03    300          200.0                   400.0
2024-01-04    400          300.0                   500.0
2024-01-05    500          400.0                     NaN
'''
```

