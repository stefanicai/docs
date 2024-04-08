# Data processing

Data processing involves several steps.

## Replace null values
Places where we don't have values for relevant attributes. We can replace them with `mean` or `meadian` for numeric. If it's not a number, we could use `mode`.

## Removing duplicates
If we have the same data several times in our data set

## Clean-up the data
Numbers are not correct or not in the right formats etc. Unusable for whatever reason

## Convert text values to numbers

This can be cases where numeric data is stored as text in the source data set - e.g. `"15" -> 15`

Or it can be representing text data in a numeric way. E.g. say we have the gender and we decide to use something like this
```
female = 0
male = 1
other = 2
```
