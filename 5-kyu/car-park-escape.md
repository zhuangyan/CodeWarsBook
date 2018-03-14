https://www.codewars.com/kata/car-park-escape/train/python

## Introduction
A multi-storey car park (also called a parking garage, parking structure, parking ramp, parkade, parking building, parking deck or indoor parking) is a building designed for car parking and where there are a number of floors or levels on which parking takes place. It is essentially an indoor, stacked car park. Parking structures may be heated if they are enclosed. Design of parking structures can add considerable cost for planning new developments, and can be mandated by cities or states in new building parking requirements. Some cities such as London have abolished previously enacted minimum parking requirements (Source Wikipedia)

## Task
Your task is to escape from the carpark using only the staircases provided to reach the exit. You may not jump over the edge of the levels (you’re not Superman!) and the exit is always on the far right of the ground floor.
## Rules
~~~
1. You are passed the carpark data as an argument into the function.
2. Free carparking spaces are represented by a 0
3. Staircases are represented by a 1
4. Your parking place (start position) is represented by a 2
5. The exit is always the far right element of the ground floor.
6. You must use the staircases to go down a level.
7. You will never start on a staircase.
8. The start level may be any level of the car park.
~~~
## Returns
~~~
Return an array of the quickest route out of the carpark
R1 = Move Right one parking space.
L1 = Move Left one parking space.
D1 = Move Down one level.
~~~
## Example
### Initialise
~~~
carpark = [[1, 0, 0, 0, 2],
           [0, 0, 0, 0, 0]]
~~~           
### Working Out
~~~
You start in the most far right position on level 1
You have to move Left 4 places to reach the staircase => "L4"
You then go down one flight of stairs => "D1"
To escape you have to move Right 4 places => "R4"
~~~
### Result
~~~
result = ["L4", "D1", "R4"]
~~~
Good luck and enjoy!


## Best Practices

**Py First:**
~~~py
def escape(carpark):

    while 2 not in carpark[0]: carpark.pop(0)
    r, ground, pos = [], len(carpark) - 1, carpark[0].index(2)
    for f, floor in enumerate(carpark):
        stairs = floor.index(1) if f != ground else len(floor) - 1
        if stairs != pos:
            r, pos = r + ['RL'[stairs < pos] + str(abs(pos - stairs))], stairs
        if f != ground:
            r += [('D' + str(int(r.pop()[1:]) +1)) if 'D' in r[-1] else 'D1']
    return r

~~~

**Py Second:**
~~~py
def escape(carpark):
    floor, car = next((floor, car)
                      for floor, f in enumerate(carpark)
                      for car, c in enumerate(f) if c == 2)
    route, carpark[-1][-1] = [], 1
    while floor < len(carpark) - 1 or carpark[floor][car] != 1:
        start = floor, car
        while floor < len(carpark) - 1 and carpark[floor][car] == 1:
            floor += 1
        if floor > start[0]: route.append('D%d' % (floor - start[0]))
        car = carpark[floor].index(1)
        if car > start[1]: route.append('R%d' % (car - start[1]))
        if car < start[1]: route.append('L%d' % (start[1] - car))
    return route

~~~

**Py Third:**
~~~py
def escape(carpark):
    movements = []
    
    # Find starting point
    x = -1
    y = 0
    while x == -1:
        try:
            x = carpark[y].index(2)
        except ValueError:
            y += 1
    
    # Find finish
    end_y = len(carpark) - 1
    end_x = len(carpark[end_y]) - 1
    
    # Calculate movement
    while x != end_x or y != end_y:        
        # Move vertical
        move = 0
        while carpark[y][x] == 1:
            move += 1
            y += 1
        if move > 0:
            movements.append('D{}'.format(move))
    
        # Move horizontal
        try:
            goal_x = carpark[y].index(1)
        except ValueError:
            goal_x = end_x
        
        move = goal_x - x
        if move:
            movements.append('{}{}'.format('L' if move < 0 else 'R', abs(move)))
        x = goal_x

    return movements

~~~

**Py Fourth:**
~~~py
def escape(carpark):

    car, stairs, start, moves, x = -1, -1, -1, [], 0
    
    while x < len(carpark):
        line = ''.join(map(str, carpark[x]))                                                           # Use string to avoid troubles with absence of 1 or 2
        stairs = line.find("1")                                                                        # Search for stairs
        if start == -1: start = line.find("2")                                                         # Do this only while the car had not been found yet
        
        if start >= 0: car, start = start, -2                                                          # Car found, start moving the "car" and declare that the car has been already found (start = -2)
        
        if start == -2:
            if x == len(carpark)-1:                                                                    # Car is at ground level
                if car != len(carpark[x])-1: moves.append( "R" + str(len(carpark[x])-1-car) )          # Move the car to the exit if needed
                return moves
                
            moves.append( ["L", "R"][stairs-car > 0] + str(abs(stairs-car)) )                          # Archive the move needed
            car, comingFrom = stairs, x                                                                # Move the car to the stair, collect the current level
            while carpark[x][car] == 1: x += 1                                                         # Go down while stairs are present
            moves.append("D" + str(x-comingFrom))                                                      # Archive the whole descent
            
        else: x += 1                                                                                   # If you reach this, car has not been found yet, so serach one level "lower"

~~~
