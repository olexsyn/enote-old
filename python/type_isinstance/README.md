# `type()` vs `isinstance()`

Функція `type()` повертає тип переданого аргументу, з її допомогою можна перевірити, чи належить аргумент того чи іншого типу:

```python
a = 10
b = [1,2,3]
type(a) == int    # True
type(b) == list   # True
type(a) == float  # False
```

Функція `isinstance()` спеціально створена для перевірки належності даних певного класу (типу даних):

```python
isinstance(a,int)    # True
isinstance(b,list)   # True
isinstance(b,tuple)  # False
c = (4,5,6)
isinstance(c,tuple)  # True
```

Крім того, `isinstance()` порівняно з `type()` дозволяє перевірити дане на приналежність хоча б одному типу з кортежу, переданого як другий аргумент:

```python
isinstance(a,(float, int, str))    # True
isinstance(a,(list, tuple, dict))  # False
```

Інша відмінність isinstance(). Ця функція підтримує спадкування. Для isinstance() екземпляр похідного класу також є екземпляром базового класу. Для type() це не так:

```python
class A (list):
... pass
...

a = A()
type(a) == list     # False
type(a) == A        # True
isinstance(a,A)     # True
isinstance(a,list)  # True
```
