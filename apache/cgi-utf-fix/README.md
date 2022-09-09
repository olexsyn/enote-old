# Корректное отображение UTF8 в CGI-скриптах

#### Проблема:

**TODO!**

Простой скрипт на perl или python, запускаемый, как cgi, некорректно выводят кириллицу (и другие utf символы тоже).

```perl
#!/usr/bin/perl

print("Content-Type: text/html\n\n");
print("Привет, МИР!");
```

```python
#!/usr/bin/python3

print("Content-Type: text/html\n")
print("Привет, МИР!")
```

`charset=utf-8` в заголовках, decode/encode не помогают. Прописывание кодировок по умолчанию в **.htaccess** - тоже.

Сгенерированная HTML-страница выводится в кодировке `ANSI_X3.4-1968`

#### Решение:

<https://stackoverflow.com/questions/9322410/set-encoding-in-python-3-cgi-scripts>

1\. В файле **/etc/apache2/envvars** раскоментировать (если закоментирована) строку
```
#. /etc/default/locale
```

2\. В конфирурационном файле виртуального хоста в разделе _ScriptAlias/Directory_ прописать строку `PassEnv LANG en_US.UTF-8`:

```apache
    ScriptAlias /cgi-bin/ /www/example.com/cgi-bin/
    <Directory "/www/example.com/cgi-bin">
        ...
        Options +ExecCGI -MultiViews
        PassEnv LANG en_US.UTF-8
        ...
    </Directory>
```

3\. И, теперь, да: в выводимый заголовок `Content-Type` CGI-скрипта добавлять кодировку `utf-8`

```python
print("Content-Type: text/html; charset=utf-8\n\n");  # Perl

print('Content-Type: text/html; charset=utf-8\n')  # Python
```

<span сlass="info">Увага!</span> Якщо скрипти виконуються не лише у директорії `cgi-bin`, то в інших директоріях зі скриптами слід також розмістити файл `.htaccess`:
```apache
AddHandler cgi-script .py
Options +ExecCGI -MultiViews
PassEnv LANG en_US.UTF-8
```

Див. також
https://stackoverflow.com/questions/4374455/how-to-set-sys-stdout-encoding-in-python-3

python3.7

```python
sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach())
```
---

https://stackoverflow.com/questions/4374455/how-to-set-sys-stdout-encoding-in-python-3

---

```
У меня была похожая проблема. Для меня изначально переменная среды LANG не была установлена (вы можете проверить это, запустив env )

$ python3 -c 'import locale; print(locale.getdefaultlocale())'
(None, None)
$ python3 -c 'import locale; print(locale.getpreferredencoding())'
ANSI_X3.4-1968

Доступные локали для меня были (на свежем изображении Ubuntu 18.04 Docker):

$ locale -a
C
C.UTF-8
POSIX

Поэтому я выбрал utf-8:

$ export LANG="C.UTF-8"

И тогда все работает

$ python3 -c 'import locale; print(locale.getdefaultlocale())'
('en_US', 'UTF-8')
$ python3 -c 'import locale; print(locale.getpreferredencoding())'
UTF-8

Если вы выберете locale, который недоступен, например

export LANG="en_US.UTF-8"

это не сработает:

$ python3 -c 'import locale; print(locale.getdefaultlocale())'
('en_US', 'UTF-8')
$ python3 -c 'import locale; print(locale.getpreferredencoding())'
ANSI_X3.4-1968

и вот почему locale выдает сообщения об ошибках:

locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
```
