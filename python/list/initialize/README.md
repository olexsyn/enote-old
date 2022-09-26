# Ініціалізація списків


## Використання функції list() для ініціалізації

```python
list_1 = list()
print (list_1)

res = []
print (data == res)
```
```
[]
TRUE
```

## Using comprehensions to initialize the list

```python
list = [i for i in range(5)]
print (list)
```
```
[0,1,2,3,4]
```

## Initialize lists using the * operator

```python
list = [5]*10
print (list)
```
```
[5,5,5,5,5,5,5,5,5,5]
```

## Що таке список списків?

У будь-якій мові програмування списки використовуються для зберігання більш ніж одного елемента в одній змінній. У Python ми можемо створити список, узявши всі елементи в квадратні дужки [] і розділивши кожен елемент комами. Його можна використовувати для зберігання цілих чисел, чисел з плаваючою точкою, рядків тощо.

Python надає можливість створення списку в списку. Простіше кажучи, це вкладений список, але з одним або кількома списками всередині як елемент.

Ось приклад списку списків, щоб було зрозуміліше:

```
[[a,b],[c,d],[e,f]]
```

## Використання функції append() для створення списку списків

```python
# Create 2 independent lists
list_1 = [a,b,c]
list_2 = [d,e,f]

# Create an empty list
list = []

# Create List of lists
list.append(list_1)
list.append(list_2)
print (list)
```
```
[[a,b,c],[d,e,f]]
```

## Створення списку списків за допомогою ініціалізатора списку

```python
# Create 2 independent lists 
list_1 = [a,b,c] 
list_2 = [d,e,f]

# Create List of lists 
list = [list1, list2]

# Display result
print(list)
```
```
[[a,b,c],[d,e,f]]
```

## Using list comprehension to create a list of lists

```python
list_1 = [a,b,c]
list = [l1 for i in range(3)]
print(list)
```
```
[[a,b,c],[a,b,c],[a,b,c]]
```

## Using for-loop to create a list of lists

```python
list = []

# Create List of list
for i in range(2):
    list.append([])
    for j in range(3): 
        list[i].append(j)

print(lst)
```
```
[[a,b,c],[a,b,c]]
```
