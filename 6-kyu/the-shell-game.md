## Task: 
"The Shell Game" involves three shells/cups/etc upturned on a playing surface, with a ball placed underneath one of them. The shells are then rapidly swapped round, and the game involves trying to track the swaps and, once they are complete, identifying the shell containing the ball.

This is usually a con, but you can assume this particular game is fair...

Your task is as follows. Given the shell that the ball starts under, and list of swaps, return the location of the ball at the end. All shells are indexed by the position they are in at the time.

For example, given the starting position 0 and the swap sequence [(0, 1), (1, 2), (1, 0)]:

The first swap moves the ball from 0 to 1
The second swap moves the ball from 1 to 2
The final swap doesn't affect the position of the ball.

So

find_the_ball(0, [(0, 1), (2, 1), (0, 1)]) == 2
There aren't necessarily only three cups in this game, but there will be at least two. You can assume all swaps are valid, and involve two distinct indices.


**Kata's link:** [The Shell Game](http://www.codewars.com/kata/the-shell-game/)


## Best Practices

**Py First:**
~~~py
def find_the_ball(start, swaps):
    pos = start
    for (a, b) in swaps:
        if a == pos:
            pos = b
        elif b == pos:
            pos = a
    return pos

~~~

**Py Second:**
~~~py
def find_the_ball(start, swaps):
  pos = start
  for tup in swaps:
    if pos == tup[0]: pos = tup[1]
    elif pos == tup[1]: pos = tup[0]
  return pos

~~~

**Py Third:**
~~~py
def find_the_ball(start, swaps):
    for sw in swaps:
        if start in sw:
            start = sw[1-sw.index(start)]
    return start
~~~
