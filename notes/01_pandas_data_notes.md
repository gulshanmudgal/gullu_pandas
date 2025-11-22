# Notes for 01_Pandas_Data.ipynb

## What is a DataFrame?

A DataFrame is a two-dimensional, size-mutable, potentially heterogeneous tabular data structure with labeled axes (rows and columns). It is one of the primary data structures in pandas, similar to a spreadsheet or SQL table.

Key characteristics:
- **2D Structure**: Rows and columns
- **Labeled**: Rows have indices, columns have names
- **Heterogeneous**: Different columns can have different data types
- **Size-mutable**: Can add/remove rows and columns

## Creating DataFrames

DataFrames can be created from various sources:
- CSV files: `pd.read_csv('file.csv')`
- Dictionaries: `pd.DataFrame({'col1': [1, 2, 3], 'col2': ['a', 'b', 'c']})`
- Lists of lists, Excel files, SQL queries, etc.

## Associated Data Types

### Pandas Data Structures
- **Series**: 1-dimensional labeled array (single column)
- **DataFrame**: 2-dimensional labeled data structure (multiple columns)

### Column Data Types (dtypes)
Common data types in pandas DataFrames:
- **int64**: Integer numbers (64-bit)
- **float64**: Floating-point numbers (64-bit)
- **object**: String/text data or mixed types
- **bool**: Boolean values (True/False)
- **datetime64**: Date and time data
- **category**: Categorical data (limited set of values)
- **timedelta64**: Time differences

### Checking and Converting Data Types
- Check dtypes: `df.dtypes` or `df.info()`
- Convert dtypes: `df['column'].astype('new_type')`

### Accessing Data
- Single column: `df['column_name']` or `df.column_name`
- Multiple columns: `df[['col1', 'col2']]`
- Rows by index: `df.loc[index]` or `df.iloc[position]`

## DataFrame Manipulations

DataFrames support various manipulation operations:

### Indexing and Selection
- **iloc**: Integer-based indexing
  - `df.iloc[0]` - Select first row (returns Series)
  - `df.iloc[[0, 2]]` - Select multiple rows (returns DataFrame)
  - `df.iloc[[0, 1], [1, 2]]` - Select subset of rows and columns (returns DataFrame)

- **loc**: Label-based indexing
  - `df.loc[0]` - Select row by label (returns Series)
  - `df.loc[[0, 2]]` - Select multiple rows by labels (returns DataFrame)
  - `df.loc[[0, 2], ['first', 'email']]` - Select rows and columns by labels (returns DataFrame)
  - `df.loc[0:10, 'RemoteWork':'YearsCode']` - Slice rows and columns by labels (returns DataFrame)

### Column Operations
- `df.columns` - Get column names (returns Index)
- `df.shape` - Get dimensions (returns tuple: rows, columns)

### Value Analysis
- `df['column'].value_counts()` - Count unique values in a column (returns Series)

## Impact on Data Types After Operations

Operations on DataFrames can change the returned data type:

- **Single column access** (`df['col']` or `df.col`): Returns a **Series** (1D)
- **Multiple columns access** (`df[['col1', 'col2']]`): Returns a **DataFrame** (2D)
- **Single row selection** (`df.iloc[0]` or `df.loc[0]`): Returns a **Series**
- **Multiple rows selection** (`df.iloc[[0,1]]` or `df.loc[[0,1]]`): Returns a **DataFrame**
- **Subset selection** (`df.iloc[[0,1], [1,2]]`): Returns a **DataFrame**
- **Slicing** (`df.loc[0:10, 'col1':'col2']`): Returns a **DataFrame**
- **Value counts** (`df['col'].value_counts()`): Returns a **Series** with counts
- **Shape** (`df.shape`): Returns a **tuple** (int, int)
- **Columns** (`df.columns`): Returns an **Index** object

Understanding these return types is crucial for chaining operations and avoiding errors in data manipulation workflows.

DataFrames are the core of data manipulation in pandas, allowing for efficient data analysis, cleaning, and transformation operations.