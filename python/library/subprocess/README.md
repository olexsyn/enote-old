# subprocess

## Запуск внешних приложений

- [call - системные всплывающие уведомления](call)
- [Выполнение shell команд с Python](os-system_subprocess-run)

пример cgi-скрипта, который выводит версию Python:

```python
import subprocess

print("Content-Type: text/html\n\n")
version = subprocess.run(["python3","-V"], stdout=subprocess.PIPE, text=True)
print('<h3>',version.stdout,'</h3>')
```

Подробнее:

- <https://docs.python.org/3/library/subprocess.html>
- <https://natenka.gitbook.io/pyneng/part_ii/12_useful_modules/subprocess>
- <https://pythonworld.ru/moduli/modul-subprocess.html>
- <https://ru.wikibooks.org/wiki/Учебник_Python/Процессы_и_потоки>
- <https://proft.me/2009/04/9/zapusk-vneshnih-prilozhenij-v-python/>
- <https://python-scripts.com/subprocess>
