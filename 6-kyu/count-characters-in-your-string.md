https://www.codewars.com/kata/count-characters-in-your-string/train/python

## Task
The main idea is to count all the occuring characters(UTF-8) in string. If you have string like this aba then the result should be { 'a': 2, 'b': 1 }

What if the string is empty ? Then the result should be empty object literal { }

For C#: Use a Dictionary<char, int> for this kata!

## Best Practices

**Py First:**
~~~py
from collections import Counter as count

~~~

**Py Second:**
~~~py
def count(string):
  
    return {i: string.count(i) for i in string}

~~~