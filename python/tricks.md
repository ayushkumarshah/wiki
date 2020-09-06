# Python tips and tricks

## 1. Itertools()

```python
a = [1, 2, 3]
b = [3, 5, 6]
c = [4, 6, 7]

iters = [a, b, c]

import itertools
res  = itertools.chain.from_iterable(iters)
list(res)

```

    [1, 2, 3, 3, 5, 6, 4, 6, 7]


Runs at runtime


```python
res  = itertools.chain(*iters)
list(res)
```

    [1, 2, 3, 3, 5, 6, 4, 6, 7]


```python
dir(itertools)
```

    ['__doc__',
     '__loader__',
     '__name__',
     '__package__',
     '__spec__',
     '_grouper',
     '_tee',
     '_tee_dataobject',
     'accumulate',
     'chain',
     'combinations',
     'combinations_with_replacement',
     'compress',
     'count',
     'cycle',
     'dropwhile',
     'filterfalse',
     'groupby',
     'islice',
     'permutations',
     'product',
     'repeat',
     'starmap',
     'takewhile',
     'tee',
     'zip_longest']


Explore above yourself , groupby is important

## 2. Underscore for large number


```python
a = 100000000000

```


```python
a = 1_000_000_000_000_000
type(a)
```

    int


## 3. If else in one line


## 4. Tuples

```python
a, b = 1, 2
```

```python
x = 3, 6
tuple(x)
```

    (3, 6)

```python
x = (3, 5)
type(x)
```

    tuple



```python
x = (3)
type(x)
```




    int



Comma is responsible for deciding as tuple


```python
x = (3, )
type(x)
```




    tuple



## 5. For else

Use case: If break in for loop, then else executed.

A collection of functions to be

## 6. Help and dir

Use this instead of google.

- help - docstring
- dir - list of attributes


```python
help(int)
```

## 7. Reset recursion limit


```python
def fact(n):
    if n < 2:
        return n
    else:
        return n * fact(n - 1)
```


```python
fact(5)
```




    120




```python
fact(1000000)
```


    ---------------------------------------------------------------------------

    RecursionError                            Traceback (most recent call last)

    <ipython-input-33-15618cfba3d1> in <module>
    ----> 1 fact(1000000)
    

    <ipython-input-31-08b3380bd40b> in fact(n)
          3         return n
          4     else:
    ----> 5         return n * fact(n - 1)
    

    ... last 1 frames repeated, from the frame below ...


    <ipython-input-31-08b3380bd40b> in fact(n)
          3         return n
          4     else:
    ----> 5         return n * fact(n - 1)
    

    RecursionError: maximum recursion depth exceeded in comparison



```python
import sys
sys.getrecursionlimit()
```
    3000


```python
sys.setrecursionlimit(1000000)
```


```python
fact(100000)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-4-e4841ba32a3d> in <module>
    ----> 1 fact(100000)
    

    NameError: name 'fact' is not defined


### For memory


```python
from functools import lru_cache

```


## 8. `__slots__`


```python
class WithSlots:
    __slots__ = ('x', 'y', 'z')
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z
        
class WithoutSlots:
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z        
```


```python
ws = WithSlots(1, 2, 3)
wos = WithoutSlots(1, 2, 3)
```


```python
sys.getsizeof(wos)
```




    56




```python
sys.getsizeof(ws)
```




    64



Use slots in small classes where Attribute not created at runtime

## 9. Sorting


```python
a = {"apple": 32, "mango": 43, "banana": 23}
sorted(a.items())
```




    [('apple', 32), ('banana', 23), ('mango', 43)]




```python
sorted(a.items(), key=lambda item: item[1])
```




    [('banana', 23), ('apple', 32), ('mango', 43)]




```python
sorted(a.items(), key=lambda item: item[1], reverse=True)
```




    [('mango', 43), ('apple', 32), ('banana', 23)]




```python
from collections import Counter
c = Counter(a)

c.most_common()[::-1]
```




    [('banana', 23), ('apple', 32), ('mango', 43)]




```python
b = {"watermelon": 54}
c = {**a, **b}
```


```python
c
```




    {'apple': 32, 'mango': 43, 'banana': 23, 'watermelon': 54}



## 10. Use typing


```python
def add (x: int, y: int) -> int:
    return x + y
```


```python
from typing import List
```


```python
def add (x: List, y: List) -> List:
    return x + y
```


```python
add([1,2], [3,4])
```


    [1, 2, 3, 4]

