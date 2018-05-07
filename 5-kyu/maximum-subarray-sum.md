## 🍕Maximum subarray sum

The maximum sum subarray problem consists in finding the maximum sum of a contiguous subsequence in an array or list of integers:
~~~
maxSequence([-2, 1, -3, 4, -1, 2, 1, -5, 4])
# should be 6: [4, -1, 2, 1]
~~~
Easy case is when the list is made up of only positive numbers and the maximum sum is the sum of the whole array. If the list is made up of only negative numbers, return 0 instead.

Empty list is considered to have zero greatest sum. Note that the empty list or array is also a valid sublist/subarray.

## Best Practices

**Py First:**
~~~py
def maxSequence(arr):
    max,curr=0,0
    for x in arr:
        curr+=x
        if curr<0:curr=0
        if curr>max:max=curr
    return max
~~~

**Py Second:**
~~~py
def maxSequence(arr):
  lowest = ans = total = 0
  for i in arr:
    total += i
    lowest = min(lowest, total)
    ans = max(ans, total - lowest)
  return ans

~~~

**Py Third:**
~~~py
def maxSequence(arr):
    maxl = 0
    maxg = 0
    for n in arr:
        maxl = max(0, maxl + n)
        maxg = max(maxg, maxl)
    return maxg
~~~

**Py Fourth:**
~~~py
def maxSequence(arr):
  m, a, s = 0, 0, 0
  for e in arr:
    s += e
    m = min(s, m)
    a = max(a, s - m)
  return a
~~~