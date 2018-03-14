**Kata's link:** [Longest palindrome](http://www.codewars.com/kata/longest-palindrome/)

## Task: 
Find the length of the longest substring in the given string s that is the same in reverse.

As an example, if the input was “I like racecars that go fast”, the substring (racecar) length would be 7.

If the length of the input string is 0, return value must be 0.


## Example: 
~~~
"a" -> 1 
"aab" -> 2  
"abcde" -> 1
"zzbaabcd" -> 4
"" -> 0
~~~



## Best Practices

**Py First:**
~~~py
def longest_palindrome (s):
    longest = 0
    for left in xrange(len(s)):
        for right in xrange(len(s), left, -1):
            if s[left:right] in (s[left:right])[::-1]:
                longest = max(right-left, longest)
                break
    return longest

~~~

**Py Second:**
~~~py
def longest_palindrome(s):
    for c in xrange(len(s), -1, -1):
        for i in xrange(len(s) - c + 1):
            if s[i:i + c] == s[i:i + c][::-1]:
                return c

~~~

**Py Third:**
~~~py
def longest_palindrome(s):
    """Manacher algorithm - Complexity O(n)"""
    # Transform S into T.
    # For example, S = "abba", T = "^#a#b#b#a#$".
    # ^ and $ signs are sentinels appended to each end to avoid bounds checking
    T = '#'.join('^{}$'.format(s))
    n = len(T)
    P = [0] * n
    C = R = 0
    for i in range (1, n - 1):
        P[i] = (R > i) and min(R - i, P[2*C - i]) # equals to i' = C - (i-C)
        # Attempt to expand palindrome centered at i
        while T[i + 1 + P[i]] == T[i - 1 - P[i]]:
            P[i] += 1

        # If palindrome centered at i expand past R,
        # adjust center based on expanded palindrome.
        if i + P[i] > R:
            C, R = i, i + P[i]

    # Find the maximum element in P.
    maxLen, centerIndex = max((n, i) for i, n in enumerate(P))
    return maxLen

~~~

**Py Fourth:**

~~~py
def longest_palindrome (s):
    if not s: return 0
    substrings = [s[i:j] for i in range(0,len(s)) for j in range(i,len(s)+1)]
    return max(len(s) for s in substrings if s == s[::-1])
~~~
