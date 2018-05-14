# 🏧Find the Partition with Maximum Product Value

You are given a certain integer, n, n > 0. You have to search the partition or partitions, of n, with maximum product value.

Let'see the case for n = 8.
~~~
Partition                 Product
[8]                          8
[7, 1]                       7
[6, 2]                      12
[6, 1, 1]                    6
[5, 3]                      15
[5, 2, 1]                   10
[5, 1, 1, 1]                 5
[4, 4]                      16
[4, 3, 1]                   12
[4, 2, 2]                   16
[4, 2, 1, 1]                 8
[4, 1, 1, 1, 1]              4
[3, 3, 2]                   18   <---- partition with maximum product value
[3, 3, 1, 1]                 9
[3, 2, 2, 1]                12
[3, 2, 1, 1, 1]              6
[3, 1, 1, 1, 1, 1]           3
[2, 2, 2, 2]                16
[2, 2, 2, 1, 1]              8
[2, 2, 1, 1, 1, 1]           4
[2, 1, 1, 1, 1, 1, 1]        2
[1, 1, 1, 1, 1, 1, 1, 1]     1
So our needed function will work in that way for Python and Ruby:
~~~
find_part_max_prod(8) == [[3, 3, 2], 18]
For javascript
~~~
findPartMaxProd(8) --> [[3, 3, 2], 18]
~~~
If there are more than one partition with maximum product value, the function should output the patitions in a length sorted way. Python and Ruby
~~~
find_part_max_prod(10) == [[4, 3, 3], [3, 3, 2, 2], 36]
~~~
Javascript
~~~
findPartMaxProd(10) --> [[4, 3, 3], [3, 3, 2, 2], 36]
~~~
Enjoy it!

## Best Practices

**Py First:**
~~~py
def find_part_max_prod(n):
  if n == 1: return [[1], 1]
  q, r = divmod(n, 3)
  if r == 0: return [[3]*q, 3**q]
  if r == 1: return [[4] + [3]*(q - 1), [3]*(q - 1) + [2, 2], 3**(q - 1) * 2**2]
  return [[3]*q + [2], 3**q * 2]
~~~

**Py Second:**
~~~py
def find_part_max_prod(n):
    if n % 3 == 0:
        return [[3]*(n/3),3**(n/3)]
    if n % 3 == 2:
        return [[3]*(n//3)+[2],3**(n//3)*2]
    if n == 1:
        return 1
    if n % 3 == 1:
        return [[4]+[3]*(n//3-1),[3]*(n//3-1)+[2,2],3**(n//3-1)*4]
            
~~~

**Py Third:**
~~~py
def partitions(n, s=float('inf')):
    if not n: yield []; return
    for i in range(min(n, s), 0, -1):
        for p in partitions(n - i, i):
            yield [i] + p

from collections import defaultdict
from functools import reduce
from operator import mul
def find_part_max_prod(n):
    products = defaultdict(list)
    for p in partitions(n):
        products[reduce(mul, p)].append(p)
    m = max(products)
    return products[m] + [m]
~~~

**Py Fourth:**
~~~py
from itertools import groupby

def partition(n, k):
    result = [n / k for _ in xrange(k)]
    for i in xrange(n % k):
        result[i] += 1
    return result

def prod(arr):
    return reduce(lambda x,y:x*y, arr)

def find_part_max_prod(n):
    partitions = sorted((partition(n, i) for i in xrange(1, n+1)), key=prod)
    data = [(k, list(group)) for k, group in groupby(partitions, key=prod)][-1]
    
    return data[1] + [data[0]]

~~~
