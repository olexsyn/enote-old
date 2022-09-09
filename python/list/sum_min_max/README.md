# sum, min, max

```python
l = [3, 5, 1]
t = (6, 2, 4)
d = dict(a = 0, b = 2, c = 3)

print( sum(l) )           # 6
print( sum(t) )           # 12
print( sum(d.values()) )  # 6

print()

print( max(l) )           # 5
print( max(t) )           # 6
print( max(d.values()) )  # 3

print()

print( min(l) )           # 1
print( min(t) )           # 2
print( min(d.values()) )  # 0

l = 'abrakadabra'
t = ('F', 'A', 'C')
d = dict(a = 'abra', b = 'kada', c = 'bra')

# sum - не работает со строками

print()

print( max(l) )           # 'r'
print( max(t) )           # 'F'
print( max(d.values()) )  # 'kada'

print()

print( min(l) )           # 'a'
print( min(t) )           # 'A'
print( min(d.values()) )  # 'abra'

```
