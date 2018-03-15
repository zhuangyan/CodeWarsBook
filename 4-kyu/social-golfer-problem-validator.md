https://www.codewars.com/kata/social-golfer-problem-validator/train/python

A group of N golfers wants to play in groups of G players for D days in such a way that no golfer plays more than once with any other golfer. For example, for N=20, G=4, D=5, the solution at Wolfram MathWorld is
~~~
 Mon:    ABCD    EFGH    IJKL    MNOP    QRST
 Tue:    AEIM    BJOQ    CHNT    DGLS    FKPR
 Wed:    AGKO    BIPT    CFMS    DHJR    ELNQ
 Thu:    AHLP    BKNS    CEOR    DFIQ    GJMT
 Fri:    AFJN    BLMR    CGPQ    DEKT    HIOS
~~~ 
Write a function that validates a proposed solution, a list of list of strings, as being a solution to the social golfer problem. Each character represents a golfer, and each string is a group of players. Rows represent days. The solution above would be encoded as:
~~~
 [
  ['ABCD', 'EFGH', 'IJKL', 'MNOP', 'QRST'],
  ['AEIM', 'BJOQ', 'CHNT', 'DGLS', 'FKPR'],
  ['AGKO', 'BIPT', 'CFMS', 'DHJR', 'ELNQ'],
  ['AHLP', 'BKNS', 'CEOR', 'DFIQ', 'GJMT'],
  ['AFJN', 'BLMR', 'CGPQ', 'DEKT', 'HIOS']
 ]
~~~ 
You need to make sure (1) that each golfer plays exactly once every day, (2) that the number and size of the groups is the same every day, and (3) that each player plays with every other player at most once.

So although each player must play every day, there can be particular pairs of players that never play together.

It is not necessary to consider the case where the number of golfers is zero; no tests will check for that. If you do wish to consider that case, note that you should accept as valid all possible solutions for zero golfers, who (vacuously) can indeed play in an unlimited number of groups of zero.

## Best Practices

**Py First:**
~~~py
def valid(a):   
    d = {}
    day_length = len(a[0])
    group_size = len(a[0][0])
    golfers = {g for p in a[0] for g in p}
    
    for day in a:
        if len(day) != day_length: return False
        for group in day:
            if len(group) != group_size: return False
            for player in group:
                if player not in golfers: return False
                if player not in d:
                    d[player] = set(group)
                else:
                    if len(d[player] & set(group)) > 1: return False
                    else: d[player].add(group)
    return True

~~~

**Py Second:**
~~~py
from itertools import permutations

def get_all_players(a):
    players_str = ''.join([''.join(day) for day in a])
    return set(list(players_str))
    
    
def all_players_play_everyday(a, players):
    for day in a:
        if not set(list(''.join(day))) == players:
            return False
    return True
    

def check_if_play_twice_together(a, players):
    # Get all possible 2 player combos, and remove them as we find them
    all_2mers = list(permutations(players, 2))
    for day in a:
        for team in day:
            team_2mers = list(permutations(list(team), 2))
            for t in team_2mers:
                try:
                    all_2mers.remove(t)
                except:
                    return False
    return True
    
    
def valid(a):
    players = get_all_players(a)
    if len(players) < 2:
        return False
    if not all_players_play_everyday(a, players):
        return False
    return check_if_play_twice_together(a, players)
~~~

**Py Third:**
~~~py
import string
def valid(a):
    l = [j for i in a for j in i]
    days = [''.join(i) for i in a]
    players = string.uppercase[:len(set(''.join(days)))]
    group_size = len(set([len(i) for i in l]))  == 1
    once_a_day = all( [len(set(i)) == len(i) for i in days])
    ll = [''.join([j.replace(i, '') for e in a for j in e if i in j]) for i in players]
    not_twice = all([len(set(i)) == len(i) for i in ll])
    unknown_player = set(''.join(days)) == set(players)
    return group_size * once_a_day * not_twice * unknown_player *len(set(len(i) for i in days)) == 1

~~~
