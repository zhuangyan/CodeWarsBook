## Task: 
From wikipedia https://en.wikipedia.org/wiki/Partition_(number_theory)

In number theory and combinatorics, a partition of a positive integer n, also called an integer partition, is a way of writing n as a sum of positive integers. Two sums that differ only in the order of their summands are considered the same partition.

For example, 4 can be partitioned in five distinct ways:

4, 3 + 1, 2 + 2, 2 + 1 + 1, 1 + 1 + 1 + 1.

We can write:

enum(4) -> [[4],[3,1],[2,2],[2,1,1],[1,1,1,1]] and

enum(5) -> [[5],[4,1],[3,2],[3,1,1],[2,2,1],[2,1,1,1],[1,1,1,1,1]].

The number of parts in a partition grows very fast. For n = 50 number of parts is 204226, for 80 it is 15,796,476 It would be too long to tests answers with arrays of such size. So our task is the following:

1 - n being given (n integer, 1 <= n <= 50) calculate enum(n) ie the partition of n. We will obtain something like that:
enum(n) -> [[n],[n-1,1],[n-2,2],...,[1,1,...,1]] (order of array and sub-arrays doesn't matter). This part is not tested.

2 - For each sub-array of enum(n) calculate its product. If n = 5 we'll obtain after removing duplicates and sorting:

prod(5) -> [1,2,3,4,5,6]

prod(8) -> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 15, 16, 18]

If n = 40 prod(n) has a length of 2699 hence the tests will not verify such arrays. Instead our task number 3 is:

3 - return the range, the average and the median of prod(n) in the following form (example for n = 5):

"Range: 5 Average: 3.50 Median: 3.50"

Range is an integer, Average and Median are float numbers rounded to two decimal places (".2f" in some languages).

## Notes: Range : difference between the highest and lowest values.

Mean or Average : To calculate mean, add together all of the numbers in a set and then divide the sum by the total count of numbers.

Median : The median is the number separating the higher half of a data sample from the lower half. (https://en.wikipedia.org/wiki/Median)

## Hints: Try to optimize your program to avoid timing out.

Memoization can be helpful but it is not mandatory for being successful.


**Kata's link:** [Getting along with Integer Partitions](https://www.codewars.com/kata/getting-along-with-integer-partitions/)


## Best Practices

**Py First:**
~~~py
def prod(u):
    p = 1
    for x in u:
        p *= x
    return p

cache = {}
def part_aux(s, k):
    k0 = min(s, k)
    if k0 < 1:
        return []
    i = (s - 1) * s / 2 + k0 - 1
    ret = cache.get(i)
    if ret:
        return ret
    res = []
    for n in range(k0, 0, -1):
        r = s - n
        if (r > 0):
            for t in part_aux(r, n):
                if type(t) is list: 
                    res.append([n] + t)
                else: res.append([n, t])
        else:
            res.append([n])
    cache[i] = res
    return res

def part(n):
    r = sorted(set(map(prod, part_aux(n, n))))
    lg = len(r)
    avg = reduce(lambda x, y : x + y, r, 0)  / float(lg)
    rge = r[lg - 1] -  r[0]
    md = (r[(lg - 1) // 2] + r[lg // 2]) / 2.0
    return "Range: %d Average: %.2f Median: %.2f" % (rge, avg, md)

~~~

**Py Second:**
~~~py
def prod(n):
    ret = [{1.}]
    for i in range(1, n+1):
        ret.append({(i - x) * j for x, s in enumerate(ret) for j in s})
    return ret[-1]

def part(n):
    p = sorted(prod(n))
    return "Range: %d Average: %.2f Median: %.2f" % \
            (p[-1] - p[0], sum(p) / len(p), (p[len(p)//2] + p[~len(p)//2]) / 2)

~~~

**Py Third:**
~~~py
def memoize(f):
    memo = {}
    def helper(x):
        if x not in memo:
            memo[x] = f(x)
        return memo[x]
    return helper

@memoize
def enum(n):
    result = [[n]]
    for i in range(1, n):
        left = n - i
        righthand = enum(i)
        for right in righthand:
            if right[0] <= left:
                result.append([left] + right)
    return result


def reduce_prod(l):
    result = 1
    for num in l:
        result *= num
    return result

def prod(n):
    e = enum(n)[:]
    for i,x in enumerate(e):
        e[i] = reduce_prod(x)
    return sorted(list(set(e)))


def median(x):
    l = len(x)
    if l % 2 == 1:
        return x[l // 2]
    else:
        return sum(x[l // 2 - 1:l // 2+1]) / 2.0


def part(n):
    p = prod(n)
    range = max(p) - min(p)
    avg = sum(p) / float(len(p))
    med = median(p)
    return "Range: %d Average: %.2f Median: %.2f" % (range, avg, med)

~~~
