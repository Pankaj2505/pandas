---
layout: post
title:  "Basics of panda"
categories: pandas
background: '/img/posts/panda/cheetSheet.png'
date:   2021-01-02 15:12:01 +0530
permalink: /:categories/:title
---



[Taken reference from ](https://jakevdp.github.io/PythonDataScienceHandbook/)
<br>
<a href="\img\posts\numpy\cheetSheet.pdf" download>Download CheetSheet</a>



- To display all the content of pandas documantation - pd.<tab>
- pandas can be thought enhanced version of numpy 
- Three pandas data structure
    - series
    - data frame
    - index

# Recap of numpy array 
These included indexing (e.g., arr[2, 1]), slicing (e.g., arr[:, 1:5]), masking (e.g., arr[arr > 0]), fancy indexing (e.g., arr[0, [1, 5]]),

## Series
- Series is one dimensional index array

- difference between np array and panda series
    - the difference is of index, np has implicit index always in integer . while series can have user defined index.
    
- Series is like dictionary 
    as dictionary has key value pair , panda series has index value pair
    
- syntax
    - pd.Series(data, index=index)
    
- in series , index can be user defined but they will implicity have integer index also , can be used by iloc func

    - First, the loc attribute allows indexing and slicing that always references the explicit index:
    - The iloc attribute allows indexing and slicing that always references the implicit Python-style index:


```python
import pandas as pd
import numpy as np

data = pd.Series([11,12,13,14,15], index=['a','b','c','d','e'])
print(data)
print(type(data))
```

    a    11
    b    12
    c    13
    d    14
    e    15
    dtype: int64
    <class 'pandas.core.series.Series'>
    


```python
# how to check value of a series
print('value of a series \n', data.values)

print("\n"*4)

# check index of a series
print('index of a series \n',data.index)


print("\n"*4)

# accessing data using index
print('access data using index \n',data['b'])


print("\n"*4)

# data slicing
print('data slicing \n',data['b':'e'])


# slicing by explicit index
print(data['a':'c'])


# slicing by implicit integer index
print(data[0:2])

# masking
print(data[(data > 13) & (data < 18)])


# fancy indexing
print(data[['a', 'e']])
```

    value of a series 
     [11 12 13 14 15]
    
    
    
    
    
    index of a series 
     Index(['a', 'b', 'c', 'd', 'e'], dtype='object')
    
    
    
    
    
    access data using index 
     12
    
    
    
    
    
    data slicing 
     b    12
    c    13
    d    14
    e    15
    dtype: int64
    a    11
    b    12
    c    13
    dtype: int64
    a    11
    b    12
    dtype: int64
    d    14
    e    15
    dtype: int64
    a    11
    e    15
    dtype: int64
    


```python
# user defind index
data = pd.Series([0.25, 0.5, 0.75, 1.0],
                 index=['a', 'b', 'c', 'd'])
print(data)


# a panda series is more like dictionary

population_dict = {'California': 38332521,
                   'Texas': 26448193,
                   'New York': 19651127,
                   'Florida': 19552860,
                   'Illinois': 12882135}
population = pd.Series(population_dict)
print(population)


print("\n"*4)

print(population.index)
# using loc attribute
print('data at index california :',population.loc['California'])

print("\n"*4)

# using iloc attribute 
print('data at using slixing \n',population.iloc[1:3])
```

    a    0.25
    b    0.50
    c    0.75
    d    1.00
    dtype: float64
    California    38332521
    Texas         26448193
    New York      19651127
    Florida       19552860
    Illinois      12882135
    dtype: int64
    
    
    
    
    
    Index(['California', 'Texas', 'New York', 'Florida', 'Illinois'], dtype='object')
    data at index california : 38332521
    
    
    
    
    
    data at using slixing 
     Texas       26448193
    New York    19651127
    dtype: int64
    

# Dataframe
- If a Series is an analog of a one-dimensional array with flexible indices,
- DataFrame as a sequence of aligned Series objects. Here, by "aligned" we mean that they share the same index.



- Index is immutable


- lets say we want to compare two data frame based on some column , we can change them to index and get union and intersection of them using | and ^ operator


```python
#COnstruction from single series object 
population = pd.Series(np.random.randint(10, size = 5))
print(pd.DataFrame(population, columns=['population']))
```

       population
    0           2
    1           3
    2           7
    3           1
    4           4
    


```python
# Construction of series using two dimensional array 

arr= np.random.randint(12, size =12).reshape(4,3)
x = pd.DataFrame(arr, index= ['a','b','c','d'])
print(x)

print('\n'*4)

x = pd.DataFrame(arr, index= ['a','b','c','d'], columns = ['col1', 'col2','col3'])
print(x)
```

       0  1   2
    a  7  2  11
    b  5  6   2
    c  1  7   5
    d  5  1   3
    
    
    
    
    
       col1  col2  col3
    a     7     2    11
    b     5     6     2
    c     1     7     5
    d     5     1     3
    


```python
# access index 
ind = x.index
print(x.index , end='\n'*3)

print(x.index[1], end='\n'*3)


print(ind.size, ind.shape, ind.ndim, ind.dtype)
```

    Index(['a', 'b', 'c', 'd'], dtype='object')
    
    
    b
    
    
    4 (4,) 1 object
    


```python
ind[1] = 0
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-38-906a9fa1424c> in <module>
    ----> 1 ind[1] = 0
    

    ~\Anaconda3\lib\site-packages\pandas\core\indexes\base.py in __setitem__(self, key, value)
       4275     @final
       4276     def __setitem__(self, key, value):
    -> 4277         raise TypeError("Index does not support mutable operations")
       4278 
       4279     def __getitem__(self, key):
    

    TypeError: Index does not support mutable operations



```python

```
