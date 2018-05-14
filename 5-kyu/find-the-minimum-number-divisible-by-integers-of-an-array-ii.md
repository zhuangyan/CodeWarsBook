# 💷Find The Minimum Number Divisible by Integers of an Array II

Given a certain array of integers, create a function that may give the minimum number that may be divisible for all the numbers of the array.

This will be a harder version of Find The Minimum Number Divisible by integers of an array I

This is an example that shows how many times, a brute force algorithm cannot give a fast solution. We need the help of maths, in this case of number theory.

We need to apply the prime factorization of a number:


<img src="http://i.imgur.com/KYanmyW.png?1">

Think in doing the prime factorization of the product of all the different values of the array and think how to obtain from it the minimum number that is divisible by all the values of the array.

See the same cases as the previous part:
~~~
min_special_mult([2, 3 ,4 ,5, 6, 7]) == 420
~~~
The array may have integers that occurs more than once:
~~~
min_special_mult([18, 22, 4, 3, 21, 6, 3]) == 2772
~~~
The array should have all its elements integer values. If the function finds an invalid entry (or invalid entries) like strings of the alphabet or symbols will not do the calculation and will compute and register them, outputting a message in singular or plural, depending on the number of invalid entries.
~~~
min_special_mult([16, 15, 23, 'a', '&', '12']) == "There are 2 invalid entries: ['a', '&']"

min_special_mult([16, 15, 23, 'a', '&', '12', 'a']) == "There are 3 invalid entries: ['a', '&', 'a']"

min_special_mult([16, 15, 23, 'a', '12']) == "There is 1 invalid entry: a"
~~~
If the string is a valid number, the function will convert it as an integer.
~~~
min_special_mult([16, 15, 23, '12']) == 5520

min_special_mult([16, 15, 23, '012']) == 5520
~~~
All the None elements of the array will be ignored:
~~~
min_special_mult([18, 22, 4, , None, 3, 21, 6, 3]) == 2772
~~~
If the array has a negative number, the function will convert to a positive one.
~~~
min_special_mult([18, 22, 4, , None, 3, -21, 6, 3]) == 2772

min_special_mult([16, 15, 23, '-012']) == 5520
~~~
The test for this part will be more challenging having arrays up to 5000 elements and up to 800 different values.

A simple brute force algorithm will not be able to pass the tests. Enjoy it!

## Best Practices

**Py First:**
~~~py
from fractions import gcd

def min_special_mult(arr):
    try:
        arr = [abs(int(x)) for x in arr if x is not None]
        return reduce(lambda x,y: x*y/gcd(x,y), arr)
    except ValueError:
        invalids = [x for x in arr if isinstance(x, str) and not x.isdigit()]
        if len(invalids) == 1:
            return "There is 1 invalid entry: {}".format(invalids[0])
        else:
            return "There are {} invalid entries: {}".format(len(invalids), invalids)
~~~

**Py Second:**
~~~py
from fractions import gcd
from functools import reduce

def lcm(a,b): return a*b/gcd(a,b) 

def min_special_mult(arr):
    invalids = [v for v in arr if v and isinstance(v,str) and not v[v[0]=='-':].isdigit()]
    if invalids: return "There {1} {0} invalid entr{2}: {3}".format(len(invalids), *(('is','y',invalids[0]) if len(invalids)==1 else ('are','ies',invalids)) )
    else:        return reduce(lcm, [abs(v if isinstance(v,int) else int(v)) for v in arr if v])
~~~

**Py Third:**
~~~py
from fractions import gcd
from functools import reduce
import math
def min_special_mult(arr):
    a = filter(lambda x:type(x)!=int, [i for i in arr if not str(i).lstrip("-").isdigit() and i!=None])
    arr = [int(i) for i in arr if str(i).lstrip("-").isdigit()]
    if a:
        return "There {} {} invalid entr{}: {}".format("are" if len(a)>1 else "is",len(a),"ies" if len(a)>1 else "y",a if len(a)>1 else a[0])
    return abs(reduce((lambda x,y : x*y/gcd(x,y)),arr))
~~~

**Py Fourth:**
~~~py
def gcd(a,b):
    while b > 0: a, b = b, a % b
    return a
    
def lcm(a, b):
    return a * b / gcd(a, b)

def min_special_mult(arr):
    try:
        return reduce(lcm, map(abs, map(int, filter(None, arr))))
    
    except:
        invalid = [i for i in arr if type(i) == str and not i.isdigit()]
        
        if len(invalid) == 1:
            return "There is 1 invalid entry: %s" % invalid[0]
        
        return "There are %s invalid entries: %s" % (len(invalid), invalid)

~~~
