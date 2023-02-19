# list

```python
mylist = ["apple", "banana", "cherry"]  # ['apple', 'banana', 'cherry']
print(mylist)
print(type(mylist))

mylist = [1, 3, 5]                      # [1, 3, 5]
print(mylist)
print(type(mylist))

# mylist = list(1, 3, 5)                # ERROR!

mylist = list((1, 3, 5))                # !!! [1, 3, 5]
print(mylist)
print(type(mylist))

mylist = []                             # []
print(mylist)
print(type(mylist))

mylist = list()                         # []
print(mylist)
print(type(mylist))

mylist = list("abra")                   # !!! ['a', 'b', 'r', 'a']
print(mylist)
print(type(mylist))

mylist = list(("abra"))                 # !!! ['a', 'b', 'r', 'a']
print(mylist)
print(type(mylist))

mylist = list(("abra",))                # !!! ['abra']
print(mylist)
print(type(mylist))
```

## tuple

```python
mytuple = ("apple", "banana", "cherry")  # ('apple', 'banana', 'cherry')
print(mytuple)
print(type(mytuple))

mytuple = (1, 3, 5)                      # (1, 3, 5)
print(mytuple)
print(type(mytuple))

# mytuple = tuple(1, 3, 5)               # ERROR!

mytuple = tuple((1, 3, 5))               # !!! (1, 3, 5)
print(mytuple)
print(type(mytuple))

mytuple = ()                             # ()
print(mytuple)
print(type(mytuple))

mytuple = tuple()                        # ()
print(mytuple)
print(type(mytuple))

mytuple = tuple("abra")                  # !!! ('a', 'b', 'r', 'a')
print(mytuple)
print(type(mytuple))

mytuple = tuple(("abra"))                # !!! ('a', 'b', 'r', 'a')
print(mytuple)
print(type(mytuple))

mytuple = tuple(("abra",))               # !!! ('abra',)
print(mytuple)
print(type(mytuple))

```
