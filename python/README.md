# Python


## Строки

- [Строки в python 3: методы, функции, форматирование](https://pythonru.com/osnovy/stroki-python) :link: :onion:
- [Форматування виводу](output-formatting)
- [Форматирование строк с помощью format()](https://pythonru.com/osnovy/formatirovanie-v-python-s-pomoshhju-format) :link:
- [10 примеров использования методов строк в python](https://pythonru.com/primery/10-primerov-ispolzovanija-metodov-stok-v-python) :link:
- [Конвертация между байтами и строками](https://pyneng.readthedocs.io/ru/latest/book/16_unicode/python_3_convert.html) :link:
- [Ведущие нули](leading_zeros/)
- [Яка різниця між `isdigit()`, `isdecimal()`, `isnumeric()` і як їх використовувати?](https://miguendes.me/python-isdigit-isnumeric-isdecimal) :link:
- [`type()` vs `isinstance()`](type_isinstance)

### split i join

```python
txt = "welcome to the jungle"
x = txt.split()
print(x)          # ['welcome', 'to', 'the', 'jungle']
y = txt.split('o')
print(y)          # ['welc', 'me t', 'the jungle']
```
див.також `.rsplit()`, `.partition()`, `.splitlines()`, 

```python
my_tuple = ("John", "Peter", "Vicky")
x = "-".join(my_tuple)
print(x)          # 'John-Peter-Vicky'
```


## Списки

- [Функции `any` и `all`](list/any_all/)
- [Функции `sum`, `min` и `max`](list/sum_min_max/)
- [Метод списка `list.sort()` и функция `sorted()`](list/sort_sorted)

## Бібліотеки
- [datetime](datetime)
- [json](json)

### Словари

[Как объединить два словаря в Python](https://pythobyte.com/how-to-merge-two-dictionaries-in-python-48547651/) :link:

### Синтаксис

- [Глобальні змінні `global`](global)
- [if](syntax_if)
- [yield](yield)

## Арифметика

### Три простых способа поменять знак числа на противоположный

```python
positive_digit = 30

b = positive_digit * -1
print(b)  # -30

c = 0 - positive_digit
print(c)  # -30

d = - positive_digit
print(d)  # -30
```

## Аргументы командной строки

```python
import sys

if __name__ == '__main__':
	if len(sys.argv)<=2:
		print('usage:', sys.argv[0], '<integer1> <integer2>')
		sys.exit(1)

	val1 = round(float(sys.argv[1]))
	val2 = round(float(sys.argv[2]))
	print('Сумма целых чисел:', val1+val2)
```

```
  $ python argv.py
  usage: argv.py <integer1> <integer2>

  $ python argv.py 3 5
  Сумма целых чисел: 8

  $ python argv.py 3.2 5.7
  Сумма целых чисел: 9

  $ python argv.py -3.2 5.3
  Сумма целых чисел: 2
```

см. также [argparse, click и др.](library)

---


- [Обработка ошибок и исключений](https://pythonru.com/osnovy/znachenija-iskljuchenij-i-oshibok-v-python)
- [Конструкция try - except для обработки исключений](https://pythonworld.ru/tipy-dannyx-v-python/isklyucheniya-v-python-konstrukciya-try-except-dlya-obrabotki-isklyuchenij.html)

---

- [Цветной вывод текста в Python](https://all-python.ru/osnovy/tsvetnoj-vyvod-teksta.html)
- [Асинхронность python на примере asyncio](https://pythonru.com/primery/asinhronnost-python-na-primere)
- [Работа с документацией в Python: поиск информации и соглашения](https://proglib.io/p/python-docs/)
- [Списки VS кортежи. Оптимизации](https://habr.com/ru/post/417783/)
- [Есть ли в Python оператор switch case?](https://ru.stackoverflow.com/questions/460207/%D0%95%D1%81%D1%82%D1%8C-%D0%BB%D0%B8-%D0%B2-python-%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80-switch-case)
- [Creating PDF Reports with Pandas, Jinja and WeasyPrint](https://pbpython.com/pdf-reports.html)

- [Форма + AJAX](form_ajax)
- [Вывод цветного текста](https://all-python.ru/osnovy/tsvetnoj-vyvod-teksta.html)
- [Локализация приложений на Python](localization)

- [Отправка e-mail](email)
- [Примеры CGI](cgi-examples)
- [Удаление дубликатов из списка. Сохранить порядок элементов](remove_dubl)

## Завершение программ

```python
sys.exit(code)  # code - не обязателен
```

```python
os._exit(code)  # code - необходим!
```
''code'' = **0** - нормальное завершение; другие значения, если возникли проблемы

[подробнее](exit)


## Ошибки

* `malformed header from script 'script.py': Bad header: NameError, referer: http://...`

Скрипт в терминале отрабатывает без ошибок, а в браузере получаем Error 500.

Одна из причин: вероятно, что скрипт пишет в лог. И когда запуск производился через терминал, то файл лога создался владельцем текущей учетной записи. При запуске через http, владелец уже `www-data` который не имеет прав записи в этот файл. Нужно просто удалить файл лога и запустить скрипт через http еще раз.

* `python3: Relink '/lib/x86_64-linux-gnu/libsystemd.so.0' with '/lib/x86_64-linux-gnu/librt.so.1' for IFUNC symbol 'clock_gettime'`

Скрипт в терминале показывает это сообщение, а в браузере получаем Error 500.

Аналогичная предыдущей проблема, возникающая при подключении модуля логирования logging, при настройке записи в файл, который уже создан от другого пользователя. Удалить файл лога или назначить ему разрешение 777.
