# 🏸Closest and Smallest
## Input

* a string strng of n positive numbers (n = 0 or n >= 2)
Let us call weight of a number the sum of its digits. For example 99 will have "weight" 18, 100 will have "weight" 1.

Two numbers are "close" if the difference of their weights is small.

## Task:

For each number in strng calculate its "weight" and then find two numbers of strng that have:

* the smallest difference of weights ie that are the closest
* with the smallest weights
* and with the smallest indices (or ranks, numbered from 0) in strng

## Output:

* an array of two arrays, each subarray in the following format:
~~~
[number-weight, index in strng of the corresponding number, original corresponding number instrng]
~~~
or a pair of two subarrays (Haskell, Clojure, FSharp) or an array of tuples (Elixir, C++)

or a (char*) in C mimicking an array of two subarrays

or a matrix in R (2 rows, 3 columns, no columns names)

The two subarrays are sorted in ascending order by their number weights if these weights are different, by their indexes in the string if they have the same weights.

## Examples:
Let us call that function closest
~~~
strng = "103 123 4444 99 2000"
the weights are 4, 6, 16, 18, 2 (ie 2, 4, 6, 16, 18)

closest should return [[2, 4, 2000], [4, 0, 103]] (or ([2, 4, 2000], [4, 0, 103])
or [{2, 4, 2000}, {4, 0, 103}] or ... depending on the language)
because 2000 and 103 have for weight 2 and 4, ther indexes in strng are 4 and 0.
The smallest difference is 2.
4 (for 103) and 6 (for 123) have a difference of 2 too but they are not 
the smallest ones with a difference of 2 between their weights.
....................

strng = "80 71 62 53"
All the weights are 8.
closest should return [[8, 0, 80], [8, 1, 71]]
71 and 62 have also:
- the smallest weights (which is 8 for all)
- the smallest difference of weights (which is 0 for all pairs)
- but not the smallest indices in strng.
....................

strng = "444 2000 445 544"
the weights are 12, 2, 13, 13 (ie 2, 12, 13, 13)

closest should return [[13, 2, 445], [13, 3, 544]] or ([13, 2, 445], [13, 3, 544])
or [{13, 2, 445}, {13, 3, 544}] or ...
444 and 2000 have the smallest weights (12 and 2) but not the smallest difference of weights;
they are not the closest.
Here the smallest difference is 0 and in the result the indexes are in ascending order.
...................

closest("444 2000 445 644 2001 1002") --> [[3, 4, 2001], [3, 5, 1002]] or ([3, 4, 2001], 
[3, 5, 1002]]) or [{3, 4, 2001}, {3, 5, 1002}] or ...
Here the smallest difference is 0 and in the result the indexes are in ascending order.
...................

closest("239382 162 254765 182 485944 468751 49780 108 54")
The weights are: 27, 9, 29, 11, 34, 31, 28, 9, 9.
closest should return  [[9, 1, 162], [9, 7, 108]] or ([9, 1, 162], [9, 7, 108]) 
or [{9, 1, 162}, {9, 7, 108}] or ...
108 and 54 have the smallest difference of weights too, they also have 
the smallest weights but they don't have the smallest ranks in the original string.
..................

closest("54 239382 162 254765 182 485944 468751 49780 108")
closest should return  [[9, 0, 54], [9, 2, 162]] or ([9, 0, 54], [9, 2, 162])
or [{9, 0, 54}, {9, 2, 162}] or ...
Notes :
If n == 0, `closest("") should return [] or ([], []) in Haskell, Clojure, FSharp or [{}, {}] in Elixir or {{0,0,0},{0,0,0}} in C++, "{{0,0,0},{0,0,0}}" in C, NULL in R.
See Example tests for the format of the results in your language.
~~~

## Best Practices

**Py First:**
~~~py
def closest(s):
    wght = sorted([ [sum(int(c) for c in n), i, int(n)] for i, n in enumerate(s.split()) ], key=lambda k: (k[0], k[1]))
    diff = [ abs(a[0] - b[0]) for a, b in zip(wght, wght[1:]) ]
    return  [ wght [diff.index(min(diff)) ], wght [diff.index(min(diff)) + 1] ] if wght else []
~~~

**Py Second:**
~~~py
def closest(strng):
    if (strng == ""): return []
    nums, l, i = strng.split(), [], 0
    for n in nums:
        s = sum(list(int(i) for i in n))
        l += [[s, i, int(n)]]
        i += 1
    l.sort()
    valmin, argmin = min((l[i][0] - l[i - 1][0], i) for i in range(1, len(l)))
    return [l[argmin - 1], l[argmin]]
~~~

**Py Third:**
~~~py
def closest(ss):
  if not ss: return []
  a = sorted([sum(int(d) for d in s), i, int(s)] for i,s in enumerate(ss.split()))
  d = min(y[0] - x[0] for x,y in zip(a, a[1:]))
  return next([x, y] for x,y in zip(a, a[1:]) if y[0] - x[0] == d)
~~~

**Py Fourth:**
~~~py
def closest(strng):
    if (strng == ""): return []
    nums, l, i = strng.split(), [], 0
    for n in nums:
        s = sum(list(int(i) for i in n))
        l += [[s, i, int(n)]]
        i += 1
    l.sort()
    valmin, argmin = min((l[i][0] - l[i - 1][0], i) for i in range(1, len(l)))
    return [l[argmin - 1], l[argmin]]

~~~
