https://www.codewars.com/kata/look-and-say-numbers/train/python

## Task
There exists a sequence of numbers that follows the pattern
~~~
          1
         11
         21
        1211
       111221
       312211
      13112221
     1113213211
          .
          .
          .
~~~          
Starting with "1" the following lines are produced by "saying what you see", so that line two is "one one", line three is "two one(s)", line four is "one two one one".

Write a function that given a starting value as a string, returns the appropriate sequence as a list. The starting value can have any number of digits. The termination condition is a defined by the maximum number of iterations, also supplied as an argument.

## Best Practices

**Py First:**
~~~py
from itertools import groupby

def look_and_say(data='1', maxlen=5):
    L = []
    for i in range(maxlen):
        data = "".join(str(len(list(g)))+str(n) for n, g in groupby(data))
        L.append(data)
    return L

~~~

**Py Second:**
~~~py
def say(string):
  current, count, res = string[0], 0, ''
  for char in string:
    if char == current: count += 1
    else:
      res += str(count) + str(current)
      current, count = char, 1
  res += str(count) + str(current)
  return res

def look_and_say(data='1', maxlen=5):
  res = list()
  for x in range(maxlen):
    if x == 0: res.append(say(data))
    else: res.append(say(res[x - 1]))
  return res
~~~

**Py Third:**
~~~py
from itertools import groupby                                                   
                                                                                  
def look_and_say(data='1', maxlen=5):                                                    
      read_string = [[k, len(list(g))] for k, g in groupby(data)]                 
      output = ""                                                                 
      for item in read_string:                                                    
          output += str(item[1]) + item[0]
    
      maxlen -= 1
      if maxlen == 0:
        return [output]
      return [output] + look_and_say(output, maxlen)

~~~

**Py Fourth:**
~~~py
from itertools import groupby
def look_and_say(data='1', maxlen=5):
    data = "".join(str(len(list(n))) + c for c, n in groupby(data))
    return [data] + look_and_say(data, maxlen - 1) if maxlen else []
~~~

**Py Fifth:**
~~~py
from itertools import groupby


def look_and_say(data='1', maxlen=5):
    fmt = '{}{}'.format
    result = []
    for _ in xrange(maxlen):
        data = ''.join(fmt(sum(1 for _ in g), k) for k, g in groupby(data))
        result.append(data)
    return result

~~~

