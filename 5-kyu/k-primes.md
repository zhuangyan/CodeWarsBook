## 🏆k-Primes

https://www.codewars.com/kata/k-primes/train/python

A natural number is called k-prime if it has exactly k prime factors, counted with multiplicity.

A natural number is thus prime if and only if it is 1-prime.

Examples:
~~~
k = 2 -> 4, 6, 9, 10, 14, 15, 21, 22, …
k = 3 -> 8, 12, 18, 20, 27, 28, 30, …
k = 5 -> 32, 48, 72, 80, 108, 112, …
~~~
## Task:

Write function count_Kprimes (or countKprimes or count-K-primes or kPrimes) which given parameters k, start, end (or nd) returns an array (or a list or a string depending on the language - see "Solution" and "Sample Tests") of the k-primes between start (inclusive) and end (inclusive).

## Example:
~~~
countKprimes(5, 500, 600) --> [500, 520, 552, 567, 588, 592, 594]
~~~
...............................................................................

for all languages except Bash shell
Given positive integers s and a, b, c where a is 1-prime, b 3-prime, c 7-prime find the number of solutions of a + b + c = s. Call this function puzzle(s).

Examples:
~~~
puzzle(138) --> 1 ([2 + 8 + 128] is solution)
puzzle(143) --> 2 ([3 + 12 + 128, 7 + 8 + 128] are solutions)
~~~
...............................................................................

Notes:

The first function would have been better named: findKprimes or kPrimes :-)

In C some helper functions are given (see declarations in 'Solution').

For Go: nil slice is expected when there are no k-primes between start and end.




## Best Practices

**Py First:**
~~~py
def count_Kprimes(k, start, end):
    return [n for n in range(start, end+1) if find_k(n) == k]


def puzzle(s):
    a = count_Kprimes(1, 0, s)
    b = count_Kprimes(3, 0, s)
    c = count_Kprimes(7, 0, s)
    
    return sum(1 for x in a for y in b for z in c if x + y + z == s)


def find_k(n):
    res = 0
    i = 2
    while i * i <= n:
        while n % i == 0:
            n //= i
            res += 1
        i += 1
    if n > 1: res += 1
    return res

~~~

**Py Second:**
~~~py
def primes(n):
    primfac = 0
    d = 2
    while d * d <= n:
        while (n % d) == 0:
            primfac += 1  
            n //= d
        d += 1
    if n > 1:
       primfac += 1
    return primfac
    
def count_Kprimes(k, start, nd):
    return [i for i in range(start, nd + 1) if primes(i) == k]

def puzzle(s):
    res = 0
    for a in count_Kprimes(1, 1, s - 2):
        for b in count_Kprimes(3, 1, s - a):
            c = s - a - b
            if c > 0 and primes(c) == 7:
                res += 1
    return res

~~~

**Py Third:**
~~~py
from math import floor, sqrt

def prime_factors(n):
    res, fac = [], 2
    while fac <= int(floor(sqrt(n))):
        count = 0
        while n % fac == 0:
            n /= fac
            res.append(fac)
        fac += 1
    if (n > 1): res.append(n)
    return len(res)
def count_Kprimes(k, start, nd):
    kprimes = []
    i = start
    while (i <= nd):
        if (prime_factors(i) == k): kprimes.append(i)
        i += 1
    return kprimes
def puzzle(s):
    a = count_Kprimes(1, 0, s)
    b = count_Kprimes(3, 0, s)
    c = count_Kprimes(7, 0, s)
    cnt = 0
    ia = 0
    while (ia < len(a)):
        ib = 0
        while (ib < len(b)):
            ic = 0
            while (ic < len(c)):
                if (a[ia] + b[ib] + c[ic] == s):
                    cnt += 1
                ic += 1
            ib += 1
        ia += 1
    return cnt

~~~

**Py Fourth:**
~~~py
def primes(n):
    primfac = []
    d = 2
    while d*d <= n:
        while (n % d) == 0:
            primfac.append(d)
            n //= d
        d += 1
    if n > 1:
       primfac.append(n)
    return len(primfac)
    
def count_Kprimes(k, start, nd):
    return [i for i in range(start, nd+1) if primes(i)==k]
    
def puzzle(s):
    a, b, c = count_Kprimes(1, 2, s), count_Kprimes(3, 8, s), count_Kprimes(7, 128, s)
    return sum(i + j + k == s for i in a for j in b for k in c)

~~~
