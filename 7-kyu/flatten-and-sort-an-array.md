## Challenge:

Given a two-dimensional array of integers, return the flattened version of the array with all the integers in the sorted (ascending) order.

## Example:

Given [[3, 2, 1], [4, 6, 5], [], [9, 7, 8]], your function should return [1, 2, 3, 4, 5, 6, 7, 8, 9].

**Kata's link:** [Flatten and sort an array](https://www.codewars.com/kata/flatten-and-sort-an-array/)


## Best Practices
**Py First:**
~~~py
from itertools import chain
def flatten_and_sort(array):
    return sorted((chain(*array)))

~~~

**Py Second:**
~~~py
def flatten_and_sort(array):
    return sorted([j for i in array for j in i])

~~~

**Py Third:**
~~~py
def flatten_and_sort(array):
    return sorted(sum(array, []))
~~~

**Py Fourth:**
~~~py
from itertools import chain

def flatten_and_sort(array):
    return sorted(chain.from_iterable(array))

~~~

**Py Fifth:**
~~~py
#from functools import reduce    # for Python 3

def flatten_and_sort(array):
    return sorted(reduce(list.__add__, array, []))
~~~

