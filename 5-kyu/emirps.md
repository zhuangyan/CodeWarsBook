# 💶Emirps

If you reverse the word "emirp" you will have the word "prime". That idea is related with the purpose of this kata: we should select all the primes that when reversed are a different prime (so palindromic primes should be discarded).

For example: 13, 17 are prime numbers and the reversed respectively are 31, 71 which are also primes, so 13 and 17 are "emirps". But primes 757, 787, 797 are palindromic primes, meaning that the reversed number is the same as the original, so they are not considered as "emirps" and should be discarded.

The emirps sequence is registered in OEIS as A006567

## Your task
Create a function that receives one argument n, as an upper limit, and the return the following array:
~~~
[number_of_emirps_below_n, largest_emirp_below_n, sum_of_emirps_below_n]
~~~
## Examples

~~~
find_emirp(10)
[0, 0, 0] ''' no emirps below 10 '''

find_emirp(50)
[4, 37, 98] ''' there are 4 emirps below 50: 13, 17, 31, 37; largest = 37; sum = 98 '''

find_emirp(100)
[8, 97, 418] ''' there are 8 emirps below 100: 13, 17, 31, 37, 71, 73, 79, 97; largest = 97; sum = 418 '''
~~~

Happy coding!!

Advise: Do not use a primality test. It will make your code very slow. Create a set of primes using a prime generator or a range of primes producer. Remember that search in a set is faster that in a sorted list or array

## Best Practices

**Py First:**
~~~py
def prime_seive(n):
    start = range(n)
    for i1 in start:
        if i1 > 1:
            for i2 in range(i1*2,n,i1):
                start[i2] = 0
    return [i for i in start if i > 1]

def prime(n):
    if n % 2 == 0 or n < 3:return n == 2
    for i in range(3,int(n**0.5)+1,2):
        if n % i == 0:return False
    return True


def find_emirp(n):
    primes = prime_seive(n)
    emirps = [i for i in primes if prime(int(str(i)[::-1])) and i != int(str(i)[::-1])]
    return [len(emirps),emirps[-1] if len(emirps) > 0 else 0,sum(emirps)]

~~~

**Py Second:**
~~~py
from math import log, ceil

def makeSieveEmirp(n):
    sieve, setPrimes = [0]*n, set()
    for i in range(2, n):
        if not sieve[i]:
            setPrimes.add(i)
            for j in range(i**2, n, i): sieve[j] = 1
    return { n for n in setPrimes if n != int(str(n)[::-1]) and int(str(n)[::-1]) in setPrimes }


def find_emirp(n):
    setEmirp = makeSieveEmirp( 10**(int(ceil(log(n,10)))) )
    crunchL = [p for p in setEmirp if p <= n]
    return [len(crunchL), max(crunchL), sum(crunchL)]

~~~

**Py Third:**
~~~py
def sieve(n):
    isprime = [True for _ in xrange(n+1)]
    for i in xrange(2, int(n ** 0.5) + 1):
        if isprime[i]:
            for j in xrange(i*i, n+1, i):
                isprime[j] = False
    result = []
    for i in xrange(13, n+1):
        if isprime[i]: result.append(i)
    return result
    
primes = set(sieve(10**6))

def is_emirp(p):
    rev = int(str(p)[::-1])
    return p != rev and rev in primes

def find_emirp(n):
    emirps = [p for p in primes if p < n and is_emirp(p)]
    return [len(emirps), max(emirps), sum(emirps)]
~~~

**Py Fourth:**
~~~py
def find_emirp(n):
    limit = 10 ** len(str(n))
    sieve = [0, 0] + [1] * (limit - 1)
    for i in xrange(int(limit ** .5) + 1):
        if not sieve[i]: continue
        for m in range(i * i, limit + 1, i):
            sieve[m] = 0
    primes = {i for i, b in enumerate(sieve) if b and i != int(str(i)[::-1])}
    semirp = [p for p in xrange(n + 1) if {p, int(str(p)[::-1])} <= primes]
    return [len(semirp), len(semirp) and semirp[-1], sum(semirp)]
~~~