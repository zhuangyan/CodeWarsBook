# ⛽Rotate a square matrix like a vortex

Your task is to rotate a square matrix of numbers like a vortex.

> In most vortices, the fluid flow velocity is greatest next to its axis and decreases in inverse proportion to the distance from the axis.
So the rotation speed increases with every ring nearer to the middle.

For this kata this means, that the outer "ring" of the matrix rotates one step. The next ring rotates two steps. The next ring rotates three steps. And so on...

The rotation is always "to the left", so against clockwise!

An example:
~~~
The given matrix:
5 3 6 1
5 8 7 4
1 2 4 3
3 1 2 2

First step:
The outer ring is rotated once to the left.
5 3 6 1  ->  1 4 3 2
5 8 7 4  ->  6 8 7 2
1 2 4 3  ->  3 2 4 1
3 1 2 2  ->  5 5 1 3

Second step:
The second ring is rotated twice to the left.
8 7 -> 7 4 -> 4 2
2 4 -> 8 2 -> 7 8 

In the whole square the second step looks like this:
1 4 3 2  ->  1 4 3 2
6 8 7 2  ->  6 4 2 2
3 2 4 1  ->  3 7 8 1
5 5 1 3  ->  5 5 1 3

No more rings. So the result is clear.

~~~
Task Create the method for rotating like a vortex. The method has one input parameter:

The sqaure matrix as an array of arrays 

Your method have to return the rotated matrix. You must not change the input array! Create a new array for the output.

The square matrix will always be at least 1x1 and at most 20x20 and of course the array will never be null. 


Have fun coding it and please don't forget to vote and rank this kata! :-)

I have also created other katas. Take a look if you enjoyed this kata!

## Best Practices

**Py First:**
~~~py
def rotate_like_a_vortex(matrix):
  length = len(matrix);
  nArr = [];
  
  for i in range(length):    
    nArr.append([])
    for j in range(length):    
      nArr[i].append(0)
  
  for h in range(int(length/2)):      
    for i in range(h, length-h):
      for j in range(h,length-h):
        nArr[length-1-j][i] = matrix[i][j];          
    
    matrix = [];
    for i in range(length):    
      matrix.append(nArr[i][::])
  
  return matrix;
~~~

**Py Second:**
~~~py
from math import ceil

def split_ring(matrix, ring):
    """Extract a ring from a matrix, and replace all other values with zero"""
    targets = [ring, len(matrix) - ring - 1]
    check = lambda x: targets[0] <= x <= targets[1]
    is_ring = lambda r, c: (r in targets and check(c)) or (c in targets and check(r))
    return [[v if is_ring(r, c) else 0 for c, v in enumerate(row)] for r, row in enumerate(matrix)]

def rotate(matrix, n=1):
    """Rotate a matrix n quarter turns anti-clockwise"""
    for _ in range(n % 4):
        matrix = [[row[c] for row in matrix] for c in range(len(matrix) - 1, -1, -1)]
    return matrix

def rotate_like_a_vortex(matrix):
    # Rotate each ring
    rings = [rotate(split_ring(matrix, ring), ring + 1) for ring in range(int(ceil(len(matrix) / 2)))]
    # Sum the rings
    while len(rings) > 1:
        rings[0:2] = [[[v1 + v2 for v1, v2 in zip(row1, row2)] for row1, row2 in zip(rings[0], rings[1])]]
    return rings[0]
            
~~~

**Py Third:**
~~~py
def rotate(m):
    return list(zip( *[l[::-1] for l in m] ))           # rotate 90 degrees, counter clockwise

def rotate_like_a_vortex(matrix):
    m = [ tuple(l) for l in matrix ]                    # make a copy with tuples (compatibility of concatenations)
    r, l = 0, len(m[0])
    while l-r > 1:
        subM = rotate( [line[r:l] for line in m[r:l]] ) # rotate submatrix
        for subI,i in enumerate(range(r,l)):
            m[i] = m[i][:r] + subM[subI] + m[i][l:]     # update concerned lines of the main matrix
        r += 1
        l -= 1
    return [ list(l) for l in m ]                       # convert to list
~~~

**Py Fourth:**
~~~py
import numpy as np

def rotate_like_a_vortex(matrix):
    m = np.array(matrix)
    for i in range(len(matrix)//2):
        m[i:len(m)-i, i:len(m)-i] = np.rot90(m[i:len(m)-i, i:len(m)-i])

    return m.tolist()

~~~
