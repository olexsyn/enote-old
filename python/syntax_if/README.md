# Синтаксиc if

## if/elif/else

```python
username = input('Введіть ім’я користувача: ')
password = input('Введіть пароль: ')

if len(password) < 8:
    print('Пароль занадто короткий')
elif username in password:
    print('Пароль містить ім'я користувача')
else:
    print('Пароль для користувача {} встановлений'.format(username))
```

# Тернарний вираз (ternary expression)

Іноді зручніше використовувати тернарний оператор, ніж розгорнуту форму:

```python
s = [1, 2, 3, 4]
result = True if len(s) > 5 else False
```
