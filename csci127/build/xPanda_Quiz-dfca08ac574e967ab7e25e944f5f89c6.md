# **Pandas Quiz: Test Your Knowledge**

## **Part 1: Data Creation**

1. What function would you use to create a one-dimensional labeled array in Pandas?
   - a) `pd.DataFrame()`
   - b) `pd.Series()`
   - c) `pd.read_csv()`
   - d) `pd.to_excel()`
1. Which function creates a two-dimensional labeled table in Pandas?
   - a) `pd.DataFrame()`
   - b) `pd.Series()`
   - c) `pd.pivot()`
   - d) `pd.melt()`

------

## **Part 2: Data Input/Output (I/O)**

1. Which function reads a CSV file into a DataFrame?
   - a) `pd.read_csv()`
   - b) `pd.read_sql()`
   - c) `pd.read_excel()`
   - d) `pd.to_csv()`
1. If you need to export a DataFrame to an Excel file, which function should you use?
   - a) `pd.read_excel()`
   - b) `pd.to_csv()`
   - c) `pd.to_excel()`
   - d) `pd.read_csv()`

------

## **Part 3: Data Inspection**

1. Which function provides a summary of a DataFrame, including data types and non-null counts?
   - a) `df.head()`
   - b) `df.describe()`
   - c) `df.info()`
   - d) `df.shape`
1. How would you return the dimensions (number of rows and columns) of a DataFrame?
   - a) `df.describe()`
   - b) `df.shape`
   - c) `df.dtypes`
   - d) `df.head()`

------

## **Part 4: Data Selection**

1. What function allows you to select rows or columns based on index positions?
   - a) `df.loc[]`
   - b) `df.iloc[]`
   - c) `df['column_name']`
   - d) `df.groupby()`
1. How would you access multiple columns (e.g., 'col1' and 'col2') in a DataFrame?
   - a) `df[['col1', 'col2']]`
   - b) `df['col1']`
   - c) `df.loc[]`
   - d) `df.iloc[]`

------

## **Part 5: Data Cleaning**

1. Which function detects missing values in a DataFrame?
   - a) `df.dropna()`
   - b) `df.notnull()`
   - c) `df.isnull()`
   - d) `df.fillna()`
1. What function replaces missing values with a specified value?
   - a) `df.dropna()`
   - b) `df.fillna(value)`
   - c) `df.rename()`
   - d) `df.replace()`

------

## **Part 6: Data Transformation**

1. To sort rows of a DataFrame based on a specific column, which function would you use?
   - a) `df.groupby()`
   - b) `df.sort_index()`
   - c) `df.sort_values(by='column')`
   - d) `df.apply()`
1. Which function groups data for aggregation or transformation?
   - a) `df.pivot_table()`
   - b) `df.groupby()`
   - c) `df.astype()`
   - d) `df.corr()`

------

## **Part 7: Data Aggregation**

1. Which function computes the mean of numeric columns in a DataFrame?
   - a) `df.sum()`
   - b) `df.mean()`
   - c) `df.mode()`
   - d) `df.median()`
1. How would you calculate the cumulative sum of numeric values in a DataFrame?
   - a) `df.cumsum()`
   - b) `df.sum()`
   - c) `df.mean()`
   - d) `df.count()`

------

## **Part 8: Merging and Reshaping**

1. If you need to combine two DataFrames based on a common column, which function should you use?
   - a) `pd.concat()`
   - b) `pd.merge()`
   - c) `df.join()`
   - d) `df.melt()`
1. What function converts a DataFrame from wide format to long format?
   - a) `pd.pivot()`
   - b) `df.melt()`
   - c) `df.pivot_table()`
   - d) `pd.concat()`

------

## **Part 9: Statistical Operations**

1. Which function calculates the correlation between numeric columns?
   - a) `df.cov()`
   - b) `df.var()`
   - c) `df.corr()`
   - d) `df.std()`
1. How would you compute the variance of numeric columns?
   - a) `df.corr()`
   - b) `df.var()`
   - c) `df.cumsum()`
   - d) `df.median()`

------

## **Part 10: Time Series Functions**

1. What function converts data into a datetime object in Pandas?
   - a) `pd.to_datetime()`
   - b) `df.resample()`
   - c) `df.shift()`
   - d) `df.groupby()`
1. Which function aggregates time series data in Pandas?
   - a) `df.shift()`
   - b) `pd.to_datetime()`
   - c) `df.resample()`
   - d) `df.groupby()`

------

**Answer Key** (for self-assessment):

1. b | 2. a | 3. a | 4. c | 5. c | 6. b | 7. b | 8. a | 9. c | 10. b | 11. c | 12. b | 13. b | 14. a | 15. b | 16. b | 17. c | 18. b | 19. a | 20. c