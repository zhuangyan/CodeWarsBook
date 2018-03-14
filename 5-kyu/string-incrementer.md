https://www.codewars.com/kata/string-incrementer/train/python

## Task
Your job is to write a function which increments a string, to create a new string. If the string already ends with a number, the number should be incremented by 1. If the string does not end with a number the number 1 should be appended to the new string.

## Examples:
~~~
foo -> foo1

foobar23 -> foobar24

foo0042 -> foo0043

foo9 -> foo10

foo099 -> foo100
~~~
Attention: If the number has leading zeros the amount of digits should be considered.

## Best Practices

**Py First:**
~~~py
def increment_string(strng):
    head = strng.rstrip('0123456789')
    tail = strng[len(head):]
    if tail == "": return strng+"1"
    return head + str(int(tail) + 1).zfill(len(tail))
~~~

**Py Second:**
~~~py
import re

def increment_string(input):
    match = re.search("(\d*)$", input)
    if match:
        number = match.group(0)
        if number is not "":
            return input[:-len(number)] + str(int(number) + 1).zfill(len(number))
    return input + "1"

~~~

**Py Third:**
~~~py
def increment_string(s):
    if s and s[-1].isdigit():
        return increment_string(s[:-1]) + "0" if s[-1] == "9" else s[:-1] + `int(s[-1]) + 1`
    return s + "1"

~~~

**Py Fourth:**
~~~py
def increment_string(strng):
    
    # strip the decimals from the right
    stripped = strng.rstrip('1234567890')
    
    # get the part of strng that was stripped
    ints = strng[len(stripped):]
    
    if len(ints) == 0:
        return strng + '1'
    else:
        # find the length of ints
        length = len(ints)
    
        # add 1 to ints
        new_ints = 1 + int(ints)
    
        # pad new_ints with zeroes on the left
        new_ints = str(new_ints).zfill(length)
    
        return stripped + new_ints

~~~
