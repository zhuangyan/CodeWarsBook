## 🏓Recreation One

Divisors of 42 are : 1, 2, 3, 6, 7, 14, 21, 42. These divisors squared are: 1, 4, 9, 36, 49, 196, 441, 1764. The sum of the squared divisors is 2500 which is 50 * 50, a square!

Given two integers m, n (1 <= m <= n) we want to find all integers between m and n whose sum of squared divisors is itself a square. 42 is such a number.

The result will be an array of arrays or of tuples (in C an array of Pair) or a string, each subarray having two elements, first the number whose squared divisors is a square and then the sum of the squared divisors.

## Examples:

list_squared(1, 250) --> [[1, 1], [42, 2500], [246, 84100]]
list_squared(42, 250) --> [[42, 2500], [246, 84100]]
The form of the examples may change according to the language, see Example Tests: for more details.

## Best Practices

**Py First:**
~~~py
CACHE = {}

def squared_cache(number):
    if number not in CACHE:
        divisors = [x for x in range(1, number + 1) if number % x == 0]
        CACHE[number] = sum([x * x for x in divisors])
        return CACHE[number] 
    
    return CACHE[number]

def list_squared(m, n):
    ret = []

    for number in range(m, n + 1):
        divisors_sum = squared_cache(number)
        if (divisors_sum ** 0.5).is_integer():
            ret.append([number, divisors_sum])

    return ret
~~~

**Py Second:**
~~~py
from math import floor, sqrt, pow

def sum_squared_factors(n):
    s, res, i = 0, [], 1
    while (i <= floor(sqrt(n))):
        if (n % i == 0):
            s += i * i
            nf = n // i
            if (nf != i):
                s += nf * nf
        i += 1
    if (pow(int(sqrt(s)), 2) == s):
        res.append(n)
        res.append(s)
        return res
    else:
        return None
        
def list_squared(m, n):
    res, i = [], m
    while (i <= n):
        r = sum_squared_factors(i)
        if (r != None):
            res.append(r);
        i += 1
    return res
    
~~~

**Py Third:**
~~~py
WOAH = [1, 42, 246, 287, 728, 1434, 1673, 1880, 
        4264, 6237, 9799, 9855, 18330, 21352, 21385, 
        24856, 36531, 39990, 46655, 57270, 66815, 
        92664, 125255, 156570, 182665, 208182, 212949, 
        242879, 273265, 380511, 391345, 411558, 539560, 
        627215, 693160, 730145, 741096]

list_squared = lambda HUH, YEAH: [[YES, DUH(YES)] for YES in WOAH if YES >= HUH and YES <= YEAH]
DUH = lambda YEP: sum(WOW**2 for WOW in range(1, YEP + 1) if YEP % WOW == 0)

~~~

**Py Fourth:**
~~~py
def list_squared(m, n):
  list = [[1, 1], [42, 2500], [246, 84100], [287, 84100], [728, 722500], [1434, 2856100], [1673, 2856100], [1880, 4884100], [4264, 24304900], [6237, 45024100], [9799, 96079204], [9855, 113635600], [18330, 488410000], [21352, 607622500], [21385, 488410000], [24856, 825412900]]
  left = -1
  right = -1
  for i, r in enumerate(list):
    if left == -1 and r[0] >= m:
      left = i
    if right == -1 and r[0] >= n:
      right = i - 1
  print('left={0},right={1}'.format(m, n))
  return list[left: right + 1]

~~~
