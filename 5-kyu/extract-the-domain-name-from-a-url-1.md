# 💱Extract the domain name from a URL

Write a function that when given a URL as a string, parses out just the domain name and returns it as a string. For example:

~~~
domain_name("http://github.com/carbonfive/raygun") == "github" 
domain_name("http://www.zombie-bites.com") == "zombie-bites"
domain_name("https://www.cnet.com") == "cnet"
~~~

## Best Practices

**Py First:**
~~~py
def domain_name(url):
    return url.split("//")[-1].split("www.")[-1].split(".")[0]
~~~

**Py Second:**
~~~py
import re
def domain_name(url):
    return re.search('(https?://)?(www\d?\.)?(?P<name>[\w-]+)\.', url).group('name')
    
~~~

**Py Third:**
~~~py
def domain_name(url):
    from re import findall, VERBOSE
    
    try:
        url = findall("""\A
                        (?: http
                        s?
                        ://)?         # matches http:// or https:// or nothing
                        
                        (?: www.)?    # matches www. or nothing
                        
                        ([- a-z]+)    # matches a sequence of letters and dashes
                        
                        (?: .com|.ru)     # matches either .com or .ru
                        (?: [/ a-z]+)?    # matches a sequence or letters and slashes
                        \Z""", url, VERBOSE)
        return url[0]
    except:
        return "Invalid URL."
~~~

**Py Fourth:**
~~~py
def domain_name(url):
    
   if ("www" not in url): return url.split("//")[1].split(".")[0]
   else: return url.split(".")[1]
~~~