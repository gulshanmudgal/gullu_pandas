# Notes for 02_Pandas_Indexes.ipynb

## What are Pandas Indexes?

Indexes in pandas are immutable arrays that label the rows of a DataFrame or Series. They provide a way to uniquely identify and access data points.

Key characteristics:
- **Immutable**: Cannot be changed after creation
- **Unique labels**: Typically unique identifiers for rows
- **Efficient access**: Enable fast lookups and operations
- **Flexible types**: Can be integers, strings, dates, etc.

## Default Indexes

When creating a DataFrame without specifying an index, pandas automatically assigns a **RangeIndex** (0, 1, 2, ..., n-1).

## Setting Custom Indexes

### Using set_index()
Set a column as the index:
```python
df.set_index('column_name')  # Returns new DataFrame
df.set_index('column_name', inplace=True)  # Modifies original DataFrame
```

### During Data Loading
Specify index column when reading files:
```python
pd.read_csv('file.csv', index_col='column_name')
```

## Resetting Indexes

### Using reset_index()
Reset index back to default RangeIndex:
```python
df.reset_index()  # Returns new DataFrame with old index as column
df.reset_index(inplace=True)  # Modifies original DataFrame
```

## Index Operations

### Accessing Data with Indexes
- `df.loc['label']` - Access row by index label
- `df.loc[['label1', 'label2']]` - Access multiple rows

### Sorting by Index
```python
df.sort_index()  # Sort by index labels
df.sort_index(inplace=True)  # Modify in place
```

## Index Types

- **RangeIndex**: Default integer index (0, 1, 2, ...)
- **Index**: Generic index for various data types
- **DatetimeIndex**: For datetime data
- **CategoricalIndex**: For categorical data
- **MultiIndex**: Hierarchical indexes (multiple levels)

## Best Practices

- Choose meaningful indexes that uniquely identify rows
- Use `inplace=True` when you want to modify the original DataFrame
- Be aware that operations like `set_index()` without `inplace=True` return a new DataFrame
- Indexes enable efficient data alignment and merging operations

Indexes are fundamental to pandas' powerful data manipulation capabilities, enabling fast lookups, alignment, and relational operations.