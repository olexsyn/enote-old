# Простой пример cgi-скрипта подключающего шаблон Jinja

**Главный шаблон** /home/user/local/test.net/_tpl/ **test.htm**


{% raw %}
```html
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Test Jinja</title>
  </head>
  <body>
  	{% include '_nav.htm' %}
    <h3>Test 2 Jinja</h3>
    {%- for item in range(5) %}
      <p>Hello {{ user }}!</p>
    {%- endfor %}
    {% include '_footer.htm' %}
  </body>
</html>
```

**Шаблон** /home/user/local/test.net/_tpl/ **_nav.htm**

```html
<nav>
    <a href="/home">{{ home }}</a>
    <a href="/blog">Blog</a>
    <a href="/contact">Contact</a>
</nav>
```

**Шаблон** /home/user/local/test.net/_tpl/ **_footer.htm**

```html
<hr>
<p>Copyright {{ corp }}</p>
```
{% endraw %}



**CGI-скрипт**


```python
#!/usr/local/bin/python3.7

import sys

# Определяем, где запускается скрипт и подключаем директорию с модулями
SERVER = 0

if SERVER:
	DIR_ROOT = '/var/www/some/server/path.net'
else:
	import cgitb
	cgitb.enable()
	DIR_ROOT = '/home/user/local/test.net'
	PY_LIB   = DIR_ROOT + '/lib'
	sys.path.insert(0, PY_LIB)

# Подключаем установленные и свои модули
from jinja2 import Template , Environment, FileSystemLoader

# Директория с шаблонами
TPL_DIR = DIR_ROOT + '/test.net/_tpl'

# charset необходим для корректной работы с кириллицей
print('Content-Type: text/html; charset=utf-8\n')

# Подключаем шаблон test.htm, в котором подключается еще два
env = Environment(loader=FileSystemLoader(TPL_DIR))
template = env.get_template('test.htm')

corp = 'Копирайт'

# Собираем шаблон, передав строки для заполнения определенных в шаблонах переменных
rendered = template.render(home='Home Page', user="Вася", corp=corp)
print(rendered)
```


**Вывод в браузер:**

```html
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Test Jinja</title>
  </head>
  <body>
  	<nav>
    <a href="/home">Home Page</a>
    <a href="/blog">Blog</a>
    <a href="/contact">Contact</a>
</nav>
    <h3>Test 2 Jinja</h3>
      <p>Hello Вася!</p>
      <p>Hello Вася!</p>
      <p>Hello Вася!</p>
      <p>Hello Вася!</p>
      <p>Hello Вася!</p>
    <hr>
<p>Copyright Копирайт</p>
  </body>
</html>
```
