https://www.codewars.com/kata/simplifying-multilinear-polynomials/train/python

When we attended middle school were asked to simplify mathematical expressions like "3x-yx+2xy-x" (or usually bigger), and that was easy-peasy ("2x+xy"). But tell that to your pc and we'll see! 

Write a function:
~~~
simplify(poly)
~~~
that takes a string in input, representing a multilinear non-constant polynomial in integers coefficients (like "3x-zx+2xy-x"), and returns another string as output where the same expression has been simplified in the following way ( -> means application of simplify):

* All possible sums and subtraction of equivalent monomials ("xy==yx") has been done, e.g.:
~~~
"cb+cba" -> "bc+abc", "2xy-yx" -> "xy", "-a+5ab+3a-c-2a" -> "-c+5ab" 
~~~

* All monomials appears in order of increasing number of variables, e.g.:
~~~
"-abc+3a+2ac" -> "3a+2ac-abc", "xyz-xz" -> "-xz+xyz" 
~~~
* If two monomials have the same number of variables, they appears in lexicographic order, e.g.:
~~~
"a+ca-ab" -> "a-ab+ac", "xzy+zby" ->"byz+xyz" 
~~~
* There is no leading + sign if the first coefficient is positive, e.g.:
~~~
"-y+x" -> "x-y", but no restrictions for -: "y-x" ->"-x+y" 
~~~
N.B. to keep it simplest, the string in input is restricted to represent only multilinear non-constant polynomials, so you won't find something like `-3+yx^2'. Multilinear means in this context: of degree 1 on each variable.

Warning: the string in input can contain arbitrary variables represented by lowercase characters in the english alphabet.

Good Work :)

## Best Practices

**Py First:**
~~~py
def simplify(poly):
    # I'm feeling verbose today
    
    # get 3 parts (even if non-existent) of each term: (+/-, coefficient, variables)
    import re
    matches = re.findall(r'([+\-]?)(\d*)([a-z]+)', poly)
    
    # get the int equivalent of coefficient (including sign) and the sorted variables (for later comparison)
    expanded = [[int(i[0] + (i[1] if i[1] != "" else "1")), ''.join(sorted(i[2]))] for i in matches]
    
    # get the unique variables from above list. Sort them first by length, then alphabetically
    variables = sorted(list(set(i[1] for i in expanded)), key=lambda x: (len(x), x))
    
    # get the sum of coefficients (located in expanded) for each variable
    coefficients = {v:sum(i[0] for i in expanded if i[1] == v) for v in variables}
    
    # clean-up: join them with + signs, remove '1' coefficients, and change '+-' to '-'
    return '+'.join(str(coefficients[v]) + v for v in variables if coefficients[v] != 0).replace('1','').replace('+-','-')

~~~

**Py Second:**
~~~py
import re
def simplify(poly):
    terms = {}
    for sign, coef, vars in re.findall(r'([\-+]?)(\d*)([a-z]*)', poly):
        sign = (-1 if sign == '-' else 1)
        coef = sign * int(coef or 1)
        vars = ''.join(sorted(vars))
        terms[vars] = terms.get(vars, 0) + coef
    # sort by no. of variables
    terms = sorted(terms.items(), key=lambda (v, c): (len(v), v))
    return ''.join(map(format_term, terms)).strip('+')

def format_term((vars, coef)):
    if coef == 0:
        return ''
    if coef == 1:
        return '+' + vars
    if coef == -1:
        return '-' + vars
    return '%+i%s' % (coef, vars)
~~~

