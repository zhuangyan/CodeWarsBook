# 🍪Write out numbers

Create a function that transforms any positive number to a string representing the number in words. The function should work for all numbers between 0 and 999999.

## Examples
~~~
number2words(0)  ==>  "zero"
number2words(1)  ==>  "one"
number2words(9)  ==>  "nine"
number2words(10)  ==>  "ten"
number2words(17)  ==>  "seventeen"
number2words(20)  ==>  "twenty"
number2words(21)  ==>  "twenty-one"
number2words(45)  ==>  "forty-five"
number2words(80)  ==>  "eighty"
number2words(99)  ==>  "ninety-nine"
number2words(100)  ==>  "one hundred"
number2words(301)  ==>  "three hundred one"
number2words(799)  ==>  "seven hundred ninety-nine"
number2words(800)  ==>  "eight hundred"
number2words(950)  ==>  "nine hundred fifty"
number2words(1000)  ==>  "one thousand"
number2words(1002)  ==>  "one thousand two"
number2words(3051)  ==>  "three thousand fifty-one"
number2words(7200)  ==>  "seven thousand two hundred"
number2words(7219)  ==>  "seven thousand two hundred nineteen"
number2words(8330)  ==>  "eight thousand three hundred thirty"
number2words(99999)  ==>  "ninety-nine thousand nine hundred ninety-nine"
number2words(888888)  ==>  "eight hundred eighty-eight thousand eight hundred eighty-eight"
~~~

## Best Practices

**Py First:**
~~~py
words = "zero one two three four five six seven eight nine" + \
" ten eleven twelve thirteen fourteen fifteen sixteen seventeen eighteen nineteen twenty" + \
" thirty forty fifty sixty seventy eighty ninety"
words = words.split(" ")

def number2words(n):
    if n < 20:
        return words[n]
    elif n < 100:
        return words[18 + n // 10] + ('' if n % 10 == 0 else '-' + words[n % 10])
    elif n < 1000:
        return number2words(n // 100) + " hundred" + (' ' + number2words(n % 100) if n % 100 > 0 else '')
    elif n < 1000000:
        return number2words(n // 1000) + " thousand" + (' ' + number2words(n % 1000) if n % 1000 > 0 else '')
~~~

**Py Second:**
~~~py
def number2words(n):
    if n == 0: return "zero"
    if n == 10: return "ten"
    
    numbers_11_19={
    "0":"ten",
    "1":"eleven",
    "2":"twelve",
    "3":"thirteen",
    "4":"fourteen",
    "5": "fifteen",
    "6":"sixteen",
    "7":"seventeen",
    "8":"eighteen",
    "9":"nineteen"
    }
    numbers_1_9={
    "0":"",
    '1':'one',
    '2':'two',
    "3":"three",
    "4":"four",
    "5":"five",
    "6":"six",
    "7":"seven",
    "8":"eight",
    "9":"nine",
    }
    numbers_20_100={
    "0":"",
    "2":"twenty",
    "3":"thirty",
    "4":"forty",
    "5":"fifty",
    "6":"sixty",
    "7":"seventy",
    "8":"eighty",
    "9":"ninety",
    }
  
    nStr=str(n)
    print (nStr)
    s=""
    L=len(nStr)
    pos=0
    if pos==L-6:#4 simvol sotni tisyzcg
        s+=numbers_1_9.get(nStr[pos])
        if nStr[pos]!="0":s+=" hundred "
        pos+=1
    if pos==L-5:#4simvol - desytki ticych
        if nStr[pos]=="1": #11 - 19
            s+=numbers_11_19.get(nStr[pos+1])
            pos=+1
        else:
            s+=numbers_20_100.get(nStr[pos])
            if nStr[pos+1]!="0" and nStr[pos]!="0" : s+="-"
        pos+=1
    if pos==L-4:#3 simvol - tisycha
        if nStr[pos-1]!="1": s+=numbers_1_9.get(nStr[pos])
        s+=" thousand "
        pos+=1
    if pos==L-3:#2 simbol - sotka
        s+=numbers_1_9.get(nStr[pos])
        if nStr[pos]!="0":s+=" hundred "
        pos+=1
    if pos==L-2: #1 simvol, desytok
        if nStr[pos]=="1": #11 - 19
            s+=numbers_11_19.get(nStr[pos+1])
            pos=-1
        else:
            s+=numbers_20_100.get(nStr[pos])
            if nStr[pos+1]!="0" and nStr[pos]!="0" : s+="-"
        pos+=1
    if pos==L-1: #0 simvol, edinici
        s+=numbers_1_9.get(nStr[pos]) 
    return s.strip()


~~~

**Py Third:**
~~~py
d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five',
     6: 'six', 7: 'seven', 8: 'eight', 9: 'nine', 10: 'ten',
     11: 'eleven', 12: 'twelve', 13: 'thirteen', 14: 'fourteen',
     15: 'fifteen', 16: 'sixteen', 17: 'seventeen', 18: 'eighteen', 
     19: 'nineteen', 20: 'twenty', 30: 'thirty', 40: 'forty', 
     50: 'fifty', 60: 'sixty', 70: 'seventy', 80: 'eighty', 
     90: 'ninety', 0:''}

def number2words(n):   
    s = (htu(n // 1000) + ' thousand ' if n // 1000 else '') + htu(n % 1000)
        
    return ' '.join(s.split()) if s else 'zero'

    
def htu(n):
    h, tu, u = n//100, n % 100, n % 10
    t = (d[tu] if tu in d else d[tu//10*10] + '-' + d[u]).strip('-')
    return d[h] + ' hundred ' + t if h else t

~~~

**Py Fourth:**
~~~py
def number2words(n):
    """ works for numbers between 0 and 999999 """
    b=["zero","one","two","three","four","five","six","seven","eight","nine","ten","eleven","twelve","thirteen","fourteen","fifteen","sixteen","seventeen","eighteen","nineteen"]
    b2=["twenty","thirty","forty","fifty","sixty","seventy","eighty","ninety"]
    if 0 <= n <= 19:
        return b[n]
    elif 20 <= n <= 99:
        return "{}{}".format(b2[int(str(n)[0])-2],"" if int(str(n)[1]) == 0 else "-" + number2words(int(str(n)[1])))
    elif 100 <= n <= 999:
        return "{}{}".format(number2words(int(str(n)[0])) + " hundred","" if int(str(n)[1:]) == 0 else " " + number2words(int(str(n)[1:])))
    else:
        return "{}{}".format(number2words(int(str(n)[:-3])) + " thousand","" if int(str(n)[-3:]) == 0 else " " + number2words(int(str(n)[-3:])))
~~~