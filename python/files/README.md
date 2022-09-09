# Работа с файлами

- {% include a.htm url="https://pyneng.readthedocs.io/ru/latest/book/07_files/index.html" text="Python для сетевых инженеров. Работа с файлами" %}
- {% include a.htm url="https://pythonru.com/osnovy/fajly-v-python-vvod-vyvod" text="Файлы в python, ввод-вывод" %}
- {% include a.htm url="https://tproger.ru/articles/files-in-python/" text="Основы работы с файлами в Python" %}

## Обычно

Прочитать файл целиком

```python
f = open('path_to/file.txt', mode)
    text = f.read()
f.close()
```
где `mode` - режим работы с файлом: `'r'` - read; `'a'` - append; `'w'` - write

- `'r'` - Открыть файл только для чтения (значение по умолчанию)
- `'w'` - Открыть файл для записи. Если файл существует, то его содержимое удаляется
- `'a'` - Открыть файл для добавления записей. Данные добавляются в конец файла
- `'r+'` - Открыть файл для чтения и записи. <span class="warn">Проверь это!</span>
    - если файл существует, то его содержимое удаляется.
    - если файл не существует - будет вызвано исключение. 
- `'w+'` - открыть файл для чтения и записи
    - если файл существует, то его содержимое удаляется
    - если файл не существует, то создается новый
- `'a+'` - открыть файл для чтения и записи. Данные добавляются в конец файла
    - если файл существует, <span class="ques">что тут?</span>
    - если файл не существует, то <span class="ques">что тут?</span>

Объект класса io.TextIOWrapper, возвращается функцией `open()`.

- `name` — название файла;
- `mode` — режим, в котором этот файл открыт;
- `closed` — возвращает True, если файл был закрыт.


## with

```python
with open('path_to/file', mode) as f:
    text = f.read()
```

Отличие от `open()`: python самостоятельно закрывает файл, разработчику нет необходимости помнить об этом. Не вызываются исключения при открытии файла (например, если файл не существует).


## Пример работы с файлом с исключениями

```python
try:
   fh = open("testfile", "w")
   try:
      fh.write("This is my test file for exception handling!!")
   finally:
      print ("Going to close the file")
      fh.close()
except IOError:
   print ("Error: can\'t find file or read data")
```

## Работа с двумя файлами одновременно

```python
with open(fname + '.inp') as f_inp:
	with open(fname + '.out', 'w') as f_out:
		for line in f_inp:
			line = re.sub('\s{4}','\t',line)
			f_out.write(line)
	f_out.close()
f_inp.close()
```

- json
- yaml
- ini
- csv
- xls

