https://www.codewars.com/kata/number-of-proper-fractions-with-denominator-d/train/python

## Task
If n is the numerator and d the denominator of a fraction, that fraction is defined a (reduced) proper fraction if and only if GCD(n,d)==1.

For example 5/16 is a proper fraction, while 6/16 is not, as both 6 and 16 are divisible by 2, thus the fraction can be reduced to 3/8.

Now, if you consider a given number d, how many proper fractions can be built using d as a denominator?

For example, let's assume that d is 15: you can build a total of 8 different proper fractions between 0 and 1 with it: 1/15, 2/15, 4/15, 7/15, 8/15, 11/15, 13/15 and 14/15.

You are to build a function that computes how many proper fractions you can build with a given denominator:
~~~
proper_fractions(1)==0
proper_fractions(2)==1
proper_fractions(5)==4
proper_fractions(15)==8
proper_fractions(25)==20
~~~
Be ready to handle big numbers.

Edit: to be extra precise, the term should be "reduced" fractions, thanks to girianshiido for pointing this out and sorry for the use of an improper word :)

## Best Practices

**Py First:**
~~~py
def proper_fractions(n):
    phi = n > 1 and n
    for p in range(2, int(n ** .5) + 1):
        if not n % p:
            phi -= phi // p
            while not n % p:
                n //= p
    if n > 1: phi -= phi // n
    return phi

~~~

**Py Second:**
~~~py
def euler(n):
    res = 1.0*n
    p = 2
    while p*p <= n:
        if n%p == 0:
            while n%p == 0:
                n = n/p
            res *= (1.0 - (1.0/p) )
        p += 1
    
    if n > 1:
        res *= (1.0 - (1.0/n) )
    
    return int(res)

def proper_fractions(d):
    if d == 1:
        return 0
    return euler(d)
~~~

**Py Third:**
~~~py
primes=[2,3,5,7,11,13,17,19,23,29,31]

def is_prime(n):
    limit=int(n**.5)+1
    for div in primes:
        if div>limit: break
        if n%div==0: return False
    return True

def expand_primes(n):
    global primes
    for i in range(primes[-1]/6*6,n+6,6):
        if is_prime(i-1) and (i-1)>primes[-1]: primes+=[i-1]
        if is_prime(i+1) and (i+1)>primes[-1]: primes+=[i+1]

def divisors(n):
    res,orig=[],n
    for prime in primes:
        if prime**2>n: break
        if n%prime==0:
            res+=[prime]
            while n%prime==0: n/=prime
        if prime==primes[-1] and n>prime**2: expand_primes(int(n**.5)+1)
    return res if n==1 else res+[n]

def proper_fractions(n):
    if n<2: return 0
    for div in divisors(n):
        n=n/div*(div-1)
    return n

~~~
