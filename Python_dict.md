## Python Dictionary ##
-Dictionaries are used to store data values in **key : value pairs**
- It is ordered.
- It is mutable(changeable)
- It doesn't allow duplicate keys.
- It is denoted with curly brackets {} 

**Syntax**
- dictname = {key : value , key : value}

**Accessing**
- #accessing through key
- print(dictname[key])
- type() = <class 'dict'>

- #accessing through get() method
- variable = dictname.get(key)


**dict constructor**
- dictname = dict(name = value , name = value)

**Nested dictionar**

- mydict = {1:{1.1:val,1.2:val},2:{key:val}}
- accessing = dictname[key[key]]

**Important methods**
- .keys() = Gives a list of all keys 
- .values() = Gives a list of all values
- .items() = Gives both keys and values
- .update() = updates value if key exists  if not, creates new key and assign it
- pop() = removes elements (dictname.pop(key))
- popitem() = removes last inserted item
- del = removes items (del dictname(key))
- clear = empty the whole dictionary(dictname.clear())
- looping 
 - for i in dictname: (prints keys)
 - for i in dictname.values(prints values)
 - for i,j in dict.items(print both key & val)
- copy dict = newdict = olddict.copy()


