# subprocess

## call

- системные всплывающие уведомления

Вы можете легко отображать системные всплывающие уведомления из программ на Python или любом другом языке.

Вам понадобится обвязка **libnotify** для Python:

    pacman -S python-notify

<small>(pacman - установщик для Archlinux, Manjaro)</small>

Вот простой "hello world" пример:

```python
import subprocess

def notify(title, mess):
    subprocess.call(['notify-send', title, mess])

path = "/home/user/tmp"
notify('Copied to', path)
```


- [Выполнение shell команд с Python](../os-system_subprocess-run)

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
