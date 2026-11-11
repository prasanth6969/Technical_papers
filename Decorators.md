## DECORATORS ##
- A decorator is a function that takes a function, adds extra behaviour, and returns a new function. The original code is not changed. 

**Example without decorator**
```
def division(a,b):
    return a / b
result = division(5,10)

```
**Swappings variables inside function**
```

def division(a,b):
    if a<b:
        a,b = b,a
    return a / b
result = division(5,10)

```
- Now if you need this swapping method again  for subtraction method
```
def sub(a,b):
    if a<b:
        a,b = b,a
    return a - b
result1 = sub(5,10)

```
**Now if you need this same condition for different this is not the efficient way to achieve that specific condition** 

```

def swapping(func): # func holds the sub or division here
    def modify(a,b):
        if a < b:
            a,b = b,a 
        return func(a,b) # After swapping values now its call the original function which sub(a,b)
    return modify

@swapping # we can use sub = swapping(sub) 
def sub(a,b): # Here sub(a,b) = modify function calling modify(a,b)
    return a - b
result = sub(5,10)

@swapping
def division(a,b):
    return a / b
result = division(5,10)

```
**We can achieve this without decorators**

```  
def swap_if_needed(a, b):
    if a < b:
        a, b = b, a
    return a, b

def sub(a, b):
    a, b = swap_if_needed(a, b)
    return a - b

def division(a, b):
    a, b = swap_if_needed(a, b)
    return a / b

``` 
- With a decorator, you add @swapping above the function, and the function body stays untouched
- Works on functions you can’t edit

 - Helper: you must change the function body to call it, so it can’t work if the code isn’t yours (like a library function).
 - Decorator: you wrap the function from outside, so you don’t touch its code.
 ```
import math

safe_sqrt = swapping(math.sqrt)   # math.sqrt is not edited


 ```
**Login Check**
```
def login_required(func):
    def wrapper(user):
        if not user["logged_in"]:
            return "Please login first"
        return func(user)
    return wrapper

@login_required
def view_profile(user):
    return f"Welcome {user['name']}"

name = input("Enter your name: ")
status = input("Are you logged in? (yes/no): ").lower()

user = {"name": name, "logged_in": status == "yes"}

print(view_profile(user))

```
