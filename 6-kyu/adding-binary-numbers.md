**Kata's link:** [Adding Binary Numbers](http://www.codewars.com/kata/adding-binary-numbers/)

## Task: 
You have to write a function add which takes two binary numbers as strings and returns their sum as a string.

## Note:

* You are not allowed to convert binary to decimal & vice versa.
* The sum should contain No leading zeroes.

## Examples:
~~~
add('111','10'); => '1001'
add('1101','101'); => '10010'
add('1101','10111') => '100100'
~~~


## Best Practices

**Py First:**
~~~py
from itertools import izip_longest

ADDER = {
    ('0', '0', '0'): ('0', '0'),
    ('0', '0', '1'): ('1', '0'),
    ('0', '1', '0'): ('1', '0'),
    ('0', '1', '1'): ('0', '1'),
    ('1', '0', '0'): ('1', '0'),
    ('1', '0', '1'): ('0', '1'),
    ('1', '1', '0'): ('0', '1'),
    ('1', '1', '1'): ('1', '1'),
}


def add(x, y):
    x = x.lstrip('0')
    y = y.lstrip('0')

    if not x:
        return y or '0'
    elif not y:
        return x

    sum_digits, carry = [], '0'
    for x_digit, y_digit in izip_longest(x[::-1], y[::-1], fillvalue='0'):
        sum_digit, carry = ADDER[(x_digit, y_digit, carry)]
        sum_digits.append(sum_digit)

    if carry == '1':
        sum_digits.append(carry)

    return ''.join(sum_digits)[::-1]

~~~

**Py Second:**
~~~py
def add(a,b):
  out, ap, bp, r = '', list(a.lstrip('0')), list(b.lstrip('0')), 0
  while (len(ap) > 0 or len(bp) > 0 or r > 0):
    ac, bc = ap.pop() if len(ap) > 0 else None, bp.pop() if len(bp) else None
    total = r + (ac == '1') + (bc == '1')
    out = ('1' if total % 2 else '0') + out
    r = 0 if total < 2 else 1
  return out or '0'
~~~

**Py Third:**
~~~py
def binary_string_to_int(string):
    return sum((d == '1') * 2**i for i, d in enumerate(string[::-1]))

def add(a, b):
    return '{:b}'.format(binary_string_to_int(a) + binary_string_to_int(b))
~~~
