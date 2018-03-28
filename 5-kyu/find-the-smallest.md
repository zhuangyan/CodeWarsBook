# ⛹️Find the smallest

You have a positive number n consisting of digits. You can do at most one operation: Choosing the index of a digit in the number, remove this digit at that index and insert it back to another place in the number.

Doing so, find the smallest number you can get.

## Task: Return an array or a tuple or a string depending on the language (see "Sample Tests") with

* 1) the smallest number you got
* 2) the index i of the digit d you took, i as small as possible
* 3) the index j (as small as possible) where you insert this digit d to have the smallest number.

## Example:

smallest(261235) --> [126235, 2, 0] or (126235, 2, 0) or "126235, 2, 0"
126235 is the smallest number gotten by taking 1 at index 2 and putting it at index 0

smallest(209917) --> [29917, 0, 1] or ...

[29917, 1, 0] could be a solution too but index `i` in [29917, 1, 0] is greater than 
index `i` in [29917, 0, 1].
29917 is the smallest number gotten by taking 2 at index 0 and putting it at index 1 which gave 029917 which is the number 29917.

smallest(1000000) --> [1, 0, 6] or ...

## Note
Have a look at "Sample Tests" to see the input and output in each language

## Best Practices

**Py First:**
~~~py
def smallest(n):
  s = str(n)
  min1, from1, to1 = n, 0, 0
  for i in range(len(s)):
    removed = s[:i] + s[i+1:]
    for j in range(len(removed)+1):
      num = int(removed[:j] + s[i] + removed[j:])
      if (num < min1):
        min1, from1, to1 = num, i, j
  return [min1, from1, to1]

~~~

**Py Second:**
~~~py
def smallest(n):
    s = list(str(n))
    def swap(i, p):
        t = s[:]
        t.insert(i, t.pop(p))
        return int(''.join(t))
    return min([swap(i, p), p, i] for i in range(len(s)) for p in range(len(s)))

~~~

**Py Third:**
~~~py
def smallest(n):
    digits = list(map(lambda x: x, str(n)))
    vars = []
    for i, digit in enumerate(digits):
        dgs = list(digits)
        dgs.pop(i)
        for j in range(len(digits)):
            var = list(dgs)
            var.insert(j, digit)
            var = int(''.join(var))
            vars.append([var, i, j])

    return min(vars, key=lambda x: x[0])

~~~

**Py Fourth:**
~~~py
def smallest(n):
    s = str(n)
    iD = next( x for x,v in enumerate(s) if v > s[x+1] )                # first non increasing digit
    minD, fullMin = min(s[iD:]), min(s)
    
    i = s.rfind(minD)                                                   # rightmost minimal digit in "s except the first increasing part"
    while s[i-1] == minD: i -= 1                                        # if several consecutive min digits, step backward to minimize i
    j = next( x for x in range(i) if s[x] >= minD )                     # find the first digit from the beginnning whose the value of "minD"
    ans = [ [int(s[:j] + s[i] + s[j:i] + s[i+1:]), i, j] ]              # store the first answer
    
    j = next( (x for x in range(iD+1,len(s)) if s[x] > s[iD]), len(s))  # seek the place where first non increasing digit could be placed (search the next digit that is strictly bigger)
    while j > 0 and s[j-1] == s[iD]: j -= 1                             # if the previous digit is/are equal to s[i], step backward to minimize j
    ans.append([ int(s[:iD] + s[iD+1:j] + s[iD] + s[j:]), iD, j-1 ])    # store the datas
    
    return min(ans)                                                     # pick the good one...

~~~
