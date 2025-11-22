# Notes for 03_Pandas_Filtering.ipynb

## DataFrame Filtering in Pandas

Filtering allows you to select specific rows from a DataFrame based on conditions. This is essential for data analysis and cleaning, enabling you to focus on relevant subsets of data for deeper insights.

## Basic Filtering

### Boolean Conditions
Create filters using comparison operators that return boolean Series:

```python
# Create a sample DataFrame
people = {
    "first": ["gullu", "shiv", "laxman"],
    "last": ["Ji", "Doe", "Doe"],
    "email": ["gullu@test.com", "shiv@test.com", "laxman@test.com"]
}
df = pd.DataFrame(people)

# Create a boolean filter
lastNameFilter = (df['last'] == "Doe")
print(lastNameFilter)
# Output: 0    False, 1     True, 2     True

# Apply the filter
df[lastNameFilter]
# Returns DataFrame with rows where last == "Doe"
```

### Using loc for Filtering
`loc` is preferred for filtering as it allows both row filtering and column selection in one operation:

```python
# Filter rows only
df.loc[lastNameFilter]

# Filter rows and select specific columns
df.loc[lastNameFilter, ['first', 'email']]
# Returns DataFrame with rows where last == "Doe", showing only 'first' and 'email' columns
```

**Why use `loc`?**
- More readable than direct boolean indexing
- Allows simultaneous row and column selection
- Explicit about what you're selecting

## Complex Filtering

### Multiple Conditions with AND (&)
Combine conditions where ALL must be true:

```python
# Filter for people with last name "Doe" AND first name "shiv"
complexFilter = (df["last"] == "Doe") & (df['first'] == "shiv")
df.loc[complexFilter]
# Returns only the row for "shiv Doe"
```

**Important:** Always use parentheses around each condition when combining with `&` or `|`.

### Multiple Conditions with OR (|)
Combine conditions where AT LEAST ONE must be true:

```python
# Filter for people with last name "Doe" OR first name "gullu"
complexFilter2 = (df["last"] == "Doe") | (df['first'] == "gullu")
df.loc[complexFilter2]
# Returns rows for "gullu Ji", "shiv Doe", and "laxman Doe"
```

## Advanced Filtering Techniques

### Filtering by Multiple Values
Use `isin()` to check if values are in a list - more efficient than multiple OR conditions:

```python
# Load survey data
data_df = pd.read_csv('../data/survey_results_public.csv')

# Filter for specific countries
countries = ['United States of America', 'India']
countryFilter = data_df['Country'].isin(countries)
data_df.loc[countryFilter]
# Returns all rows where Country is either 'United States of America' or 'India'
```

### String-based Filtering
Filter text columns using string methods. Handle NaN values carefully:

```python
# Filter for respondents who have worked with Python
languageFilter = data_df["LanguageHaveWorkedWith"].str.contains("Python", na=False)
data_df.loc[languageFilter, 'LanguageHaveWorkedWith']
# Returns the LanguageHaveWorkedWith column for rows containing "Python"
```

**Why `na=False`?**
- String methods on NaN values raise errors
- `na=False` treats NaN as False (not containing the string)
- Alternative: `na=True` treats NaN as True

### Numerical Filtering
Filter based on numerical conditions for data analysis:

```python
# Filter for high salaries
high_salary = data_df["ConvertedCompYearly"] > 90000
data_df.loc[high_salary, ['Country', 'ConvertedCompYearly']]
# Returns Country and ConvertedCompYearly for respondents earning > $90,000
```

## Handling Edge Cases

### Dealing with NaN Values
NaN values can cause issues in filtering:

```python
# Check for NaN in a column
df['column'].isna()  # Returns True for NaN values
df['column'].notna()  # Returns True for non-NaN values

# Filter out NaN values
df.loc[df['column'].notna()]

# Include NaN in filters
df.loc[df['column'].isna() | (df['column'] > 100)]
```

### Case Sensitivity in String Filtering
String filtering is case-sensitive by default:

```python
# Case-sensitive search
df['column'].str.contains('Python')

# Case-insensitive search
df['column'].str.contains('python', case=False)
```

## Best Practices

- **Use descriptive variable names** for filters (e.g., `high_salary_filter`, `python_users`)
- **Prefer `loc`** over direct boolean indexing for better readability and functionality
- **Always handle NaN values** in string operations to avoid errors
- **Use parentheses** for complex conditions: `(cond1) & (cond2)`
- **Use `isin()`** for multiple value checks instead of chaining OR conditions
- **Test filters** on small DataFrames first to verify logic
- **Consider performance** - filters on indexed columns are faster

## Filter Operations Summary

| Operation | Syntax | Purpose | Example |
|-----------|--------|---------|---------|
| Equality | `df['col'] == 'value'` | Exact match | `df['status'] == 'active'` |
| Inequality | `df['col'] > 100` | Numerical comparison | `df['age'] > 30` |
| Multiple values | `df['col'].isin(['a', 'b'])` | Check membership | `df['country'].isin(['US', 'CA'])` |
| String contains | `df['col'].str.contains('text')` | Text search | `df['skills'].str.contains('Python')` |
| Is null | `df['col'].isna()` | Find missing values | `df['salary'].isna()` |
| Is not null | `df['col'].notna()` | Find non-missing values | `df['email'].notna()` |
| AND | `cond1 & cond2` | Both conditions true | `(df['age'] > 20) & (df['age'] < 65)` |
| OR | `cond1 \| cond2` | Either condition true | `(df['status'] == 'new') \| (df['status'] == 'active')` |

## Common Filtering Patterns

### Filtering Date Ranges
```python
# Assuming 'date_col' is datetime
start_date = '2023-01-01'
end_date = '2023-12-31'
date_filter = (df['date_col'] >= start_date) & (df['date_col'] <= end_date)
df.loc[date_filter]
```

### Filtering by Row Index
```python
# Filter by position
df.iloc[10:20]  # Rows 10-19

# Filter by label (if custom index)
df.loc['label1':'label5']
```

### Complex Multi-Column Filters
```python
# Advanced filter combining multiple columns
advanced_filter = (
    (df['country'] == 'USA') & 
    (df['salary'] > 50000) & 
    (df['experience'] >= 5) &
    (df['skills'].str.contains('Python', na=False))
)
df.loc[advanced_filter, ['name', 'salary', 'skills']]
```

Filtering is fundamental to data analysis, enabling you to focus on relevant subsets of your data for deeper insights and more accurate analysis.