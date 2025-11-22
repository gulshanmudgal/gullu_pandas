# 00_Pandas Demo Notes

This notebook demonstrates basic data exploration using Pandas on the Stack Overflow Developer Survey dataset.

## Importing Libraries
- `import pandas as pd`: Imports the Pandas library, essential for data manipulation and analysis in Python.

## Loading Data
- `df = pd.read_csv('./data/survey_results_public.csv')`: Loads the main survey results into a DataFrame named `df`. This dataset contains responses from developers worldwide.
- `schema_df = pd.read_csv('./data/survey_results_schema.csv')`: Loads the schema file, which provides descriptions for each column in the main dataset.

## DataFrame Display Options
- `pd.set_option('display.max_columns', 114)`: Sets the maximum number of columns to display when printing a DataFrame, ensuring all columns are visible.
- `pd.set_option('display.max_rows', 85)`: Sets the maximum number of rows to display, allowing more data to be shown at once.

## Basic Data Exploration
- `df.shape`: Returns the dimensions of the DataFrame (rows, columns). Useful for understanding the size of the dataset.
- `df.info()`: Provides a summary of the DataFrame, including column names, non-null counts, and data types. Helps identify missing data and data types.
- `df.columns.to_list()`: Lists all column names as a Python list. Useful for iterating over columns or checking specific ones.
- `df.dtypes`: Shows the data type of each column. Important for understanding how data is stored and what operations are possible.

## Viewing Data
- `df.head()`: Displays the first 5 rows of the DataFrame. Good for a quick look at the data structure and sample values.
- `df.head(10)`: Shows the first 10 rows, providing more context.
- `df.tail()`: Displays the last 5 rows. Useful for checking the end of the dataset.
- `df.tail(10)`: Shows the last 10 rows.

## Schema Information
- The schema DataFrame (`schema_df`) contains explanations for each column in the main dataset, helping to understand what each field represents.

## Additional Notes
- This dataset is from the Stack Overflow Developer Survey, which collects information about developers' experiences, technologies used, salaries, etc.
- For larger datasets, setting display options prevents truncation and allows better inspection.
- Common next steps after loading data include data cleaning (handling missing values, duplicates), filtering, grouping, and visualization.
- Pandas provides powerful tools for data manipulation: filtering with boolean indexing, grouping with `groupby()`, merging DataFrames, etc.
- Always check for data quality issues like missing values (`df.isnull().sum()`) and outliers before analysis.