# Python Array #

- List are acting as array in python
- lists are ordered.
- lists are mutable(changeable).
- lists allows duplicates.
- syntax
  - list_name = [1,2,3]
- type(list_name) = <class list>
- list length = len(list_name)
- list_accesing = list_name[index]
- list constructor = list(("a","b","c"))
- list negative indexing = list_name[-1] (last item)
- list range
  - thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
  - print(thislist[2:5])
- This example returns the items from the beginning to, but NOT including, "kiwi":
  - thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
  - print(thislist[:4])
- This example returns the items from "orange" (-4) to, but NOT including "mango" (-1):
  - thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
  - print(thislist[-4:-1])
- changing list item
  - thislist = ["apple", "banana", "cherry"]
  - thislist[1] = "blackcurrant"
  - print(thislist)
- Change the values "banana" and "cherry" with the values "blackcurrant" and "watermelon":
  - thislist = ["apple", "banana", "cherry", "orange", "kiwi", "mango"]
  - thislist[1:3] = ["blackcurrant", "watermelon"]
  - print(thislist)
- Change the second value by replacing it with two new values:
  - thislist = ["apple", "banana", "cherry"]
  - thislist[1:2] = ["blackcurrant", "watermelon"]
  - print(thislist)

# List comprehension #

- This list comprehension offers a shorter syntax when you want to create a new list based on the values of an existing list
- **syntax**
  - newlist = [expression for item in iterable if condition == True]
- example
  - fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
  - newlist = [x for x in fruits if "a" in x]
  - print(newlist)

# Built-in list methods #

| Method | Explanation |
|--------|-------------|
| append() | Adds an item at the end of the list |
| clear() | Removes all items from the list |
| copy() | Returns a copy of the list |
| count() | Returns the number of items with the given value |
| extend() | Adds the items of another list (or iterable) to the end of the list |
| index() | Returns the index of the first item with the given value |
| insert() | Adds an item at the given position |
| pop() | Removes and returns the item at the given position (last item by default) |
| remove() | Removes the first item with the given value |
| reverse() | Reverses the order of the list |
| sort() | Sorts the list |

# More built-in functions and operations used with lists #

| Name | Explanation |
|------|-------------|
| len(list) | Returns the number of items in the list |
| sum(list) | Returns the total of all the numbers in the list |
| min(list) | Returns the smallest item in the list |
| max(list) | Returns the largest item in the list |
| sorted(list) | Returns a new sorted list and does not change the original list |
| reversed(list) | Returns an iterator that gives the items in reverse order |
| enumerate(list) | Gives each item together with its index number |
| zip(list1, list2) | Pairs up items from two lists, item by item |
| any(list) | Returns True if at least one item is true |
| all(list) | Returns True only if every item is true |
| list(iterable) | Converts a tuple, string, set or range into a list |
| del list[i] | Deletes the item at index i (also works on slices) |
| x in list | Returns True if the value x is in the list |
| x not in list | Returns True if the value x is not in the list |
| list1 + list2 | Joins two lists into a new list |
| list * n | Repeats the list n times in a new list |
