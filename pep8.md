## What is PEP 8 ? ##
- Generally the code is mainly meant to be Read by others rather than writing.
- For better readability we need to write the code with some guide lines , so that people can understand easily.

**PEP 8 -**- PEP stands for **Python Enhancement Proposal** THESE are numbered documents where python developers propose and record changes or guidelines.

### The main rules ###
- **Indentation**: use 4 spaces for each level. Don’t mix tabs and spaces.
- **Line length**: keep each line under 80 characters, and comments or docstrings under 72.
- **Naming**:
**snake_case for variables and functions** : total_score, calc_area
- **PascalCase for classes** : SnakeGame
UPPER_CASE for constants: MAX_SPEED
-**Spacing** : use spaces around operators (x = a + b), but not inside brackets or before a comma.
- **Imports** : place them at the top of the file, one per line, in this order: standard library, third-party packages, then your own modules.
- **Blank lines** : leave two blank lines between top-level functions and classes, and one between methods inside a class.

### Example ###

```python
# Hard to read

def CalcArea(w,h):
    return w*h

# Follows PEP 8
# Better naming of variables

def calc_area(width, height):
    return width * height
```
### Modules ###
- There is some modules which used to check our code has been write with PEP 8 guideline or not.
 - **pycodestyle** reports PEP 8 violations.
 - **flake8** checks style and common errors together.
 - **black** rewrites your code into a PEP 8-compliant format automatically.