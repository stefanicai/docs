# Numpy

Numpy is a library that enables better handling of arrays and matrixes (arrays of arrays). 

Standard library arrays have some limitations. They have to contain the same type of value. More importantly, they don't perform that well for large arrays.

```python
import numpy as np
```


## Arrays

```python
import numpy as np

# create standard array
arr_str = [ "value1", "value2" ]

# convert 
np_arr_str = np.array(arr_str)

print(type(np_arr_str))
```

### np.arrange

Creates a numpy array with values between two numbers (first included, last not), with a specific step.

These statements are equivalent:

```python
np.array(list(range(0, 10))) # uses standard library range

np.arrange(start=0, stop=10, step=1) # using keyword params

np.arrange(0, 10) # using positional params
```

### np.linspace, np.zeros, np.ones, np.eye

Used to generate arrays.

`np.linspace` creates an evenly distributed array, starting from a start value x1, ending with and end value x2, containing a specific number of elements y. It is used like `np.linspace(x1, x2, y)`

`np.zeros` - creates a matrix of zero values. The size of the matrix is given by the first parameter, an array of two elements, first being the row number, second the column. You can also specify the type of each element, float being the default. E.g. `np.zeros( [rows, columns], float)`

`np.ones` - is identical to the above, but creates matrixes of ones.

`np.eye` - returns a square matrix, with `1` on the first diagonal (left top corner to right bottom corner), and zeros otherwise. It's used like `np.eye(n, float)`

### np.reshape

Reorganizes an array into a matrix

```python
# create an array 1-10
arr = np.arrange(0,10)

# convert it to a matrix
arr_matrix = arr.reshape(2, 5)

```

### Arithmetic operations on arrays and matrixes

Numpy arrays enable us to add, remove values of arrays, rather than concatenate them.

```python
# create two arrays
arr7 = [1 2 3 4 5]
arr8 = [3 4 5 6 7]

print('Addition: ',arr7+arr8)
print('Subtraction: ',arr8-arr7)
print('Multiplication:' , arr7*arr8)
print('Division:', arr7/arr8)
print('Inverse:', 1/arr7)
print('Powers:', arr7**arr8) # in python, powers are achieved using **

# the above will result in an array of the same dimension (5 in our case) where each element is the result of applying the specific operation between the corresponding values on the same position
# Addition:         [4 6 8 10 12]
# Subtraction:      [2 2 2 2 2]
# Multiplication:   [3 8 15 24 35]
# etc
```

The same goes on `matrixes`, the operations will apply between elements at the same position.

> Note: If the operation is undefined, e.g. dividing by 0, the result will be `inf` and a warning will be printed


### Transpose matrix - np.tranpose or via .T property

```python
# create a matrix
matr = np.arrange(1,10).reshape(3,3)

# get the transpose function
transp_matr = np.transpose(matr)

# get the transpose via the T property
transp_matr = matr.T
```

### np.min, np.max, np.mean, np.std

They are utility functions to apply on a matrix or array.

```python
# if matr is a matrix and arr is an array
np.min(matr)
np.min(arr)

# calculate the mean
np.mean(arr)

# calculate standard distribution
np.std(arr)
```

## Trigonometric functions

### np.sin, np.cos, np.tan, np.exp, np.log

Allows applying trigonometric and logarithmic functions easily.

```python
np.sin(4)

np.log10(8) # log base 10

np.log(2) # uses 'e' number as default base
```

## Generate random numbers

### np.random.rand
Generates an array or matrix of random values from the uniform distribution over [0, 1]

```python
# array
rand_arr = np.random.rand(5)

# matrix
rand_mat = np.random.rand(2, 3)
```

### np.random.randn
The same as above, but generates numbers from a standard distribution (mean ~= 0, std ~= 1)

### np.random.randint

Same as above, but the values are integers

```python
# array of 10, values from 1 to 5
np.random.randint(1, 5, 10)

# matrix or 5x5, values from 1 to 10
np.random.randint(1, 10, [5, 5])
```

## Accessing elements

Accessing elements can be done via the usual square brackets `arr[index]`, but it can also be done to access several elements at the same time


```python
rand_arr = np.random.randn(10)

# access one element - third element
rand_arr[2]

# access all elements bigger than 1, via condition
rand_arr[rand_arr > 1]

# access elements between indexes 2 inclusive, and 4 exclusive
rand_arr[2:4]
```

For matrixes, it would be the same. The only difference is that matrixes allow an extra format compared to the standard library. All the other operations otherwise apply exactly the same for matrixes as for arrays.

```python
rand_mat = np.random.randn(10, 10)
# these are equivalent
rand_mat[2][5] == rand_mat[2, 5]
```

## Changing array and matrixes values

Other than the usual, these are allowed too

```python
# change values of elements 3 and 4 to be equal to the value 1
rand_arr[3:5] = 1
# a different way to get the same outcome as above
rand_arr[3:5] = [1, 1]

# change all elements that have a value more than 1, to be 65 - using logical references
rand_arr[rand_arr > 1] = 65
```

For matrixes
```python
# change all elements of a matrix to the value 3
rand_mat[:] = 3

# change the elements of the below submatrix to 3
rand_mat[2:5,1:3] = 3
```

### Use copy to keep original array/matrix intact

When selecting elements from an array or matrix, the result is a pointer to the original array/matrix. If we don't want to modify the original array/matrix, we must use the `copy` function.

```python
rand_mat = np.random.randint(1, 10, [5, 5])

# selects the first column and creates a copy to detatch it from the original rand_mat matrix
sub_mat = rand_mat[0:5, 0:1].copy()

# sets the value of the selection to 1. Because we used the copy function above, this will only change sub_mat. Otherwise it would have changed rand_mat too
sub_mat[:] = 1

```

# Save to disk and load

```python
# one array
np.save('path/to/file', arr)
loaded_arr = np.load('path/to/file.npy') # note the extension required here, not provided at save
print(loaded_arr) #just one so print it

# several arrays/matrixes
np.savez('path/to/files', matr_name1=matr1, matr_name2=matr2)
loaded_multi = loaded_arr = np.load('path/to/file.npz')
print(loaded_multi['matr_name1']) # since there's more than one, we can only access them like this
```

Or as text (e.g. csv)
```python
np.savetxt('path/to/file.txt', matr1, delimiter=',') # note file extension provided here, but not in previous examples
matr1 = np.loadtxt('path/to/file.txt', delimiter=',')

```