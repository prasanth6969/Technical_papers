## Strings ## 
- String is a collection of characters in between single quotes or double quotes is known as strings.
- **multiline strings** is denoted by """content""" 
- Stirngs is like arrays we can access them by index.
- String slicing - u can return a range of characters using string slicing.
- a = "wolrd" print(a[start:end])
- slice from start = a[:5]
- slice from end = a[2:]
- negative indexing = a[-3:-1]
- String concatenation a+b 
- f string used to add content or vallues in between strings
- **Modifiers** - if we want to print two decimal points after number is {variable_name :.2f}.
- escaping charcters 
- \'	Single Quote	
- \\	Backslash	
- \n	New Line	
- \r	Carriage Return	
- \t	Tab	
- \b	Backspace	
- \f	Form Feed	
- \ooo	Octal value	
- \xhh	Hex value

## String Methods ##
- Strings are immutable, so every method returns a **new** string (or value) and the original stays unchanged.

**Case methods**
- **capitalize()** - makes the first character uppercase and the rest lowercase. `"hello WORLD".capitalize()` → `"Hello world"`
- **casefold()** - lowercases aggressively, used for case-insensitive comparison. `"Straße".casefold()` → `"strasse"`
- **lower()** - converts all characters to lowercase. `"HeLLo".lower()` → `"hello"`
- **upper()** - converts all characters to uppercase. `"hello".upper()` → `"HELLO"`
- **swapcase()** - swaps uppercase to lowercase and vice versa. `"Hello".swapcase()` → `"hELLO"`
- **title()** - makes the first letter of every word uppercase. `"hello world".title()` → `"Hello World"`

**Search and count methods**
- **count()** - returns how many times a substring appears. `"banana".count("a")` → `3`
- **find()** - returns the index of the first match, or -1 if not found. `"hello".find("l")` → `2`
- **rfind()** - same as find() but searches from the right. `"hello".rfind("l")` → `3`
- **index()** - same as find() but raises ValueError if not found. `"hello".index("e")` → `1`
- **rindex()** - same as index() but searches from the right. `"hello".rindex("l")` → `3`
- **startswith()** - returns True if the string begins with the given text. `"hello".startswith("he")` → `True`
- **endswith()** - returns True if the string ends with the given text. `"hello".endswith("lo")` → `True`

**Check methods (return True or False)**
- **isalnum()** - True if all characters are letters or digits. `"abc123".isalnum()` → `True`
- **isalpha()** - True if all characters are letters. `"abc".isalpha()` → `True`
- **isascii()** - True if all characters are ASCII (code 0-127). `"abc".isascii()` → `True`
- **isdecimal()** - True if all characters are decimal digits (0-9). `"123".isdecimal()` → `True`
- **isdigit()** - True if all characters are digits, including things like superscripts. `"²".isdigit()` → `True`
- **isnumeric()** - True if all characters are numeric, including fractions like ½. `"½".isnumeric()` → `True`
- **isidentifier()** - True if the string is a valid Python variable name. `"my_var".isidentifier()` → `True`
- **islower()** - True if all letters are lowercase. `"hello".islower()` → `True`
- **isupper()** - True if all letters are uppercase. `"HELLO".isupper()` → `True`
- **istitle()** - True if every word starts with an uppercase letter. `"Hello World".istitle()` → `True`
- **isprintable()** - True if all characters are printable (no \n, \t, etc.). `"hello".isprintable()` → `True`
- **isspace()** - True if the string contains only whitespace. `"   ".isspace()` → `True`

**Modify and clean methods**
- **replace()** - replaces every occurrence of a substring with another. `"cat".replace("c", "b")` → `"bat"`
- **strip()** - removes whitespace (or given characters) from both ends. `"  hi  ".strip()` → `"hi"`
- **lstrip()** - removes whitespace (or given characters) from the left end. `"  hi".lstrip()` → `"hi"`
- **rstrip()** - removes whitespace (or given characters) from the right end. `"hi  ".rstrip()` → `"hi"`
- **removeprefix()** - removes the given text from the start if present (Python 3.9+). `"unhappy".removeprefix("un")` → `"happy"`
- **removesuffix()** - removes the given text from the end if present (Python 3.9+). `"file.txt".removesuffix(".txt")` → `"file"`
- **expandtabs()** - replaces each tab (\t) with spaces. `"a\tb".expandtabs(4)` → `"a   b"`
- **translate()** - replaces characters using a translation table. `"abc".translate(str.maketrans("a", "x"))` → `"xbc"`
- **maketrans()** - builds the translation table used by translate(). `str.maketrans("a", "x")` → `{97: 120}`

**Split and join methods**
- **split()** - splits the string into a list at a separator (default is whitespace). `"a,b,c".split(",")` → `['a', 'b', 'c']`
- **rsplit()** - same as split() but splits from the right, useful with a max split count. `"a,b,c".rsplit(",", 1)` → `['a,b', 'c']`
- **splitlines()** - splits the string into a list at line breaks. `"a\nb".splitlines()` → `['a', 'b']`
- **partition()** - splits at the first match into a 3-part tuple (before, separator, after). `"a-b-c".partition("-")` → `('a', '-', 'b-c')`
- **rpartition()** - same as partition() but splits at the last match. `"a-b-c".rpartition("-")` → `('a-b', '-', 'c')`
- **join()** - joins items of an iterable into one string using the string as separator. `"-".join(["a", "b"])` → `"a-b"`

**Alignment and formatting methods**
- **center()** - centers the string in a given width, padding with spaces or a chosen character. `"hi".center(6, "*")` → `"**hi**"`
- **ljust()** - left-aligns the string in a given width. `"hi".ljust(5, ".")` → `"hi..."`
- **rjust()** - right-aligns the string in a given width. `"hi".rjust(5, ".")` → `"...hi"`
- **zfill()** - pads the string with zeros on the left to a given width. `"42".zfill(5)` → `"00042"`
- **format()** - inserts values into `{}` placeholders. `"Hi {}".format("Ram")` → `"Hi Ram"`
- **format_map()** - like format() but takes values from a dictionary. `"Hi {name}".format_map({"name": "Ram"})` → `"Hi Ram"`

**Encoding**
- **encode()** - converts the string to bytes using an encoding (default UTF-8). `"hi".encode()` → `b'hi'`
