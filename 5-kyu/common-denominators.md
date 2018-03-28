# 🇳Common Denominators

You will have a list of rationals in the form
~~~
 { {numer_1, denom_1} , ... {numer_n, denom_n} }
~~~
or
~~~
 [ [numer_1, denom_1] , ... [numer_n, denom_n] ]
~~~
or
~~~
 [ (numer_1, denom_1) , ... (numer_n, denom_n) ]
~~~
where all numbers are positive ints.

You have to produce a result in the form
~~~
 (N_1, D) ... (N_n, D)
~~~
or
~~~
 [ [N_1, D] ... [N_n, D] ]
~~~
or
~~~
 [ (N_1', D) , ... (N_n, D) ]
~~~
or
~~~
{{N_1, D} ... {N_n, D}}
~~~
depending on the language (See Example tests)

in which D is as small as possible and

 N_1/D == numer_1/denom_1 ... N_n/D == numer_n,/denom_n.
## Example:
~~~
convertFracs [(1, 2), (1, 3), (1, 4)] `shouldBe` [(6, 12), (4, 12), (3, 12)]
~~~
## Note for Bash
input is a string, e.g "2,4,2,6,2,8"

output is then "6 12 4 12 3 12"

## Best Practices

**Py First:**
~~~py
from fractions import gcd

def get_lcm(lst):
  return reduce(lambda x, y : x*y/gcd(x,y), lst)

def convertFracts(lst):
  lcm = get_lcm([ y for x, y in lst])
     return [ [x*lcm/y, lcm] for x, y in lst]

~~~

**Py Second:**
~~~py
def gcd(a, b):
    """Return greatest common divisor using Euclid's Algorithm."""
    while b:      
        a, b = b, a % b
    return a

def lcm(a, b):
    """Return lowest common multiple."""
    return a * b // gcd(a, b)

def lcmm(*args):
    """Return lcm of args."""   
    return reduce(lcm, args)

def convertFracts(lst):
    new_den = lcmm(*[den for num, den in lst])
    return [[num * (new_den / den), new_den] for num, den in lst]

~~~

**Py Third:**
~~~py
from fractions import gcd
from functools import reduce

def lcmm(*numbers): 
    def lcm(a, b):
        return (a * b) // gcd(a, b)
    return reduce(lcm, numbers)
    
def convertFracts(lst):
    denums = tuple(i[1] for i in lst)
    lc = lcmm(*denums)   
    return [[i[0]*(lc//i[1]), lc] for i in lst]

~~~
