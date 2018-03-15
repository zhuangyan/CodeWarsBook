https://www.codewars.com/kata/longest-common-subsequence/train/python

Write a function called LCS that accepts two sequences and returns the longest subsequence common to the passed in sequences.

## Subsequence
A subsequence is different from a substring. The terms of a subsequence need not be consecutive terms of the original sequence.

##Example subsequence
Subsequences of "abc" = "a", "b", "c", "ab", "ac", "bc" and "abc".
~~~
LCS examples
lcs( "abcdef" , "abc" ) => returns "abc"
lcs( "abcdef" , "acf" ) => returns "acf"
lcs( "132535365" , "123456789" ) => returns "12356"
~~~

## Notes
* Both arguments will be strings
* Return value must be a string
* Return an empty string if there exists no common subsequence
* Both arguments will have one or more characters (in JavaScript)
* All tests will only have a single longest common subsequence. Don't worry about cases such as LCS( "1234", "3412" ), which would have two possible longest common subsequences: "12" and "34".

Note that the Haskell variant will use randomized testing, but any longest common subsequence will be valid.

Note that the OCaml variant is using generic lists instead of strings, and will also have randomized tests (any longest common subsequence will be valid).

## Tips
Wikipedia has an explanation of the two properties that can be used to solve the problem:

* [First property](http://en.wikipedia.org/wiki/Longest_common_subsequence_problem#First_property)
* [Second property](http://en.wikipedia.org/wiki/Longest_common_subsequence_problem#Second_property)

## Best Practices

**Py First:**
~~~py
def lcs(x, y):
    if len(x) == 0 or len(y) == 0:
        return ''
    if x[-1] == y[-1]:
        return lcs(x[:-1], y[:-1]) + x[-1]
    else:
        lcs1 = lcs(x,y[:-1])
        lcs2 = lcs(x[:-1],y)
        if len(lcs1) > len(lcs2):
            return lcs1
        else:
            return lcs2

~~~

**Py Second:**
~~~py
from itertools import combinations

def subsequences(s):
    """Returns set of all subsequences in s."""
    return set(''.join(c) for i in range(len(s) + 1) for c in combinations(s, i))

def lcs(x, y):
    """Returns longest matching subsequence of two strings."""
    return max(subsequences(x).intersection(subsequences(y)), key=len)

~~~

**Py Third:**
~~~py
def lcs(x, y):
  res=[]
  i=0
  for item in y:
     if item in x[i:]:
        res+=[item]
        i=x.index(item)+1
  return "".join(res)

~~~
