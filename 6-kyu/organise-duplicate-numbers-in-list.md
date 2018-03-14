
## Task

Sam is an avid collector of numbers. Every time he finds a new number he throws it on the top of his number-pile. Help Sam organise his collection so he can take it to the International Number Collectors Conference in Cologne.

Given an array of numbers, your function should return an array of arrays, where each subarray contains all the duplicates of a particular number. Subarrays should be in the same order as the first occurence of the number they contain:
~~~
group([3, 2, 6, 2, 1, 3])
>>> [[3, 3], [2, 2], [6], [1]]
~~~
Assume the input is always going to be an array of numbers. If the input is an empty array, an empty array should be returned.

**Kata's link:** [Organise duplicate numbers in list](http://www.codewars.com/kata/organise-duplicate-numbers-in-list/)

## Best Practices

**Py First:**
~~~py
group=lambda arr: [[n]*arr.count(n) for n in sorted(set(arr), key=arr.index)]

~~~

**Py Second:**
~~~py
from collections import Counter, OrderedDict

class OrderedCounter(Counter, OrderedDict): 
    pass

def group(arr):
    return [[k] * v for k, v in OrderedCounter(arr).items()]
~~~

**Py Third:**
~~~py
def group(arr):
    b = []
    c = []
    [b.append([i]*arr.count(i)) for i in arr]
    [c.append(i) for i in b if i not in c]
    return c
~~~

**Py Fourth:**
~~~py
import collections

def group(arr):
    d=collections.OrderedDict()
    for s in arr:
        d.setdefault(s, []).append(s)
    return(list(d.values()))
~~~
