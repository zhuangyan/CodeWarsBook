https://www.codewars.com/kata/base-conversion/train/

In this kata you have to implement a base converter, which converts positive integers between arbitrary bases / alphabets. Here are some pre-defined alphabets:
~~~
bin      = '01'
oct      = '01234567'
dec      = '0123456789'
hex      = '0123456789abcdef'
allow    = 'abcdefghijklmnopqrstuvwxyz'
allup    = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
alpha    = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
alphanum = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
~~~
The function convert() should take an input (string), the source alphabet (string) and the target alphabet (string). You can assume that the input value always consists of characters from the source alphabet. You don't need to validate it.

## Examples
~~~
convert("15", dec, bin)       ==>  "1111"
convert("15", dec, oct)       ==>  "17"
convert("1010", bin, dec)     ==>  "10"
convert("1010", bin, hex)     ==>  "a"
convert("0", dec, alpha)      ==>  "a"
convert("27", dec, allow)     ==>  "bb"
convert("hello", allow, hex)  ==>  "320048"
~~~
## Additional Notes:

* The maximum input value can always be encoded in a number without loss of precision in JavaScript. In Haskell, intermediate results will probably be too large for Int.
* The function must work for any arbitrary alphabets, not only the pre-defined ones
You don't have to consider negative numbers

## Best Practices

**Py First:**
~~~py
def convert(input, source, target):
    base_in = len(source)
    base_out = len(target)
    acc = 0
    out = ''
    for d in input:
        acc *= base_in
        acc += source.index(d)
    while acc != 0:
        d = target[acc%base_out]
        acc = acc/base_out
        out = d+out
    return out if out else target[0] 

~~~

**Py Second:**
~~~py
from math import log

def convert(value, source, target):
    value = sum(source.find(c) * (len(source) ** i) for i, c in enumerate(reversed(value)))
    return ''.join(target[(value / (len(target) ** i)) % len(target)] for i in xrange(0 if not value else int(log(value, len(target))),-1,-1))

~~~

**Py Third:**
~~~py
def to_base(n, base, alphabet):
    if n < base:
        return alphabet[n]
    else:
        q, r = divmod(n, base)
        return to_base(q, base, alphabet) + alphabet[r]
    
def convert(input, source, target):
    b = len(source)
    n = sum(source.index(x) * b ** i for i, x in enumerate(reversed(input)))
    return to_base(n, len(target), target)

~~~
