---
title: pandas
description: pandas
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
---
- _pandas (panel data)_ provides high-level data structures and functions designed to make working with structured or tabular data fast, easy, and expressive.
- It provides sophisticated indexing functionality to make it easy to
  - reshape
  - slice and dice
  - aggregations
  - selecting subsets of data

### Install

`pip install pandas`

### Import

```python
import pandas as pd
```

- The primary objects in pandas are
  - **DataFrame**
    - a tabular, column-oriented data structure with both row and column labels.
  - **Series**
    - a one-dimensional labelled array object.

### Dataframe

```python
import pandas as pd

if __name__ == "__main__":
    df = pd.DataFrame({'name': ['Jeff', 'Esha', 'Jia'],
                        'age': [30, 56, 8]})
    first_name = df.name[0]
    print(first_name)
```

- A `DataFrame` is how Pandas stores data in rectangular grids to manipulate it easily.
- It can contain:
  - **Pandas DataFrame**
  - **Pandas Series**:= a one-dimensional labelled array capable of holding any data type with axis labels or index. i.e. one column from a `DataFrame`.
  - **NumPy ndarray** := a record or structured
  - **2D ndarray**
  - **Dictionaries of 1D ndarray's, lists, dictionaries or Series**

- A `DataFrame` consists of three main components:
    1. Data
    2. Index
    3. Columns

```python
df = pd.DataFrame({<key>: <value>, <key>: value})

# Copy a df to another
<new_df> = df.copy()

# Indexing a DataFrame
df['<col_name>']['<row_name>'] # accessing the data using names
df.<col_name>['<row_name>'] # accessing the data using names
df.loc['<row_name>', '<col_name>'] # accessing the data using names
df.iloc['<row_index>', '<col_index>'] # accessing the data using indices
df_new = df[['<first_col_name>', '<second_col_name>']] # selecting some columns
df = pd.read_csv("<file.csv>", index_col='<col_name>') # read csv file. Here `index_col` parameter uses <col_name> column for the index.
df.shape # (#row, #col)
df.head() #

# Slicing a Dataframe
df['<col_name>'] # type: Series
df[['<col_name>']] # type: DataFrame
df['<col_name>'][<first_col_index:second_col_index>] # part of the <col_name>
df.loc[:, '<first_col_name>':'<second_col_name>'] # all rows some columns
df.loc['<first_row_name>':'<second_row_name>', :] # all cols some rows
df.loc['<first_row_name>':'<second_row_name>', '<first_col_name>':'<second_col_name>'] # some cols some rows
df.loc['<first_row_name>':'<second_row_name', ['<first_col_name>', '<second_col_name>']] # give cols as a list
df.iloc[:, '<first_col_index>':'<second_col_index>'] # all rows some columns
df.iloc['<first_row_index>':'<second_row_index>', :] # all cols some rows
df.iloc['<first_row_index>':'<second_row_index>', '<first_col_index>':'<second_col_index>'] # some cols some rows
df.iloc['<first_row_index>':'<second_row_index', ['<first_col_index>', '<second_col_index>']] # give cols as a list

# Filtering a `Dataframe`: Selecting based on its properties
## Filtering with a Boolean Series
df[df.<col_name> > <value>]
# OR
<var> = df.<col_name> > <value>
df[<var>]
## Combining Filters
df[(df.<col_name> >= <value>) & (df.<col_name> < <value>)]
df[(df.<col_name> >= <value>) | (df.<col_name> < <value>)]

## It excludes columns with zero entries
df.loc[:, df.all()]

## It excludes columns with all zeros
df.loc[:, df.any()]

## It excludes columns with a NaN
df.loc[:, df.isnull().any()]

## It excludes column with all NaNs
df.loc[:, df.notnull().all()]

## Remove rows with NaN entry
df.dropna(how='any')

## Filtering a column based on another
df.<first_col_name>[df.<second_col_name> > <value>]

## Modifying a column based on another
df.<first_col_name>[df.<second_col_name> > <value>] += <value>

# Transforming a DataFrame
## DataFrame Vectorized Methods
def <function_name>(<variable>):
    return <operations on variable>
df.apply(<function_name>)
## OR
df.apply(lambda <variable>:<operations on variable>)

## Storing a Transformation
df[<new_column_name>] = df.<existing_column_name>.<operations>

# Changing the name of columns
df.columns = [<first_col_name>, <second_col_name>]

## DataFrame Index
df.index # a special kind of Series containing strings in this instance.

## Working with String Values
df.index = df.index.str.upper() # i.e.,
df.index = df.index.map(str.lower) # for the index apply is not working, use map instead.

## Defining Columns Using Other Columns
df.<new_column_name> = df.<existing_column_name_1> <operation> df.<existing_column_name_2>
```

[Ref](https://campus.datacamp.com/courses/manipulating-dataframes-with-pandas/extracting-and-transforming-data?ex=5)

### pandas.DataFrame.floordiv

- `DataFrame.floordiv(other, axis='columns', level=None, fill_value=None)`
- Get Integer division of dataframe and other, element-wise (binary operator floordiv).
- Equivalent to dataframe // other, but with support to substitute a fill_value for missing data in one of the inputs.

[Ref](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.floordiv.html)

### pandas.DataFrame.dropna

[Ref](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dropna.html)

### Hello world

```python
import pandas as pd

# pd.DataFrame() is a table.
# index := row names
pd.DataFrame({'Bob': ['I liked it.', 'It was awful.'], 
              'Sue': ['Pretty good.', 'Bland.']},
              index=['Product A', 'Product B'])
df_= pd.read_csv("<dir>/<file_name>.csv", index_col=0) # if you have index column
df_.iloc[<index>]
df_.loc[<index>]
df_['<col_name>'] # whole col
df_[<col_name>][col_index] # value in <col_name>

## iloc is conceptually simpler than loc.

### iloc selects data based on its numerical position in the data (index-based selection)
df_.iloc[<index>] # select the <index>th row (row-first, col-second)
df_.iloc[:, 0] # select the <index>th col

### loc selects attributes (label-based selection)
df_.loc[0, '<col_name>'] # (row-first, col-second)
df_.loc[:, ['<col_name>', '<col_name>']]
df_.loc[(df_.<col_name> == '<col_name>') & (df_.<col_name> == '<col_name>') | (df_.<col_name>.isin(['<col_name>', '<col_name>'])) & (df_.<col_name>.notnull())] # selects the rows of which col equals to the <col_name> ... |

## the index is not immutable.

df_.set_index("<title_name>") # creates a new title instead of overriding

df_[<col_name>] = '<str>' # sets whole col <str>

df_.<col_name>.describe() # details of df_

df_.<col_name>.mean()

df_.<col_name>.unique()

df_.<col_name>.value_counts()

df_.<col_name>.map(lambda p:p-1)

df_.apply(<function_name>, axis='columns')

df_.shape # (<no_recs>, <no_cols>)
df_.head() # the first 5 recs
df_.head(<no_records>)

###################################

# pd.Series() is a list, a single column of a DataFrame.
# index := row names
# name := a column name
```

### pandas.DataFrame.astype

[Ref](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.astype.html)

### pandas.pivot_table

```python
pandas.pivot_table(data, values=None, index=None, columns=None, aggfunc='mean',fill_value=None, margins=False, dropna=True, margins_name='All', observed=False)
```

- `data`: DataFrame
- `values`: column to aggregate, optional
- `aggfunc`:
- `fill_value`: scalar, default none. Value to replace missing values with.
- `dropna`: bool, default True

[Ref](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.pivot_table.html)
