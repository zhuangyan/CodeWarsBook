## Task: 
Write a function that removes every lone 9 that is inbetween 7s.


## Examples:

~~~
seven_ate9('79712312') => '7712312'
seven_ate9('79797') => '777'
~~~

**Kata's link:** [SevenAte9](https://www.codewars.com/kata/sevenate9/)


## Best Practices

**Py First:**
~~~py
def seven_ate9(str_):
   while str_.find('797') != -1:
       str_ = str_.replace('797','77')
   return str_
~~~

**Py Second:**
~~~py
import re

def seven_ate9(str_):
    return re.sub(r'79(?=7)', r'7', str_)

~~~

**Py Third:**
~~~py
seven_ate9 = lambda s:''.join(x for i, x in enumerate(s) if s[i-1:i+2] != "797")
~~~
