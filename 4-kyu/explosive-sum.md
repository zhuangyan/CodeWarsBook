https://www.codewars.com/kata/explosive-sum/train/python

## How many ways can you make the sum of a number?
From wikipedia: https://en.wikipedia.org/wiki/Partition_(number_theory)#

In number theory and combinatorics, a partition of a positive integer n, also called an integer partition, is a way of writing n as a sum of positive integers. Two sums that differ only in the order of their summands are considered the same partition. If order matters, the sum becomes a composition. For example, 4 can be partitioned in five distinct ways:
~~~
4
3 + 1
2 + 2
2 + 1 + 1
1 + 1 + 1 + 1
~~~
## Examples
### Trivial
~~~
sum(-1) # 0
sum(1) # 1
~~~
### Basic
~~~
sum(2) # 2  -> 1+1 , 2
sum(3) # 3 -> 1+1+1, 1+2, 3
sum(4) # 5 -> 1+1+1+1, 1+1+2, 1+3, 2+2, 4
sum(5) # 7 -> 1+1+1+1+1, 1+1+1+2, 1+1+3, 1+2+2, 1+4, 5, 2+3

sum(10) # 42
~~~

### Explosive
~~~
sum(50) # 204226
sum(80) # 15796476
sum(100) # 190569292
~~~

## Best Practices

**Py First:**
~~~py
def exp_sum(n):
  if n < 0:
    return 0
  dp = [1]+[0]*n
  for num in xrange(1,n+1):
    for i in xrange(num,n+1):
      dp[i] += dp[i-num]
  return dp[-1]

~~~

**Py Second:**
~~~py
class Memoize:
    def __init__(self, func): 
        self.func = func
        self.cache = {}
    def __call__(self, arg):
        if arg not in self.cache: 
            self.cache[arg] = self.func(arg)
        return self.cache[arg]

@Memoize
def exp_sum(n):
    if n == 0: return 1
    result = 0; k = 1; sign = 1; 
    while True:
        pent = (3*k**2 - k) // 2        
        if pent > n: break
        result += sign * exp_sum(n - pent) 
        pent += k
        if pent > n: break
        result += sign * exp_sum(n - pent) 
        k += 1; sign = -sign; 
    return result
~~~

