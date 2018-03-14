https://www.codewars.com/kata/regexp-basics-is-it-ipv4-address/train/python

## Task
Implement String#ipv4_address?, which should return true if given object is an IPv4 address - four numbers (0-255) separated by dots.

It should only accept addresses in canonical representation, so no leading 0s, spaces etc.

## Best Practices

**Py First:**
~~~py
from re import compile, match

REGEX = compile(r'((\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.){4}$')


def ipv4_address(address):
    # refactored thanks to @leonoverweel on CodeWars
    return bool(match(REGEX, address + '.'))

~~~

**Py Second:**
~~~py
import socket
def ipv4_address(address):
    try: # No need to do work that's already been done
        socket.inet_pton(socket.AF_INET,address)
        return True
    except socket.error: # Better to ask forgiveness than permission
        return False

~~~

**Py Third:**
~~~py
def ipv4_address(address):
    return address.count(".")==3 and all([str.isdigit(s) and s==str(int(s)) and int(s)>=0 and int(s)<256 for s in address.split(".")])
~~~
