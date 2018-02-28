# Description

You need to write regex that will validate a password to make sure it meets the following criteria:

* At least six characters long
* contains a lowercase letter
* contains an uppercase letter
* contains a number

Valid passwords will only be alphanumeric characters.

**Kata's link**: [Regex Password Validation](https://www.codewars.com/kata/regex-password-validation/)

# Best Practices

**JavaScript First:**
```js
function validate(password) {
  return /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])[a-zA-Z0-9]{6,}$/.test(password);
}
```

**JavaScript Second:**
```js
function validate(password) {
  return  /^[A-Za-z0-9]{6,}$/.test(password) &&
          /[A-Z]+/           .test(password) &&
          /[a-z]+/           .test(password) &&
          /[0-9]+/           .test(password) ;
}
```

**Python First:**
```py
regex="^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[^\W_]{6,}$"

```

**Python Second:**
```py
from re import compile, VERBOSE

regex = compile("""
^              # begin word
(?=.*?[a-z])   # at least one lowercase letter
(?=.*?[A-Z])   # at least one uppercase letter
(?=.*?[0-9])   # at least one number
[A-Za-z\d]     # only alphanumeric
{6,}           # at least 6 characters long
$              # end word
""", VERBOSE)
```