# 🏦Prime Sextuplets

We are interested in collecting the sets of six prime numbers, that having a starting prime p, the following values are also primes forming the sextuplet
~~~
[p, p + 4, p + 6, p + 10, p + 12, p + 16]
~~~
The first sextuplet that we find is
~~~
[7, 11, 13, 17, 19, 23]
~~~
The second one is
~~~
[97, 101, 103, 107, 109, 113]
~~~
Given a number
sum_limit
, you should give the first sextuplet which sum (of its six primes) surpasses the sum_limit value.
~~~
 find_primes_sextuplet(70) == [7, 11, 13, 17, 19, 23]

find_primes_sextuplet(600) == [97, 101, 103, 107, 109, 113]
~~~
Features of the tests:
~~~
Number Of Tests = 18
10000 < sum_limit < 29700000
~~~
If you have solved this kata perhaps you will find easy to solve this one: Primes with Two, Even and Double Even Jumps.

Enjoy it!!

## Best Practices

**Py First:**
~~~py
def find_primes_sextuplet(limit):
    for p in [7, 97, 16057, 19417, 43777, 1091257, 1615837, 1954357, 2822707, 2839927, 3243337, 3400207, 6005887]:
        if p * 6 + 48 > limit:
            return [p, p + 4, p + 6, p + 10, p + 12, p + 16]
~~~

**Py Second:**
~~~py
def find_primes_sextuplet(sum_limit):
    p = (sum_limit - 48) // 6 + 1
    if not p%2:
        if p%3 == 2: p += 3
        else: p += 1
    elif p%2 and p%3 == 0: p += 2

    while 1:
        lst = [p+x for x in (0,4,6,10,12,16)]
        for i in xrange(3, 1+int(lst[-1]**0.5), 2):
            if not all(num%i for num in lst): break
        else: return lst
        if p%3 == 2: p += 2
        else: p += 4

~~~

**Py Third:**
~~~py
sextuplets = []

def is_prime(i):
    if   i<=1: return False
    elif i==2: return True
    else:
        for j in xrange(3, int(i**0.5), 2):
            if i%j==0:  return False
        return True    

def all_6tuplets():
    for i in xrange(3*10**5):
        p = 30*i + 7
        if is_prime(p) and is_prime(p+4) and is_prime(p+6) and is_prime(p+10) and is_prime(p+12) and is_prime(p+16):
            sextuplets.append([p, p+4, p+6, p+10, p+12, p+16])

all_6tuplets()

def find_primes_sextuplet(sum_limit):
    for tuplet in sextuplets:
        if sum(tuplet)>=sum_limit:  return tuplet
~~~

**Py Fourth:**
~~~py
def find_primes_sextuplet(sum_limit):
  # 7 times (24680) x (13579) 1+4=5x 3+12=15x 5x 9x
    num = (sum_limit-48)//6//10*10 + 7
    while True:
      # 3 times
      if sum(int(x) for x in str(num)) % 3 != 0:
        nums = [num+x for x in (0, 4, 6, 10, 12, 16)]
        # mul prime judgement
        for i in xrange(3, int(nums[-1]**0.5)+1, 2):
          if not all(n%i for n in nums):
            break
        else:
          return nums
      num += 10
~~~