# Pandas

Pandas is a library used to work with series or matrixes of values.

```python
import pandas as pd
```

## Series
One dimensional labeled array, able to hold any data. The labels are called `index`
```python
# standard array, but it could also be a numpy array
arr = [ 12, 3, 4 ]

# create a series using default numbered indexes
pd.Series(arr)

# use custom indexes
med_series = pd.Series(arr, index = [ 'ibuprofen', 'paracetamol', 'nurofen' ])
```

### Mathematical operations on series

```python
# med prices
med_prices = pd.Series([ 12, 3, 4 ], index = [ 'ibuprofen', 'paracetamol', 'nurofen' ])

# add 5 to each element of the series
new_med_prices = med_prices + 5

# we can check the price diffence
diff_prices = new_med_prices - med_prices
```

### Accessing Series
```python
# by index - all apply like for arrays
med_prices[0]
# first 3 elements, so index 0-2
med_prices[:3]
# last 2 elements
med_prices[-2:]
# multiple elements
med_prices[0,2]

# by index label
med_prices['nurofen']
# multiple - use array in array
med_prices[ [ 'nurofen', 'ibuprofen' ] ]
```

## DataFrame

Two dimensional tabular data structure with labeled axes (rows and columns)

```python
students = [ 'Adi', 'Juli', 'Lux', 'Greg' ]

# from array (or it could be Series)
stud_df = pd.DataFrame(students, columns=['Student'])

grades = [ 5, 7, 4, 9 ]
# table from dictionary/map
stud_grades = pd.DataFrame({'Student':students, 'Grade':grades})
```

Above creates the table:
|| Student| Grade|
|---|---|---|
|0| Adi  |5|
|1| Juli |7|
|2| Lux  |4|
|3| Greg |9|

### Accessing DataFrame

```python
# first two rows - row 0 and 1
stud_grades[:2]
# every 2 rows - use :: for that
stud_grades[::2]
# every 2 rows in reverse
stud_grades[::-2]
```

#### Using `loc` and `iloc`
Both `loc` and `iloc` use the following format. The only difference is that `iloc` only uses indexes, while loc uses index labels
> dataframe.loc[row selection, column selection]

```python
# second row, index here is numeric
stud_grades.loc[1]

# get students grade for second and third student
stud_grades.loc[ [1, 2], ['Grade'] ]
# same via iloc
stud_grades.iloc[ [1, 2], [1] ]
```

#### Condition based
```python
# get students with passing grades
stud_grades.loc[ stud_grades['Grade'] >= 5 ]
```

#### Utility functions:  head, tail, shape, info, min, max, unique, value_counts, mean, median, mode
Utility functions used to access various info
```python
stud_grades.min() or stud_grades['grade'].min()

#info about the columns and types
stud_grades.info()

# top 5 rows
stud_grades.head()

# no of rows and columns. Note it's a property, not function
stud_grades.shape

# first mode in a multi mode data set. Not our case. Drop the index at the end if it's just one
stud_grades.mode()[0]
```

#### Date time functions
```python
# when column is date
df1['date'].dt.strftime('%m/%d/%Y')
# access month
df1['date'].dt.month

# when field is not
pd.to_datetime(df['date'], dayFirst=True)
```

#### Group By
Used to split data into groups
```python
# median of the grades of students in the same location
stud_grades.groupby(['location'])['grade'].median()
```

### Add/Remove column

```python
# add column
stud_grades['location'] = ['bucharest', 'london', 'sydney', 'melbourne']

# remove the new column in place. axis = 1 means column, while 0 is row
stud_grades.drop('location', axis=1, inplace=True)

# remove row with index 1 (second row). Note axis=0
stud_grades.drop(1, axis=0)

# reset index, since it's inconsistent after removal of row 1. drop=True removes the old index, otherwise it gets saved as a column labeled 'index'
stud_grades.reset_index(drop=True, inplace=True)
```
> Note: if you don't want to use `inplace` above to change the original data frame, use `copy` function to create a copy of the result, same as with numpy arrays

### Combining DataFrames

```python
# df1 comes on top, df2 bottom, contact vertically. Would be horizontally if axis=1. Note, if columns are different, NaN will be used for missing values
pd.concat([df1, df2], axis=0)

# use merge to merge two frames - same as a SQL outer join. Also possible left, right and inner joins/merge
pd.merge(df1, df2, how='outer', on='columnName')

# join uses index labels, so no 'on'
df1.join(df2, how='left')
```

### Applying functions to DataFrame

```python
# define function to calculate if student has passed
passed = lambda grade: grade >= 5

# add column for status if a student passed the class
stud_grades['passed'] = stud_grades['grade'].apply(passed)
```
