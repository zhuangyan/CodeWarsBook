## Task: 
Given a string and an array of integers representing indices, capitalize all letters at the given indices.

For example:
~~~
capitalize("abcdef",[1,2,5]) = "aBCdeF"
capitalize("abcdef",[1,2,5,100]) = "aBCdeF". There is no index 100.
~~~
The input will be a lowercase string with no spaces and an array of digits.

Good luck!



**Kata's link:** [Indexed capitalization](https://www.codewars.com/kata/indexed-capitalization/)


## Best Practices

**Py First:**
~~~py
def capitalize(s,ind):
    ind = set(ind)
    return ''.join(c.upper() if i in ind else c for i,c in enumerate(s))
~~~

**Py Second:**
~~~py
def capitalize(s, ind):
    result = list(s)
    for index in ind:
        try:
            result[index] = result[index].upper()
        except IndexError:
            break  # assumes the indexes are sorted
    return ''.join(result)

~~~

**Py Third:**
~~~py
def capitalize(s,ind):
    return ''.join(c.upper() if i in ind else c for i, c in enumerate(s))
~~~

**Js First:**
~~~js
function capitalize(s,arr){
  
var capS = s.split("");

for(var i = 0; i < arr.length; i++) {
  if(capS[arr[i]]) {
    capS[arr[i]] = capS[arr[i]].toUpperCase();
  }
}

capS = capS.join("");
return capS
};

~~~

**Js Second:**
~~~js
function capitalize(s,arr){
  return arr.reduce((a,b) => {
    if (a[b]) {
      a[b] = a[b].toUpperCase();
    }
    return a;
  }, [...s]).join('');
}

~~~

**Js Third:**
~~~js
function capitalize(s,arr){
  return [...s].map((x,i)=>arr.includes(i)?x.toUpperCase():x).join('')
};

~~~
