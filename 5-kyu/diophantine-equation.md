# Description
In mathematics, a Diophantine equation is a polynomial equation, usually in two or more unknowns, such that only the integer solutions are sought or studied.

In this kata we want to find all integers x, y (x >= 0, y >= 0) solutions of a diophantine equation of the form
~~~
 x ^ 2 - 4 * y ^ 2 = n
~~~ 
where the unknowns are x and y and n is a given positive number. Solutions x, y will be given as an array of arrays (Ruby, Python, Clojure, JS, CS, TS)
~~~
 [[x1, y1], [x2, y2] ....]
~~~ 
as an array of tuples (Haskell, C++, Elixir)
~~~
 [(x1, y1), (x2, y2) ....] or { {x1, y1}, {x2, y2} ....} or [{x1, y1}, {x2, y2} ....]
~~~
as an array of pairs (C, see example tests)
~~~
{{x1, y1}{x2, y2} ....}
~~~
and as a string (Java, C#)
~~~
 "[[x1, y1], [x2, y2] ....]"
~~~ 
in decreasing order of the positive xi. If there is no solution returns [] or "[]".

# Examples
~~~
sol_equa(90005) -->  [[45003, 22501], [9003, 4499], [981, 467], [309, 37]]

sol_equa(90002) --> []

(Java, C#)

solEquaStr(90005) --> "[[45003, 22501], [9003, 4499], [981, 467], [309, 37]]"

solEquaStr(90002) --> "[]"
~~~

# Hints: x ^ 2 - 4 y ^ 2 = (x - 2y) (x + 2y).


**Kata's link:** [Diophantine Equation](http://www.codewars.com/kata/diophantine-equation/)

# Best Practices

**Py First:**
~~~py
import math
def sol_equa(n):
    res = []
    for i in range(1, int(math.sqrt(n)) + 1):
        if n % i == 0:
            j = n // i
            if (i + j) % 2 == 0 and (j - i) % 4 == 0:
                x = (i + j) // 2
                y = (j - i) // 4
                res.append([x, y])
            
    return res
~~~

**Py Second:**
~~~py

def sol_equa(n):
    return [[(n/i + i)/2,(n/i - i)/4] for i in range(1, int(n ** 0.5) + 1)
    if n % i == 0 and (n/i + i) % 2 ==0 and (n/i - i) % 4 ==0]
~~~

**Py Third:**
~~~py
def sol_equa(n):
    res = []
    for a in range(1, int(n**0.5 + 1) + 1 ):
        if n % a == 0:
            b = n / a
            if (a + b) % 2 == 0 and (b - a) % 4 == 0:
                res.append( [(a+b)/2, (b-a)/4] )
    return res
~~~
