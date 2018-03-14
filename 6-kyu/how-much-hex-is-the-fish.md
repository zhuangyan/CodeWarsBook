**Kata's link:** [How much hex is the fish](http://www.codewars.com/kata/how-much-hex-is-the-fish/)

## How much is the fish! (- Scooter )
The ocean is full of colorful fishes. We as programmers want to know the hexadecimal value of these fishes.

## Task
Take all hexadecimal valid characters (a,b,c,d,e,f) of the given name and XOR them. Return the result as an integer.

## Input
The input is always a string, which can contain spaces, upper and lower case letters but no digits.

## Example
~~~
fisHex("redlionfish") -> e,d,f -> XOR -> 12
~~~


## Best Practices

**Py First:**
~~~py
VALID = frozenset('abcdefABCDEF')


def fisHex(s):
    return reduce(lambda b, c: b ^ c, (int(a, 16) for a in s if a in VALID), 0)

~~~

**Py Second:**
~~~py
def fisHex(name):
    # fish is 15
    hexdict={'A':10,'B':11,'C':12,'D':13,'E':14,'F':15}
    res=0
    for c in name.upper():
        if c in hexdict:
          res^=hexdict[c]
    return res

~~~

**Py Third:**
~~~py
from operator import xor

def fisHex(name):
    return reduce(xor, (ord(c) - 87 for c in name.lower() if c in "abcdef"), 0)
~~~

**Py Fourth:**
~~~py
def fisHex(name):
  return reduce(int.__xor__, [int(x, 16) for x in name.lower() if x in "abcdef"], 0)
~~~
