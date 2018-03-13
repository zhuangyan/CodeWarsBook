## Challenge:
My friend John likes to go to the cinema. He can choose between system A and system B.
~~~
System A : buy a ticket (15 dollars) every time
System B : buy a card (500 dollars) and every time 
    buy a ticket the price of which is 0.90 times the price he paid for the previous one.
~~~    
## Example: If John goes to the cinema 3 times:
~~~
System A : 15 * 3 = 45
System B : 500 + 15 * 0.90 + (15 * 0.90) * 0.90 + (15 * 0.90 * 0.90) * 0.90 ( = 536.5849999999999, no rounding for each ticket)
~~~
John wants to know how many times he must go to the cinema so that the final result of System B, when rounded up to the next dollar, will be cheaper than System A.

The function movie has 3 parameters: card (price of the card), ticket (normal price of a ticket), perc (fraction of what he paid for the previous ticket) and returns the first n such that
~~~
ceil(price of System B) < price of System A.
~~~
More examples:
~~~
movie(500, 15, 0.9) should return 43 
    (with card the total price is 634, with tickets 645)
movie(100, 10, 0.95) should return 24 
    (with card the total price is 235, with tickets 240)
~~~
**Kata's link:** [Going to the cinema](https://www.codewars.com/kata/going-to-the-cinema/)


## Best Practices
**Py First:**
~~~py
from itertools import takewhile, count, accumulate
def movie(card, ticket, perc):
    sys_b = accumulate(ticket*perc**n for n in count(1))
    sys_a = accumulate(ticket for m in count(1))
    return sum(1 for a in takewhile(lambda x: round(x[0] + card + 0.49) >= x[1], zip(sys_b, sys_a))) + 1

~~~

**Py Second:**
~~~py
from itertools import count
from math import ceil
def movie(card, ticket, perc):
    return next(n for n in count(1) if ceil(card + ticket * perc * (1 - perc ** n) / (1 - perc)) < ticket * n)

~~~

**Py Third:**
~~~py
from math import ceil

def movie(card, ticket, rate):
    count = 0
    totalA = 0.0
    totalB = 0.0
    
    while (ceil(card + totalB) >= totalA):
        totalA += ticket
        totalB = (totalB + ticket) * rate
        count += 1

    return count
~~~

**Py Fourth:**
~~~py
from itertools import count
from math import ceil

def movie(card, ticket, perc):
    return next( x for x in count(card//ticket)
                 if ticket * x > ceil(card + ticket * perc * (1 - perc**x)/(1 - perc)) )

~~~


