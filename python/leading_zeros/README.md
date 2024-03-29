# Ведущие нули

Для Python >= 3.6, используйте **f-string**:

```
>>> x = 10
>>> print(f'{x:05}')
                ^ желаемая длина строки
00010
```

или метод **format** строки, который работает в любой версии:

```
'{:05}'.format(10)   # '00010'
    ^ желаемая длина строки
```

## АЛЕ!

**Якщо значення - строка, а не число - нулі додадуться позаду!**

Числа:

```python
year = 2022
mon = 9
day = 5

print(f'{year}-{mon:02}-{day:02}')  # '2022-09-05'
```

Строки, які зазвичай отримуємо з web-форм, вводу з консолі:

```python
year = '2022'
mon = '9'
day = '5'

print(f'{year}-{mon:02}-{day:02}')  # '2022-90-50' !!!!
```

## Для строк: `string.zfill()` - доповнює строку нулями зліва.

```python
a = "hello"
b = "welcome to the jungle"
c = "10.000"

print(a.zfill(10))  # '00000hello'
print(b.zfill(10))  # 'welcome to the jungle'
print(c.zfill(10))  # '000010.000'
```

## Более подробно:

Желательно знать или вычислить максимальное количество позиций, которое потребуется для вывода числа _max_width_.

Если есть отрицательные числа, нужно учитывать, что знак будет занимать одну из позиций. Можно сделать так, чтобы знак выводился всегда.

Для дробных чисел нужно учитывать позицию для точки (запятой).

```
max_width = 5
print(f'{10:0{max_width}}')      # 00010   - вывод с добавлением нолей
print(f'{-10:0{max_width}}')     # -0010   - минус забирает одну позицию
print(f'{-10000:0{max_width}}')  # -10000  - если число слишком большое, 
                                 #           строка будет длиннее, чем max_width
print(f'{10:+0{max_width}}')     # +0010   - обязательный вывод знака
print(f'{10.5:0{max_width}}')    # 010.5   - точка забирает одну позицию
print(f'{10:{max_width}}')       #    10   - можно заполнять пробелами
```

Подробнее про возможности форматирования можно почитать в документации:

- Описание мини-языка форматирования <https://docs.python.org/3/library/string.html#format-specification-mini-language>
- f-string <https://docs.python.org/3/reference/lexical_analysis.html#f-strings>
- str.format <https://docs.python.org/3/library/stdtypes.html#str.format>
